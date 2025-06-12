# Problem 1

## Equivalent resistance

>**Equivalent resistance** is the total resistance measured in a parallel or series circuit, either for the whole circuit or a part of it.

Equivalent resistance is defined between two terminals or nodes of the network and represents the total effect of all resistors in the circuit.

>The formula for equivalent resistance $R_{eq}$  in a **parallel** combination is expressed as:

$$
\frac{1}{R_{eq}} = \frac{1}{R_{1}} + \frac{1}{R_{2}} + \dots + \frac{1}{R_{n}}
$$

where $R_i$ indicates the resistance of the $i_{th}$ resistor. 

>The formula for equivalent resistance $R_{eq}$ in a **series** combination is expressed as:

$$
R_{eq} = R_{1} + R_{2} + \dots + R_{n}
$$

where $R_i$ indicates the resistance of the $i_{th}$ resistor. 

![Pasted image 20250526210631](https://github.com/user-attachments/assets/cdcd6bbd-eca5-4410-b783-3f0287512543)


## Approach Overview

1. **Graph Representation**
   - Nodes represent circuit junctions.
   - Edges represent resistors with resistance values as weights.

2. **Simplification Strategy**
   - Detect and merge series resistors (resistors connected end-to-end).
   - Detect and combine parallel resistors (resistors connected between the same two nodes).
   - Repeat until the circuit reduces to a single equivalent resistor.

3. **Implementation Tools**
   - Use the `networkx` library for graph manipulation.
   - Use depth-first search (DFS) to identify series chains.
   - Use graph analysis to find parallel connections, especially cycles.

## Theoretical background

>Circuit as a graph:

We will represent the circuit as a **unidirected weighted graph** $G = (V, E)$, where vertices $V$ are circuit nodes and edges (links) $E$ are resistors with weights equal to resistance values.

>Series and parallel reductions:

- _Series:_ Two edges connected end-to-end with a single intermediate node of degree 2 can be replaced by a single edge with resistance equal to the sum of the two resistors.
- _Parallel:_ Multiple edges connecting the same pair of nodes can be replaced by a single edge with resistance given by the reciprocal of the sum of reciprocals (conductances).

>Graph simplification approach:

Iteratively detect and reduce series chains and parallel edges until the graph reduces to a single equivalent resistor between the two nodes of interest.


For complex circuits, graph spectral methods and matrix formulations involving the Laplacian matrix can be used to compute effective resistance, but iterative simplification is more intuitive and suitable for programming.

## Algorithm outline

1. **Input**: Graph $G$ with nodes and weighted edges (resistances), and two nodes $s$ and $t$ between which equivalent resistance is required.
2. **Preprocessing:**
    - Remove any isolated nodes not connected to $s$ or $t$.        
    - Identify series chains: nodes with degree $2$ not equal to $s$ or $t$.
    - Identify parallel edges between the same nodes.
3. **Iterative Simplification:**
	- Replace series chains by single edges with summed resistance.
	- Replace parallel edges by single edges with combined resistance using parallel formula:

$$
R_{eq} = \left( \sum_{i} \frac{1}{R_{i}}  \right)^{-1}
$$
- Repeat until only one edge remains between $s$ and $t$.

## Implementation


```Python
import networkx as nx
import matplotlib.pyplot as plt
from copy import deepcopy

def plot_graph(G, step):
    pos = nx.spring_layout(G)
    labels = nx.get_edge_attributes(G, 'resistance')
    nx.draw(G, pos, with_labels=True, node_color='lightblue', node_size=500)
    nx.draw_networkx_edge_labels(G, pos, edge_labels=labels)
    plt.title(f'Circuit after step {step}')
    plt.show()

def combine_series(G):
    """
    Find and combine series edges:
    A series connection is when a node has exactly two neighbors,
    and is not a terminal node (degree 2),
    and edges can be combined by summing resistances.
    """
    G = deepcopy(G)
    changed = False

    # List nodes to check for series
    for node in list(G.nodes()):
        # Skip if node is terminal (degree != 2)
        if G.degree(node) != 2:
            continue
        neighbors = list(G.neighbors(node))
        # Check if node is not a self loop or parallel edges only
        if len(neighbors) != 2:
            continue

        # Check if node is not an endpoint (avoid terminals)
        # Also ensure no parallel edges between neighbors through this node
        # Combine the two edges in series
        # Get resistances on edges (MultiGraph can have multiple edges)
        edges1 = G.get_edge_data(node, neighbors[0])
        edges2 = G.get_edge_data(node, neighbors[1])

        # Sum resistances of all parallel edges between node and neighbors
        r1 = sum(d['resistance'] for d in edges1.values())
        r2 = sum(d['resistance'] for d in edges2.values())

        # Remove node and its edges
        G.remove_node(node)
        # Add new edge between neighbors with resistance = r1 + r2
        # If edge already exists, add in parallel (combine parallel)
        if G.has_edge(neighbors[0], neighbors[1]):
            # Combine parallel edges
            existing_edges = G.get_edge_data(neighbors[0], neighbors[1])
            existing_r = sum(d['resistance'] for d in existing_edges.values())
            # Parallel combination: 1/Req = 1/Rexisting + 1/(r1+r2)
            Req = 1 / (1 / existing_r + 1 / (r1 + r2))
            # Remove old edges and add one with Req
            G.remove_edges_from([(neighbors[0], neighbors[1], k) for k in existing_edges.keys()])
            G.add_edge(neighbors[0], neighbors[1], resistance=Req)
        else:
            G.add_edge(neighbors[0], neighbors[1], resistance=r1 + r2)
        changed = True
        break  # Restart after modification

    return G, changed

def combine_parallel(G):
    """
    Combine parallel edges between the same two nodes:
    1/Req = sum(1/Ri)
    """
    G = deepcopy(G)
    changed = False

    for u, v in list(G.edges()):
        edges = G.get_edge_data(u, v)
        if len(edges) > 1:
            # Combine all parallel resistors
            resistances = [d['resistance'] for d in edges.values()]
            Req = 1 / sum(1 / r for r in resistances)
            # Remove all parallel edges
            G.remove_edges_from([(u, v, k) for k in edges.keys()])
            # Add single edge with Req
            G.add_edge(u, v, resistance=Req)
            changed = True
            break  # Restart after modification

    return G, changed

def reduce_circuit(G):
    """
    Reduce the circuit graph step by step:
    1. Combine series edges
    2. Combine parallel edges
    Repeat until no changes.
    """
    step = 0
    intermediate_graphs = []

    current_graph = deepcopy(G)
    intermediate_graphs.append((step, deepcopy(current_graph)))

    while True:
        step += 1
        # Combine series
        current_graph, changed_series = combine_series(current_graph)
        if changed_series:
            intermediate_graphs.append((step, deepcopy(current_graph)))
            continue

        # Combine parallel
        current_graph, changed_parallel = combine_parallel(current_graph)
        if changed_parallel:
            intermediate_graphs.append((step, deepcopy(current_graph)))
            continue

        # If no changes, stop
        break

    return current_graph, intermediate_graphs

# Example circuit construction
G = nx.MultiGraph()
# Add edges with resistance attribute
G.add_edge('A', 'B', resistance=5)
G.add_edge('B', 'C', resistance=20)
G.add_edge('B', 'C', resistance=100)
G.add_edge('C', 'D', resistance=2)
G.add_edge('B', 'E', resistance=9)
G.add_edge('E', 'C', resistance=3)

# Reduce circuit and get intermediate graphs
final_graph, intermediates = reduce_circuit(G)

# Print and plot intermediate graphs
for step, g in intermediates:
    print(f"Step {step}:")
    for u, v, data in g.edges(data=True):
        print(f"  {u}-{v} : {data['resistance']:.4f} Ω")
    plot_graph(g, step)

# Final equivalent resistance
edges = list(final_graph.edges(data=True))
if len(edges) == 1:
    u, v, data = edges[0]
    print(f"Equivalent resistance between {u} and {v} is {data['resistance']:.4f} Ω")
else:
    print("Circuit could not be fully reduced to a single resistor.")

```

Output:

```
Step 0:
  A-B : 5.0000 Ω
  B-C : 20.0000 Ω
  B-C : 100.0000 Ω
  B-E : 9.0000 Ω
  C-D : 2.0000 Ω
  C-E : 3.0000 Ω
```

![1](https://github.com/user-attachments/assets/99a21619-e556-4fcb-b7c9-c1b867446173)

```
Step 1:
  A-B : 5.0000 Ω
  B-C : 10.9091 Ω
  C-D : 2.0000 Ω
```


![2](https://github.com/user-attachments/assets/045ba4c6-2ddd-4133-82be-761356d5d359)

```
Step 2:
  A-C : 15.9091 Ω
  C-D : 2.0000 Ω
```


![3](https://github.com/user-attachments/assets/33c6f41c-2841-48c7-b3e6-15abe1ea83dc)

```
Step 3:
  A-D : 17.9091 Ω
```

![4](https://github.com/user-attachments/assets/26bed2b4-55ef-4fad-b139-6d8fb50b572e)

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

def equivalent_resistance(graph, node_start, node_end):
    G = graph.copy()
    
    # Helper function to combine parallel edges
    def combine_parallel_edges(G):
        for u, v in list(G.edges()):
            edges = list(G.get_edge_data(u, v).values()) if G.is_multigraph() else [G[u][v]]
            if len(edges) > 1:
                # Calculate combined parallel resistance
                combined_resistance = 1 / sum(1 / e['resistance'] for e in edges)
                # Remove all parallel edges and add one combined edge
                G.remove_edges_from([(u, v)] * len(edges))
                G.add_edge(u, v, resistance=combined_resistance)
        return G

    # Helper function to reduce series chains
    def reduce_series(G):
        for node in list(G.nodes()):
            if node in (node_start, node_end):
                continue
            if G.degree(node) == 2:
                neighbors = list(G.neighbors(node))
                r1 = G[node][neighbors[0]]['resistance']
                r2 = G[node][neighbors[1]]['resistance']
                new_resistance = r1 + r2
                G.add_edge(neighbors[0], neighbors[1], resistance=new_resistance)
                G.remove_node(node)
                return G, True
        return G, False

    # Iterative simplification
    changed = True
    while changed:
        G = combine_parallel_edges(G)
        G, changed = reduce_series(G)

    # After simplification, the equivalent resistance is the resistance of the edge between node_start and node_end
    if G.has_edge(node_start, node_end):
        return G[node_start][node_end]['resistance']
    else:
        return None  # No path between nodes

# Example usage:
# Create a graph with resistors as edges
G = nx.Graph()
G.add_edge('A', 'B', resistance=100)
G.add_edge('B', 'C', resistance=200)
G.add_edge('A', 'C', resistance=300)

req = equivalent_resistance(G, 'A', 'C')
print(f"Equivalent resistance between A and C: {req} Ω")
```
Output:

```bash
Equivalent resistance between A and C: 300 Ω
```

# Problem 2

### Part 1

The Monte Carlo method estimates π by leveraging the ratio of points falling inside a circle to the total number of points randomly generated within a square that bounds the circle.

- For a unit circle (radius = 1) centered at the origin, the area is $π·r^2 = π$. The area of the bounding square (with sides of length 2, from -1 to 1) is 4.
- If we randomly generate points uniformly within the square, the probability that a point falls inside the circle is the ratio of the circle's area to the square's area:

$$
P=\frac{\text{Area of square}}{\text{Area of circle}}=\frac{4}{π}
$$

- If $N_{in}$ is the number of points inside the circle and $N_{total}$ is the total number of points, then

$$
\frac{N_{in}}{N_{total}} \approx \frac{\pi}{4} \implies \pi \approx 4 \cdot \frac{N_{in}}{N_{total}}
$$


Let's visualize this:

- [Link to `matplotlib.online`]()

```Python
import numpy as np
import matplotlib.pyplot as plt

# Parameters
N = 10000  # Number of points

# Generate random points in [-1, 1] x [-1, 1]
x = np.random.uniform(-1, 1, N)
y = np.random.uniform(-1, 1, N)

# Check which points are inside the unit circle
inside = x**2 + y**2 <= 1
N_in = np.sum(inside)

# Estimate pi
pi_estimate = 4 * N_in / N
print(f"Estimated π: {pi_estimate}")

plt.figure(figsize=(6, 6))
plt.scatter(x[inside], y[inside], color='blue', s=1, label='Inside Circle')
plt.scatter(x[~inside], y[~inside], color='red', s=1, label='Outside Circle')
circle = plt.Circle((0, 0), 1, color='black', fill=False, linewidth=2)
plt.gca().add_patch(circle)
plt.xlim([-1, 1])
plt.ylim([-1, 1])
plt.gca().set_aspect('equal')
plt.legend()
plt.title('Monte Carlo Estimation of π')
plt.show()
```
![pi_circle](https://github.com/user-attachments/assets/2ee43e46-6744-4d8d-8d8a-d24d52543273)



```Python
Estimated π: 3.1716
```

- As the number of points increases, the estimate of $π$ converges to the true value.
- The error decreases as $\frac{1}{\sqrt{ N }}$, characteristic of Monte Carlo methods.
- The method is simple but converges slowly compared to some deterministic algorithms.
### Part 2

Buffon’s Needle is a classic probability problem for estimating $π$:

- Parallel lines are drawn on a plane, spaced a distance $d$ apart. A needle of length $l \leq d$ is dropped randomly onto the plane.


![Pasted image 20250605124731](https://github.com/user-attachments/assets/ae520ef4-b57b-4c48-b130-916736ece60e)



- The probability $P$ that the needle crossed the line is:

$$
P = \frac{2l}{\pi d}
$$

- If the needle is dropped $N$ times and crossed a line $N_{c}$ times, then:

$$
\pi \approx \frac{2lN}{dN_{c}}
$$

A great visualization can also be found [here](https://www.ventrella.com/Buffon/).

Let's visualize this ourselves:


```Python
import numpy as np
import matplotlib.pyplot as plt

# Set parameters
d = 1.0  # Distance between parallel lines
l = 0.8  # Length of the needle (less than or equal to d)
N = 5000  # Number of needle drops

# Seed for reproducibility
np.random.seed(42)

# Generate random positions of the needle centers (x, y)
# Since the lines are horizontal and spaced by d, y positions are uniformly distributed within [0, d]
x_centers = np.random.uniform(0, 10*d, N)  # x can be anywhere, but for visualization, limit to some range
y_centers = np.random.uniform(0, d, N)

# Generate random orientations: angles between 0 and pi
angles = np.random.uniform(0, np.pi, N)

# Calculate the endpoints of each needle
# Half-length components
dx = (l / 2) * np.cos(angles)
dy = (l / 2) * np.sin(angles)

# Needle endpoints
x_start = x_centers - dx
x_end = x_centers + dx
y_start = y_centers - dy
y_end = y_centers + dy

# Check if each needle crosses a line
# Since lines are at y = 0, d, 2d, etc., check if the needle crosses any line
# For each needle, check if the lines y=0 and y=d are crossed
crossings = []

for y1, y2 in zip(y_start, y_end):
    # The line crosses the needle if the segment between y1 and y2 crosses y=0 or y=d
    crosses = ((y1 < 0 and y2 > 0) or (y1 > 0 and y2 < 0) or
               (y1 < d and y2 > d) or (y1 > d and y2 < d))
    crossings.append(crosses)

crossings = np.array(crossings)
N_cross = np.sum(crossings)

# Estimate pi
# From the probability P = 2l / (pi * d), rearranged as pi ≈ 2lN / (d Nc)
pi_estimate = (2 * l * N) / (d * N_cross) if N_cross > 0 else np.nan

# --- Visualization ---

fig, ax = plt.subplots(figsize=(10, 6))

# Plot the parallel lines
for line_idx in range(int(np.max(y_end) // d) + 2):
    y_line = line_idx * d
    ax.plot([-1, 11 * d], [y_line, y_line], 'k-', linewidth=1)

# Plot needles
# Needles that crossed the lines in red, others in blue
ax.plot([x_start[crossings], x_end[crossings]], [y_start[crossings], y_end[crossings]],
        'r-', linewidth=0.8, label='Crossed line' if line_idx == 0 else "")
ax.plot([x_start[~crossings], x_end[~crossings]], [y_start[~crossings], y_end[~crossings]],
        'b-', linewidth=0.8, label='Did not cross' if line_idx == 0 else "")

# Setting plot limits
ax.set_xlim(-d, 11 * d)
ax.set_ylim(-0.5, max(y_end) + 0.5)

ax.set_title(f"Buffon's Needle Simulation: Approximate Pi = {pi_estimate:.4f}")
ax.set_xlabel("X position")
ax.set_ylabel("Y position")
ax.legend()

plt.show()
```

- $N=5000$:

![needle](https://github.com/user-attachments/assets/a4404d97-dd23-4e98-bede-e2d80ca5018d)


- Increasing `N` improves the approximation.

$N=100$:

![n100](https://github.com/user-attachments/assets/d2bfeb49-e623-4b37-bb3a-c8fa17e7ab5e)


$N=500$:

![n500](https://github.com/user-attachments/assets/b389015e-bda6-4233-a8f9-5d6add80a467)


$N=1000$:

![n1000](https://github.com/user-attachments/assets/01bb9d6f-edca-4d11-9806-f131fde23020)

- We can adjust `l` and `d` to see how the estimate varies:

Same as above, but $d=2.0$, and $l=1.5$:
![changleld](https://github.com/user-attachments/assets/8f89da1b-8950-4f5a-af99-392eb6ad6405)



- The visualization helps understand the random placement and crossing behavior.

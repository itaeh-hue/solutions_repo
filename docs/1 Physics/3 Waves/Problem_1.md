# Problem 1

## Theory

A circular wave from a single point source located at $(x_0, y_0)$ on the water surface is described by the displacement function:

$$
\eta(x, y, t) = \frac{A}{\sqrt{r}} \cos\left(kr - \omega t + \phi\right)
$$

where:

- $\eta(x, y, t)$ is the displacement at point $(x, y)$ and time $t$,
- $A$ is the amplitude,
- $r = \sqrt{(x - x_0)^2 + (y - y_0)^2}$ is the distance from the source,
- $k = \frac{2\pi}{\lambda}$ is the wave number,
- $\omega = 2\pi f$ is the angular frequency,
- $\phi$ is the initial phase.

For $N$ sources placed at vertices $\{(x_i, y_i)\}_{i=1}^N$ of a regular polygon, the total displacement is given by the superposition principle:

$$
\eta_{\text{sum}}(x, y, t) = \sum_{i=1}^N \frac{A}{\sqrt{r_i}} \cos\left(k r_i - \omega t + \phi_i\right)
$$

where $r_i = \sqrt{(x - x_i)^2 + (y - y_i)^2}$.

  
- When multiple sources emit waves, the total displacement at any point is the **sum** of the individual waves (superposition principle). 
- For **steady-state** visualization, we often fix a specific time (like $t=0$) and sum the wave contributions at that instant.

Constructive interference occurs where waves arrive in phase, amplifying displacement; destructive interference occurs where waves are out of phase, reducing or canceling displacement.

## Methodology

1. **Select Polygon:** Choose a regular polygon (e.g., equilateral triangle, square, pentagon).
2. **Source Placement:** Calculate vertices coordinates assuming a circumradius $R$.
3. **Parameters:** Set amplitude $A$, wavelength $\lambda$, frequency $f$, and initial phases $\phi_i=0$ (coherent sources).
4. **Grid:** Define a 2D spatial grid $(x,y)$ covering the region around the polygon.
5. **Compute Displacement:** For each point on the grid and fixed time $t$, compute $\eta_{\text{sum}}(x,y,t)$.
6. **Visualization:** Plot the resulting interference pattern as a 3D surface showing displacement amplitude using Matplotlib.

## Interference formed on the water surface due to the superposition of waves emitted from point sources placed at the vertices of a square

As an example, we will take a square at the vertices of which the waves will be emitted. 

Given $N=4$ sources located at vertices of a square, the total displacement will be:
$$
\eta_{\text{total}}(x, y, t) = \sum_{i=1}^4 \eta_i(x, y, t)
$$

Since we're interested in the steady-state interference pattern, we often consider the superimposed wave at a fixed time $t=0$:

$$
\eta_{\text{total}}(x, y) = \sum_{i=1}^4 \frac{A}{\sqrt{r_i}} \cos\left(k r_i + \phi_i\right)
$$
## 2D Python visualization

Below is the code that visualizes interference of waves formed on the water surface due to the superposition of waves emitted from point sources placed at the vertices of a square:

```Python
import numpy as np
import matplotlib.pyplot as plt

# Parameters
A = 1.0             # Amplitude
L = 10.0            # Side length of the square
lambda_wave = 2.0   # Wavelength
f = 1.0             # Frequency in Hz
phi = 0             # Initial phase

# Derived parameters
k = 2 * np.pi / lambda_wave
omega = 2 * np.pi * f

# Source positions (vertices of the square)
half_L = L / 2
sources = [
    (-half_L, -half_L),  # bottom-left
    (half_L, -half_L),   # bottom-right
    (half_L, half_L),    # top-right
    (-half_L, half_L)    # top-left
]

# Create a grid over the region
grid_size = 200  # resolution of the grid
x = np.linspace(-L, L, grid_size)
y = np.linspace(-L, L, grid_size)
X, Y = np.meshgrid(x, y)

# Compute the superposed wave at t=0
eta_total = np.zeros_like(X)

for (x_i, y_i) in sources:
    r = np.sqrt((X - x_i)**2 + (Y - y_i)**2) + 1e-6  # add small term to avoid division by zero
    eta_i = (A / np.sqrt(r)) * np.cos(k * r + phi)
    eta_total += eta_i

# Plotting
plt.figure(figsize=(8, 6))
contour = plt.contourf(X, Y, eta_total, levels=100, cmap='viridis')
plt.colorbar(contour, label='Wave Displacement')
plt.title('Interference Pattern from 4 Water Wave Sources (Square Configuration)')
plt.xlabel('x')
plt.ylabel('y')

# Plot source points
for (x_i, y_i) in sources:
    plt.plot(x_i, y_i, 'ro')  # source positions

plt.grid(True)
plt.axis('equal')
plt.show()
```

Here is the 2D graph output:

![wave_4_sources](https://github.com/user-attachments/assets/27da1a4c-080c-4406-a21f-3e3d452282f6)

Animated:

![animated_2d](https://github.com/user-attachments/assets/f4f4af70-592f-4465-a1e4-432b597557fe)



Link on `matplotlib.online`: https://share.matplotlib.online/3fd83dc9eb7e4d3abb484fc9faaf9841

## 3D Python visualization

The next script illustrates the same interference as above, but in a 3D graph:

```Python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

# Parameters
A = 1.0             # Amplitude
L = 10.0            # Side length of the square
lambda_wave = 2.0   # Wavelength
f = 1.0             # Frequency in Hz
phi = 0             # Initial phase

# Derived parameters
k = 2 * np.pi / lambda_wave
omega = 2 * np.pi * f

# Source positions (vertices of the square)
half_L = L / 2
sources = [
    (-half_L, -half_L),  # bottom-left
    (half_L, -half_L),   # bottom-right
    (half_L, half_L),    # top-right
    (-half_L, half_L)    # top-left
]

# Create a grid over the region
grid_size = 200
x = np.linspace(-L, L, grid_size)
y = np.linspace(-L, L, grid_size)
X, Y = np.meshgrid(x, y)

# Compute the superposed wave at t=0
eta_total = np.zeros_like(X)

for (x_i, y_i) in sources:
    r = np.sqrt((X - x_i)**2 + (Y - y_i)**2) + 1e-6
    eta_i = (A / np.sqrt(r)) * np.cos(k * r + phi)
    eta_total += eta_i

# Plotting the 3D surface
fig = plt.figure(figsize=(10, 8))
ax = fig.add_subplot(111, projection='3d')

# Plot the surface
surf = ax.plot_surface(X, Y, eta_total, cmap='viridis', linewidth=0, antialiased=False)

# Add color bar to indicate amplitude
fig.colorbar(surf, shrink=0.5, aspect=10, label='Wave Displacement')

# Title and labels
ax.set_title('3D Interference Pattern from 4 Water Wave Sources (Square Configuration)')
ax.set_xlabel('x')
ax.set_ylabel('y')
ax.set_zlabel('Displacement')

# Plot source points for reference
for (x_i, y_i) in sources:
    ax.scatter(x_i, y_i, 0, color='red', s=50)

plt.show()
```

Here is the graph output:

![wave_4_sources_3D](https://github.com/user-attachments/assets/48c0f595-524b-4923-bca2-031078b00805)

Animation:
![3d_visualization](https://github.com/user-attachments/assets/fcb14137-d406-4f77-b634-c4680a131d26)



## Results and Discussion

When multiple wave sources emit waves simultaneously, the resulting wave at any point on the water surface is the sum of the individual waves from each source. This principle, known as **superposition**, leads to regions of:

- **Constructive interference**: where wave crests align, resulting in higher amplitude peaks.
- **Destructive interference**: where a crest from one wave aligns with a trough from another, canceling each other out or reducing amplitude.

The pattern of these high and low amplitude regions depends on the relative phase and amplitude of the waves arriving at each point.

In our setup:

- Four sources are placed at the vertices of a square.
- Each source emits circular waves with the same amplitude, wavelength, and frequency.
- The waves propagate outward in all directions.

Key factors:

- **Distance from each source**: the phase of each wave at a point depends on the distance $r_{i}$ from source $i$.
- **Wave phase**: determined by $kr_i$, where $k = \frac{2\pi}{\lambda}$

### Interference pattern formation

**Near the sources:**

- Close to a source, the wave amplitude is large, and the pattern is dominated by the local wavefronts emanating from that source.
- The wavefronts are roughly circular, and superposition creates concentric interference fringes.

**At the center of the square:**

- The center point of the square is equidistant from all four sources.
- Because of symmetry, the waves from each source arrive in phase (assuming initial phases are zero).
- **Result**: **Constructive interference** occurs at the center, producing a bright, high-amplitude region.

**Along the diagonals and edges:**

- At points along the diagonals, the distances to opposing sources are equal.
- The waves from these sources tend to arrive in phase, creating regular interference fringes.
- At points where phase differences are significant (due to differing distances), partial cancellation or reinforcement occurs, producing a pattern of alternating high and low amplitude regions.

**Far from the sources:**

- As the distance increases, the wavefronts spread out, and interference patterns become more complex.
- The superposition results in a grid-like pattern of bright spots (constructive interference) and dark regions (destructive interference).

**Interpretation:**

- The pattern results from the **phase differences** between waves arriving at each point.
- When the phase difference is an integer multiple of $2\pi$, waves reinforce each other (constructive interference).
- When the phase difference is an odd multiple of $\pi$, waves cancel out (destructive interference).

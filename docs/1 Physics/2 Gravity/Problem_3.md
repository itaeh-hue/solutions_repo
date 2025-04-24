

Analyzing the possible trajectories of a payload released near Earth requires a careful consideration of the initial conditions and the forces acting on it. A simple "parabolic" trajectory, often taught in introductory physics, is a _simplified_ approximation. The real trajectory can be elliptical, hyperbolic, or even a complex combination depending on the payload's initial velocity vector relative to the Earth.

### Step 1: Defining the Physical Context

The motion of a payload released from a moving rocket near Earth is governed by gravity and the initial velocity imparted by the rocket. The possible trajectories follow conic sections:

- **Elliptical** (bound orbit)
- **Parabolic** (escape trajectory)    
- **Hyperbolic** (unbound trajectory)
    

The trajectory classification depends on the **specific energy** of the payload:

$$
\varepsilon = \frac{v^2}{2} - \frac{\mu}{r}
$$

where:

- $v$ is the velocity magnitude,
- $μ=GM$ is Earth's standard gravitational parameter ($G$ is the gravitational constant, $M$ is Earth's mass),
- $r$ is the initial radial distance from Earth's center.

The conditions for trajectory classification:

- **Bound Elliptical Orbit**: $\varepsilon < 0$
- **Parabolic Escape**: $\varepsilon = 0$    
- **Hyperbolic Escape**: $ε>0$

| Energy Condition | Eccentricity | Trajectory |
| ---------------- | ------------ | ---------- |
| $ε<0$            | $0≤e<1$      | Elliptical |
| $ε=0$            | $e=1$        | Parabolic  |
| $ε>0$            | $e>1$        | Hyperbolic |

### Step 2: Equations of Motion


Newton's Law of Gravitation governs the payload’s acceleration:

$$
\mathbf{a} = -\frac{\mu}{r^2} \hat{r}
$$

where $\hat{r}$ is the unit vector pointing radially outward.

The velocity components in a general two-dimensional orbital plane are:

$$
\frac{dv_r}{dt} = \frac{h^2}{r^3} - \frac{\mu}{r^2}
$$

$$
\frac{dv_\theta}{dt} = -\frac{v_r v_\theta}{r}
$$

where:

- $h=rv_{\theta}$ is the specific angular momentum,
- $v_r$ and $v_\theta$ are the radial and tangential velocity components.

### Step 3: Computing the Trajectory Numerically

For numerical simulations, we use **orbital integration** based on the discretized equations:


1. Define initial conditions:

$$
r_0,\quad v_r0,\quad v_\theta0
$$

2. Time-step integration using numerical methods (e.g., Runge-Kutta): 

$$
r_{n+1} = r_n + v_{rn} \Delta t
$$

$$
v_{rn+1} = v_{rn} + \left(\frac{h_n^2}{r_n^3} - \frac{\mu}{r_n^2} \right) \Delta t
$$

$$
v_{\theta n+1} = v_{\theta n} - \frac{v_{rn} v_{\theta n}}{r_n} \Delta t
$$


### Step 4: Applications and Implications

- **Orbital Insertion**: If the payload is released with the right speed and direction, it can be placed in a stable orbit.
    
- **Reentry Scenarios**: If the speed is low and the altitude is not high enough, it will **fall back to Earth** due to drag.
    
- **Escape Trajectory**: If $v \geq v_{\text{escape}}$, the payload will enter an unbound trajectory, escaping Earth’s gravitational influence.

Escape velocity is given by:

$$
v_{\text{escape}} = \sqrt{\frac{2\mu}{r}}
$$

For a release near **Low Earth Orbit (~400 km altitude, r ≈ 6778 km)**:

$$
v_{\text{escape}} \approx 11.2 \text{ km/s}
$$


## Computational model

```Python
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.patches import Circle

# Constants
G = 6.67430e-11  # m^3 kg^-1 s^-2
M = 5.972e24     # kg
R_earth = 6.371e6  # m
mu = G * M

# Initial conditions (release point)
r0 = R_earth + 400e3  # 400 km altitude
theta0 = 0

def compute_trajectory(v0, theta0, max_time=3e4, dt=60):
    """Compute trajectory using polar coordinate equations"""
    # Initial state vector [r, theta, vr, vtheta]
    state = np.array([r0, theta0, 
                      v0 * np.sin(theta0), 
                      v0 * np.cos(theta0) / r0])
    
    # Storage
    positions = []
    
    # Time stepping
    for t in np.arange(0, max_time, dt):
        r, theta, vr, vtheta = state
        
        # Store position (convert to Cartesian)
        x = r * np.cos(theta)
        y = r * np.sin(theta)
        positions.append((x, y))
        
        # Break if collision occurs
        if r <= R_earth:
            break
            
        # Derivatives
        drdt = vr
        dthetadt = vtheta
        dvrdt = r * vtheta**2 - mu/r**2
        dvthetadt = -2 * vr * vtheta / r
        
        # Euler integration (for simplicity - use RK4 for real missions)
        state = state + np.array([drdt, dthetadt, dvrdt, dvthetadt]) * dt
    
    return np.array(positions)

# Velocity thresholds
v_circular = np.sqrt(mu/r0)
v_escape = np.sqrt(2*mu/r0)

# Compute trajectories
elliptical_traj = compute_trajectory(0.9 * v_escape, np.pi/4)
parabolic_traj = compute_trajectory(v_escape, np.pi/4)
hyperbolic_traj = compute_trajectory(1.1 * v_escape, np.pi/4)

# Plotting
plt.figure(figsize=(10, 8))
ax = plt.gca()

# Earth
earth = Circle((0, 0), R_earth, color='#1f77b4', alpha=0.9)
ax.add_patch(earth)

# Trajectories
plt.plot(elliptical_traj[:,0], elliptical_traj[:,1], 'g-', 
         label=f'Elliptical ($v_0 = 0.9v_{{esc}}$ = {0.9*v_escape/1000:.1f} km/s)')
plt.plot(parabolic_traj[:,0], parabolic_traj[:,1], 'b--', 
         label=f'Parabolic ($v_0 = v_{{esc}}$ = {v_escape/1000:.1f} km/s)')
plt.plot(hyperbolic_traj[:,0], hyperbolic_traj[:,1], 'r:', 
         label=f'Hyperbolic ($v_0 = 1.1v_{{esc}}$ = {1.1*v_escape/1000:.1f} km/s)')

# Release point
plt.plot(r0 * np.cos(np.pi/4), r0 * np.sin(np.pi/4), 'k*', markersize=15)

# Formatting
plt.title('Payload Trajectories from 400 km Altitude', pad=20)
plt.xlabel('X Position (m)')
plt.ylabel('Y Position (m)')
plt.legend(loc='upper right')
plt.grid(True)
plt.axis('equal')
plt.xlim(-10*r0, 10*r0)
plt.ylim(-10*r0, 10*r0)

plt.tight_layout()
plt.show()

```
[🖉trajectories_of_a_freely_released_payload_near_Earth.md](https://github.com/user-attachments/files/19889842/trajectories_of_a_freely_released_payload_near_Earth.md)

# Problem 1

## Simulating the Effects of the Lorentz Force

The Lorentz force governs the motion of charged particles in electric and magnetic fields and is fundamental in many areas of physics such as plasma physics, particle accelerators, and astrophysics. It is expressed as:

$$
\mathbf{F} = q\mathbf{E} + q\mathbf{v} \times \mathbf{B}
$$

where  
- $q$ is the charge of the particle,  
- $\mathbf{E}$ is the electric field,  
- $\mathbf{v}$ is the particle velocity,  
- $\mathbf{B}$ is the magnetic field,  
- $\times$ denotes the vector cross product.


>The **electric field $\mathbf{E}$** exerts a force proportional to the charge and field strength, accelerating or decelerating particles along the field direction.

>The **magnetic field $\mathbf{B}$** exerts a force perpendicular to both the particle velocity and the magnetic field, causing circular or helical motion without changing particle speed.

- Combined fields allow complex control of particle motion, including drift phenomena when fields are crossed.

The Lorentz force is fundamental in many areas of physics. Here is where it's key:

- **Particle Accelerators:** Use magnetic fields to steer and focus beams of charged particles.
- **Mass Spectrometers:** Separate ions based on their mass-to-charge ratio by applying electric and magnetic fields.
- **Plasma Confinement Devices (e.g., Tokamaks):** Use magnetic fields to contain hot plasma for fusion research.
- **Astrophysics:** Charged cosmic rays and plasma interact with magnetic fields in space, influencing their trajectories.

The particle's motion follows Newtons's second law:

$$
m \frac{dv}{dt} = \mathbf{F} = q(\mathbf{E} + \mathbf{v} \times \mathbf{B})
$$

The particle acceleration is expressed as:

$$
a = \frac{\mathbf{F}}{m}
$$

where $m$ is the particle's mass.

We implement a numerical integration (e.g., Euler or Runge-Kutta) to update position and velocity over small time steps.

## 2D simulation of particle motion

```Python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

# Constants
q = 1.0  # Charge (Coulombs)
m = 1.0  # Mass (kg)

# Time parameters
dt = 0.01  # Time step
t_max = 10  # Total simulation time
num_steps = int(t_max / dt)

# Initial conditions
v0 = np.array([1.0, 0.0, 0.0])  # Initial velocity
r0 = np.array([0.0, 0.0, 0.0])  # Initial position

def simulate_particle(E_field, B_field, r0, v0, q, m, dt, num_steps):
    """
    Simulate the motion of a charged particle under given electric and magnetic fields.
    """
    r = np.zeros((num_steps, 3))
    v = np.zeros((num_steps, 3))
    r[0] = r0
    v[0] = v0

    for i in range(1, num_steps):
        # Compute Lorentz force
        F = q * (E_field + np.cross(v[i-1], B_field))
        # Update velocity
        v[i] = v[i-1] + (F / m) * dt
        # Update position
        r[i] = r[i-1] + v[i] * dt
    return r, v

# Example scenarios:

# 1. Uniform Magnetic Field (e.g., B along z-axis)
B_uniform = np.array([0, 0, 1])  # Tesla
E_zero = np.array([0, 0, 0])  # No electric field
r_b, v_b = simulate_particle(E_zero, B_uniform, r0, v0, q, m, dt, num_steps)

# 2. Electric and Magnetic Fields (e.g., E along x, B along z)
E_field = np.array([1, 0, 0])  # V/m
B_field = np.array([0, 0, 1])  # Tesla
r_em, v_em = simulate_particle(E_field, B_field, r0, v0, q, m, dt, num_steps)

# 3. Crossed Electric and Magnetic Fields (perpendicular setup)
E_cross = np.array([0, 1, 0])  # V/m
B_cross = np.array([0, 0, 1])  # Tesla
r_cross, v_cross = simulate_particle(E_cross, B_cross, r0, v0, q, m, dt, num_steps)



# 2D Trajectory Plot (x-y plane)
plt.figure(figsize=(12, 4))

# Magnetic field only
plt.subplot(1, 3, 1)
plt.plot(r_b[:,0], r_b[:,1])
plt.title('Magnetic Field Only')
plt.xlabel('x (m)')
plt.ylabel('y (m)')
plt.axis('equal')

# E + B fields
plt.subplot(1, 3, 2)
plt.plot(r_em[:,0], r_em[:,1])
plt.title('E and B Fields')
plt.xlabel('x (m)')
plt.ylabel('y (m)')
plt.axis('equal')

# Crossed E and B
plt.subplot(1, 3, 3)
plt.plot(r_cross[:,0], r_cross[:,1])
plt.title('Crossed E and B')
plt.xlabel('x (m)')
plt.ylabel('y (m)')
plt.axis('equal')

plt.tight_layout()
plt.show()
```
![2D_lorentz](https://github.com/user-attachments/assets/4ae91c9a-fbe6-4d42-b27c-9928887e66d5)


## 3D simulation of particle motion

```Python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

# Constants
q = 1.0  # Charge (Coulombs)
m = 1.0  # Mass (kg)

# Time parameters
dt = 0.01  # Time step
t_max = 10  # Total simulation time
num_steps = int(t_max / dt)

# Initial conditions
v0 = np.array([1.0, 0.0, 0.0])  # Initial velocity
r0 = np.array([0.0, 0.0, 0.0])  # Initial position

def simulate_particle(E_field, B_field, r0, v0, q, m, dt, num_steps):
    """
    Simulate the motion of a charged particle under given electric and magnetic fields.
    """
    r = np.zeros((num_steps, 3))
    v = np.zeros((num_steps, 3))
    r[0] = r0
    v[0] = v0

    for i in range(1, num_steps):
        # Compute Lorentz force
        F = q * (E_field + np.cross(v[i-1], B_field))
        # Update velocity
        v[i] = v[i-1] + (F / m) * dt
        # Update position
        r[i] = r[i-1] + v[i] * dt
    return r, v

# Example scenarios:

# 1. Uniform Magnetic Field (e.g., B along z-axis)
B_uniform = np.array([0, 0, 1])  # Tesla
E_zero = np.array([0, 0, 0])  # No electric field
r_b, v_b = simulate_particle(E_zero, B_uniform, r0, v0, q, m, dt, num_steps)

# 2. Electric and Magnetic Fields (e.g., E along x, B along z)
E_field = np.array([1, 0, 0])  # V/m
B_field = np.array([0, 0, 1])  # Tesla
r_em, v_em = simulate_particle(E_field, B_field, r0, v0, q, m, dt, num_steps)

# 3. Crossed Electric and Magnetic Fields (perpendicular setup)
E_cross = np.array([0, 1, 0])  # V/m
B_cross = np.array([0, 0, 1])  # Tesla
r_cross, v_cross = simulate_particle(E_cross, B_cross, r0, v0, q, m, dt, num_steps)

fig = plt.figure(figsize=(15, 5))

# Magnetic Field only
ax1 = fig.add_subplot(131, projection='3d')
ax1.plot(r_b[:,0], r_b[:,1], r_b[:,2])
ax1.set_title('Magnetic Field Only')
ax1.set_xlabel('x')
ax1.set_ylabel('y')
ax1.set_zlabel('z')

# E + B Fields
ax2 = fig.add_subplot(132, projection='3d')
ax2.plot(r_em[:,0], r_em[:,1], r_em[:,2])
ax2.set_title('E and B Fields')
ax2.set_xlabel('x')
ax2.set_ylabel('y')
ax2.set_zlabel('z')

# Crossed E and B
ax3 = fig.add_subplot(133, projection='3d')
ax3.plot(r_cross[:,0], r_cross[:,1], r_cross[:,2])
ax3.set_title('Crossed E and B')
ax3.set_xlabel('x')
ax3.set_ylabel('y')
ax3.set_zlabel('z')

plt.tight_layout()
plt.show()
```
![3D_lorentz](https://github.com/user-attachments/assets/176460c3-95cf-4342-8efd-2fd88bb89eba)


## Parameter variation and physical phenomena

>**Varying field strengths:**

- Increase $|\mathbf{B}|$ to see tighter circular or helical motion:

![increase_B](https://github.com/user-attachments/assets/58acad92-bb39-431a-907b-2eea92820b2f)


- Increase $|E|$ to see faster drift or acceleration:

![increase_E](https://github.com/user-attachments/assets/9351ce35-90af-4dd4-9aca-49309f58d939)


>**Varying initial velocity**: 

- Change initial speed and direction to see different trajectories (e.g., circular vs. helical):

![increase_v](https://github.com/user-attachments/assets/0984a212-33b3-4b1b-899a-7dc43b44078d)


### Observations

- The **Larmor radius** is the radius of circular motion in a magnetic field. It's expressed as:

$$
r_{L} = \frac{mv_{\perp}}{|q|B}
$$

where $v_{\perp}$ is the component of velocity perpendicular to $\mathbf{B}$.

- The **drift velocity** in crossed $\mathbf{E}$ and $\mathbf{B}$ fields:

$$
\mathbf{v}_{d} = \frac{{\mathbf{E}\times \mathbf{B}}}{B^2}
$$

which results in a steady drift of the particle perpendicular to both fields. 

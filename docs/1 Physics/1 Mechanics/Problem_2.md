# Problem 2

## Pendulum motion: small angles

The motion of a forced damped pendulum is described by the following second-order differential equation:

$$
\frac{d^2\theta}{dt^2} + b \frac{d\theta}{dt} + \frac{g}{L}\sin \theta = A \cos(wt)
$$

This is a second-order differential equation governing the angular displacement $\theta$ of a pendulum with damping and driven forces.

![pendulum](https://github.com/user-attachments/assets/a1606c43-5671-40b9-ab19-a6e47ee5df2f)

Here:

| Notation                 | Description                                                                                                                 |
| ------------------------ | --------------------------------------------------------------------------------------------------------------------------- |
| $\theta$                 | Angular displacement from the vertical (**equilibrium**) position; measured in radians.                                     |
| $\frac{d^2\theta}{dt^2}$ | Angular acceleration of the pendulum.                                                                                       |
| $b$                      | Damping coefficient (which accounts for friction or air resistance).                                                        |
| $\frac{d\theta}{dt}$     | Angular velocity of the pendulum (the rate of change of the angle $\theta$)                                                 |
| $g$                      | Acceleration due to gravity.                                                                                                |
| $L$                      | The length of the pendulum.                                                                                                 |
| $A\cos(\omega t)$        | Represents the external driving force; $A$ is the amplitude, and $\omega$ is the angular frequency of the external forcing. |



For small angles ($\theta$ approaching to $0$ or $\theta \approx 0$), we can use the approximation $\sin(\theta) \approx \theta$. With this, the equation simplifies to:

$$
\frac{d^2\theta}{dt^2} + b \frac{d\theta}{dt} + \frac{g}{L}\sin \theta = A \cos(wt) \implies \frac{d^2\theta}{dt^2} + b \frac{d\theta}{dt} + \frac{g}{L} \theta = A \cos(wt)
$$

## Solving differential equation of a damped pendulum for small-angle approximations

To solve the equation, we first consider the homogeneous part (setting the driving force to zero):

$$
\frac{d^2\theta}{dt^2} + b \frac{d\theta}{dt} + \frac{g}{L} \theta = 0
$$


This is a standard form for a damped harmonic oscillator. To solve this linear differential equation, we assume a solution of the form:

$$
\theta(t) = e^{rt}
$$


Here, $r$ is the constant we want to determine.

The first derivative of our assumed solution is $\frac{d\theta}{dt} = re^{rt}$.
The second is $\frac{d^2\theta}{dt^2} = r^2e^{rt}$.

Substituting, gives

$$
r^2e^{rt} + b(re^{rt}) + \frac{g}{L}(e^{rt}) = 0
$$

Factoring out $e^{rt}$:

$$
e^{rt}(r^2 + br + \frac{g}{L}) = 0
$$


The term $e^{rt}$ does not contribute any solutions since it is always positive for real values of $r$. Therefore, we obtain our characteristic equation from the remaining polynomial:

$$
r^2+br+\frac{g}{L} =0
$$

To find $r$, we need to solve the above equation:


$$
r = \frac{-b\pm \sqrt{ b^2 -4\frac{g}{L} }}{2}
$$

Where $D= b^2 -4\frac{g}{L}$.

Roots and behavior:

- **Underdamped**
	- Condition: $D > 0 \implies b^2 \gt 4 \frac{g}{L}$
	- Result: Two distinct real roots, leading to oscillatory motion with gradually decreasing amplitude (oscillations).
	- Physically, this means the pendulum swings back and forth across the vertical position, with the amplitude decreasing over time due to damping. The oscillations gradually lose energy (due to friction or air resistance), resulting in a motion that resembles a sine wave, but one that progressively decays. This is the pendulum we usually think about, i.e., a swinging pendulum that slowly stops swinging as it loses energy.

- **Critically damped**
	- Condition: $D = 0 \implies b^2 = 4 \frac{g}{L}$
	- Result: Two identical real roots, leading to the system returning to equilibrium as quickly as possible without oscillating.
	- In this case, the pendulum will move towards its lowest point but won't overshoot or undergo any oscillation. It smoothly comes to rest at the vertical position. Take a door as an example: its damping mechanism shuts the door quickly without bouncing back.

- **Overdamped**
	- Condition: $D < 0 \implies b^2 < 4 \frac{g}{L}$
	 - Result: Two complex conjugate roots, leading to a non-oscillatory return toward equilibrium. The system takes longer to return than in the critically damped case.
	 - Here, the pendulum slowly returns to its resting position without any oscillations, typically taking a longer time to settle compared to the critically damped case. For example, a pendulum that is heavily damped (like a long jump rope acting as a pendulum) that gently settles down without swinging back and forth.

## No damping

Below there is a diagram comparing three cases: underdamped pendulum motion, motion with no damping, and critically damped motion: 

```Python
import numpy as np
import matplotlib.pyplot as plt

# Constants
g = 9.81  # acceleration due to gravity (m/s^2)
L = 1.0   # length of the pendulum (m)

# Time array
t = np.linspace(0, 10, 500)

# 1. Underdamped case parameters (b > 0, b^2 < 4g/L)
b_underdamped = 1.0  # Damping Coefficient (low but positive)
omega_d_underdamped = np.sqrt(g / L - (b_underdamped / 2) ** 2)
theta_underdamped = np.exp(-b_underdamped / 2 * t) * np.cos(omega_d_underdamped * t)

# 2. No Damping case parameters (b = 0)
b_no_damping = 0.0  # No Damping
omega_no_damping = np.sqrt(g / L)
theta_no_damping = np.cos(omega_no_damping * t)  # Simple harmonic motion

# 3. Critically Damped case parameters (b^2 = 4g/L)
b_critical = 2.0 * np.sqrt(g / L)  # Adjusted for critical damping
theta_critical = (1 + b_critical*t) * np.exp(-b_critical / 2 * t)  # Critically damped response

# Create plots
plt.figure(figsize=(12, 10))

# Underdamped Motion Plot
plt.subplot(3, 2, 1)
plt.plot(t, theta_underdamped, label='Underdamped', color='blue')
plt.title('Underdamped Motion')
plt.xlabel('Time (s)')
plt.ylabel('Angle (radians)')
plt.grid()
plt.legend()

# Underdamped Phase Diagram
plt.subplot(3, 2, 2)
plt.plot(theta_underdamped[:-1], np.diff(theta_underdamped) / np.diff(t), color='blue')
plt.title('Underdamped Phase Diagram')
plt.xlabel('Angular Position (radians)')
plt.ylabel('Angular Velocity (rad/s)')
plt.grid()

# No Damping Motion Plot
plt.subplot(3, 2, 3)
plt.plot(t, theta_no_damping, label='No Damping', color='green')
plt.title('Pendulum Motion with No Damping')
plt.xlabel('Time (s)')
plt.ylabel('Angle (radians)')
plt.grid()
plt.legend()

# No Damping Phase Diagram
plt.subplot(3, 2, 4)
plt.plot(theta_no_damping[:-1], np.diff(theta_no_damping) / np.diff(t), color='green')
plt.title('No Damping Phase Diagram')
plt.xlabel('Angular Position (radians)')
plt.ylabel('Angular Velocity (rad/s)')
plt.grid()

# Critically Damped Motion Plot
plt.subplot(3, 2, 5)
plt.plot(t, theta_critical, label='Critically Damped', color='orange')
plt.title('Critically Damped Motion')
plt.xlabel('Time (s)')
plt.ylabel('Angle (radians)')
plt.grid()
plt.legend()

# Critically Damped Phase Diagram
plt.subplot(3, 2, 6)
plt.plot(theta_critical[:-1], np.diff(theta_critical) / np.diff(t), color='orange')
plt.title('Critically Damped Phase Diagram')
plt.xlabel('Angular Position (radians)')
plt.ylabel('Angular Velocity (rad/s)')
plt.grid()

# Adjust layout
plt.tight_layout()
plt.show()
```
![no_damping](https://github.com/user-attachments/assets/8c0d4367-fec7-43d3-97e9-56706f6a82c0)



## Underdamped, Critically Damped, and Overdamped

The next diagram compares three cases: underdamped, critically damped, and overdamped motion:

```Python
import numpy as np
import matplotlib.pyplot as plt

# Constants
g = 9.81  # acceleration due to gravity (m/s^2)
L = 1.0   # length of the pendulum (m)

# Time array
t = np.linspace(0, 10, 500)

# Underdamped case parameters (b^2 > 4g/L)
b_underdamped = 1.0
omega_d_underdamped = np.sqrt(g / L - (b_underdamped / 2) ** 2)
theta_underdamped = np.exp(-b_underdamped / 2 * t) * np.cos(omega_d_underdamped * t)

# Critically damped case parameters (b^2 = 4g/L)
b_critically_damped = 2 * np.sqrt(g / L)
theta_critically_damped = np.exp(-b_critically_damped / 2 * t) * (1 + (b_critically_damped / 2) * t)

# Overdamped case parameters (b^2 < 4g/L)
b_overdamped = 3.0  # Choose a value greater than 2*sqrt(g/L)
omega_0_overdamped = np.sqrt((b_overdamped / 2) ** 2 - g / L)
theta_overdamped = np.exp(-b_overdamped / 2 * t) * (np.cosh(omega_0_overdamped * t) - (b_overdamped / (2 * omega_0_overdamped)) * np.sinh(omega_0_overdamped * t))

# Calculate angular velocities for the phase diagrams
omega_underdamped = -b_underdamped / 2 * theta_underdamped - (g / L) * np.sin(theta_underdamped)
omega_critically_damped = np.diff(theta_critically_damped) / np.diff(t)  # Numerical derivative
omega_critically_damped = np.append(omega_critically_damped, omega_critically_damped[-1])  # Append last value for length compatibility
omega_overdamped = -b_overdamped / 2 * theta_overdamped + omega_0_overdamped * np.cosh(omega_0_overdamped * t) 

# Plotting
plt.figure(figsize=(12, 12))

# Underdamped
plt.subplot(3, 2, 1)
plt.plot(t, theta_underdamped, label='Underdamped', color='blue')
plt.title('Underdamped Motion')
plt.xlabel('Time (s)')
plt.ylabel('Angle (radians)')
plt.grid()
plt.legend()

# Underdamped Phase Diagram
plt.subplot(3, 2, 2)
plt.plot(theta_underdamped[:-1], omega_underdamped[:-1], color='blue')
plt.title('Underdamped Phase Diagram')
plt.xlabel('Angular Position (radians)')
plt.ylabel('Angular Velocity (rad/s)')
plt.grid()

# Critically Damped
plt.subplot(3, 2, 3)
plt.plot(t, theta_critically_damped, label='Critically Damped', color='orange')
plt.title('Critically Damped Motion')
plt.xlabel('Time (s)')
plt.ylabel('Angle (radians)')
plt.grid()
plt.legend()

# Critically Damped Phase Diagram
plt.subplot(3, 2, 4)
plt.plot(theta_critically_damped[:-1], omega_critically_damped[:-1], color='orange')
plt.title('Critically Damped Phase Diagram')
plt.xlabel('Angular Position (radians)')
plt.ylabel('Angular Velocity (rad/s)')
plt.grid()

# Overdamped
plt.subplot(3, 2, 5)
plt.plot(t, theta_overdamped, label='Overdamped', color='green')
plt.title('Overdamped Motion')
plt.xlabel('Time (s)')
plt.ylabel('Angle (radians)')
plt.grid()
plt.legend()

# Overdamped Phase Diagram
plt.subplot(3, 2, 6)
plt.plot(theta_overdamped[:-1], omega_overdamped[:-1], color='green')
plt.title('Overdamped Phase Diagram')
plt.xlabel('Angular Position (radians)')
plt.ylabel('Angular Velocity (rad/s)')
plt.grid()

# Adjust layout
plt.tight_layout()
plt.show()
```
![damped](https://github.com/user-attachments/assets/eafa738e-02bb-403b-87e4-058e2aae4807)



## Exploring initial conditions of an underdamped pendulum 

You can also use [this](https://www.myphysicslab.com/pendulum/pendulum-en.html) website to see demonstrations. These are not mine, but I think the resource is useful.

### Changing damping coefficient

```Python
import numpy as np
import matplotlib.pyplot as plt

# Constants
g = 9.81  # acceleration due to gravity (m/s^2)
L = 1.0   # length of the pendulum (m)

# Time array
t = np.linspace(0, 10, 500)

# Plotting
plt.figure(figsize=(12, 8))

b_underdamped = 1.0
omega_d_underdamped = np.sqrt(g / L - (b_underdamped / 2) ** 2)
theta_underdamped = np.exp(-b_underdamped / 2 * t) * (np.cos(omega_d_underdamped * t) + np.sin(omega_d_underdamped * t))
# Underdamped
plt.subplot(3, 1, 1)
plt.plot(t, theta_underdamped, label='Underdamped: b = 1', color='blue')
plt.title('Underdamped Motion')
plt.xlabel('Time (s)')
plt.ylabel('Angle (radians)')
plt.grid()
plt.legend()


b_underdamped = 2.0
omega_d_underdamped = np.sqrt(g / L - (b_underdamped / 2) ** 2)
theta_underdamped = np.exp(-b_underdamped / 2 * t) * (np.cos(omega_d_underdamped * t) + np.sin(omega_d_underdamped * t))
plt.subplot(3, 1, 2)
plt.plot(t, theta_underdamped, label='Underdamped: b = 2', color='violet')
plt.xlabel('Time (s)')
plt.ylabel('Angle (radians)')
plt.grid()
plt.legend()

b_underdamped = 3.0
omega_d_underdamped = np.sqrt(g / L - (b_underdamped / 2) ** 2)
theta_underdamped = np.exp(-b_underdamped / 2 * t) * (np.cos(omega_d_underdamped * t) + np.sin(omega_d_underdamped * t))
# Overdamped
plt.subplot(3, 1, 3)
plt.plot(t, theta_underdamped, label='Underdamped: b = 3', color='red')
plt.xlabel('Time (s)')
plt.ylabel('Angle (radians)')
plt.grid()
plt.legend()

# Adjust layout
plt.tight_layout()
plt.show()
```

![changing_damping_coeff](https://github.com/user-attachments/assets/806569b3-5143-45cc-9504-67bb4aa5a959)

We see that, as we increase the damping coefficient, underdamped motion approaches to critically damped.

Here is another thing. If we continue to increase the damping coefficient, at some point, the graph will disappear (overdamped). The red line below shows the maximum damping I could obtain by increasing the damping coefficient before the graph disappears:

![critically](https://github.com/user-attachments/assets/811e59fe-3ba4-4dad-bb08-3ae29ef11a88)

### Changing pendulum length


```Python
import numpy as np
import matplotlib.pyplot as plt

# Constants
g = 9.81  # acceleration due to gravity (m/s^2)

# Time array
t = np.linspace(0, 10, 500)

# Plotting
plt.figure(figsize=(12, 8))

L = 1.0   # length of the pendulum (m)
b_underdamped = 1.0
omega_d_underdamped = np.sqrt(g / L - (b_underdamped / 2) ** 2)
theta_underdamped = np.exp(-b_underdamped / 2 * t) * (np.cos(omega_d_underdamped * t) + np.sin(omega_d_underdamped * t))
# Underdamped
plt.subplot(3, 1, 1)
plt.plot(t, theta_underdamped, label='L = 1', color='blue')
plt.title('Underdamped Motion')
plt.xlabel('Time (s)')
plt.ylabel('Angle (radians)')
plt.grid()
plt.legend()

L = 2.0   # length of the pendulum (m)
b_underdamped = 1.0
omega_d_underdamped = np.sqrt(g / L - (b_underdamped / 2) ** 2)
theta_underdamped = np.exp(-b_underdamped / 2 * t) * (np.cos(omega_d_underdamped * t) + np.sin(omega_d_underdamped * t))
plt.subplot(3, 1, 2)
plt.plot(t, theta_underdamped, label='L = 2', color='violet')
plt.xlabel('Time (s)')
plt.ylabel('Angle (radians)')
plt.grid()
plt.legend()

L = 3.0   # length of the pendulum (m)
b_underdamped = 1.0
omega_d_underdamped = np.sqrt(g / L - (b_underdamped / 2) ** 2)
theta_underdamped = np.exp(-b_underdamped / 2 * t) * (np.cos(omega_d_underdamped * t) + np.sin(omega_d_underdamped * t))
# Overdamped
plt.subplot(3, 1, 3)
plt.plot(t, theta_underdamped, label='L = 3', color='red')
plt.xlabel('Time (s)')
plt.ylabel('Angle (radians)')
plt.grid()
plt.legend()

# Adjust layout
plt.tight_layout()
plt.show()
```


![changing_length](https://github.com/user-attachments/assets/5c16d2d4-5f5d-44a8-b1a5-5755ea25063b)

## Investigating forced pendulum


```Python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import odeint

# Parameters
g = 9.81      # acceleration due to gravity (m/s^2)
L = 1.0       # length of the pendulum (m)
A_resonance = 1.0  # amplitude of the driving force for resonance
A_chaotic = 0.5     # reduced amplitude for chaotic case
b = 0.1       # damping coefficient

# Natural frequency
omega_0 = np.sqrt(g / L)

# Time values
t = np.linspace(0, 30, 1000)  # Time from 0 to 30 seconds

# Differential equations for the driven pendulum
def model(y, t, A, b, omega):
    theta, omega = y
    dtheta_dt = omega
    domega_dt = -b * omega - (g / L) * np.sin(theta) + A * np.cos(omega * t)
    return [dtheta_dt, domega_dt]

# Case 1: Resonance
omega_resonance = omega_0  # Driving frequency at resonance
initial_conditions = [0.1, 0]  # Starting angle and angular velocity
solution_resonance = odeint(model, initial_conditions, t, args=(A_resonance, b, omega_resonance))
theta_resonance = solution_resonance[:, 0]
omega_resonance_vals = solution_resonance[:, 1]

# Case 2: Chaotic Motion
omega_chaotic = 1.5 * omega_0  # Non-harmonic driving frequency
initial_conditions = [0.1, 0]  # Same starting angle and velocity for comparison
solution_chaotic = odeint(model, initial_conditions, t, args=(A_chaotic, b, omega_chaotic))
theta_chaotic = solution_chaotic[:, 0]
omega_chaotic_vals = solution_chaotic[:, 1]

# Plotting
fig, ax = plt.subplots(2, 2, figsize=(12, 8))

# Resonance plot
ax[0, 0].plot(t, theta_resonance, color='blue')
ax[0, 0].set_title('Resonance Case')
ax[0, 0].set_xlabel('Time (s)')
ax[0, 0].set_ylabel('Angular Displacement (radians)')
ax[0, 0].grid()

# Chaos plot
ax[0, 1].plot(t, theta_chaotic, color='red')
ax[0, 1].set_title('Chaotic Case')
ax[0, 1].set_xlabel('Time (s)')
ax[0, 1].set_ylabel('Angular Displacement (radians)')
ax[0, 1].grid()

# Phase Diagrams
# Resonance Phase Diagram
ax[1, 0].plot(theta_resonance[:-1], omega_resonance_vals[:-1], color='blue')
ax[1, 0].set_title('Resonance Phase Diagram')
ax[1, 0].set_xlabel('Angular Position (radians)')
ax[1, 0].set_ylabel('Angular Velocity (rad/s)')
ax[1, 0].grid()

# Chaos Phase Diagram
ax[1, 1].plot(theta_chaotic[:-1], omega_chaotic_vals[:-1], color='red')
ax[1, 1].set_title('Chaotic Phase Diagram')
ax[1, 1].set_xlabel('Angular Position (radians)')
ax[1, 1].set_ylabel('Angular Velocity (rad/s)')
ax[1, 1].grid()

plt.tight_layout()
plt.show()
```



![driven](https://github.com/user-attachments/assets/2ecf5729-47b0-40e3-a77f-6c100b41798a)


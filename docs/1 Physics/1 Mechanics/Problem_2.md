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

 Take a look at my Python demonstration:

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
theta_underdamped = np.exp(-b_underdamped / 2 * t) * (np.cos(omega_d_underdamped * t) + np.sin(omega_d_underdamped * t))

# Critically damped case parameters (b^2 = 4g/L)
b_critically_damped = 2 * np.sqrt(g / L)
theta_critically_damped = np.exp(-b_critically_damped / 2 * t) * (1 + (b_critically_damped / 2) * t)

# Overdamped case parameters (b^2 < 4g/L)
b_overdamped = 3.0  # Choose a value greater than 2*sqrt(g/L)
omega_0_overdamped = np.sqrt((b_overdamped / 2) ** 2 - g / L)
theta_overdamped = np.exp(-b_overdamped / 2 * t) * (np.cosh(omega_0_overdamped * t) - (b_overdamped / (2*omega_0_overdamped)) * np.sinh(omega_0_overdamped * t))

# Plotting
plt.figure(figsize=(12, 8))

# Underdamped
plt.subplot(3, 1, 1)
plt.plot(t, theta_underdamped, label='Underdamped', color='blue')
plt.title('Underdamped Motion')
plt.xlabel('Time (s)')
plt.ylabel('Angle (radians)')
plt.grid()
plt.legend()

# Critically Damped
plt.subplot(3, 1, 2)
plt.plot(t, theta_critically_damped, label='Critically Damped', color='orange')
plt.title('Critically Damped Motion')
plt.xlabel('Time (s)')
plt.ylabel('Angle (radians)')
plt.grid()
plt.legend()

# Overdamped
plt.subplot(3, 1, 3)
plt.plot(t, theta_overdamped, label='Overdamped', color='green')
plt.title('Overdamped Motion')
plt.xlabel('Time (s)')
plt.ylabel('Angle (radians)')
plt.grid()
plt.legend()

# Adjust layout
plt.tight_layout()
plt.show()
```

 ![damped](https://github.com/user-attachments/assets/de76576f-b96c-4199-a60d-d681c5367afe)


## Exploring initial conditions of an underdamped pendulum 

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

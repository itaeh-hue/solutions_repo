# Problem 2

## Pendulum motion: small angles

The motion of a forced damped pendulum is described by the following second-order differential equation:
$$\frac{d^2\theta}{dt^2} + b \frac{d\theta}{dt} + \frac{g}{L}\sin \theta = A \cos(wt)$$

Here:
- $L$ is the length of a string
- $b$ is the damping coefficient (proportional to the velocity, affects how quickly the pendulum loses energy)
- $g$ is the gravity constant
- $\theta$ is the initial displace angle
- $\omega$ is the angular frequency of the pendulum motion
- $A$ is the amplitude

For small angles ($\theta$ approaching to $0$ or $\theta \approx 0$), we can use the approximation $\sin(\theta) \approx \theta$. Therefore, the equation simplifies to:

$$\frac{d^2\theta}{dt^2} + b \frac{d\theta}{dt} + \frac{g}{L} \theta = A \cos(wt)$$

This is a forced damped harmonic oscillator equation.

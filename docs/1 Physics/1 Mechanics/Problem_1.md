## Deriving basic formulas of the projectile motion

- Suppose a projectile is launched at an angle $\theta$ above the horizontal with an initial velocity $v_{0}$. 
- For simplicity, assume no air resistance.

We can split the motion of the projectile into two components: 

##### **Horizontal motion ($x$-direction)**

$$x(t)=v_{0}\cos (\theta) t$$

---
Deriving:

Starting from the basic kinematic equation of a path: 

$$x(t) = v_{0x}t$$

But since here we calculate solely the $x$ component of the motion, and the projectile is launched at a certain angle $\theta$, we substitute $v_{0x}$ with its **projection** to the $x$-axis, $v_{0x}=v_0 \cos(\theta)t$: 

$$\boxed{x(t)=v_{0}\cos (\theta) t}$$

##### **Vertical motion ($y$-direction)**:

$$\boxed{y(t) = v_{0}\sin(\theta)t-\frac{1}{2}gt^2}$$

where $g$ is the acceleration due to gravity, which brings the projectile back (so the minus sign).

---
Deriving:

Similar to the $x$-axis equation, the path would be given by $y(t)= v_{0y}t$. But this time, the $y$ component of the motion is influenced by the $g$ gravity acceleration:  $y(t)= v_{0y}t - \frac{1}{2}gt^2$.

##### **When the projectile hits the ground**
## Deriving basic formulas of the projectile motion

- Suppose a projectile is launched at an angle $\theta$ above the horizontal with an initial velocity $v_{0}$. 
- For simplicity, assume no air resistance.

We can split the motion of the projectile into two components: 

##### **Horizontal motion ($x$-direction)**

$$x(t)=v_{0}\cos (\theta) t$$

---
Deriving:

Starting from the basic kinematic equation of a path: 

$$x(t) = v_{0x}t$$

But since here we calculate solely the $x$ component of the motion, and the projectile is launched at a certain angle $\theta$, we substitute $v_{0x}$ with its **projection** to the $x$-axis, $v_{0x}=v_0 \cos(\theta)t$: 

$$\boxed{x(t)=v_{0}\cos (\theta) t}$$

##### **Vertical motion ($y$-direction)**:

$$\boxed{y(t) = v_{0}\sin(\theta)t-\frac{1}{2}gt^2}$$

where $g$ is the acceleration due to gravity, which brings the projectile back (so the minus sign).

---
Deriving:

Similar to the $x$-axis equation, the path would be given by $y(t)= v_{0y}t$. But this time, the $y$ component of the motion is influenced by the $g$ gravity acceleration:  $y(t)= v_{0y}t - \frac{1}{2}gt^2$.

##### **When the projectile hits the ground**

To find *when* the projectile hits the ground, we set $y(t)=0$ (altitude zero):

$$0=v_{0}\sin(\theta)t -\frac{1}{2}gt^2$$

$$-\frac{1}{2}gt^2 + v_{0}\sin(\theta) = 0$$

Solving the quadratic equation:

- $D=(v_{0}\sin(\theta))^2$
- $t_{1} = \frac{-v_{0}\sin(\theta)+v_{0}\sin(\theta)}{-1g} = \frac{0}{-g} =0$ - when the projectile is launched;
- $t_{2}=\frac{-v_{0}\sin(\theta)-v_{0}\sin(\theta)}{-g}=\frac{2v_{0}\sin(\theta)}{g}$

So that, **the total flight time of a projectile launched with the velocity $v_{0}$ at the angle $\theta$**:

$$\boxed{t_{f}=\frac{2v_{0}\sin(\theta)}{g}}$$

### The horizontal range

The **range** that the projectile passes, i.e., the **horizontal distance traveled when $t=t_{f}$**, can be found by the formula:

$$R=v_{0x}(t_{f})=v_{0}\cos(\theta)\frac{2v_{0}\sin(\theta)}{g}=\frac{2v_{0}^2 \left( \frac{1}{2} \sin(2\theta)\right) }{g}=\frac{v_{0}^2\sin(2\theta) }{g}$$

$$\boxed{R=\frac{v_{0}^2\sin(2\theta) }{g}}$$

### Conclusions from the equations

- The general form of the range as a function of $\theta$. It demonstrates how varying the launch angle affects the distance traveled. Different values of $v_0$ affect the range as well. As a result, we get a family of parabolic curves when graphed.

- The range $R$ depends on the angle of projection $\theta$ through the sine function, which reaches its maximum at $90^\circ$. However, due to the sinusoidal nature of the $\sin⁡(2\theta)$, the optimal launch angle for maximum horizontal range is $45^\circ$.

Here you can see a GeoGebra graph:

https://www.geogebra.org/calculator/wqefjqxb

To find *when* the projectile hits the ground, we set $y(t)=0$ (altitude zero):

$$0=v_{0}\sin(\theta)t -\frac{1}{2}gt^2$$

$$-\frac{1}{2}gt^2 + v_{0}\sin(\theta) = 0$$
Solving the quadratic equation:

- $D=(v_{0}\sin(\theta))^2$
- $t_{1} = \frac{-v_{0}\sin(\theta)+v_{0}\sin(\theta)}{-1g} = \frac{0}{-g} =0$ - when the projectile is launched;
- $t_{2}=\frac{-v_{0}\sin(\theta)-v_{0}\sin(\theta)}{-g}=\frac{2v_{0}\sin(\theta)}{g}$

So that, **the total flight time of a projectile launched with the velocity $v_{0}$ at the angle $\theta$**:

$$\boxed{t_{f}=\frac{2v_{0}\sin(\theta)}{g}}$$

### The horizontal range

The **range** that the projectile passes, i.e., the **horizontal distance traveled when $t=t_{f}$**, can be found by the formula:

$$R=v_{0x}(t_{f})=v_{0}\cos(\theta)\frac{2v_{0}\sin(\theta)}{g}=\frac{2v_{0}^2 \left( \frac{1}{2} \sin(2\theta)\right) }{g}=\frac{v_{0}^2\sin(2\theta) }{g}$$

$$\boxed{R=\frac{v_{0}^2\sin(2\theta) }{g}}$$

### Conclusions from the equations

- The general form of the range as a function of $\theta$. It demonstrates how varying the launch angle affects the distance traveled. Different values of $v_0$ affect the range as well. As a result, we get a family of parabolic curves when graphed.

- The range $R$ depends on the angle of projection $\theta$ through the sine function, which reaches its maximum at $90^\circ$. However, due to the sinusoidal nature of the $\sin⁡(2\theta)$, the optimal launch angle for maximum horizontal range is $45^\circ$.

Here you can see a GeoGebra graph:

https://www.geogebra.org/calculator/wqefjqxb


## Taking altitude into account

Given everything discussed above, let's add another parameter into the equation: altitude.
- Suppose a projectile is launched from a height $h_{0}$ above the ground.

The equation of the vertical component of the motion then changes:

$$y(t)=h_{0}+v_{0}\sin (\theta) t - \frac{1}{2}gt^2$$

To find the time of flight with this parameter added, we need to solve the above equation at $0$:

$$0=h_{0}+v_{0}\sin (\theta) t - \frac{1}{2}gt^2$$

We get: 


Launch time:
$$t_{1}=\frac{v_{0}\sin(\theta)+\sqrt{ v_{0}^2\sin(\theta)^2 +2gh_{0} }}{g}$$

When the projectile hits the ground: $$t_{2}=\frac{v_{0}\sin(\theta)-\sqrt{ v_{0}^2\sin(\theta)^2 +2gh_{0} }}{g}$$

The horizontal range is then:

$$R=v_{0}t_{2}$$

## Demo

Below is Python code that creates a graph illustrating the motion:

```Python
import numpy as np
import matplotlib.pyplot as plt

def projectile_range(v0, angle, g=9.81):
    """Calculate the range of a projectile."""
    angle_rad = np.radians(angle)  # convert angle to radians
    R = (v0**2 * np.sin(2 * angle_rad)) / g
    return R

# parameters
initial_velocity = 30  # m/s
angles = np.linspace(0, 90, 90)  # Angles from 0° to 90°

# Calculate ranges for different angles
ranges = [projectile_range(initial_velocity, angle) for angle in angles]

# Plotting
plt.figure(figsize=(10, 6))
plt.plot(angles, ranges, label='Range vs Launch Angle', color='b')
plt.title('Projectile Range as a Function of Launch Angle')
plt.xlabel('Angle of Projection (degrees)')
plt.ylabel('Range (m)')
plt.axvline(45, color='r', linestyle='--', label='Optimal Angle (45°)')
plt.xlim(0, 90)
plt.ylim(0, max(ranges) * 1.1)
plt.grid()
plt.legend()
plt.show()
```
![plot](https://github.com/user-attachments/assets/7ef33de2-efbc-41c4-876b-8627743f451d)



### Limitations

The idealized model described above does not account for air resistance, which may be significant in certain applications.

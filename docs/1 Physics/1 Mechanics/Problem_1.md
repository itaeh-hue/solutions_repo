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

$$\frac{1}{2}gt^2 + v_{0}\sin(\theta) = 0$$

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

[Here you can see my GeoGebra graph](https://www.geogebra.org/calculator/wqefjqxb)

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

def projectile_motion(v0, angle, g=9.81):
    """Calculate the trajectory of a projectile."""
    # Convert angle to radians
    angle_rad = np.radians(angle)

    # Time of flight
    t_f = (2 * v0 * np.sin(angle_rad)) / g
    # Time points for plotting
    t = np.linspace(0, t_f, num=500)

    # Calculate x and y positions
    x = v0 * np.cos(angle_rad) * t
    y = v0 * np.sin(angle_rad) * t - 0.5 * g * t**2
    
    return x, y

# Parameters
initial_velocity = 30  # m/s
angles = [15, 30, 45, 60, 75]  # Selected launch angles (degrees)

# Setting up the plot
plt.figure(figsize=(10, 6))

# Loop through each angle to plot the trajectory
for angle in angles:
    x, y = projectile_motion(initial_velocity, angle)
    plt.plot(x, y, label=f'θ = {angle}°')

# Customize the plot
plt.title('Projectile Trajectories for Different Launch Angles')
plt.xlabel('Horizontal Distance (m)')
plt.ylabel('Vertical Distance (m)')
plt.axhline(0, color='gray', lw=0.8)  # Ground line
plt.axvline(0, color='gray', lw=0.8)  # Vertical line
plt.xlim(0, 100)  # X-axis limit
plt.ylim(0, 40)   # Y-axis limit
plt.grid()
plt.legend()
plt.show()
```
![plot](https://github.com/user-attachments/assets/18d2dad4-c2ef-4350-bef8-947afca9ef85)



### Limitations

The idealized model described above does not account for air resistance, which may be significant in certain applications.

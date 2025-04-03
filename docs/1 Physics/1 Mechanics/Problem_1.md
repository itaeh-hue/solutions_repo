## Deriving basic formulas of the projectile motion

- Suppose a projectile is launched at an angle $\theta$ above the horizontal with an initial velocity $v_{0}$. 

For this section, assume **no air resistance**.


#### Horizontal motion ($x$-direction)



- In the absence of air resistance, there is **no horizontal force** acting on the projectile:

$$
F_{x} = 0
$$

Based on the Second Newton's Law of Motion:

$$
\vec{F} = m\vec{a}
$$


Therefore,

$$
m a_{x} = 0 \implies \frac{d^2x}{dt^2}m=0
$$

Since the projectile **does not accelerate** on the $x$-axis, its **immediate velocity** (the first derivative of path) equals to the **initial velocity** with which the projectile has been launched in the first place:

$$
\frac{dx}{dt} = v_{0x}
$$

**The $x$-component of the initial velocity** is

$$
v_{0x} = v_{0}\cos(\theta)
$$

Therefore, the equation of motion of the projectile on the $x$-axis can be described with the following equation:

$$
\boxed{\frac{dt}{dx} = v_{0}\cos(\theta)}
$$
Where $\theta$ is the launch angle of the projectile.

To find the $x$-component of the position of the projectile at time $t$, we need to solve this equation for $x$.

Solving the above differential equation will give us the following:

$$
x(t) = v_{0}\cos(\theta)t + C_{1}
$$


To find $C_{1}$, set the initial condition $x(0) = 0$ (the path at time $0$ is, of course, $0$), and therefore

$$
C_{1} = 0
$$


Thus, 

$$
\boxed{x(t) = v_{0}\cos(\theta)t}
$$

This equation will give us the position of the projectile at the time $t$.

#### Vertical motion ($y$-direction)


- The only force acting *vertically* is the **force of gravity**:


$$
F_{y}=-mg
$$

The projectile doesn't experience any other acceleration and moves until it hits the ground due to gravity. Therefore, **the $y$-component of the projectile motion** can be described with the following equation:


$$
\boxed{\frac{dy}{dt} = v_{0}\sin(\theta)-gt}
$$

Where $v_{0}\sin(\theta)$ is the $y$-component of the initial velocity of the projectile, and $g$ is the acceleration due to gravity (i.e., $\frac{d^2y}{dt^2} = -g$).

This gives us

$$
\boxed{y(t)=v_{0}\sin(\theta)t -\frac{1}{2}gt^2}
$$

##### **When the projectile hits the ground**

To find *when* the projectile hits the ground, we set $y(t)=0$ (altitude zero):


$$
0=v_{0}\sin(\theta)t -\frac{1}{2}gt^2
$$

Rearranging items gives us:


$$
-\frac{1}{2}gt^2 + v_{0}\sin(\theta) = 0
$$

Solving the quadratic equation:

- $D=(v_{0}\sin(\theta))^2$
- $t_{1} = \frac{-v_{0}\sin(\theta)+v_{0}\sin(\theta)}{-1g} = \frac{0}{-g} =0$ - when the projectile is launched;
- $t_{2}=\frac{-v_{0}\sin(\theta)-v_{0}\sin(\theta)}{-g}=\frac{2v_{0}\sin(\theta)}{g}$

So that, **the total flight time of a projectile launched with the velocity $v_{0}$ at the angle $\theta$**:

$$
\boxed{t_{f}=\frac{2v_{0}\sin(\theta)}{g}}
$$

#### The horizontal range

The **range** that the projectile passes, i.e., the **horizontal distance traveled when $t=t_{f}$**, can be found by the formula:

$$R=v_{0x}(t_{f})=v_{0}\cos(\theta)\frac{2v_{0}\sin(\theta)}{g}=\frac{2v_{0}^2 \left( \frac{1}{2} \sin(2\theta)\right) }{g}=\frac{v_{0}^2\sin(2\theta) }{g}$$

$$\boxed{R=\frac{v_{0}^2\sin(2\theta) }{g}}$$

## Investigating how angle and the initial velocity influence the range of the projectile motion


## Varying angles
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
- The general form of the range as a function of $\theta$. It demonstrates how varying the launch angle affects the distance traveled. Different values of $v_0$ affect the range as well. As a result, we get a family of parabolic curves when graphed.

- The range $R$ depends on the angle of projection $\theta$ through the sine function, which reaches its maximum at $90^\circ$. However, due to the sinusoidal nature of the $\sin⁡(2\theta)$, the optimal launch angle for maximum horizontal range is $45^\circ$.

![valying_projectile_angles](https://github.com/user-attachments/assets/88b4eed5-b994-4c2a-aa16-55f1b5ce5f4b)


### Varying initial velocity 


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
angle = 45
initial_velocities = [10, 20, 30, 40, 50] # m/s


# Setting up the plot
plt.figure(figsize=(10, 6))

# Loop velocities each angle to plot the trajectory
for initial_velocity in initial_velocities:
    x, y = projectile_motion(initial_velocity, angle)
    plt.plot(x, y, label=f'v0 = {initial_velocity}')

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


![varying_projectile_velocities](https://github.com/user-attachments/assets/90ff7ba4-a44e-4d3c-a99c-84e1957fb7a7)

## Taking altitude into account

Given everything discussed above, let's add another parameter into the equation: altitude.

- Suppose a projectile is launched from a height $h_{0}$ above the ground.

The equation of the vertical component of the motion then changes:


$$
y(t)=h_{0}+v_{0}\sin (\theta) t - \frac{1}{2}gt^2
$$



To find the time of flight with this parameter added, we need to solve the above equation at $0$:


$$
0=h_{0}+v_{0}\sin (\theta) t - \frac{1}{2}gt^2
$$



Launch time:

$$
t_{1}=\frac{v_{0}\sin(\theta)+\sqrt{ v_{0}^2\sin(\theta)^2 +2gh_{0} }}{g}
$$



When the projectile hits the ground: 

$$
t_{2}=\frac{v_{0}\sin(\theta)-\sqrt{ v_{0}^2\sin(\theta)^2 +2gh_{0} }}{g}
$$



The horizontal range is then:

$$
R=v_{0}t_{2}
$$



### Demonstration

```Python
import numpy as np
import matplotlib.pyplot as plt

def projectile_motion_with_altitude(v0, angle, h0, g=9.81, dt=0.01):
    """Calculate the trajectory of a projectile launched from an altitude."""
    angle_rad = np.radians(angle)

    # Initial velocities
    v_x = v0 * np.cos(angle_rad)
    v_y = v0 * np.sin(angle_rad)
    
    # Initialize lists to store positions and time
    t_values = [0]
    x_values = [0]
    y_values = [h0]  # Start from initial height

    x, y = 0, h0  # Initial position at the height h0
    t = 0  # Initial time

    while y >= 0:  # Continue until the projectile hits the ground (y < 0)
        # Update positions
        x += v_x * dt
        y += v_y * dt
        
        # Update velocities due to gravity
        v_y -= g * dt  # Only vertical component affected by gravity

        # Record values
        t += dt
        t_values.append(t)
        x_values.append(x)
        y_values.append(y)

    return x_values, y_values

# Parameters
initial_velocity = 30  # m/s
angle = 45  # Launch angle (degrees)
altitudes = [-5, 0, 10, 20]  # Different launch heights (above or below ground level)

# Setting up the plot
plt.figure(figsize=(10, 6))

# Loop through different altitudes
for h0 in altitudes:
    x_with_altitude, y_with_altitude = projectile_motion_with_altitude(initial_velocity, angle, h0)
    plt.plot(x_with_altitude, y_with_altitude, label=f'Initial Height: {h0} m')

# Customize the plot
plt.title('Projectile Trajectories at Varying Initial Altitudes')
plt.xlabel('Horizontal Distance (m)')
plt.ylabel('Vertical Distance (m)')
plt.axhline(0, color='gray', lw=0.8)  # Ground line
plt.axvline(0, color='gray', lw=0.8)  # Vertical line
plt.xlim(-10, 150)  # X-axis limit
plt.ylim(0, 60)  # Y-axis limit, accommodating negative heights
plt.grid()
plt.legend()
plt.show()
```
![verying_altitude](https://github.com/user-attachments/assets/58a0a90a-472c-44df-85af-30c9487f4467)

## Exploring how launch altitude influences the horizontal range

## Taking into account air resistance

Let's face it: the above model is not realistic unless you live on a planed with zero-density air (actually, you have no chances to survive there). This section aims to derive equations that do take air resistance into account.

The simplest model considers a drag force proportional to the velocity (*the faster the projectile moves, the stronger the air resistance*), i.e., **linear drag**. 

#### Horizontal motion with air resistance ($x$-direction)

The total force acting on the projectile on the $x$-axis, given air resistance, is as follows:

$$
F_{x} = ma_{x} = -bv_{x}
$$

where $b$ is the drag coefficient.

Given $v_{x} = \frac{dx}{dt}$, and $a_{x} = \frac{d^2x}{dt^2}$, we derive:


$$
\begin{cases}
F_{x} = m \frac{d^2x}{dt^2} \\
F_{x} = -b \frac{dx}{dt}
\end{cases} \implies  m \frac{d^2x}{dt^2} = -b \frac{dx}{dt}
$$

Eliminating mass $m$ from the left gives:

$$
\boxed{\frac{d^2x}{dt^2} = -\frac{b}{m} \frac{dx}{dt}}
$$

To solve this, first separate variables (given that acceleration is the first derivative of velocity):

$$
\frac{dv_{x}}{dt} = -\frac{b}{m} v_{x} \implies \frac{1}{v_{x}} \frac{dv_{x}}{dt} = -\frac{b}{m}
$$

Integrating both parts over $dt$:

$$
\int{\frac{1}{v_{x}} \frac{dv_{x}}{dt} dt} =  \int-\frac{b}{m} dt
$$

Implies:

$$
\int{\frac{1}{v_{x}} dv_{x}} =  -\frac{b}{m} \int dt
$$

Integration gives:

$$
\ln | v_{x} | = -\frac{b}{m} t + C_{3}
$$

Therefore,

$$
v_{x}(t) = v_{0}\cos(\theta)e^{-b/m}t
$$

  
Integrating again to get $x(t)$:

$$
x(t) = \frac{mv_{0}\cos(\theta)}{b}(1-e^{-\frac{b}{m}t}) + C_{4}
$$

If $x(0) =0$, we find $C_{4}=0$.


#### Vertical motion with air resistance ($y$-direction)


The total force acting on the projectile on the $x$-axis, given air resistance, is as follows:


$$
F_{y} = -mg - bv_{y}
$$

where $b$ is the drag coefficient.

Given that $F_{y} = ma_{y}$, $a_{y} = \frac{d^2y}{dy^2}$, and $v_{y} = \frac{dy}{dt}$:


$$
m \frac{d^2y}{dy^2} = -mg - b \frac{dy}{dt}
$$


Eliminating mass gives:


$$
\boxed{\frac{d^2y}{dy^2} = -g - \frac{b}{m} \frac{dy}{dt}}
$$

Reorganizing items and substituting $v_y$, his can be rewritten as


$$
\frac{dv_{y}}{dt} + \frac{b}{m}v_{y} = -g
$$



This is again a first-order linear differential equation, with solution:b



$$
v_{y}(t) = \left( v_{0}\sin(\theta) + \frac{mg}{b} \right)e^{ - \frac{b}{m}t} - \frac{mg}{b}
$$

Integrating gives:

$$
y(t) = -\frac{m}{b}\left( v_{0}\sin(\theta) + \frac{mg}{b}\right)e^{-\frac{b}{m}t }  + \frac{mg}{b}t + C_{5}
$$


With $y(0) =0$: set $C_{5} = 0$.

### Demonstration

```Python
import numpy as np
import matplotlib.pyplot as plt

def projectile_motion_no_drag(v0, angle, g=9.81):
    """Calculate the trajectory of a projectile without air resistance."""
    angle_rad = np.radians(angle)
    
    # Time of flight
    t_f = (2 * v0 * np.sin(angle_rad)) / g
    # Time points for plotting
    t = np.linspace(0, t_f, num=500)

    # Calculate x and y positions
    x = v0 * np.cos(angle_rad) * t
    y = v0 * np.sin(angle_rad) * t - 0.5 * g * t**2
    
    return x, y

def projectile_motion_with_drag(v0, angle, b, g=9.81, dt=0.01):
    """Calculate the trajectory of a projectile with air resistance."""
    angle_rad = np.radians(angle)
    
    # Initial velocities
    v_x = v0 * np.cos(angle_rad)
    v_y = v0 * np.sin(angle_rad)
    
    # Initialize lists to store positions and time
    t_values = [0]
    x_values = [0]
    y_values = [0]
    
    x, y = 0, 0  # Initial position
    t = 0  # Initial time

    while y >= 0:  # Continue until the projectile hits the ground
        # Update positions
        x += v_x * dt
        y += v_y * dt
        
        # Update velocities with drag force
        v_x -= (b * v_x / np.sqrt(v_x**2 + v_y**2)) * dt  # Drag force
        v_y -= (g + (b * v_y / np.sqrt(v_x**2 + v_y**2))) * dt  # Gravitational force + Drag

        # Record values
        t += dt
        t_values.append(t)
        x_values.append(x)
        y_values.append(y)

    return x_values, y_values

# Parameters
initial_velocity = 30  # m/s
drag_coefficient = 0.1  # Drag coefficient
angle = 45  # Launch angle (degrees)

# Calculate projectile motion trajectories
x_no_drag, y_no_drag = projectile_motion_no_drag(initial_velocity, angle)
x_with_drag, y_with_drag = projectile_motion_with_drag(initial_velocity, angle, drag_coefficient)

# Setting up the plot
plt.figure(figsize=(10, 6))
plt.plot(x_no_drag, y_no_drag, label='No Air Resistance', color='blue')

drags = [0.5, 1.0, 1.5, 2.0]
colors = ['darkred', 'red', 'darkorange', 'orange']

# Loop through drag coefficients and colors simultaneously
for drag, c in zip(drags, colors):
    x_with_drag, y_with_drag = projectile_motion_with_drag(initial_velocity, angle, drag)
    plt.plot(x_with_drag, y_with_drag, label=f'Air Resistance: {drag}', color=c, linestyle='--')

# Customize the plot
plt.title('Projectile Trajectories: With Varying Air Resistance vs Without Air Resistance')
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
![varying_air_resistance](https://github.com/user-attachments/assets/ed7a35e0-5b96-44c1-94b3-8051b1416766)

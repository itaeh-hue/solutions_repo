## Definition of Cosmic velocities
### First Cosmic Velocity (Orbital Velocity)

>The **First Cosmic Velocity**, also known as the **Orbital Velocity**, is the minimum velocity required for an object to maintain a stable orbit around a celestial body without falling back to the surface. An object with orbital velocity moves in a circular path under the influence of gravity. 

The formula for the Orbital Velocity $v_{1}$ at a height $h$ above the center of a body with mass $M$ and radius $R$ is given by:

$$
v_{1} = \sqrt{ \frac{GM}{R+h} }
$$


And, for an object on the surface $h = 0$:

$$
v_{1} = \sqrt{ \frac{GM}{R} }
$$

In this case, the mass of the moving body is negligible compared to the mass of the celestial body.

### Second Cosmic Velocity (Escape Velocity)

>The **Second Cosmic Velocity**, also known as the **Escape Velocity**, is the minimum velocity required for an object to break free from a celestial body's gravitational influence and enter space.

The formula for the Escape Velocity $v_{2}$ is given by:

$$
v_{2} = \sqrt{ \frac{2GM}{R} }
$$

### Third Cosmic Velocity

>The **Third Cosmic Velocity** is the speed required to leave the gravitational influence of a star, such as the Sun. This may also require additional energy to overcome the gravitational pull of other celestial bodies, such as planets.

- For the third cosmic velocity $v_{3}$, it's calculated to escape the gravitational pull of the galaxy as well, and can be quite complex as it often depends on the system's dynamics. Generally, it can be expressed in relation to the escape velocity from the solar body's gravitational influence plus the additional velocity needed to overcome the stars in the galaxy.

This velocity can be derived by combining the escape velocity from a planet with the necessary velocity to escape the Sun's gravity assuming you are already in orbit around that planet. The formula is:

$$
v_3 = v_2 + v_{\text{orbital, Sun}}
$$

The orbital velocity of the Sum is given by:

$$
v_{\text{orbital, Sun}} = \sqrt{\frac{GM_{Sun}}{D^2}}
$$

Where $M_{Sun}$ is the mass of the Sun, and $D$ is the distance from the Sun.

### Mathematical Derivation and Parameters

### Deriving the First Cosmic Velocity 

The gravitational force acting on an object is given by:

$$
F = \frac{GMm}{R^2}
$$
The centripetal force required to keep an object moving in a circular path is:

$$
F = \frac{mv^2}{R}
$$
Setting these two forces equal provides us the basis for our derivation of the first cosmic velocity:

$$
\frac{GMm}{R^2} = \frac{mv^2}{R}
$$

Canceling $m$ and rearranging gives:

$$
v_1^2 = \frac{GM}{R} \implies v_1 = \sqrt{\frac{GM}{R}}
$$

### Deriving the Second Cosmic Velocity

For the second cosmic velocity, we can derive it from the conservation of energy. The total mechanical energy must be zero for an escape:

$$
\frac{1}{2}mv^2 - \frac{GMm}{R} = 0 \implies v_2 = \sqrt{\frac{2GM}{R}}
$$

### Parameters

- **Gravitational Constant $G$**
	- $G\approx6.674 \times 10^{-11}m^3kg^{-1}s^{-2}$;

- **Mass $M$**
	- The mass of the celestial body.
	- The higher the mass of a celestial body, the more energy it requires for an object to resist its gravitational field.

- **Radius $R$**: The radius of the celestial body.
	- The smaller the radius of a celestial body, the less energy it requires for an object to resist its gravitational field.
	
- The key parameters that affect cosmic velocities are the mass and radius of the celestial body.
## Calculating Cosmic Velocities for Different Celestial Bodies

Let’s calculate these velocities for Earth, Mars, and Jupiter.

| Parameter                | Earth                    | Mars               | Jupiter           |
| ------------------------ | ------------------------ | ------------------ | ----------------- |
| Mass $M$                 | $5.972 \times 10^{24}kg$ | $6.4171×10^{23}kg$ | $1.898×10^{27}kg$ |
| Radius $R$               | $6.371×10^6m$            | $3.3895×10^6m$     | $6.9911×10^7m$    |
| Orbital Velocity $v_{1}$ | $7909.6808$ m/s          | $3554.7122$ m/s    | $42567.5063$ m/s  |
| Escape Velocity $v_{2}$  | $11185.9779$ m/s         | $5027.1222$ m/s    | $60199.5447$ m/s  |

```Python
import math

def cosmic_velocities(mass, radius):
    G = 6.67430e-11  # Gravitational constant in m^3 kg^-1 s^-2
    orbital = math.sqrt(G * mass / radius)
    escape = math.sqrt(2 * G * mass / radius)
    return [orbital, escape]
    
# Define planet data: name, mass (in kg), radius (in meters)
planets = [
    {"name": "Earth", "mass": 5.972e24, "radius": 6.371e6},
    {"name": "Mars", "mass": 6.4171e23, "radius": 3.3895e6},
    {"name": "Jupiter", "mass": 1.898e27, "radius": 6.9911e7},
    {"name": "Venus", "mass": 4.8675e24, "radius": 6.0518e6},
    {"name": "Mercury", "mass": 3.3011e23, "radius": 2.4397e6}
]

for planet in planets:
    velocities = cosmic_velocities(planet['mass'], planet['radius'])
    v_orbital = velocities[0]
    v_escape = velocities[1]
    print(f'{planet['name']}:')
    print(f'Orbital velocity: {v_orbital:.4f} m/s')
    print(f'Escape velocity: {v_escape:.4f} m/s')
    print()

```

```
Earth:
Orbital velocity: 7909.6808 m/s
Escape velocity: 11185.9779 m/s

Mars:
Orbital velocity: 3554.7122 m/s
Escape velocity: 5027.1222 m/s

Jupiter:
Orbital velocity: 42567.5063 m/s
Escape velocity: 60199.5447 m/s

Venus:
Orbital velocity: 7326.7869 m/s
Escape velocity: 10361.6414 m/s

Mercury:
Orbital velocity: 3005.1350 m/s
Escape velocity: 4249.9027 m/s
```
### Earth

**Orbital Velocity:**

$$
v_1 = \sqrt{\frac{(6.674 \times 10^{-11})(5.972 \times 10^{24})}{6.371 \times 10^6}} \approx 7909.6808 \text{ m/s}
$$

**Escape Velocity:**

$$
v_2 = \sqrt{\frac{2 \times (6.674 \times 10^{-11})(5.972 \times 10^{24})}{6.371 \times 10^6}} \approx 11185.9779 \text{ m/s}

$$

### Mars

**Orbital Velocity:**

$$
v_1 = \sqrt{\frac{(6.674 \times 10^{-11})(6.4171 \times 10^{23})}{3.3895 \times 10^6}} \approx 3554.7122 \text{ m/s}
$$

**Escape Velocity:**

$$
v_2 = \sqrt{\frac{2 \times (6.674 \times 10^{-11})(6.4171 \times 10^{23})}{3.3895 \times 10^6}} \approx 5027.1222 \text{ m/s}
$$

### Jupiter

**Orbital Velocity:**

$$
v_1 = \sqrt{\frac{(6.674 \times 10^{-11})(1.898 \times 10^{27})}{6.9911 \times 10^7}} \approx 42567.5063 \text{ m/s}
$$


**Escape Velocity:**

$$
v_2 = \sqrt{\frac{2 \times (6.674 \times 10^{-11})(1.898 \times 10^{27})}{6.9911 \times 10^7}} \approx 60199.5447 \text{ m/s}
$$
### Importance in Space Exploration

- **Launching Satellites**: The first cosmic velocity (orbital velocity) is fundamental in placing satellites into stable orbits. Understanding it allows engineers to calculate the necessary thrust and trajectory to achieve the desired orbit.
    
- **Missions to Other Planets**: The second cosmic velocity is critical for missions that need to escape Earth's gravity and travel to other celestial bodies. A spacecraft must achieve this velocity to leave Earth and enter interplanetary space.
    
- **Interstellar Travel**: The third cosmic velocity gives insight into escaping a solar system's gravitational pull, which is essential for potential interstellar travel. Exploring technologies like nuclear propulsion or solar sails may eventually allow us to reach these speeds.

## Circular orbits

```Python
import numpy as np
import matplotlib.pyplot as plt

# Define celestial body parameters (radii in meters for visualization, scaled)
celestial_bodies = {
    'Sun': {'radius': 0.5, 'color': 'yellow'},
    'Earth': {'radius': 1.0, 'color': 'blue'},
    'Mars': {'radius': 1.5, 'color': 'red'},
    'Jupiter': {'radius': 2.0, 'color': 'orange'},
}

# Create an array of angles for the circular orbits
angles = np.linspace(0, 2 * np.pi, 360)

# Create a plot
plt.figure(figsize=(8, 8))
plt.axis('equal')
plt.xlim(-2.5, 2.5)
plt.ylim(-2.5, 2.5)

# Plot the Sun
plt.scatter(0, 0, color=celestial_bodies['Sun']['color'], s=300, label='Sun')

# Plot orbits and celestial bodies
for body, params in celestial_bodies.items():
    # Calculate x and y coordinates for the circular orbit
    x_orbit = params['radius'] * np.cos(angles)
    y_orbit = params['radius'] * np.sin(angles)
    
    # Plot the orbit
    plt.plot(x_orbit, y_orbit, linestyle='--', color='gray', alpha=0.5)
    
    # Plot the celestial body at the perimeter of its orbit
    plt.scatter(params['radius'], 0, color=params['color'], s=100, label=body)
    
# Add labels and title
plt.title('Circular Orbits of Celestial Bodies')
plt.xlabel('Distance (arbitrary units)')
plt.ylabel('Distance (arbitrary units)')
plt.axhline(0, color='black',linewidth=0.5, ls='--')
plt.axvline(0, color='black',linewidth=0.5, ls='--')
plt.grid(color = 'gray', linestyle = '--', linewidth = 0.5)
plt.legend()
plt.show()
```


![Pasted image 20250417130534](https://github.com/user-attachments/assets/ccf8ccc0-5e5e-48c2-87ed-35d0dc61f27e)

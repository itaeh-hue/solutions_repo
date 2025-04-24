## Orbital Period and Orbital Radius

## Kepler's Third Law

The **Kepler's Third Law** states that *the square of a planet's orbital period is proportional to the cube of the length of the semi-major axis of its orbit*.

Sounds convoluted. Let's recall some basic concepts from astrodynamics:

>The **orbital period** is the amount of time it takes an astronomical object (say, a planet) to complete an orbit (curved trajectory) around another object.

Recall that the **Kepler's First Law** states that the orbit of a planet is an ellipse.

So, the semi-major axis of an orbit is then the semi-major axis of the ellipse that this orbit represents.

In numerical form, the Kepler's Third Law can be written as follows:

$$
\boxed{T^2 = \frac{4\pi^2}{GM}r^3}
$$

Let's derive this formula.

## Derivation

Alright, let's start with the [Newton's law of universal gravitation](https://en.wikipedia.org/wiki/Newton's_law_of_universal_gravitation) first. It takes the following form:

$$
F = G \frac{mM}{r^2}
$$

where:

| Notion | Description                                                                                              |
| ------ | -------------------------------------------------------------------------------------------------------- |
| $F$    | The force between two masses, $m$ and $M$                                                                |
| $G$    | The [Newtonian constant of gravitation](https://en.wikipedia.org/wiki/Newtonian_constant_of_gravitation) |
| $m$    | The first mass                                                                                           |
| $M$    | The second mass                                                                                          |
| $r$    | The distance between the centers of the masses                                                           |
Derivation of the Newton's Law of gravitation can be found [here](https://imagine.gsfc.nasa.gov/observatories/learning/swift/classroom/law_grav_derivation.html).

Thanks to the Kepler's first law, we know that the motion of one planet (this is how we will abbreviate "astronomical object") relative to its Sun is an ellipse. For now, we will start with circular motion; first, we will write the [centripetal force](https://en.wikipedia.org/wiki/Centripetal_force) - the force that makes a mass follow a curved mass - with the following formula:

$$
F_{c} = \frac{mv^2}{r}
$$

For circular motion, the gravitational force provides the centripetal force, so we can set these two expressions equal:


$$
\frac{GMm}{r^2}=\frac{mv^2}{r} \implies \frac{GM}{r}={v^2}
$$

The orbital speed $v$ can be related to the orbital period $T$ (the time it takes to complete one full orbit) through the circumference of the orbit. The circumference $C$ of a circular orbit is given by:

$$
C = 2\pi r
$$

The speed can be expressed in terms of period $T$:

$$
v = \frac{C}{T} = \frac{2\pi r}{T}
$$

So, returning back to $\frac{GM}{r}={v^2}$ and substituting, we get

$$
\frac{GM}{r}={\left( \frac{2\pi r}{T} \right)^2} \implies \frac{GM}{r}={ \frac{4\pi^2 r^2}{T^2}}
$$

Multiplying both sides by $r$:


$$
GM = \frac{{4\pi^2 r^3}}{T^2}
$$

Finally, rearranging gives us the Kepler's Third Law:

$$
\boxed{T^2 = \frac{4\pi^2}{GM}r^3}
$$

This shows that the **square of the orbital period $T^2$ is proportional to the cube of the orbital radius $r^3$:**

$$
T^2 ∝ r^3
$$

This formula applies not only for circular motion, but also for elliptic. In this case, $r$ is the **semi-major axis of the ellipse**.


## Implications of Kepler's Third Law for Astronomy

### Calculating planetary masses

Kepler's Third Law can be used to determine the mass of a celestial body if the orbital period and distance of its orbiting bodies are known.

$$
T^2 = \frac{4\pi^2}{GM}r^3 \implies M= \frac{4\pi^2r^3}{GT^2}
$$

This is particularly valuable in binary star systems, where two stars orbit a common center of mass. By analyzing their orbital periods and distances, astronomers can calculate their masses, enhancing our understanding of stellar evolution and the fundamental properties of stars.

### Determining distances

Kepler's Third Law can also be used to determine the relative distances of celestial bodies. For example, by knowing the orbital period of a planet and applying the law, astronomers can infer its distance from the Sun in units of the semi-major axis (in astronomical units, where 1 AU is the average distance from the Earth to the Sun).

### Understanding orbital dynamics

The relationship encapsulated in Kepler's Third Law provides insights into the stability and behavior of orbits. It predicts how changing a planet's distance from the star affects its orbital period; for example, if a planet were to migrate inward, its orbital period would decrease, affecting climatic and environmental conditions on that planet.
## Real-World Examples

### The Moon's orbit around Earth

The Moon orbits Earth with an average distance of about $384,400$ km and a period of approximately $27.3$ days. Using Kepler's Third Law, we can check the consistency of these values:

1. Given data:

| Data       | Value                                           |
| ---------- | ----------------------------------------------- |
| Period $T$ | $\approx 27.3$ days $\approx 2,359,200$ seconds |
| Radius $r$ | $\approx 384,400$ km                            |

2. Calculations:

| Data  | Value                          |
| ----- | ------------------------------ |
| $T^2$ | $\approx 5.57\times10^{12}s^2$ |
| $r^3$ | $\approx 5.67\times10^{25}m^3$ |

3. Using $G\approx6.674 \times 10^{-11}m^3kg^{-1}s^{-2}$, calculating the expected mass of Earth:

$$
M= \frac{4\pi^2r^3}{GT^2} \approx \frac{4\pi^2\cdot5.67\times10^{25}}{6.674\times 10^{-11}\cdot 5.57 \times 10^{12}} \approx 5.97 \times 10^{24}kg
$$

This mass aligns closely with the known mass of Earth, demonstrating the reliability of Kepler's Third Law.

## Computational mode

```Python
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.animation as animation

# Constants
G = 6.67430e-11  # Gravitational constant in m^3 kg^-1 s^-2
mass_sun = 1.989e+30  # Mass of the Sun in kilograms
mass_earth = 5.972e+24  # Mass of the Earth in kilograms
mass_moon = 7.348e+22  # Mass of the Moon in kilograms

# Orbital parameters
distance_earth = 1.496e+11  # Distance from Sun to Earth in meters (1 AU)
distance_moon = 3.844e+8     # Distance from Earth to Moon in meters
T_earth = np.sqrt((4 * np.pi**2 * distance_earth**3) / (G * mass_sun))  # Orbital period of Earth
T_moon = np.sqrt((4 * np.pi**2 * distance_moon**3) / (G * mass_earth))  # Orbital period of Moon

# Simulation parameters
num_frames = 180  # Number of frames for animation
time = np.linspace(0, T_earth, num_frames)

# Position calculations
earth_x = distance_earth * np.cos(2 * np.pi * time / T_earth)
earth_y = distance_earth * np.sin(2 * np.pi * time / T_earth)

moon_x = earth_x + distance_moon * np.cos(2 * np.pi * time / T_moon)
moon_y = earth_y + distance_moon * np.sin(2 * np.pi * time / T_moon)

# Create figure and axis
fig, ax = plt.subplots(figsize=(8, 8))
ax.set_xlim(-1.6e11, 1.6e11)
ax.set_ylim(-1.6e11, 1.6e11)
ax.set_aspect('equal')
ax.set_title("Simulation of Circular Orbits")
ax.set_xlabel("Distance (m)")
ax.set_ylabel("Distance (m)")

# Initialize the Sun, Earth, and Moon
sun, = ax.plot(0, 0, 'yo', markersize=12)  # Sun in yellow
earth, = ax.plot([], [], 'bo', markersize=6)  # Earth in blue
moon, = ax.plot([], [], 'gray', markersize=4)  # Moon in gray

# Animation update function
def update(frame):
    # Update Earth position
    earth.set_data(earth_x[frame], earth_y[frame])
    # Update Moon position
    moon.set_data(moon_x[frame], moon_y[frame])
    return earth, moon

# Create animation
ani = animation.FuncAnimation(fig, update, frames=num_frames, interval=50, blit=True)

# To save the animation as a .gif, Uncomment the next line
# ani.save('circular_orbits.gif', writer='imagemagick', fps=20)

plt.show()
```
![orbits](https://github.com/user-attachments/assets/c215dd42-a03e-4fdb-be02-761ec0d88ea1)


## Plot T^3 vs r^3

```Python
import matplotlib.pyplot as plt
import numpy as np

# Data for Mercury, Venus, Earth, Mars
planets = ['Mercury', 'Venus', 'Earth', 'Mars']
T = np.array([0.241, 0.615, 1.000, 1.881])  # Orbital period in years
r = np.array([0.387, 0.723, 1.000, 1.524])  # Semi-major axis in AU

T2 = T**2
r3 = r**3

plt.figure(figsize=(7, 5))
plt.scatter(r3, T2, color='royalblue')

# Annotate each planet
for i, planet in enumerate(planets):
    plt.annotate(planet, (r3[i], T2[i]), textcoords="offset points", xytext=(5,5), ha='left')

# Plot y=x line for reference (since T^2 = r^3 in AU and years)
x = np.linspace(0, 4, 100)
plt.plot(x, x, 'k--', label=r'$T^2 = r^3$')

plt.xlabel(r'$r^3$ (AU$^3$)')
plt.ylabel(r'$T^2$ (yr$^2$)')
plt.title(r'Kepler\'s Third Law: $T^2$ vs $r^3$ for Inner Planets')
plt.legend()
plt.grid(True)
plt.tight_layout()
plt.show()
```
![t_2_r3](https://github.com/user-attachments/assets/5308e919-ec79-4e03-87e6-de87b52096a2)


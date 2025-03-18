# Orbital Period and Orbital Radius

## 1. Theortical Foundation

### Kepler's Third Law
Kepler’s Third Law states that the square of the orbital period (T) of a planet is proportional to the cube of the semi-major axis (a) of its orbit:

$$
T^2 \propto a^3
$$

For a circular orbit, this relationship can be derived using Newton’s law of universal gravitation and the centripetal force equation.

### Deriving the Relationship
For a body of mass $$ m $$ orbiting around a central mass $$ M $$ (such as a planet around the Sun), the gravitational force provides the necessary centripetal force:

$$
F_g = F_c
$$

Using Newton’s law of universal gravitation:

$$
F_g = \frac{G M m}{r^2}
$$

And the centripetal force equation:

$$
F_c = \frac{m v^2}{r}
$$

Since these forces are equal:

$$
\frac{G M m}{r^2} = \frac{m v^2}{r}
$$

Canceling mass $$ m $$ and rearranging:

$$
G M = v^2 r
$$

Since the orbital velocity is related to the period by:

$$
 v = \frac{2 \pi r}{T}
$$

Substituting this into the equation:

$$
G M = \frac{4 \pi^2 r^2}{T^2} \cdot r
$$

Rearranging:

$$
T^2 = \frac{4 \pi^2}{G M} r^3
$$

This confirms Kepler’s Third Law: 

$$
T^2 \propto r^3
$$

where the proportionality constant depends on the mass of the central body.

## 2. Implications in Astronomy

- **Determining Masses**: Using this law, astronomers can estimate the mass of celestial bodies by observing orbital periods and radii.
- **Measuring Distances**: By knowing the period of a satellite or moon, the orbital radius can be determined.
- **Orbital Resonances**: Planets and moons in stable orbits follow these principles, leading to predictable resonances and interactions.

## 3. Real-World Examples

- **Moon's Orbit around Earth**:
  - Orbital radius: $$ 3.84 \times 10^8 $$ m
  - Orbital period: $$ 2.36 \times 10^6 $$ s (27.3 days)
  - Verifying Kepler’s law for Earth-Moon system
- **Planets in the Solar System**:
  - The orbits of planets around the Sun all follow the $$ T^2 \propto r^3 $$ relationship, confirming Newtonian mechanics.

## 4. Computational Simulation
### Python Model for Circular Orbits

```python
import numpy as np
import matplotlib.pyplot as plt

def kepler_relation(radius, mass_central, G=6.67430e-11):
    """
    Compute the orbital period using Kepler's Third Law for circular orbits.
    """
    return 2 * np.pi * np.sqrt(radius**3 / (G * mass_central))

# Data: Orbital radius vs. orbital period for the Solar System planets
# Mass of the Sun (kg)
M_sun = 1.989e30 

# Orbital radii (meters) and observed periods (seconds)
planetary_data = {
    "Mercury": (5.79e10, 7.6e6),
    "Venus": (1.08e11, 1.94e7),
    "Earth": (1.496e11, 3.154e7),
    "Mars": (2.279e11, 5.94e7),
    "Jupiter": (7.785e11, 3.74e8),
    "Saturn": (1.433e12, 9.29e8),
    "Uranus": (2.877e12, 2.65e9),
    "Neptune": (4.503e12, 5.2e9)
}

# Extracting data for analysis
radii = np.array([planetary_data[planet][0] for planet in planetary_data])
periods = np.array([planetary_data[planet][1] for planet in planetary_data])

# Compute theoretical periods using Kepler's Third Law
calculated_periods = np.array([kepler_relation(r, M_sun) for r in radii])

# Graph: Period squared vs. Radius cubed
plt.figure(figsize=(8, 6))
plt.plot(radii**3, periods**2, 'o', label='Observed Data')
plt.plot(radii**3, calculated_periods**2, '-', label='Kepler Prediction', alpha=0.7)
plt.xlabel("Orbital Radius Cubed (m^3)")
plt.ylabel("Orbital Period Squared (s^2)")
plt.title("Kepler's Third Law: Period vs. Radius")
plt.legend()
plt.grid()
plt.show()
```

## 5. Extending to Elliptical Orbits
While Kepler's Third Law holds for circular orbits, it also applies to elliptical orbits by using the **semi-major axis** instead of the radius:

$$
T^2 \propto a^3
$$

- The semi-major axis replaces the circular orbital radius.
- The same proportionality constant applies for the system.
- This allows calculations for comets, exoplanets, and binary star systems.

## 6. Conclusion
This study highlights the profound connection between orbital period and radius, derived from Newtonian mechanics and verified through celestial observations. By modeling circular orbits computationally, we validate Kepler’s law and explore its astronomical significance. Future extensions could include elliptical orbits, gravitational perturbations, and general relativity corrections.

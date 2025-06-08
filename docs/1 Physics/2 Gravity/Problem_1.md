1. Derivation of Kepler's Third Law for Circular Orbits

We begin with Newton's Law of Gravitation and the concept of centripetal force.

Gravitational Force:



Centripetal Force:



Equating these for a body in circular orbit:


The orbital period  is:


Substituting for :


This is Kepler's Third Law:


2. Astronomical Implications

Mass Determination: Given  and , one can solve for the mass  of the central body:


Distance Estimation: Given the orbital period and central mass, one can determine the orbital radius.

3. Real-World Examples

Moon-Earth System:

Radius:  m

Period:  days

This data allows calculation of Earth's mass using Kepler's Law.

Planetary Orbits:

For planets in the Solar System,  holds when using the semi-major axis  for elliptical orbits.

4. Python Simulation of Circular Orbits

import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11  # m^3 kg^-1 s^-2
M_sun = 1.989e30  # kg
AU = 1.496e11  # meters
YEAR_SEC = 365.25 * 24 * 3600  # seconds

# Planetary distances in AU and conversion to meters
radii_au = np.array([0.39, 0.72, 1.0, 1.52, 5.2, 9.58, 19.2, 30.05])
radii_m = radii_au * AU

# Orbital periods in seconds using Kepler's Law
T_sec = 2 * np.pi * np.sqrt(radii_m**3 / (G * M_sun))
T_yrs = T_sec / YEAR_SEC

# T^2 and r^3 for verification
T2 = T_yrs**2
r3 = radii_au**3

# Plot T^2 vs r^3
plt.figure(figsize=(12, 5))

plt.subplot(1, 2, 1)
plt.plot(r3, T2, 'bo-', label='Kepler Data')
plt.plot(r3, r3, 'r--', label='T^2 = r^3')
plt.xlabel('r^3 (AU^3)')
plt.ylabel('T^2 (years^2)')
plt.title("Kepler's Third Law")
plt.legend()
plt.grid(True)

# Plot orbits
theta = np.linspace(0, 2 * np.pi, 100)
plt.subplot(1, 2, 2)
for r in radii_au:
    plt.plot(r * np.cos(theta), r * np.sin(theta), label=f'{r:.2f} AU')
plt.plot(0, 0, 'yo', label='Sun')
plt.axis('equal')
plt.xlabel('x (AU)')
plt.ylabel('y (AU)')
plt.title('Circular Orbits')
plt.legend()
plt.grid(True)

plt.tight_layout()
plt.show()

5. Extension to Elliptical Orbits

For elliptical orbits, the same relationship holds using the semi-major axis :



This allows analysis of:

Eccentric comets

Binary star systems

Exoplanets with non-circular orbits

6. Conclusion

Kepler's Third Law provides a powerful tool in celestial mechanics.

Real and simulated data validate .

The law extends naturally to elliptical orbits using the semi-major axis.
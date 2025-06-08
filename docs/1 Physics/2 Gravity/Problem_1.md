# Problem 1
Orbital Mechanics: Circular Orbits and Kepler's Third Law
1. Deriving the Period-Radius Relationship
For a body of mass 
𝑚
m in a circular orbit around a much larger body of mass 
𝑀
M, the gravitational force provides the necessary centripetal force:

𝐹
gravity
=
𝐺
𝑀
𝑚
𝑟
2
,
𝐹
centripetal
=
𝑚
𝑣
2
𝑟
F 
gravity
​
 = 
r 
2
 
GMm
​
 ,F 
centripetal
​
 = 
r
mv 
2
 
​
 
Equating both:

𝐺
𝑀
𝑚
𝑟
2
=
𝑚
𝑣
2
𝑟
⇒
𝑣
2
=
𝐺
𝑀
𝑟
r 
2
 
GMm
​
 = 
r
mv 
2
 
​
 ⇒v 
2
 = 
r
GM
​
 
The orbital period 
𝑇
T is related to the orbital speed 
𝑣
v by:

𝑇
=
2
𝜋
𝑟
𝑣
⇒
𝑇
2
=
4
𝜋
2
𝑟
2
𝑣
2
T= 
v
2πr
​
 ⇒T 
2
 = 
v 
2
 
4π 
2
 r 
2
 
​
 
Substituting for 
𝑣
2
v 
2
 :

𝑇
2
=
4
𝜋
2
𝑟
3
𝐺
𝑀
T 
2
 = 
GM
4π 
2
 r 
3
 
​
 
This is Kepler’s Third Law for circular orbits:

𝑇
2
∝
𝑟
3
T 
2
 ∝r 
3
 
2. Astronomical Implications
Determining Planetary Masses: Rearranging the equation:

𝑀
=
4
𝜋
2
𝑟
3
𝐺
𝑇
2
M= 
GT 
2
 
4π 
2
 r 
3
 
​
 
We can determine the mass of a central object (like Earth or the Sun) using the orbital radius and period of a satellite or planet.

Measuring Distances: Given a known mass, if we measure the orbital period, we can compute the orbital radius — a powerful tool for celestial mapping.

3. Real-World Examples
3.1 Moon Orbiting Earth
Average radius 
𝑟
≈
384
,
400
r≈384,400 km

Orbital period 
𝑇
≈
27.3
T≈27.3 days

Using the formula, the computed mass of Earth aligns well with known values.

3.2 Planets Around the Sun
Using Kepler's law normalized to Earth's orbit:

(
𝑇
𝑇
⊕
)
2
=
(
𝑟
𝑟
⊕
)
3
( 
T 
⊕
​
 
T
​
 ) 
2
 =( 
r 
⊕
​
 
r
​
 ) 
3
 
This approximation is accurate for all planets assuming circular orbits.

4. Python Simulation and Verification
Below is a Python script using matplotlib and numpy.

python
Kopyala
Düzenle
import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11  # gravitational constant (m^3 kg^-1 s^-2)
M = 1.989e30     # mass of Sun (kg)

# Simulate orbits at different radii (in AU converted to meters)
radii_au = np.array([0.39, 0.72, 1.0, 1.52, 5.2, 9.58, 19.2, 30.05])
radii_m = radii_au * 1.496e11  # AU to meters

# Compute periods using Kepler's third law
T = 2 * np.pi * np.sqrt(radii_m**3 / (G * M))  # in seconds
T_years = T / (60 * 60 * 24 * 365.25)

# Verify T^2 vs r^3
T2 = T_years**2
r3 = radii_au**3

# Plotting
plt.figure(figsize=(10, 5))

# T^2 vs r^3
plt.subplot(1, 2, 1)
plt.plot(r3, T2, 'o-')
plt.xlabel('$r^3$ (AU³)')
plt.ylabel('$T^2$ (yr²)')
plt.title('Kepler’s Third Law: $T^2$ vs $r^3$')

# Orbit visualization
theta = np.linspace(0, 2*np.pi, 100)
plt.subplot(1, 2, 2)
for r in radii_au:
    x = r * np.cos(theta)
    y = r * np.sin(theta)
    plt.plot(x, y, label=f'{r:.2f} AU')
plt.plot(0, 0, 'yo', label='Sun')
plt.axis('equal')
plt.title('Circular Orbits')
plt.xlabel('x (AU)')
plt.ylabel('y (AU)')
plt.legend()
plt.tight_layout()
plt.show()
5. Elliptical Orbits and Generalization
Kepler’s Third Law still holds for elliptical orbits when using the semi-major axis 
𝑎
a in place of radius:

𝑇
2
=
4
𝜋
2
𝑎
3
𝐺
𝑀
T 
2
 = 
GM
4π 
2
 a 
3
 
​
 
This generalization is critical in modeling:

Comets

Binary stars

Exoplanets

6. Summary
We derived Kepler’s Third Law from Newtonian mechanics.

This relationship is crucial for celestial navigation and astrophysical measurements.

Simulation confirms 
𝑇
2
∝
𝑟
3
T 
2
 ∝r 
3
 .

The law extends naturally to elliptical orbits.


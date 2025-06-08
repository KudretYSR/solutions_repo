1. Theoretical Derivation
Kepler’s Third Law, in its classical form, states that for planets orbiting the Sun:

𝑇
2
∝
𝑟
3
T 
2
 ∝r 
3
 
Where:

𝑇
T is the orbital period,

𝑟
r is the radius of the orbit (assumed circular here).

Derivation using Newton’s Laws
From Newton’s Law of Universal Gravitation and centripetal force:

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
 
Equating the two forces:

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
 
Now, orbital period 
𝑇
=
2
𝜋
𝑟
𝑣
T= 
v
2πr
​
 :

𝑇
=
2
𝜋
𝑟
𝑟
𝐺
𝑀
=
2
𝜋
𝑟
3
𝐺
𝑀
⇒
𝑇
2
=
4
𝜋
2
𝐺
𝑀
𝑟
3
T=2πr 
GM
r
​
 
​
 =2π 
GM
r 
3
 
​
 
​
 ⇒T 
2
 = 
GM
4π 
2
 
​
 r 
3
 
This proves the relationship 
𝑇
2
∝
𝑟
3
T 
2
 ∝r 
3
  for circular orbits.

2. Real-World Implications
Moon-Earth System: Measuring the Moon’s period and distance allows calculating Earth’s mass.

Solar System: Astronomers determine planetary distances from the Sun using observed orbital periods.

Exoplanet Discovery: Transit observations give 
𝑇
T, allowing estimation of 
𝑟
r and host star mass.

3. Python Simulation: Circular Orbits and Kepler’s Law
python
Kopyala
Düzenle
import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11  # m^3 kg^-1 s^-2
M = 1.989e30     # kg, mass of the Sun

# Radii from 0.1 AU to 30 AU
radii_AU = np.linspace(0.1, 30, 500)
radii_m = radii_AU * 1.496e11  # Convert AU to meters

# Compute periods using T = 2π sqrt(r^3 / GM)
periods_sec = 2 * np.pi * np.sqrt(radii_m**3 / (G * M))
periods_years = periods_sec / (60 * 60 * 24 * 365.25)

# Verify Kepler's Law: T^2 vs r^3
T2 = periods_years**2
R3 = radii_AU**3

# Plotting
plt.figure(figsize=(12, 5))

plt.subplot(1, 2, 1)
plt.plot(radii_AU, periods_years)
plt.title("Orbital Period vs Radius")
plt.xlabel("Orbital Radius (AU)")
plt.ylabel("Orbital Period (Years)")
plt.grid(True)

plt.subplot(1, 2, 2)
plt.plot(R3, T2, color='green')
plt.title("Kepler's Third Law: $T^2$ vs $r^3$")
plt.xlabel("r³ (AU³)")
plt.ylabel("T² (Years²)")
plt.grid(True)

plt.tight_layout()
plt.show()
4. Discussion on Elliptical Orbits
Kepler’s Third Law also holds for elliptical orbits when using the semi-major axis 
𝑎
a:

𝑇
2
=
4
𝜋
2
𝐺
(
𝑀
+
𝑚
)
𝑎
3
T 
2
 = 
G(M+m)
4π 
2
 
​
 a 
3
 
This is especially important for binary star systems or moons where the mass of the orbiting body isn't negligible. It also applies to artificial satellites and moons of other planets.

5. Conclusion
Kepler’s Third Law provides a foundational relationship in celestial mechanics. From planet discovery to calculating stellar masses, the 
𝑇
2
∝
𝑟
3
T 
2
 ∝r 
3
  law, rooted in Newtonian physics, is central to our understanding of orbital dynamics.

This relationship simplifies the modeling and prediction of orbits across the universe, from our Moon to exoplanets light-years away.
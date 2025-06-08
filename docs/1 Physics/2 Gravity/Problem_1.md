Problem 1
🌌 Kepler’s Third Law for Circular Orbits – A Simulation and Analysis
📐 Derivation: Orbital Period and Radius Relationship
For a body of mass 
𝑚
m orbiting a much larger mass 
𝑀
M in a circular orbit, the gravitational force provides the necessary centripetal force:

𝐹
gravity
=
𝐹
centripetal
⇒
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
F 
gravity
​
 =F 
centripetal
​
 ⇒ 
r 
2
 
GMm
​
 = 
r
mv 
2
 
​
 
Cancel 
𝑚
m and solve for orbital speed 
𝑣
v:

𝑣
=
𝐺
𝑀
𝑟
v= 
r
GM
​
 
​
 
The orbital period 
𝑇
T (time to complete one orbit) is:

𝑇
=
2
𝜋
𝑟
𝑣
=
2
𝜋
𝑟
⋅
1
𝐺
𝑀
𝑟
=
2
𝜋
𝑟
3
𝐺
𝑀
T= 
v
2πr
​
 =2πr⋅ 
r
GM
​
 
​
 
1
​
 =2π 
GM
r 
3
 
​
 
​
 
Squaring both sides:

𝑇
2
=
4
𝜋
2
𝐺
𝑀
⋅
𝑟
3
T 
2
 = 
GM
4π 
2
 
​
 ⋅r 
3
 
🌠 Implications for Astronomy
This tells us:

Orbital period squared is proportional to the orbital radius cubed.

Knowing a satellite’s period gives us its orbital radius (and vice versa).

We can deduce the mass 
𝑀
M of a central body using observed orbits.

Applications:
Measuring planetary masses from satellite orbits.

Determining distances in planetary systems and exoplanets.

Verifying Newtonian mechanics in astronomy.

🌍 Real-World Examples
1. The Moon and Earth
Radius ≈ 384,400 km

Period ≈ 27.3 days

Plugging into:

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
T 
2
 = 
GM
4π 
2
 
​
 r 
3
 
Confirms the Moon's orbital parameters match Earth's mass (~
5.97
×
10
24
5.97×10 
24
  kg).

2. Planets in the Solar System
Using Astronomical Units (AU) and Earth years:

𝑇
2
=
𝑟
3
(
if 
𝑀
=
𝑀
⊙
)
T 
2
 =r 
3
 (if M=M 
⊙
​
 )
💻 Python Simulation
Below is a Python notebook script that simulates orbits and plots 
𝑇
2
T 
2
  vs. 
𝑟
3
r 
3
 .

python
Kopyala
Düzenle
import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11  # m^3/kg/s^2
M = 1.989e30     # Mass of the Sun in kg

# Orbital radii (m) from 0.4 AU to 30 AU
AU = 1.496e11
radii = np.linspace(0.4, 30, 100) * AU

# Compute periods using T = 2π√(r^3 / GM)
periods = 2 * np.pi * np.sqrt(radii**3 / (G * M))

# Convert to Earth years
periods_years = periods / (60 * 60 * 24 * 365.25)

# Plot T^2 vs r^3
plt.figure(figsize=(8, 6))
plt.plot(radii**3, periods**2, label=r'$T^2 \propto r^3$')
plt.xlabel('Orbital Radius Cubed $r^3$ (m³)')
plt.ylabel('Orbital Period Squared $T^2$ (s²)')
plt.title('Kepler’s Third Law Verification (Circular Orbits)')
plt.grid(True)
plt.legend()
plt.tight_layout()
plt.show()

# Log-log plot to verify power law
plt.figure(figsize=(8, 6))
plt.loglog(radii, periods, label='T vs r (log-log)')
plt.xlabel('Orbital Radius r (m)')
plt.ylabel('Orbital Period T (s)')
plt.title('Log-Log Plot: Orbital Period vs Radius')
plt.grid(True, which='both')
plt.legend()
plt.tight_layout()
plt.show()
📈 Graphical Results
The graphs show:

A straight line in the 
𝑇
2
T 
2
  vs 
𝑟
3
r 
3
  plot → confirms 
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

Log-log plot slope ≈ 1.5 → confirms power-law with exponent 
3
2
2
3
​
 .

 Extensions to Elliptical Orbits
Kepler’s Third Law for elliptical orbits uses the semi-major axis 
𝑎
a:

𝑇
2
=
4
𝜋
2
𝐺
𝑀
𝑎
3
T 
2
 = 
GM
4π 
2
 
​
 a 
3
 
Implications:

Valid for any bound (elliptical) orbit.

Used in orbital mechanics for satellites, moons, and exoplanets.

For elliptical orbits:

𝑟
r varies → speed changes along the orbit (faster near periapsis).

But 
𝑇
T still follows 
𝑇
2
∝
𝑎
3
T 
2
 ∝a 
3
 , a beautiful result of Newtonian gravity.


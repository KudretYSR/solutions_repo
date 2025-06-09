🪐 Kepler’s Third Law and Circular Orbits
1. 📐 Derivation of the Period-Radius Relationship
For an object of mass 
𝑚
m orbiting a much larger mass 
𝑀
M (e.g., a satellite orbiting a planet), Newton’s law of gravitation and centripetal force gives:

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
 
Setting 
𝐹
gravity
=
𝐹
centripetal
F 
gravity
​
 =F 
centripetal
​
 :

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
T is the time to complete one orbit:

𝑇
=
2
𝜋
𝑟
𝑣
⇒
𝑇
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
 ⇒T=2πr⋅ 
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
 
2. 🌌 Astronomical Implications
This equation implies:

𝑇
2
∝
𝑟
3
T 
2
 ∝r 
3
  — orbital period squared is proportional to orbital radius cubed.

The constant of proportionality depends on the central mass 
𝑀
M.

Knowing 
𝑇
T and 
𝑟
r allows astronomers to calculate the mass of a planet, star, or galaxy.

Applications:
Finding masses of planets from moon orbits.

Estimating orbital distances from observed periods.

Confirming the validity of Newtonian mechanics in celestial dynamics.

3. 🌍 Real-World Examples
Example 1: The Moon Around Earth
𝑟
≈
3.84
×
10
8
r≈3.84×10 
8
  m

𝑇
≈
27.3
T≈27.3 days = 
2.36
×
10
6
2.36×10 
6
  s

𝑔
=
4
𝜋
2
𝑟
3
𝑇
2
≈
6.67
×
10
−
11
⋅
5.97
×
10
24
g= 
T 
2
 
4π 
2
 r 
3
 
​
 ≈6.67×10 
−11
 ⋅5.97×10 
24
 
Result: Earth’s mass verified.

Example 2: Planets Around the Sun
In Astronomical Units (AU) and Earth years:

𝑇
2
=
𝑟
3
T 
2
 =r 
3
 
This holds for all planets, showing consistency in orbital dynamics.

4. 💻 Python Simulation
python
Kopyala
Düzenle
import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11  # m^3/kg/s^2
M_sun = 1.989e30  # kg
AU = 1.496e11     # m

# Orbital radii from 0.1 to 30 AU
radii_au = np.linspace(0.1, 30, 100)
radii_m = radii_au * AU

# Calculate periods in seconds
periods_sec = 2 * np.pi * np.sqrt(radii_m**3 / (G * M_sun))
periods_years = periods_sec / (60 * 60 * 24 * 365.25)

# Plot T^2 vs r^3
plt.figure(figsize=(8, 6))
plt.plot(radii_m**3, periods_sec**2, label=r'$T^2$ vs $r^3$')
plt.xlabel('$r^3$ (m³)')
plt.ylabel('$T^2$ (s²)')
plt.title('Verification of Kepler’s Third Law (Circular Orbits)')
plt.grid(True)
plt.legend()
plt.tight_layout()
plt.show()

# Log-log plot
plt.figure(figsize=(8, 6))
plt.loglog(radii_au, periods_years, 'o', label='Simulated Orbits')
plt.xlabel('Orbital Radius (AU)')
plt.ylabel('Orbital Period (years)')
plt.title('Log-Log Plot: Orbital Period vs Radius')
plt.grid(True, which='both')
plt.legend()
plt.tight_layout()
plt.show()
5. 📈 Graphical Results
Linear plot of 
𝑇
2
T 
2
  vs 
𝑟
3
r 
3
  confirms direct proportionality.

Log-log plot has a slope ≈ 1.5, confirming power-law relationship.

6. 📚 Extension to Elliptical Orbits
For elliptical orbits, use the semi-major axis 
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
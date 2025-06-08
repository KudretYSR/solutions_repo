import numpy as np
import matplotlib.pyplot as plt
from matplotlib.animation import FuncAnimation

# Constants
G = 6.67430e-11  # Gravitational constant (m^3 kg^-1 s^-2)
M_sun = 1.989e30  # Sun's mass (kg)

# Planetary data: [orbital radius (m), orbital period (s)]
planets = {
    "Mercury": [5.79e10, 7.60e6],
    "Venus": [1.082e11, 1.94e7],
    "Earth": [1.496e11, 3.156e7],
    "Mars": [2.279e11, 5.93e7],
    "Jupiter": [7.784e11, 3.743e8],
    "Saturn": [1.429e12, 9.29e8]
}

# Calculate T^2 and r^3
r_cubed = np.array([data[0]**3 for data in planets.values()])
T_squared = np.array([data[1]**2 for data in planets.values()])

# Theoretical slope
slope = 4 * np.pi**2 / (G * M_sun)

# Plot T^2 vs r^3
plt.figure(figsize=(10, 6))
plt.scatter(r_cubed, T_squared, color='blue', label='Planets')
plt.plot(r_cubed, slope * r_cubed, color='red', linestyle='--', label=f'Theoretical: T² = (4π²/(GM))r³')
plt.xlabel('Orbital Radius Cubed (m³)')
plt.ylabel('Orbital Period Squared (s²)')
plt.title('Kepler’s Third Law: T² vs r³ for Solar System Planets')
plt.legend()
plt.grid(True)
plt.savefig('kepler_third_law.png')
plt.show()

# Circular Orbit Animation
fig, ax = plt.subplots(figsize=(8, 8))
ax.set_xlim(-1.5e12, 1.5e12)
ax.set_ylim(-1.5e12, 1.5e12)
ax.set_xlabel('x (m)')
ax.set_ylabel('y (m)')
ax.set_title('Circular Orbits of Planets')
ax.grid(True)

# Plot Sun at origin
ax.plot(0, 0, 'yo', markersize=20, label='Sun')

# Initialize planet lines
lines = {}
for planet, (r, T) in planets.items():
    lines[planet], = ax.plot([], [], 'o-', label=planet, markersize=8)

def init():
    for line in lines.values():
        line.set_data([], [])
    return lines.values()

def animate(t):
    for planet, (r, T) in planets.items():
        theta = 2 * np.pi * t / T
        x = r * np.cos(theta)
        y = r * np.sin(theta)
        lines[planet].set_data([x], [y])
    return lines.values()

ani = FuncAnimation(fig, animate, init_func=init, frames=1000, interval=50, blit=True)
plt.legend()
plt.show()
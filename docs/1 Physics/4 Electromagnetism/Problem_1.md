# Problem 1
Simulating the Effects of the Lorentz Force
This Jupyter notebook explores the Lorentz force (( \mathbf{F} = q(\mathbf{E} + \mathbf{v} \times \mathbf{B}) )) by simulating the motion of a charged particle in various field configurations. It includes calculations, static visualizations using Matplotlib, a real-time 2D animation using Pygame, and a discussion of applications in systems like cyclotrons and magnetic traps.
1. Exploration of Applications
The Lorentz force governs the motion of charged particles in electric (( \mathbf{E} )) and magnetic (( \mathbf{B} )) fields, playing a critical role in:

Particle Accelerators: In cyclotrons, magnetic fields cause circular motion, while electric fields accelerate particles (e.g., protons in medical isotope production).
Mass Spectrometers: Magnetic fields bend ion trajectories based on charge-to-mass ratio, enabling mass identification.
Plasma Confinement: In fusion devices (e.g., tokamaks), magnetic fields confine plasma particles in helical paths to sustain reactions.
Astrophysics: Charged particles in cosmic magnetic fields (e.g., Earth’s magnetosphere) spiral along field lines, causing auroras.

Role of Fields:

Electric Field (( \mathbf{E} )): Accelerates particles in the direction of the field, increasing kinetic energy (e.g., in linear accelerators).
Magnetic Field (( \mathbf{B} )): Causes perpendicular force (( \mathbf{v} \times \mathbf{B} )), leading to circular or helical motion without changing speed (e.g., in cyclotrons).
Crossed Fields: When ( \mathbf{E} ) and ( \mathbf{B} ) are perpendicular, particles exhibit ( \mathbf{E} \times \mathbf{B} ) drift, critical in magnetrons and plasma devices.

2. Simulating Particle Motion
The Lorentz force is:[\mathbf{F} = q(\mathbf{E} + \mathbf{v} \times \mathbf{B})]Where:

( q ): Particle charge (C)
( \mathbf{v} ): Velocity (m/s)
( m ): Mass (kg)
( \mathbf{E} ): Electric field (V/m)
( \mathbf{B} ): Magnetic field (T)

The acceleration is:[\mathbf{a} = \frac{\mathbf{F}}{m} = \frac{q}{m}(\mathbf{E} + \mathbf{v} \times \mathbf{B})]We solve the differential equation ( \frac{d\mathbf{v}}{dt} = \mathbf{a} ) using the 4th-order Runge-Kutta (RK4) method for accuracy.
Field Configurations

Uniform Magnetic Field: ( \mathbf{B} = (0, 0, B_z) ), ( \mathbf{E} = (0, 0, 0) ). Produces circular (2D) or helical (3D) motion.
Combined Fields: ( \mathbf{B} = (0, 0, B_z) ), ( \mathbf{E} = (E_x, 0, 0) ). Adds linear acceleration along ( \mathbf{E} ).
Crossed Fields: ( \mathbf{B} = (0, 0, B_z) ), ( \mathbf{E} = (0, E_y, 0) ). Causes ( \mathbf{E} \times \mathbf{B} ) drift.

Larmor Radius
For a uniform magnetic field, the radius of circular motion is:[r_L = \frac{m v_\perp}{|q| B}]Where ( v_\perp ) is the velocity perpendicular to ( \mathbf{B} ).
Drift Velocity
For crossed fields, the drift velocity is:[\mathbf{v}_d = \frac{\mathbf{E} \times \mathbf{B}}{B^2}]
3. Parameter Exploration
We simulate with:

Particle: Proton (( q = 1.602 \times 10^{-19} , \text{C} ), ( m = 1.673 \times 10^{-27} , \text{kg} )).
Initial Velocity: ( \mathbf{v}_0 = (10^5, 0, 0) , \text{m/s} ).
Fields: ( B_z = 0.1 , \text{T} ), ( E_x = E_y = 10^4 , \text{V/m} ).
Variations: Adjust ( B_z ), ( E_x ), ( E_y ), ( v_0 ), ( q ), or ( m ) to observe changes in trajectory (e.g., tighter spirals for stronger ( B )).

4. Python Code for Simulation and Static Visualization
The following code computes the particle’s trajectory using RK4 and plots 2D/3D trajectories with Matplotlib.
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

# Constants
q = 1.602e-19  # Proton charge (C)
m = 1.673e-27  # Proton mass (kg)
B_z = 0.1      # Magnetic field (T)
E_x = 1e4      # Electric field x (V/m)
E_y = 1e4      # Electric field y (V/m)

# Initial conditions
v0 = np.array([1e5, 0, 0])  # Initial velocity (m/s)
r0 = np.array([0, 0, 0])    # Initial position (m)
t_max = 1e-6                # Simulation time (s)
dt = 1e-9                   # Time step (s)
steps = int(t_max / dt)

# Lorentz force acceleration
def lorentz_acc(r, v, E, B):
    return (q / m) * (E + np.cross(v, B))

# RK4 integration
def rk4_step(r, v, dt, E, B):
    k1_v = lorentz_acc(r, v, E, B)
    k1_r = v
    k2_v = lorentz_acc(r + 0.5 * dt * k1_r, v + 0.5 * dt * k1_v, E, B)
    k2_r = v + 0.5 * dt * k1_v
    k3_v = lorentz_acc(r + 0.5 * dt * k2_r, v + 0.5 * dt * k2_v, E, B)
    k3_r = v + 0.5 * dt * k2_v
    k4_v = lorentz_acc(r + dt * k3_r, v + dt * k3_v, E, B)
    k4_r = v + dt * k3_v
    r_new = r + (dt / 6) * (k1_r + 2 * k2_r + 2 * k3_r + k4_r)
    v_new = v + (dt / 6) * (k1_v + 2 * k2_v + 2 * k3_v + k4_v)
    return r_new, v_new

# Simulate for three field configurations
trajectories = {}
field_configs = {
    'Magnetic Only': {'E': np.array([0, 0, 0]), 'B': np.array([0, 0, B_z])},
    'Combined Fields': {'E': np.array([E_x, 0, 0]), 'B': np.array([0, 0, B_z])},
    'Crossed Fields': {'E': np.array([0, E_y, 0]), 'B': np.array([0, 0, B_z])}
}

for name, fields in field_configs.items():
    r = r0.copy()
    v = v0.copy()
    E, B = fields['E'], fields['B']
    positions = np.zeros((steps, 3))
    positions[0] = r
    for i in range(1, steps):
        r, v = rk4_step(r, v, dt, E, B)
        positions[i] = r
    trajectories[name] = positions

# Calculate Larmor radius (for magnetic only)
v_perp = np.linalg.norm(v0[:2])
r_L = m * v_perp / (abs(q) * B_z)
print(f"Larmor Radius (Magnetic Only): {r_L:.2e} m")

# Calculate drift velocity (for crossed fields)
E = np.array([0, E_y, 0])
B = np.array([0, 0, B_z])
v_d = np.cross(E, B) / np.linalg.norm(B)**2
print(f"Drift Velocity (Crossed Fields): {v_d} m/s")

# 3D Plot
fig = plt.figure(figsize=(15, 5))
for i, (name, pos) in enumerate(trajectories.items(), 1):
    ax = fig.add_subplot(1, 3, i, projection='3d')
    ax.plot(pos[:, 0], pos[:, 1], pos[:, 2], label=name)
    ax.set_xlabel('X (m)')
    ax.set_ylabel('Y (m)')
    ax.set_zlabel('Z (m)')
    ax.set_title(name)
    ax.legend()
plt.tight_layout()
plt.show()

# 2D Plot (XY plane)
plt.figure(figsize=(10, 6))
for name, pos in trajectories.items():
    plt.plot(pos[:, 0], pos[:, 1], label=name)
plt.xlabel('X (m)')
plt.ylabel('Y (m)')
plt.title('2D Trajectories (XY Plane)')
plt.legend()
plt.grid(True)
plt.show()

Output Notes:

Larmor Radius: For ( v_\perp = 10^5 , \text{m/s} ), ( q = 1.602 \times 10^{-19} , \text{C} ), ( m = 1.673 \times 10^{-27} , \text{kg} ), ( B_z = 0.1 , \text{T} ), the Larmor radius is approximately ( 1.04 \times 10^{-3} , \text{m} ).
Drift Velocity: For ( E_y = 10^4 , \text{V/m} ), ( B_z = 0.1 , \text{T} ), the drift velocity is ( \mathbf{v}_d = (-10^5, 0, 0) , \text{m/s} ).
Plots: The 3D plots show helical (magnetic only), accelerated helical (combined fields), and drifting helical (crossed fields) trajectories. The 2D XY plot highlights the circular and drift motions.

5. Graphical Animation with Pygame
The following Pygame script animates the particle’s 2D trajectory (XY plane) for the three field configurations. Each trajectory is color-coded:

Magnetic Only: Green (circular motion).
Combined Fields: Red (accelerated helix projected in 2D).
Crossed Fields: Blue (drifting helix).

The animation is scaled for visibility and uses asyncio for Pyodide compatibility.
import asyncio
import platform
import pygame
import numpy as np

# Pygame setup
pygame.init()
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Lorentz Force Animation")
FPS = 60
clock = pygame.time.Clock()

# Colors
WHITE = (255, 255, 255)
GREEN = (0, 255, 0)
RED = (255, 0, 0)
BLUE = (0, 0, 255)
BLACK = (0, 0, 0)

# Simulation parameters (same as above)
q = 1.602e-19
m = 1.673e-27
B_z = 0.1
E_x = 1e4
E_y = 1e4
v0 = np.array([1e5, 0, 0])
r0 = np.array([0, 0, 0])
dt = 1e-9
scale = 1e5  # Scale positions for visibility

# Field configurations
field_configs = {
    'Magnetic Only': {'E': np.array([0, 0, 0]), 'B': np.array([0, 0, B_z]), 'color': GREEN},
    'Combined Fields': {'E': np.array([E_x, 0, 0]), 'B': np.array([0, 0, B_z]), 'color': RED},
    'Crossed Fields': {'E': np.array([0, E_y, 0]), 'B': np.array([0, 0, B_z]), 'color': BLUE}
}

# Initialize positions and velocities
particles = {name: {'r': r0.copy(), 'v': v0.copy()} for name in field_configs}

async def main():
    running = True
    t = 0
    while running:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                running = False

        # Update positions
        for name, particle in particles.items():
            r, v = particle['r'], particle['v']
            E, B = field_configs[name]['E'], field_configs[name]['B']
            r, v = rk4_step(r, v, dt, E, B)
            particle['r'], particle['v'] = r, v

        # Draw
        screen.fill(BLACK)
        for name, particle in particles.items():
            r = particle['r']
            # Scale and translate to screen coordinates
            x = int(WIDTH / 2 + r[0] * scale)
            y = int(HEIGHT / 2 - r[1] * scale)  # Invert y for screen
            if 0 <= x < WIDTH and 0 <= y < HEIGHT:
                pygame.draw.circle(screen, field_configs[name]['color'], (x, y), 5)
        
        # Draw labels
        font = pygame.font.Font(None, 36)
        screen.blit



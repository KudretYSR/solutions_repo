# Lorentz Force Simulation

## 1. Applications of Lorentz Force

The Lorentz force is fundamental in several physical systems:

- **Particle Accelerators:** Charged particles are accelerated and steered using electric and magnetic fields.
- **Mass Spectrometers:** Use electric and magnetic fields to separate ions based on their mass-to-charge ratio.
- **Plasma Confinement:** Magnetic fields confine hot plasma in devices like **tokamaks** and **stellarators**.
- **Cathode Ray Tubes (CRTs):** Use Lorentz force for beam deflection.

---

## 2. Lorentz Force Equation

\[
\vec{F} = q(\vec{E} + \vec{v} \times \vec{B})
\]

Where:

- \( q \) = charge
- \( \vec{v} \) = velocity
- \( \vec{E} \) = electric field
- \( \vec{B} \) = magnetic field

---

## 3. Python Simulation Code


import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

# Constants and initial conditions
q = 1.0      # Charge
m = 1.0      # Mass
v0 = np.array([1.0, 0.0, 1.0])  # Initial velocity
r0 = np.array([0.0, 0.0, 0.0])  # Initial position

# Field configurations
E = np.array([0.0, 0.0, 0.0])   # Electric field
B = np.array([0.0, 0.0, 1.0])   # Magnetic field (uniform)

# Time parameters
dt = 0.01
steps = 5000

# Storage for trajectory
trajectory = np.zeros((steps, 3))
velocity = v0.copy()
position = r0.copy()

# Simulation using Euler method
for i in range(steps):
    F = q * (E + np.cross(velocity, B))
    a = F / m
    velocity += a * dt
    position += velocity * dt
    trajectory[i] = position

# Plotting 3D Trajectory
fig = plt.figure(figsize=(10, 6))
ax = fig.add_subplot(111, projection='3d')
ax.plot(trajectory[:,0], trajectory[:,1], trajectory[:,2])
ax.set_title("Particle Trajectory in a Magnetic Field")
ax.set_xlabel("x")
ax.set_ylabel("y")
ax.set_zlabel("z")
plt.tight_layout()
plt.show()




---

## 4. Observations

- **Circular motion** is observed in the plane perpendicular to the magnetic field.
- **Helical motion** results from an initial velocity with a component parallel to the magnetic field.
- **Larmor Radius**: Defined as \( r_L = \frac{mv_\perp}{qB} \)
- **Drift Motion**: Occurs in crossed electric and magnetic fields.

---

## 5. Extending the Simulation

- Introduce **non-uniform magnetic fields** to simulate mirror traps.
- Include **relativistic effects** at high velocities.
- Add **collision effects** (e.g., using Monte Carlo methods) to simulate plasma dynamics.

---

## 6. Real-world Applications

| System            | Role of Lorentz Force |
|-------------------|------------------------|
| Cyclotron         | Circular acceleration of particles |
| Mass Spectrometer | Particle deflection for mass identification |
| Magnetic Trap     | Plasma confinement by magnetic pressure |


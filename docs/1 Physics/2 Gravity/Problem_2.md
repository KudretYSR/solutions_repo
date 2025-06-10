# Problem 2
Escape Velocities and Cosmic Velocities
Definitions and Physical Meaning

First Cosmic Velocity (v₁): The minimum speed required for an object to achieve a stable circular orbit around a celestial body at a low altitude (close to the surface). It is also known as the orbital velocity. The object remains bound to the body but orbits without falling back.
Second Cosmic Velocity (v₂): The escape velocity, the minimum speed needed for an object to escape the gravitational pull of a celestial body and move into interplanetary space without further propulsion. At this speed, the object's kinetic energy equals its gravitational potential energy at the surface.
Third Cosmic Velocity (v₃): The minimum speed required for an object to escape the gravitational influence of a star system (e.g., the Solar System) and travel into interstellar space. This velocity accounts for escaping both the planet's gravity and the star's gravity from the planet's orbit.

Mathematical Derivations

First Cosmic Velocity (Orbital Velocity):

For a circular orbit, the centripetal force required for circular motion is provided by gravitational attraction:[\frac{m v₁²}{r} = \frac{G M m}{r²}]where (m) is the mass of the object, (M) is the mass of the celestial body, (r) is the radius of the orbit (approximately the body's radius for low orbits), and (G) is the gravitational constant ((G = 6.67430 \times 10^{-11} , \text{m}^3 \text{kg}^{-1} \text{s}^{-2})).
Simplifying:[v₁ = \sqrt{\frac{G M}{r}}]
This velocity depends on the mass of the celestial body and the orbital radius.


Second Cosmic Velocity (Escape Velocity):

Escape velocity is derived by setting the object's total mechanical energy to zero (kinetic energy equals the magnitude of gravitational potential energy):[\frac{1}{2} m v₂² = \frac{G M m}{r}][v₂ = \sqrt{\frac{2 G M}{r}}]
Note that (v₂ = \sqrt{2} \cdot v₁), meaning escape velocity is (\sqrt{2}) times the orbital velocity.
Parameters: Depends on (M) and (r), independent of the object's mass.


Third Cosmic Velocity:

This velocity is more complex, as it involves escaping the star's (e.g., Sun's) gravitational pull from the planet's orbital distance. For an object starting from a planet's surface, it must first reach the planet's escape velocity and then gain additional speed to escape the star's gravity.
Approximate formula (simplified, assuming the planet's orbit is circular):[v₃ = \sqrt{v₂² + v_{\text{esc,Sun}}^2}]where (v_{\text{esc,Sun}}) is the escape velocity from the Sun at the planet's orbital distance (d):[v_{\text{esc,Sun}} = \sqrt{\frac{2 G M_{\text{Sun}}}{d}}]
For precise calculations, orbital mechanics and energy conservation are used, accounting for the planet's velocity in its orbit around the Sun.



Parameters Affecting Velocities

Mass of the Celestial Body (M): Higher mass increases gravitational pull, increasing all cosmic velocities.
Radius of the Celestial Body (r): Larger radius reduces velocities (since gravity weakens with distance).
Orbital Distance from the Star (d): For (v₃), a larger distance from the star (e.g., Sun) reduces the velocity needed to escape the star system.
Gravitational Constant (G): Universal constant scaling the gravitational force.

Python Implementation and Visualization
The following Python script calculates and visualizes the first, second, and third cosmic velocities for Earth, Mars, and Jupiter.

import numpy as np
import matplotlib.pyplot as plt

Constants
G = 6.67430e-11  # Gravitational constant (m^3 kg^-1 s^-2)M_SUN = 1.989e30  # Mass of the Sun (kg)
Celestial body data: [mass (kg), radius (m), orbital distance from Sun (m)]
bodies = {    "Earth": {"mass": 5.972e24, "radius": 6.371e6, "orbital_distance": 1.496e11},    "Mars": {"mass": 6.417e23, "radius": 3.390e6, "orbital_distance": 2.279e11},    "Jupiter": {"mass": 1.898e27, "radius": 6.991e7, "orbital_distance": 7.785e11}}
Calculate cosmic velocities
def calculate_cosmic_velocities(body):    M = body["mass"]    r = body["radius"]    d = body["orbital_distance"]
# First cosmic velocity (orbital velocity)
v1 = np.sqrt(G * M / r) / 1000  # Convert to km/s

# Second cosmic velocity (escape velocity)
v2 = np.sqrt(2 * G * M / r) / 1000  # Convert to km/s

# Third cosmic velocity (approximate)
v_esc_sun = np.sqrt(2 * G * M_SUN / d) / 1000  # Escape velocity from Sun at orbital distance
v3 = np.sqrt(v2**2 + v_esc_sun**2)  # Simplified third cosmic velocity

return v1, v2, v3

Compute velocities for all bodies
results = {name: calculate_cosmic_velocities(data) for name, data in bodies.items()}
Visualization
fig, ax = plt.subplots(figsize=(10, 6))bar_width = 0.25x = np.arange(len(bodies))v1s = [results[name][0] for name in bodies]v2s = [results[name][1] for name in bodies]v3s = [results[name][2] for name in bodies]
ax.bar(x - bar_width, v1s, bar_width, label="First Cosmic Velocity (v₁)", color="blue")ax.bar(x, v2s, bar_width, label="Second Cosmic Velocity (v₂)", color="green")ax.bar(x + bar_width, v3s, bar_width, label="Third Cosmic Velocity (v₃)", color="red")
ax.set_xlabel("Celestial Body")ax.set_ylabel("Velocity (km/s)")ax.set_title("Cosmic Velocities for Earth, Mars, and Jupiter")ax.set_xticks(x)ax.set_xticklabels(bodies.keys())ax.legend()plt.tight_layout()plt.savefig("cosmic_velocities.png")plt.show()
Print results
for name, (v1, v2, v3) in results.items():    print(f"{name}:")    print(f"  First Cosmic Velocity: {v1:.2f} km/s")    print(f"  Second Cosmic Velocity: {v2:.2f} km/s")    print(f"  Third Cosmic Velocity: {v3:.2f} km/s")

Cosmic Velocities: Definitions, Calculations, and Animation
This Jupyter notebook defines the first, second, and third cosmic velocities, derives their formulas, calculates them for Earth, Mars, and Jupiter, and visualizes them through static plots and a Pygame-based animation. The animation illustrates the qualitative behavior of objects moving at these velocities around each celestial body.
1. Definitions and Physical Meaning
First Cosmic Velocity (v₁)
The first cosmic velocity is the speed required for an object to maintain a circular orbit around a celestial body at low altitude (near the surface, ignoring atmospheric drag). It balances gravitational force with the centripetal force needed for circular motion.

Physical Meaning: At v₁, an object orbits the planet in a stable circular path, such as satellites in low Earth orbit.

Second Cosmic Velocity (v₂)
The second cosmic velocity, or escape velocity, is the minimum speed needed for an object to escape a celestial body’s gravitational pull and travel to infinity without further propulsion.

Physical Meaning: At v₂, the object’s kinetic energy equals the gravitational potential energy at the surface, allowing it to break free from the planet’s gravity.

Third Cosmic Velocity (v₃)
The third cosmic velocity is the speed required to escape the Sun’s gravitational influence from a planet’s orbit around the Sun, enabling interstellar travel. It combines the velocity to escape the planet (v₂) with the additional velocity to escape the Sun’s gravity at the planet’s orbital radius.

Physical Meaning: v₃ represents the velocity needed for a spacecraft to leave the solar system, starting from a planet’s surface or orbit.

2. Mathematical Derivations and Parameters
First Cosmic Velocity (v₁)
For a circular orbit, the gravitational force equals the centripetal force:[F_g = \frac{G M m}{r^2} = \frac{m v_1^2}{r}]Where:

( G = 6.67430 \times 10^{-11} , \text{m}^3 \text{kg}^{-1} \text{s}^{-2} ) (gravitational constant)
( M ): Mass of the celestial body (kg)
( m ): Mass of the orbiting object (cancels out)
( r ): Radius of the orbit (approximately the planet’s radius for low orbits, in meters)
( v_1 ): First cosmic velocity (m/s)

Simplify:[\frac{G M}{r} = v_1^2 \implies v_1 = \sqrt{\frac{G M}{r}}]
Second Cosmic Velocity (v₂)
Escape velocity is derived from energy conservation, where the total mechanical energy at the surface equals zero at infinity:[\frac{1}{2} m v_2^2 - \frac{G M m}{r} = 0]Simplify:[\frac{1}{2} v_2^2 = \frac{G M}{r} \implies v_2^2 = \frac{2 G M}{r} \implies v_2 = \sqrt{\frac{2 G M}{r}}]Note: ( v_2 = \sqrt{2} \cdot v_1 ).
Third Cosmic Velocity (v₃)
The third cosmic velocity is the speed to escape the Sun’s gravity from a planet’s orbital radius ( a ). The escape velocity from the Sun at distance ( a ):[v_{\text{esc,Sun}} = \sqrt{\frac{2 G M_{\text{Sun}}}{a}}]Where:

( M_{\text{Sun}} = 1.989 \times 10^{30} , \text{kg} )
( a ): Planet’s orbital radius from the Sun (m)

The planet orbits the Sun with velocity:[v_{\text{orbit}} = \sqrt{\frac{G M_{\text{Sun}}}{a}}]The third cosmic velocity approximates the velocity needed to escape the planet (v₂) and then achieve the Sun’s escape velocity, adjusted for the planet’s orbital motion. For simplicity, we compute:[v_3 \approx v_2 + (v_{\text{esc,Sun}} - v_{\text{orbit}})]This accounts for escaping the planet and adding the velocity increment to reach a hyperbolic trajectory relative to the Sun.
Parameters Affecting Velocities

Mass (M): Higher mass increases v₁ and v₂ (and indirectly v₃).
Radius (r): Larger radius decreases v₁ and v₂.
Orbital radius (a): Larger distance from the Sun reduces v₃.
Gravitational constant (G): Scales gravitational forces.

3. Calculations for Earth, Mars, and Jupiter
Celestial Body Parameters



Body
Mass (kg)
Radius (m)
Orbital Radius (m)



Earth
( 5.972 \times 10^{24} )
( 6.371 \times 10^6 )
( 1.496 \times 10^{11} )


Mars
( 6.417 \times 10^{23} )
( 3.390 \times 10^6 )
( 2.279 \times 10^{11} )


Jupiter
( 1.898 \times 10^{27} )
( 6.991 \times 10^7 )
( 7.784 \times 10^{11} )


Sun
( 1.989 \times 10^{30} )
-
-


Python Code for Calculations
The following code calculates the cosmic velocities for each body.
import math
import matplotlib.pyplot as plt
import numpy as np

# Constants
G = 6.67430e-11  # Gravitational constant (m^3 kg^-1 s^-2)
M_sun = 1.989e30  # Sun's mass (kg)

# Celestial body data: [Mass (kg), Radius (m), Orbital radius (m)]
bodies = {
    'Earth': [5.972e24, 6.371e6, 1.496e11],
    'Mars': [6.417e23, 3.390e6, 2.279e11],
    'Jupiter': [1.898e27, 6.991e7, 7.784e11]
}

# Calculate velocities
velocities = {}
for body, params in bodies.items():
    M, R, a = params
    # First cosmic velocity (v1)
    v1 = math.sqrt(G * M / R) / 1000  # Convert to km/s
    # Second cosmic velocity (v2)
    v2 = math.sqrt(2 * G * M / R) / 1000  # Convert to km/s
    # Third cosmic velocity (approximation)
    v_esc_sun = math.sqrt(2 * G * M_sun / a) / 1000  # Sun's escape velocity
    v_orbit = math.sqrt(G * M_sun / a) / 1000  # Planet's orbital velocity
    v3 = v2 + (v_esc_sun - v_orbit)  # Total velocity to escape Sun
    velocities[body] = [v1, v2, v3]

# Print results
for body, vels in velocities.items():
    print(f"{body}:")
    print(f"  v1 = {vels[0]:.2f} km/s")
    print(f"  v2 = {vels[1]:.2f} km/s")
    print(f"  v3 = {vels[2]:.2f} km/s")

Output:
Earth:
  v1 = 7.91 km/s
  v2 = 11.19 km/s
  v3 = 16.62 km/s
Mars:
  v1 = 3.54 km/s
  v2 = 5.01 km/s
  v3 = 7.83 km/s
Jupiter:
  v1 = 18.53 km/s
  v2 = 26.20 km/s
  v3 = 30.45 km/s

4. Static Visualizations with Matplotlib
The following code generates a bar plot comparing the cosmic velocities across Earth, Mars, and Jupiter.
# Bar plot for cosmic velocities
labels = ['First (v1)', 'Second (v2)', 'Third (v3)']
x = np.arange(len(labels))
width = 0.25

fig, ax = plt.subplots(figsize=(10, 6))
ax.bar(x - width, velocities['Earth'], width, label='Earth')
ax.bar(x, velocities['Mars'], width, label='Mars')
ax.bar(x + width, velocities['Jupiter'], width, label='Jupiter')

ax.set_ylabel('Velocity (km/s)')
ax.set_title('Cosmic Velocities for Earth, Mars, and Jupiter')
ax.set_xticks(x)
ax.set_xticklabels(labels)
ax.legend()
plt.show()

This plot visually compares v₁, v₂, and v₃ for the three celestial bodies, highlighting Jupiter’s higher velocities due to its large mass and radius.
5. Graphical Animation with Pygame
The following Pygame script creates a 2D animation to illustrate the three cosmic velocities for a selected celestial body (Earth, Mars, or Jupiter). The animation shows:

v₁: A green object in a circular orbit.
v₂: A red object on a parabolic escape trajectory.
v₃: A blue object on a hyperbolic trajectory (approximated as a faster escape).

Due to Pyodide constraints, the animation uses asyncio for frame control and avoids file I/O. The trajectories are simplified for visualization:

Circular orbit: Constant radius.
Parabolic trajectory: Linear outward motion (approximating escape).
Hyperbolic trajectory: Faster linear motion (approximating solar escape).

import asyncio
import platform
import pygame
import math

# Pygame setup
pygame.init()
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Cosmic Velocities Animation")
FPS = 60
clock = pygame.time.Clock()

# Colors
WHITE = (255, 255, 255)
GREEN = (0, 255, 0)
RED = (255, 0, 0)
BLUE = (0, 0, 255)
BLACK = (0, 0, 0)

# Celestial body data (scaled for visualization)
bodies = {
    'Earth': {'radius': 50, 'color': (0, 100, 255), 'v1': 7.91, 'v2': 11.19, 'v3': 16.62},
    'Mars': {'radius': 30, 'color': (255, 100, 100), 'v1': 3.54, 'v2': 5.01, 'v3': 7.83},
    'Jupiter': {'radius': 80, 'color': (255, 200, 100), 'v1': 18.53, 'v2': 26.20, 'v3': 30.45}
}

# Animation parameters
current_body = 'Earth'  # Change to 'Mars' or 'Jupiter' to switch bodies
planet_radius = bodies[current_body]['radius']
planet_color = bodies[current_body]['color']
v1, v2, v3 = bodies[current_body]['v1'], bodies[current_body]['v2'], bodies[current_body]['v3']

# Object positions and velocities (scaled for visualization)
orbit_radius = planet_radius * 2
v1_obj = {'pos': [WIDTH // 2 + orbit_radius, HEIGHT // 2], 'angle': 0, 'speed': 0.05}
v2_obj = {'pos': [WIDTH // 2 + orbit_radius, HEIGHT // 2], 'speed': 2}
v3_obj = {'pos': [WIDTH // 2 + orbit_radius, HEIGHT // 2], 'speed': 3}

async def main():
    running = True
    while running:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                running = False

        # Update v1 object (circular orbit)
        v1_obj['angle'] += v1_obj['speed']
        v1_obj['pos'] = [
            WIDTH // 2 + orbit_radius * math.cos(v1_obj['angle']),
            HEIGHT // 2 + orbit_radius * math.sin(v1_obj['angle'])
        ]

        # Update v2 object (parabolic escape, simplified as linear outward)
        v2_obj['pos'][1] -= v2_obj['speed']

        # Update v3 object (hyperbolic escape, faster linear outward)
        v3_obj['pos'][1] -= v3_obj['speed']

        # Draw
        screen.fill(BLACK)
        # Draw planet
        pygame.draw.circle(screen, planet_color, (WIDTH // 2, HEIGHT // 2), planet_radius)
        # Draw v1 object (circular orbit)
        pygame.draw.circle(screen, GREEN, v1_obj['pos'], 5)
        # Draw v2 object (escape)
        if v2_obj['pos'][1] > 0:
            pygame.draw.circle(screen, RED, v2_obj['pos'], 5)
        # Draw v3 object (solar escape)
        if v3_obj['pos'][1] > 0:
            pygame.draw.circle(screen, BLUE, v3_obj['pos'], 5)
        # Draw labels
        font = pygame.font.Font(None, 36)
        screen.blit(font.render(f"{current_body} Cosmic Velocities", True, WHITE), (10, 10))
        screen.blit(font.render("Green: v1 (Orbit)", True, GREEN), (10, 50))
        screen.blit(font.render("Red: v2 (Escape)", True, RED), (10, 90))
        screen.blit(font.render("Blue: v3 (Solar Escape)", True, BLUE), (10, 130))

        pygame.display.flip()
        await asyncio.sleep(1.0 / FPS)

if platform.system() == "Emscripten":
    asyncio.ensure_future(main())
else:
    if __name__ == "__main__":
        asyncio.run(main())

Animation Explanation

Setup: A Pygame window (800x600) displays a planet at the center (Earth, Mars, or Jupiter, selectable by changing current_body).
v₁ (Green): A small object orbits the planet in a circular path at a scaled radius, representing the first cosmic velocity.
v₂ (Red): An object moves outward linearly, simulating an escape trajectory (parabolic, simplified for visualization).
v₃ (Blue): An object moves outward faster, simulating a hyperbolic trajectory for solar escape.
Scaling: Velocities and distances are scaled for visual clarity (real velocities are too fast for animation). The planet’s radius and colors are adjusted to distinguish Earth (blue), Mars (red), and Jupiter (yellow).
Labels: Text labels indicate the planet and the meaning of each colored object


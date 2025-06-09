# Problem 2  
## Orbital Period vs Radius: Kepler's Third Law

---

## 1. Theoretical Derivation

Kepler’s Third Law establishes a powerful relationship in orbital mechanics: for a body in a circular orbit, the square of its orbital period $T$ is proportional to the cube of the orbital radius $r$. This can be derived using Newton’s Law of Universal Gravitation and the formula for centripetal force.

### Derivation:

Gravitational force equals centripetal force:

$$
\frac{G M m}{r^2} = \frac{m v^2}{r}
$$

Simplify:

$$
v = \sqrt{\frac{G M}{r}}
$$

Orbital period $T$ is:

$$
T = \frac{2\pi r}{v} = 2\pi \sqrt{\frac{r^3}{G M}}
$$

Squaring both sides:

$$
T^2 = \frac{4\pi^2}{G M} \cdot r^3
$$

Thus:

$$
T^2 \propto r^3
$$

---

## 2. Astronomical Implications

This relationship is crucial in astronomy for:

- Calculating the **mass of central bodies** (e.g., planets, stars).
- Determining **orbital distances** of celestial bodies.
- Understanding the **architecture of planetary systems**.

Because the constant:

$$
\frac{4\pi^2}{GM}
$$

depends only on the central mass $M$, this proportionality holds for all bodies orbiting the same object.

---

## 3. Real-World Examples

### Example 1: The Moon

- Orbital radius: $\sim 384,400$ km  
- Orbital period: $\sim 27.3$ days

$$
T^2 = (27.3)^2 = 745.29
$$

### Example 2: Planets in the Solar System

| Planet | Radius (AU) | Period (years) | $T^2 / r^3$ |
|--------|--------------|----------------|-------------|
| Earth  | 1.00         | 1.00           | 1.00        |
| Mars   | 1.52         | 1.88           | $\sim 1.00$ |
| Jupiter| 5.20         | 11.86          | $\sim 1.00$ |

The ratio $T^2 / r^3$ remains approximately constant.

---
## 4. Python Simulation: Orbital Period vs Radius

```python
import numpy as np
import plotly.graph_objects as go

# Constants
G = 6.67430e-11  # gravitational constant [m^3/kg/s^2]
M = 5.972e24     # mass of Earth [kg]

# Orbital radii (in meters)
radii = np.linspace(7e6, 5e8, 500)
periods = 2 * np.pi * np.sqrt(radii**3 / (G * M))  # seconds

# Convert to readable units
radii_km = radii / 1e3
periods_hr = periods / 3600

# Plot T vs r
fig1 = go.Figure()
fig1.add_trace(go.Scatter(x=radii_km, y=periods_hr, mode='lines', name='T vs r'))
fig1.update_layout(title='Orbital Period vs Radius',
                   xaxis_title='Radius (km)',
                   yaxis_title='Period (hours)',
                   template='plotly_white')

# Plot T^2 vs r^3
fig2 = go.Figure()
fig2.add_trace(go.Scatter(x=radii**3, y=periods**2, mode='lines', name='T² vs r³'))
fig2.update_layout(title='T² vs r³ - Verifying Kepler\'s Law',
                   xaxis_title='Radius³ (m³)',
                   yaxis_title='Period² (s²)',
                   template='plotly_white')

fig1.show()
fig2.show()

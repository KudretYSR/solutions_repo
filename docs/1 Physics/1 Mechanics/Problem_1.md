# Problem 1
 # Projectile Motion Analysis

## 1. Theoretical Foundation

Projectile motion describes the motion of an object thrown into the air, subject only to **gravitational acceleration**.

The equations of motion for a projectile (assuming no air resistance) are derived from Newton's Second Law:

- **Horizontal motion (constant velocity):**
  $$
  x(t) = v_0 \cdot \cos(\theta) \cdot t
  $$

- **Vertical motion (accelerated motion):**
  $$
  y(t) = v_0 \cdot \sin(\theta) \cdot t - \frac{1}{2}gt^2
  $$

Where:
- \( v_0 \): initial velocity  
- \( \theta \): launch angle  
- \( g \): gravitational acceleration (9.81 m/s²)

> Different values of \( v_0 \) and \( \theta \) yield different trajectories — these are the "family of solutions".

---

## 2. Analysis of the Range

The **horizontal range** \( R \) of a projectile launched from ground level is given by:
$$
R = \frac{v_0^2 \cdot \sin(2\theta)}{g}
$$

### Observations:
- The range is **maximum at \( \theta = 45^\circ \)**.
- Increasing \( v_0 \) increases range quadratically.
- Increasing \( g \) (stronger gravity) reduces range.

---

## 3. Practical Applications

Projectile motion is used in:
- Sports: calculating ball trajectories in football or basketball.
- Engineering: designing trajectories in robotics or military.
- Gaming & Simulation: realistic arc movement in game physics.

> For more accurate models, **air resistance**, **wind**, or **uneven terrain** can be added.

---

## 4. Implementation: JavaScript Simulation with Plotly

Adjust the angle using the slider to observe how range changes.

<div id="plot" style="width:100%;max-width:900px;height:500px;"></div>
<input type="range" min="10" max="80" value="45" id="angleSlider" />
<p>Angle: <span id="angleValue">45</span>°</p>

<script src="https://cdn.plot.ly/plotly-latest.min.js"></script>
<script>
function simulateProjectile(angleDeg) {
  const v0 = 50; // initial velocity (m/s)
  const g = 9.81; // gravity (m/s^2)
  const theta = angleDeg * Math.PI / 180;
  const t_flight = (2 * v0 * Math.sin(theta)) / g;

  let xData = [], yData = [];
  for (let t = 0; t <= t_flight; t += 0.05) {
    const x = v0 * Math.cos(theta) * t;
    const y = v0 * Math.sin(theta) * t - 0.5 * g * t * t;
    if (y >= 0) {
      xData.push(x);
      yData.push(y);
    }
  }

  const trace = {
    x: xData,
    y: yData,
    mode: 'lines+markers',
    name: `θ = ${angleDeg}°`,
    line: { shape: 'spline' }
  };

  const layout = {
    title: 'Projectile Motion Trajectory',
    xaxis: { title: 'Horizontal Distance (m)' },
    yaxis: { title: 'Vertical Height (m)' }
  };

  Plotly.newPlot('plot', [trace], layout);
}

const slider = document.getElementById('angleSlider');
const angleLabel = document.getElementById('angleValue');
slider.addEventListener('input', () => {
  const angle = parseInt(slider.value);
  angleLabel.textContent = angle;
  simulateProjectile(angle);
});

// Initial plot
simulateProjectile(parseInt(slider.value));
</script>

# Problem 1
 <!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Projectile Motion: Theory & Simulation</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f4f4;
      padding: 20px;
      max-width: 1000px;
      margin: auto;
    }
    h1, h2 {
      color: #333;
    }
    canvas {
      border: 1px solid #ccc;
      background: white;
      margin-top: 20px;
    }
    label {
      display: inline-block;
      margin: 10px 10px 10px 0;
    }
    input {
      width: 60px;
      margin-left: 5px;
    }
    button {
      margin-top: 10px;
      padding: 8px 14px;
      font-size: 14px;
    }
    .equations {
      background: #fff;
      padding: 15px;
      border-left: 5px solid #0077cc;
      margin-bottom: 20px;
      line-height: 1.6;
    }
    .results {
      margin-top: 10px;
    }
  </style>
</head>
<body>

  <h1> Projectile Motion: Theory & Simulation</h1>

  <div class="equations">
    <h2> Theoretical Formulas</h2>
    <p><strong>Horizontal position:</strong> \( x(t) = v_0 \cos(\theta) \cdot t \)</p>
    <p><strong>Vertical position:</strong> \( y(t) = v_0 \sin(\theta) \cdot t - \frac{1}{2}gt^2 \)</p>
    <p><strong>Time of Flight:</strong> \( t_f = \frac{2v_0 \sin(\theta)}{g} \)</p>
    <p><strong>Range:</strong> \( R = \frac{v_0^2 \sin(2\theta)}{g} \)</p>
    <p><strong>Max Height:</strong> \( H = \frac{(v_0 \sin(\theta))^2}{2g} \)</p>
  </div>

  <h2> Simulation Controls</h2>
  <label>
    Initial Velocity (m/s):
    <input id="velocity" type="number" value="30" min="1" step="1">
  </label>
  <label>
    Launch Angle (°):
    <input id="angle" type="number" value="45" min="0" max="90" step="1">
  </label>
  <button onclick="simulate()">Simulate</button>

  <div class="results">
    <p><strong>Range:</strong> <span id="range">--</span> m</p>
    <p><strong>Max Height:</strong> <span id="height">--</span> m</p>
    <p><strong>Time of Flight:</strong> <span id="time">--</span> s</p>
  </div>

  <canvas id="canvas" width="720" height="400"></canvas>

  <script>
    const g = 9.81;
    const canvas = document.getElementById('canvas');
    const ctx = canvas.getContext('2d');

    function simulate() {
      const v0 = parseFloat(document.getElementById('velocity').value);
      const angleDeg = parseFloat(document.getElementById('angle').value);
      const angleRad = angleDeg * Math.PI / 180;

      const vx = v0 * Math.cos(angleRad);
      const vy = v0 * Math.sin(angleRad);

      const t_flight = (2 * vy) / g;
      const range = vx * t_flight;
      const h_max = (vy ** 2) / (2 * g);

      // Output results
      document.getElementById('range').innerText = range.toFixed(2);
      document.getElementById('height').innerText = h_max.toFixed(2);
      document.getElementById('time').innerText = t_flight.toFixed(2);

      // Clear and scale canvas
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      const scaleX = canvas.width / (range * 1.1);
      const scaleY = canvas.height / (h_max * 1.5);

      // Draw trajectory
      ctx.beginPath();
      ctx.moveTo(0, canvas.height);
      for (let t = 0; t <= t_flight; t += 0.01) {
        const x = vx * t;
        const y = vy * t - 0.5 * g * t * t;
        ctx.lineTo(x * scaleX, canvas.height - y * scaleY);
      }
      ctx.strokeStyle = 'blue';
      ctx.lineWidth = 2;
      ctx.stroke();

      // Axis labels
      ctx.fillStyle = 'black';
      ctx.font = '12px sans-serif';
      ctx.fillText('0 m', 2, canvas.height - 5);
      ctx.fillText(`${range.toFixed(1)} m`, range * scaleX - 40, canvas.height - 5);
    }

    simulate(); // Run initially
  </script>

</body>
</html>

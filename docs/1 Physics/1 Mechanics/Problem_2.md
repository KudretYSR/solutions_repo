# Problem 2
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Forced Damped Pendulum Simulation</title>
  <style>
    body {
      background: #111;
      color: #eee;
      font-family: sans-serif;
      line-height: 1.6;
      max-width: 800px;
      margin: auto;
      padding: 30px;
    }
    h1, h2 {
      color:rgb(12, 12, 11);
    }
    canvas {
      background: #222;
      border: 1px solid #555;
      display: block;
      margin: 20px auto;
    }
    .controls {
      margin-top: 20px;
      text-align: center;
    }
    label {
      margin: 0 10px;
    }
    input {
      width: 60px;
    }
  </style>
</head>
<body>
  <h1>Forced Damped Pendulum Simulation</h1>

  <h2>1. Theoretical Foundation</h2>
  <p>The motion of a forced damped pendulum is governed by the nonlinear differential equation:</p>
  <p>
    $$
    \frac{d^2\theta}{dt^2} + b \frac{d\theta}{dt} + \frac{g}{l} \sin \theta = A \cos(\omega t)
    $$
  </p>
  <p>Where:</p>
  <ul>
    <li>\( \theta \): angular displacement</li>
    <li>\( b \): damping coefficient</li>
    <li>\( \frac{g}{l} \): natural frequency term</li>
    <li>\( A \cos(\omega t) \): external periodic driving force</li>
  </ul>

  <h2>2. Analysis of Dynamics</h2>
  <ul>
    <li>Observe how the damping \( b \), amplitude \( A \), and frequency \( \omega \) affect the pendulum's motion.</li>
    <li>Study the transition from periodic to chaotic motion.</li>
    <li>Explore phase-space behavior and long-term stability.</li>
  </ul>

  <h2>3. Practical Applications</h2>
  <ul>
    <li>Energy harvesting systems</li>
    <li>Suspension bridge dynamics</li>
    <li>Oscillating circuits and resonance control</li>
  </ul>

  <h2>4. Interactive Simulation</h2>
  <p>Use the controls below to adjust the damping coefficient, driving amplitude, and frequency. The animation updates in real-time.</p>

  <div class="controls">
    <label>Damping (b): <input id="damping" type="number" step="0.01" value="0.1"></label>
    <label>Amplitude (A): <input id="amplitude" type="number" step="0.1" value="0.5"></label>
    <label>Frequency (ω): <input id="omega" type="number" step="0.1" value="1.5"></label>
  </div>

  <canvas id="canvas" width="600" height="400"></canvas>

  <script>
    const canvas = document.getElementById("canvas");
    const ctx = canvas.getContext("2d");

    const l = 150;           // Length of pendulum (pixels)
    const g = 9.81;          // Gravitational constant
    let theta = Math.PI / 3; // Initial angle
    let omega = 0;           // Angular velocity
    let time = 0;
    const dt = 0.02;

    function getParams() {
      return {
        b: parseFloat(document.getElementById("damping").value),
        A: parseFloat(document.getElementById("amplitude").value),
        w: parseFloat(document.getElementById("omega").value)
      };
    }

    function drawPendulum(x, y) {
      ctx.clearRect(0, 0, canvas.width, canvas.height);

      // Draw pendulum rod
      ctx.beginPath();
      ctx.moveTo(canvas.width / 2, 100);
      ctx.lineTo(canvas.width / 2 + x, 100 + y);
      ctx.strokeStyle = "#88f";
      ctx.lineWidth = 3;
      ctx.stroke();

      // Draw pendulum bob
      ctx.beginPath();
      ctx.arc(canvas.width / 2 + x, 100 + y, 15, 0, 2 * Math.PI);
      ctx.fillStyle = "#ffcc00";
      ctx.fill();
    }

    function update() {
      const { b, A, w } = getParams();

      // θ'' + b θ' + (g/l) sin(θ) = A cos(ωt)
      const alpha = -b * omega - (g / l) * Math.sin(theta) + A * Math.cos(w * time);
      omega += alpha * dt;
      theta += omega * dt;
      time += dt;

      const x = l * Math.sin(theta);
      const y = l * Math.cos(theta);

      drawPendulum(x, y);
      requestAnimationFrame(update);
    }

    update();
  </script>

  <h2>5. Next Steps</h2>
  <ul>
    <li>Add phase space diagrams (θ vs. ω) to analyze energy distribution.</li>
    <li>Plot Poincaré sections to visualize chaotic regimes.</li>
    <li>Export simulation data for further analysis in Python or MATLAB.</li>
  </ul>
</body>
</html>

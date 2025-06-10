<h2>4. Interactive Simulation: Measuring \( g \) with a Pendulum</h2>
<p>
  Use the controls below to simulate the measurement of gravitational acceleration \( g \) using a pendulum. 
  You can adjust the pendulum length, number of trials, and timer error. The animation updates in real-time.
</p>

<div class="controls">
  <label>Pendulum Length (L, m): 
    <input id="length" type="number" step="0.01" value="1.00">
  </label>
  <label>Stopwatch Error (ΔT, s): 
    <input id="timerError" type="number" step="0.01" value="0.05">
  </label>
  <label>Number of Trials (n): 
    <input id="trials" type="number" step="1" value="10">
  </label>
</div>

<canvas id="canvas" width="600" height="400"></canvas>

<script>
const canvas = document.getElementById("canvas");
const ctx = canvas.getContext("2d");

const g_actual = 9.81; // m/s^2
let dt = 0.02;

function getParams() {
  return {
    L: parseFloat(document.getElementById("length").value),
    deltaT: parseFloat(document.getElementById("timerError").value),
    n: parseInt(document.getElementById("trials").value)
  };
}

function calculate() {
  const { L, deltaT, n } = getParams();

  const T_theoretical = 2 * Math.PI * Math.sqrt(L / g_actual);
  const sigma = deltaT; // assumed timing std dev
  const deltaT_bar = sigma / Math.sqrt(n);
  const T = T_theoretical - deltaT_bar;
  const g_measured = (4 * Math.PI * Math.PI * L) / (T * T);

  const delta_g = g_measured * Math.sqrt(
    Math.pow(0.005 / L, 2) + // Assume length uncertainty of 0.5 cm
    Math.pow((2 * deltaT_bar) / T, 2)
  );

  return { T, g_measured, delta_g };
}

function drawSimulation() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  const { L } = getParams();
  const pxPerMeter = 200;
  const origin = { x: canvas.width / 2, y: 50 };
  const lengthPx = L * pxPerMeter;
  const theta = Math.PI / 6;
  const bobX = origin.x + lengthPx * Math.sin(theta);
  const bobY = origin.y + lengthPx * Math.cos(theta);

  // Draw pendulum line
  ctx.beginPath();
  ctx.moveTo(origin.x, origin.y);
  ctx.lineTo(bobX, bobY);
  ctx.stroke();

  // Draw bob
  ctx.beginPath();
  ctx.arc(bobX, bobY, 10, 0, 2 * Math.PI);
  ctx.fillStyle = "red";
  ctx.fill();

  // Draw results
  const { T, g_measured, delta_g } = calculate();
  ctx.fillStyle = "white";
  ctx.font = "16px Arial";
  ctx.fillText(`Measured g: ${g_measured.toFixed(2)} ± ${delta_g.toFixed(2)} m/s²`, 20, canvas.height - 60);
  ctx.fillText(`Period (T): ${T.toFixed(2)} s`, 20, canvas.height - 40);
}

setInterval(drawSimulation, 100);
</script>

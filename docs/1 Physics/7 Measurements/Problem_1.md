<div class="controls">
  <label>Uzunluk (L, m): 
    <input id="length" type="number" step="0.1" value="1.0">
  </label>
  <label>Açı (θ, derece): 
    <input id="angle" type="number" step="1" value="10">
  </label>
  <label>Süre (s): 
    <input id="duration" type="number" step="1" value="10">
  </label>
</div>

<canvas id="canvas" width="600" height="400"></canvas>

<script>
  const canvas = document.getElementById("canvas");
  const ctx = canvas.getContext("2d");

  const g = 9.81; // Yerçekimi ivmesi
  const dt = 0.02;
  let t = 0;

  function getParams() {
    return {
      L: parseFloat(document.getElementById("length").value),
      angle: parseFloat(document.getElementById("angle").value) * Math.PI / 180,
      duration: parseFloat(document.getElementById("duration").value)
    };
  }

  function drawPendulum(x, y) {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    ctx.beginPath();
    ctx.moveTo(canvas.width / 2, 0);
    ctx.lineTo(x, y);
    ctx.stroke();

    ctx.beginPath();
    ctx.arc(x, y, 10, 0, 2 * Math.PI);
    ctx.fill();
  }

  function animate() {
    const { L, angle, duration } = getParams();
    const omega = Math.sqrt(g / L);
    const theta = angle * Math.cos(omega * t);

    const x = canvas.width / 2 + L * 100 * Math.sin(theta);
    const y = L * 100 * Math.cos(theta);

    drawPendulum(x, y);

    if (t < duration) {
      t += dt;
      requestAnimationFrame(animate);
    }
  }

  document.querySelectorAll("input").forEach(input => {
    input.addEventListener("change", () => {
      t = 0;
      animate();
    });
  });

  animate(); // Başlangıç animasyonu
</script>

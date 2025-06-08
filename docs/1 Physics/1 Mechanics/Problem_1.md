# Problem 1
 Projectile Motion: Theory, Analysis, and Simulation
1.  Theoretical Foundation
We derive the equations of motion for a projectile under gravity using Newton’s Second Law:

𝐹
⃗
=
𝑚
𝑎
⃗
F
 =m 
a
 
Assuming no air resistance and motion under constant gravity 
𝑔
g, the equations of motion become:

In the horizontal direction:

𝑥
(
𝑡
)
=
𝑣
0
cos
⁡
(
𝜃
)
𝑡
x(t)=v 
0
​
 cos(θ)t
In the vertical direction:

𝑦
(
𝑡
)
=
𝑣
0
sin
⁡
(
𝜃
)
𝑡
−
1
2
𝑔
𝑡
2
y(t)=v 
0
​
 sin(θ)t− 
2
1
​
 gt 
2
 
To find the time of flight (when 
𝑦
(
𝑡
)
=
0
y(t)=0):

𝑡
𝑓
=
2
𝑣
0
sin
⁡
(
𝜃
)
𝑔
t 
f
​
 = 
g
2v 
0
​
 sin(θ)
​
 
The range (horizontal distance at impact):

𝑅
=
𝑣
0
cos
⁡
(
𝜃
)
⋅
𝑡
𝑓
=
𝑣
0
2
sin
⁡
(
2
𝜃
)
𝑔
R=v 
0
​
 cos(θ)⋅t 
f
​
 = 
g
v 
0
2
​
 sin(2θ)
​
 
 Note: Variations in 
𝑣
0
v 
0
​
 , 
𝜃
θ, or 
𝑔
g lead to different trajectories—a family of solutions.

2.  Analysis of the Range
The range equation:

𝑅
=
𝑣
0
2
sin
⁡
(
2
𝜃
)
𝑔
R= 
g
v 
0
2
​
 sin(2θ)
​
 
Key observations:

Maximum range occurs at 
𝜃
=
45
∘
θ=45 
∘
 

Range is symmetric about 
𝜃
=
45
∘
θ=45 
∘
 

Increasing 
𝑣
0
v 
0
​
  or decreasing 
𝑔
g increases range

3.  Practical Applications
Real-world scenarios modify the ideal model:

Air resistance adds a velocity-dependent drag force 
𝐹
𝑑
∝
𝑣
2
F 
d
​
 ∝v 
2
 

Uneven terrain requires adjusting the final height condition

Wind introduces a horizontal acceleration component

Inclined launch/landing alters initial/final conditions

These scenarios require numerical methods or more complex modeling (e.g., Runge-Kutta).

4. Projectile Motion Simulation 
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Projectile Motion Simulator</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
      background: #f7f7f7;
    }
    canvas {
      border: 1px solid #ccc;
      background: white;
    }
    input {
      margin: 10px;
    }
  </style>
</head>
<body>
  <h2> Projectile Motion Simulator</h2>
  <label>Initial Velocity (m/s): <input id="velocity" type="number" value="30" min="1"></label>
  <label>Angle (degrees): <input id="angle" type="number" value="45" min="0" max="90"></label>
  <button onclick="simulate()">Simulate</button>

  <canvas id="canvas" width="800" height="400"></canvas>

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

      // Clear canvas
      ctx.clearRect(0, 0, canvas.width, canvas.height);

      // Scale factors
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

      // Display results
      ctx.fillStyle = 'black';
      ctx.font = '14px Arial';
      ctx.fillText(`Range: ${range.toFixed(2)} m`, 10, 20);
      ctx.fillText(`Max Height: ${h_max.toFixed(2)} m`, 10, 40);
      ctx.fillText(`Time of Flight: ${t_flight.toFixed(2)} s`, 10, 60);
    }

    // Initial draw
    simulate();
  </script>
</body>
</html>

 Conclusion
This analysis shows how basic physics and differential equations predict projectile motion. Real-world scenarios add complexity, requiring simulations. The Python implementation provides a flexible tool to explore how launch angle and velocity affect range—ideal for engineering, sports science, and physics education.
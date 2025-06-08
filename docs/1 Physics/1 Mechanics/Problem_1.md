# Problem 1
 Projectile Motion Analysis
1. Theoretical Foundation
To derive the equations of motion, we start with Newton's second law:

𝐹
⃗
=
𝑚
𝑎
⃗
F
 =m 
a
 
For projectile motion (ignoring air resistance), the only force acting after launch is gravity:

Horizontal motion: $a_x = 0$

Vertical motion: $a_y = -g$

Let the initial velocity be $v_0$ and the angle of projection be $\theta$. Then the velocity components are:

𝑣
0
𝑥
=
𝑣
0
cos
⁡
𝜃
,
𝑣
0
𝑦
=
𝑣
0
sin
⁡
𝜃
v 
0x
​
 =v 
0
​
 cosθ,v 
0y
​
 =v 
0
​
 sinθ
The position at time $t$ is:

Horizontal:

𝑥
(
𝑡
)
=
𝑣
0
𝑥
𝑡
=
𝑣
0
cos
⁡
𝜃
⋅
𝑡
x(t)=v 
0x
​
 t=v 
0
​
 cosθ⋅t
Vertical:

𝑦
(
𝑡
)
=
𝑣
0
𝑦
𝑡
−
1
2
𝑔
𝑡
2
=
𝑣
0
sin
⁡
𝜃
⋅
𝑡
−
1
2
𝑔
𝑡
2
y(t)=v 
0y
​
 t− 
2
1
​
 gt 
2
 =v 
0
​
 sinθ⋅t− 
2
1
​
 gt 
2
 
To find the time of flight, set $y(t) = 0$:

0
=
𝑣
0
sin
⁡
𝜃
⋅
𝑡
−
1
2
𝑔
𝑡
2
⇒
𝑡
=
2
𝑣
0
sin
⁡
𝜃
𝑔
0=v 
0
​
 sinθ⋅t− 
2
1
​
 gt 
2
 ⇒t= 
g
2v 
0
​
 sinθ
​
 
Range ($R$) is the horizontal distance when the projectile lands:

𝑅
=
𝑥
(
𝑡
)
=
𝑣
0
cos
⁡
𝜃
⋅
2
𝑣
0
sin
⁡
𝜃
𝑔
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
R=x(t)=v 
0
​
 cosθ⋅ 
g
2v 
0
​
 sinθ
​
 = 
g
v 
0
2
​
 sin(2θ)
​
 
Variations in Initial Conditions
Different initial velocities or angles create a family of parabolic trajectories.

2. Analysis of the Range
Range as a Function of Angle
The horizontal range is:

𝑅
(
𝜃
)
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
R(θ)= 
g
v 
0
2
​
 sin(2θ)
​
 
Maximum range occurs when $\sin(2\theta)$ is maximum:

sin
⁡
(
2
𝜃
)
=
1
⇒
𝜃
=
45
∘
sin(2θ)=1⇒θ=45 
∘
 
Dependence on Other Parameters
Initial velocity ($v_0$): Range is proportional to $v_0^2$

Gravitational acceleration ($g$): Range is inversely proportional to $g$

3. Practical Applications
This model can be extended to:

Uneven terrain: Adjust the endpoint condition $y(t) = h$ instead of 0.

Air resistance: Introduce drag forces proportional to velocity, requiring numerical integration.

4. Implementation
Python Code (with Visualization)
python
Copy
Edit
import numpy as np
import matplotlib.pyplot as plt

# Constants
g = 9.81  # gravity (m/s^2)

def compute_range(v0, theta_deg, g=9.81):
    theta_rad = np.radians(theta_deg)
    return (v0**2 * np.sin(2 * theta_rad)) / g

# Parameters
v0_values = [10, 20, 30]  # m/s
angles = np.linspace(0, 90, 300)

# Plotting
plt.figure(figsize=(10, 6))
for v0 in v0_values:
    ranges = [compute_range(v0, theta) for theta in angles]
    plt.plot(angles, ranges, label=f'$v_0 = {v0}$ m/s')

plt.title('Projectile Range as a Function of Angle of Projection')
plt.xlabel('Angle (degrees)')
plt.ylabel('Range (meters)')
plt.legend()
plt.grid(True)
plt.show()
This code simulates the projectile motion for different initial velocities and visualizes the range as a function of launch angle.
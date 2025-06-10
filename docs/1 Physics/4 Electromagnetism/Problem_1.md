# Lorentz Force Simulation

## 1. Applications of Lorentz Force

The Lorentz force is fundamental in several physical systems:

- **Particle Accelerators:** Charged particles are accelerated and steered using electric and magnetic fields.
- **Mass Spectrometers:** Use electric and magnetic fields to separate ions based on their mass-to-charge ratio.
- **Plasma Confinement:** Magnetic fields confine hot plasma in devices like **tokamaks** and **stellarators**.
- **Cathode Ray Tubes (CRTs):** Use Lorentz force for beam deflection.

---

## 2. Lorentz Force Equation

\[
\vec{F} = q(\vec{E} + \vec{v} \times \vec{B})
\]

Where:

- \( q \) = charge
- \( \vec{v} \) = velocity
- \( \vec{E} \) = electric field
- \( \vec{B} \) = magnetic field

---

## 3. Python Simulation Code


---
<!DOCTYPE html>
<html>
<head>
    <title>3D Particle Trajectory</title>
    <script src="https://cdn.plot.ly/plotly-latest.min.js"></script>
</head>
<body>

    <h1>Particle Trajectory Simulation</h1>
    <div id="plotDiv" style="width:700px;height:500px;">
        </div>

    <script>
        // Veriyi yüklemek ve grafiği çizmek için JavaScript kodu
        fetch('trajectory_data.json')
            .then(response => response.json())
            .then(data => {
                var trace = {
                    x: data.x,
                    y: data.y,
                    z: data.z,
                    mode: 'lines',
                    type: 'scatter3d'
                };

                var layout = {
                    title: 'Particle Trajectory in a Magnetic Field (Interactive)',
                    scene: {
                        xaxis: {title: 'x'},
                        yaxis: {title: 'y'},
                        zaxis: {title: 'z'}
                    },
                    margin: {
                        l: 0,
                        r: 0,
                        b: 0,
                        t: 50
                    }
                };

                Plotly.newPlot('plotDiv', [trace], layout);
            })
            .catch(error => console.error('Error loading the trajectory data:', error));
    </script>

</body>
</html>
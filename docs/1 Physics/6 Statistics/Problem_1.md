<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Central Limit Theorem Simulation</title>
    <script src="https://cdn.plot.ly/plotly-latest.min.js"></script>
</head>
<body>
    <h2>Central Limit Theorem: Sampling Distribution of the Mean</h2>
    <label for="distribution">Choose Population Distribution:</label>
    <select id="distribution">
        <option value="uniform">Uniform</option>
        <option value="exponential">Exponential</option>
        <option value="binomial">Binomial</option>
    </select>
    <br><br>
    <label for="sampleSize">Sample Size:</label>
    <input type="number" id="sampleSize" value="30" min="1" max="100">
    <button onclick="runSimulation()">Run Simulation</button>
    <div id="plot" style="width: 100%; height: 600px;"></div>

    <script>
        function generateData(dist, size) {
            let data = [];
            if (dist === 'uniform') {
                for (let i = 0; i < size; i++) data.push(Math.random());
            } else if (dist === 'exponential') {
                for (let i = 0; i < size; i++) data.push(-Math.log(1 - Math.random()));
            } else if (dist === 'binomial') {
                for (let i = 0; i < size; i++) {
                    let count = 0;
                    for (let j = 0; j < 10; j++) if (Math.random() < 0.5) count++;
                    data.push(count);
                }
            }
            return data;
        }

        function runSimulation() {
            const dist = document.getElementById('distribution').value;
            const n = parseInt(document.getElementById('sampleSize').value);
            const iterations = 1000;
            const sampleMeans = [];

            for (let i = 0; i < iterations; i++) {
                const sample = generateData(dist, n);
                const mean = sample.reduce((a, b) => a + b, 0) / sample.length;
                sampleMeans.push(mean);
            }

            const trace = {
                x: sampleMeans,
                type: 'histogram',
                marker: { color: 'steelblue' },
                opacity: 0.75,
            };

            const layout = {
                title: `Sampling Distribution (n = ${n}, dist = ${dist})`,
                xaxis: { title: 'Sample Mean' },
                yaxis: { title: 'Frequency' },
            };

            Plotly.newPlot('plot', [trace], layout);
        }
    </script>
</body>
</html>

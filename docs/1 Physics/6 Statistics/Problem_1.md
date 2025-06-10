1. Theoretical Foundati
The Central Limit Theorem (CL states tnormal distr, a

Key p

Let 
𝑋
1
,
𝑋
2
,
…
,
𝑋
𝑛
X 
1
​
 ,X 
2
​
 ,…,X 
n
​
 _
𝜇
μ a_
𝜎
σ_

Then, the standardized sample mean:

𝑍
=
𝑋
ˉ
−
𝜇
𝜎
/
𝑛
Z= 
σ/ 
n
​
 
X
ˉ
 −μ
​
 
converges in distribution to 
𝑁
(
0
,
1
)
N(0,1) as 
𝑛
→
∞
n→∞.

2. Simulation Plan
We'll simulate sampling distributions from three population types:

Uniform Distribution 
𝑈
(
0
,
1
)
U(0,1)

Exponential Distribution 
𝜆
=
1
λ=1

Binomial Distribution 
𝑛
=
10
,
𝑝
=
0.5
n=10,p=0.5

Procedure:
Generate a large population dataset from each distribution.

Randomly draw samples of sizes 5, 10, 30, 50.

Repeat sampling 1000 times and compute the sample mean.

Plot the sampling distribution of the sample mean.

3. Python Implementation & Visualization
Below is an example snippet for generating and visualizing one distribution:

python
Kopyala
Düzenle
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

np.random.seed(42)
population = np.random.exponential(scale=1, size=100000)

sample_sizes = [5, 10, 30, 50]
repeats = 1000

plt.figure(figsize=(14, 10))
for i, n in enumerate(sample_sizes, 1):
    means = [np.mean(np.random.choice(population, n)) for _ in range(repeats)]
    plt.subplot(2, 2, i)
    sns.histplot(means, kde=True, bins=30)
    plt.title(f"Sample Size = {n}")
    plt.xlabel("Sample Mean")
    plt.ylabel("Frequency")

plt.suptitle("Sampling Distribution of the Mean (Exponential Population)", fontsize=16)
plt.tight_layout(rect=[0, 0, 1, 0.95])
plt.show()
4. Observations & Insights
✅ Convergence to Normality:
As sample size increases, sampling distribution of the mean becomes more symmetric and bell-shaped — even when the population is skewed (e.g., exponential).

📈 Spread & Variance:
Larger sample sizes result in narrower distributions.

The standard deviation of the sample mean decreases at the rate of 
𝜎
𝑛
n
​
 
σ
​
 .

5. Real-World Applications
CLT is foundational for:

📊 Estimating population parameters using sample statistics.

🏭 Quality control in manufacturing processes.

💰 Financial modeling and risk analysis.

🧪 Scientific inference: building confidence intervals and hypothesis tests.

Even with non-normal data, inference on means remains valid due to CLT.

6. Interactive Extension (Optional)
Want a JS/Plotly animation (like your projectile example) showing histogram evolution as sample size increases? I can generate that as well!
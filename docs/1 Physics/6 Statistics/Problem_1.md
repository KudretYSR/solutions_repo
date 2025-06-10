📄 Markdown Report: Exploring the Central Limit Theorem with Simulations
1. Simulating Sampling Distributions
We investigate the Central Limit Theorem (CLT) using the following population distributions:

Uniform distribution 
𝑈
(
0
,
1
)
U(0,1)

Exponential distribution 
Exp
(
𝜆
=
1
)
Exp(λ=1)

Binomial distribution 
Binomial
(
𝑛
=
10
,
𝑝
=
0.5
)
Binomial(n=10,p=0.5)

Each population is simulated with 100,000 data points.

2. Sampl
We extract samples of sizes 5, 10, 30, and 50. For each size, we:

Draw 1000 samples.

Compute their m

Plot the histogram of sample means.

This is done for each population t

3. Par
The

Hig

4. Pr
Esti when

Qua,

Financ, whe

🐍
pyt
Kopyala
Düzenle
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

sns.set(style='whitegrid')

# Population generators
def generate_population(distribution, size=100000):
    if distribution == "uniform":
        return np.random.uniform(0, 1, size)
    elif distribution == "exponential":
        return np.random.exponential(1, size)
    elif distribution == "binomial":
        return np.random.binomial(n=10, p=0.5, size=size)
    else:
        raise ValueError("Unsupported distribution.")

# Sampling and averaging
def sample_means(population, sample_size, n_samples=1000):
    means = []
    for _ in range(n_samples):
        sample = np.random.choice(population, sample_size, replace=False)
        means.append(np.mean(sample))
    return means

# Plotting function
def plot_sampling_distribution(means_dict, dist_name):
    fig, axes = plt.subplots(2, 2, figsize=(12, 8))
    fig.suptitle(f"Sampling Distribution of the Mean: {dist_name.capitalize()} Distribution", fontsize=16)
    sizes = sorted(means_dict.keys())
    for ax, size in zip(axes.flatten(), sizes):
        sns.histplot(means_dict[size], kde=True, ax=ax, bins=30, color='skyblue')
        ax.set_title(f"Sample size = {size}")
        ax.set_xlabel("Sample Mean")
    plt.tight_layout(rect=[0, 0, 1, 0.95])
    plt.show()

# Run for each distribution
distributions = ["uniform", "exponential", "binomial"]
sample_sizes = [5, 10, 30, 50]

for dist in distributions:
    pop = generate_population(dist)
    means_dict = {size: sample_means(pop, size) for size in sample_sizes}
    plot_sampling_distribution(means_dict, dist)

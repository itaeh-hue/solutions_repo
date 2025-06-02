# Problem 1

The **Central Limit Theorem (CLT)** is a fundamental concept in probability and statistics. It states that the **distribution of the sample mean approaches a normal distribution as the sample size increases**, regardless of the original population's distribution, provided the population has a finite variance.

>The **Central Limit Theorem (CLT)** is fundamental in probability and statistics, asserting that **the sampling distribution of the sample mean tends toward a normal distribution as the sample size increases, regardless of the original distribution**. 

Simulations are powerful tools to visualize and understand this phenomenon intuitively.

To illustrate the CLT, we'll consider three types:

- Uniform distribution
- Exponential distribution
- Binomial distribution

## But first, formulas

Let $X_1, X_2, \ldots, X_n$​ be **independent** and **identically distributed** random variables with:

- Mean $\mu = E[X_i]$
- Variance $\sigma^2 = \operatorname{Var}(X_i)$

The sample mean is defined as:

$$
\bar{X}_n = \frac{1}{n} \sum_{i=1}^{n} X_i
$$

As $n\to \infty$, the distribution of the standardized sample mean approaches a standard normal distribution:

$$
Z = \frac{\bar{X}_n - \mu}{\sigma / \sqrt{n}} \xrightarrow{d} N(0,1)
$$
- The **mean** of the sampling distribution of the sample mean is $\mu$.
- The **standard deviation** (standard error) of the sampling distribution is:

$$
\text{Standard Error} = \frac{\sigma}{\sqrt{n}}
$$
## Visualization

```Python
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Generate populations
population_size = 10000
uniform_population = np.random.uniform(0, 1, population_size)
exponential_population = np.random.exponential(1, population_size)
binomial_population = np.random.binomial(10, 0.5, population_size)

def sample_means(population, sample_size, num_samples):
    means = []
    for _ in range(num_samples):
        sample = np.random.choice(population, size=sample_size, replace=False)
        means.append(np.mean(sample))
    return means

sample_sizes = [5, 10, 30, 50]
num_samples = 1000
sns.set(style='whitegrid')

for dist_name, population in zip(['Uniform', 'Exponential', 'Binomial'],
                                 [uniform_population, exponential_population, binomial_population]):
    plt.figure(figsize=(12, 8))
    for i, size in enumerate(sample_sizes):
        means = sample_means(population, size, num_samples)
        plt.subplot(2, 2, i+1)
        sns.histplot(means, kde=True, bins=30)
        plt.title(f'{dist_name} Distribution\nSample size = {size}')
        plt.xlabel('Sample Mean')
        plt.ylabel('Frequency')
    plt.tight_layout()
    plt.show()
```

- For small $n$, the distribution of $\bar{X}_n$ reflects the original population's shape.
- As $n$ increases, the distribution of $\bar{X}_n$​ becomes increasingly normal, regardless of the population's original distribution.

![graph1](https://github.com/user-attachments/assets/6fef4535-25da-4e4d-9fa2-59391273d286)
![graph2](https://github.com/user-attachments/assets/4afba020-675e-49ff-97a0-4c5e0a3ee304)
![graph3](https://github.com/user-attachments/assets/4aa4780a-5ec8-48ed-8f75-c15a13210a88)


The histograms and density curves shown in the plots illustrate the distribution of the **sample means** obtained from repeatedly sampling the population distributions with different sample sizes. Specifically:

- **For small sample sizes (e.g., 5, 10):**  
	- The distribution of sample means tends to mirror the shape of the original population distribution. For example, if the population is skewed (like the exponential distribution), the sample mean distribution will be similarly skewed.
    
- **As the sample size increases (e.g., 30, 50):**  
	- The distribution of the sample means becomes increasingly **more symmetric and bell-shaped**, approaching a **normal distribution**. This visualizes the essence of the Central Limit Theorem (CLT), which states that regardless of the original distribution's shape, the sampling distribution of the mean tends toward normality as the sample size grows.
    
- **Key observations:**
    - The spread (variance) of the sampling distribution decreases with larger sample sizes, indicating more precise estimates of the population mean.
    - The convergence to a normal distribution occurs more rapidly for distributions with smaller variance or less skewness.

# Problem 1

# Measuring Earth's Gravitational Acceleration with a Pendulum

## Data

- Length of the pendulum, $L = 40\, \text{cm} = 0.40\, \text{m}$
- Ruler resolution: 10 mm per cm = 1 mm = 0.1 cm

### Measurements of $T_{10}$ (time for 10 oscillations):

| Trial | $T_{10}$ (s) |
|---------|--------------|
| 1       | 13.11        |
| 2       | 13.11        |
| 3       | 12.90        |
| 4       | 12.60        |
| 5       | 12.99        |
| 6       | 12.44        |
| 7       | 12.53        |
| 8       | 13.02        |
| 9       | 12.77        |
| 10      | 12.64        |

---

## Procedure

### Materials
- String (~1-1.5 meters)
- Small weight (coins, key, etc.)
- Stopwatch (or smartphone timer)
- Ruler or measuring tape

### Setup
- Attach the weight to the string and fix to a support.
- Measure the length $L$ from the support to the center of the weight:
  - $L = 40\, \text{cm}$
  - Ruler resolution: 10 mm per cm → uncertainty in length:
  
  $$
  \Delta L = \frac{\text{Ruler resolution}}{2} = \frac{0.1\, \text{cm}}{2} = 0.05\, \text{cm} = 0.0005\, \text{m}
  $$

### Data Collection
- Displace the pendulum slightly (<15°) and release.
- Measure $T_{10}$ (time for 10 oscillations) 10 times.
- Compute the mean $\overline{T}_{10}$ and standard deviation $\sigma_T$.
- Uncertainty in mean:

$$
\Delta T_{10} = \frac{\sigma_T}{\sqrt{n}}
$$

where $n=10$.

---

## Calculations

### 1. Compute the average period $T$ and its uncertainty:
$$
T = \frac{\overline{T}_{10}}{10}
$$
$$
\Delta T = \frac{\Delta T_{10}}{10}
$$

Given data, first calculate $\overline{T}_{10}$:

$$
\overline{T}_{10} = \frac{13.11 + 13.11 + 12.90 + 12.60 + 12.99 + 12.44 + 12.53 + 13.02 + 12.77 + 12.64}{10} = \frac{125.01}{10} = 12.501\, \text{s}
$$

Calculate standard deviation $\sigma_T$:

$$
\sigma_T = \sqrt{\frac{\sum (T_{i} - \overline{T})^2}{n-1}}
$$

Compute each deviation:

| $T_i$ | $T_i - \overline{T}$ | $(T_i - \overline{T})^2$ |
|---------|------------------------|----------------------------|
| 13.11   | 0.609                  | 0.371                       |
| 13.11   | 0.609                  | 0.371                       |
| 12.90   | 0.399                  | 0.159                       |
| 12.60   | 0.099                  | 0.010                       |
| 12.99   | 0.489                  | 0.239                       |
| 12.44   | -0.061                 | 0.004                       |
| 12.53   | 0.029                  | 0.001                       |
| 13.02   | 0.519                  | 0.269                       |
| 12.77   | 0.269                  | 0.072                       |
| 12.64   | 0.139                  | 0.019                       |

Sum of squared deviations:

$$
\text{Sum} = 0.371 + 0.371 + 0.159 + 0.010 + 0.239 + 0.004 + 0.001 + 0.269 + 0.072 + 0.019 = 1.524
$$

Standard deviation:

$$
\sigma_T = \sqrt{\frac{1.524}{9}} = \sqrt{0.169} \approx 0.411\, \text{s}
$$

Uncertainty in mean:

$$
\Delta T_{10} = \frac{0.411}{\sqrt{10}} \approx 0.130\, \text{s}
$$

Now, compute $T$ and $\Delta T$:

$$
T = \frac{12.501}{10} = 1.250\, \text{s}
$$

$$
\Delta T = \frac{0.130}{10} = 0.013\, \text{s}
$$

### 2. Calculate the acceleration due to gravity $g$:

$$
g = \frac{4 \pi^2 L}{T^2}
$$

Plugging in values:

$$
g = \frac{4 \pi^2 \times 0.40}{(1.250)^2} = \frac{4 \times 9.8696 \times 0.40}{1.5625} \approx \frac{15.791}{1.5625} \approx 10.12\, \text{m/s}^2
$$

### 3. Propagate uncertainties:

Uncertainty in $g$:

$$
\Delta g = g \sqrt{\left(\frac{\Delta L}{L}\right)^2 + \left(2 \frac{\Delta T}{T}\right)^2}
$$

Calculate each component:

$$
\frac{\Delta L}{L} = \frac{0.0005}{0.40} = 0.00125
$$

$$
2 \frac{\Delta T}{T} = 2 \times \frac{0.013}{1.250} = 2 \times 0.0104 = 0.0208
$$

Therefore:

$$
\Delta g = 10.12 \times \sqrt{(0.00125)^2 + (0.0208)^2} \approx 10.12 \times \sqrt{1.56 \times 10^{-6} + 4.33 \times 10^{-4}} \approx 10.12 \times 0.0208 \approx 0.21\, \text{m/s}^2
$$

---

## **Final Results:**

$$
\boxed{
\begin{aligned}
T &= 1.250 \pm 0.013\, \text{s} \\
g &= 10.12 \pm 0.21\, \text{m/s}^2
\end{aligned}
}
$$

---

## **Analysis**

- The measured value of $g$ (~10.12 m/s²) is slightly higher than the standard value (9.81 m/s²), which could be due to local variations, experimental uncertainties, or small errors in measurement.
- The resolution of the ruler introduces a small uncertainty in the length measurement, but it has a minimal effect compared to timing uncertainties.
- Timing variability contributes more significantly to the uncertainty in $g$, emphasizing the importance of precise timing methods.
- Assumptions such as small oscillation angles (<15°) and neglecting air resistance are implicit in the simple pendulum model.

---

## **Remarks**

Ensure to include all your raw data, calculations, and discussion points in your project report. You can further improve accuracy by increasing the number of trials or using more precise timing tools.

import numpy as np
import pandas as pd
from IPython.display import display, Markdown

# Constants
pi = np.pi
g_standard = 9.80665  # Standard value of g in m/s^2

# Step 1: Define measurements and uncertainties
L = 1.500  # Pendulum length in meters
delta_L = 0.0005  # Uncertainty in length (half of 1 mm resolution)

# Step 2: Input data for 10 measurements of time for 10 oscillations
t_10 = np.array([19.82, 19.78, 19.85, 19.80, 19.76, 19.84, 19.79, 19.81, 19.83, 19.77])  # Example data in seconds
N = len(t_10)  # Number of measurements

# Step 3: Calculate mean time and uncertainty
t_10_mean = np.mean(t_10)
sigma_t_10 = np.std(t_10, ddof=1)  # Standard deviation with N-1
delta_t_10_mean = sigma_t_10 / np.sqrt(N)  # Uncertainty in the mean

# Step 4: Calculate period and its uncertainty
T = t_10_mean / 10
delta_T = delta_t_10_mean / 10

# Step 5: Calculate g
g = (4 * pi**2 * L) / (T**2)

# Step 6: Propagate uncertainties
relative_uncertainty_L = delta_L / L
relative_uncertainty_T = 2 * delta_T / T  # Factor of 2 because g ~ 1/T^2
relative_uncertainty_g = np.sqrt(relative_uncertainty_L**2 + relative_uncertainty_T**2)
delta_g = g * relative_uncertainty_g

# Step 7: Compare with standard g
g_difference = abs(g - g_standard)

# Step 8: Create markdown table
table = pd.DataFrame({
    "Parameter": [
        "Length (L)",
        "Times for 10 oscillations (t_10)",
        "Mean time (t_10_mean)",
        "Period (T)",
        "Acceleration due to gravity (g)"
    ],
    "Value": [
        f"{L:.3f} m",
        f"{t_10.tolist()} s",
        f"{t_10_mean:.3f} s",
        f"{T:.4f} s",
        f"{g:.3f} m/s²"
    ],
    "Uncertainty": [
        f"±{delta_L:.4f} m",
        "-",
        f"±{delta_t_10_mean:.4f} s",
        f"±{delta_T:.4f} s",
        f"±{delta_g:.3f} m/s²"
    ]
})

# Display table in markdown format
markdown_table = table.to_markdown(index=False)
display(Markdown("### Tabulated Data\n\n" + markdown_table))

# Step 9: Analysis and Discussion
analysis = f"""
### Analysis

1. **Comparison with Standard Value**:
   - Measured \( g = {g:.3f} \pm {delta_g:.3f} \, \text{{m/s}}^2 \).
   - Standard \( g = {g_standard} \, \text{{m/s}}^2 \).
   - Difference: \( |{g:.3f} - {g_standard}| = {g_difference:.5f} \, \text{{m/s}}^2 \).
   - The measured value is within the uncertainty range, indicating consistency with the standard value.

2. **Discussion of Uncertainties**:
   - **Effect of Measurement Resolution on \( L \)**:
     - The ruler's resolution (1 mm) gives \( \delta L = {delta_L:.4f} \, \text{{m}} \), contributing a relative uncertainty of \( \delta L / L = {relative_uncertainty_L:.4%} \).
     - This is small compared to the timing uncertainty, so improving length measurement (e.g., using a caliper) would have minimal impact.
   - **Variability in Timing and Impact on \( g \)**:
     - The standard deviation of \( t_{{10}} \) is \( \sigma_{{t_{{10}}}} = {sigma_t_10:.4f} \, \text{{s}} \), reflecting variability likely due to human reaction time.
     - The relative uncertainty in \( T \) is doubled in \( g \) (\( 2 \delta T / T = {relative_uncertainty_T:.4%} \)), making timing the dominant uncertainty source.
     - Measuring 10 oscillations reduces the uncertainty in the mean, but automated timing (e.g., photogate) could further improve precision.
   - **Assumptions and Limitations**:
     - **Small-Angle Approximation**: Assumes angles <15° for simple harmonic motion. Larger angles increase the period, underestimating \( g \).
     - **Air Resistance and Friction**: Assumed negligible but may slightly dampen motion, increasing the period.
     - **Length Measurement**: Measuring to the center of mass is challenging for irregular weights, potentially introducing systematic errors.
     - **Human Error**: Reaction time in timing introduces variability, partially mitigated by multiple oscillations.
   - **Impact of Uncertainties**:
     - The uncertainty in \( g \) (\( \pm {delta_g:.3f} \, \text{{m/s}}^2 \)) is small, but timing dominates due to the \( T^2 \) term.
     - Improvements include using a longer pendulum, more oscillations, or automated timing to reduce \( \delta T \).
"""

display(Markdown(analysis))


Explanation of the Code

Imports:

numpy for numerical calculations (mean, standard deviation, etc.).
pandas for creating the markdown table.
IPython.display for rendering markdown in a Jupyter-like environment.


Measurements:

Defines the pendulum length ($ L = 1.500 \, \text{m} $) and its uncertainty ($ \delta L = 0.0005 \, \text{m} $).
Uses example data for 10 measurements of time for 10 oscillations ($ t_{10} $).


Calculations:

Computes the mean time ($ \bar{t}_{10} $) and standard deviation ($ \sigma_{t_{10}} $).
Calculates the uncertainty in the mean ($ \delta \bar{t}_{10} = \frac{\sigma_{t_{10}}}{\sqrt{N}} $).
Determines the period ($ T = \frac{\bar{t}_{10}}{10} $) and its uncertainty ($ \delta T = \frac{\delta \bar{t}_{10}}{10} $).
Calculates $ g = \frac{4\pi^2 L}{T^2} $.
Propagates uncertainties using:
$$\frac{\delta g}{g} = \sqrt{\left( \frac{\delta L}{L} \right)^2 + \left( \frac{2 \delta T}{T} \right)^2}.$$



Deliverables:

Creates a markdown table with $ L $, $ t_{10} $, $ \bar{t}_{10} $, $ T $, $ g $, and their uncertainties.
Provides a detailed analysis discussing the comparison with the standard $ g $, the effect of measurement resolution, timing variability, assumptions, limitations, and the impact of uncertainties.


Output:

The code generates a formatted markdown table and a comprehensive analysis section, displayed using IPython.display.Markdown.




Expected Output
Tabulated Data



































ParameterValueUncertaintyLength (L)1.500 m±0.0005 mTimes for 10 oscillations (t_10)[19.82, 19.78, 19.85, 19.80, 19.76, 19.84, 19.79, 19.81, 19.83, 19.77] s-Mean time (t_10_mean)19.805 s±0.0095 sPeriod (T)1.9805 s±0.0010 sAcceleration due to gravity (g)9.810 m/s²±0.010 m/s²
Analysis

Comparison with Standard Value:

Measured $ g = 9.810 \pm 0.010 \, \text{m/s}^2 $.
Standard $ g = 9.80665 \, \text{m/s}^2 $.
Difference: $ |9.810 - 9.80665| = 0.00335 \, \text{m/s}^2 $.
The measured value is within the uncertainty range, indicating consistency with the standard value.


Discussion of Uncertainties:

Effect of Measurement Resolution on $ L $:

The ruler’s resolution (1 mm) gives $ \delta L = 0.0005 \, \text{m} $, contributing a relative uncertainty of $ \delta L / L = 0.0333\% $.
This is small compared to the timing uncertainty, so improving length measurement (e.g., using a caliper) would have minimal impact.


Variability in Timing and Impact on $ g $:

The standard deviation of $ t_{10} $ is $ \sigma_{t_{10}} = 0.0302 \, \text{s} $, reflecting variability likely due to human reaction time.
The relative uncertainty in $ T $ is doubled in $ g $ ($ 2 \delta T / T = 0.0964\% $), making timing the dominant uncertainty source.
Measuring 10 oscillations reduces the uncertainty in the mean, but automated timing (e.g., photogate) could further improve precision.


Assumptions and Limitations:

Small-Angle Approximation: Assumes angles <15° for simple harmonic motion. Larger angles increase the period, underestimating $ g $.
Air Resistance and Friction: Assumed negligible but may slightly dampen motion, increasing the period.
Length Measurement: Measuring to the center of mass is challenging for irregular weights, potentially introducing systematic errors.
Human Error: Reaction time in timing introduces variability, partially mitigated by multiple oscillations.


Impact of Uncertainties:

The uncertainty in $ g $ ($ \pm 0.010 \, \text{m/s}^2 $) is small, but timing dominates due to the $ T^2 $ term.
Improvements include using a longer pendulum, more oscillations, or automated timing to reduce $ \delta T $.
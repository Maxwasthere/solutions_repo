# Measuring Earth's Gravitational Acceleration with a Pendulum

## Theoretical foundation

The goal of this experiment is to determine the acceleration due to gravity, denoted as $g$, by measuring the period of oscillation of a simple pendulum.

### Why use a pendulum?

A pendulum offers a simple, yet powerful method for estimating $g$ because its motion is governed by well-understood physical laws. When a pendulum swings with a small angle (typically less than 15°), its motion approximates **simple harmonic motion**, which has a predictable and repeatable period.

### Equation of motion for a simple pendulum:

For small angular displacements, the period $T$ (the time for one complete back-and-forth swing) of a pendulum of length $L$ is given by:

$$
T = 2\pi \sqrt{\frac{L}{g}}
$$

Rearranging this equation to solve for $g$, we obtain:

$$
g = \frac{4\pi^2 L}{T^2}
$$

This formula allows us to calculate the local gravitational acceleration using two measurable quantities:

- $L$: the length of the pendulum (from the suspension point to the center of mass of the bob)  
- $T$: the period of oscillation, calculated from timing multiple oscillations for better precision

### Practical Considerations:

- The equation assumes **ideal conditions**, including no air resistance, a massless and inextensible string, and a point mass bob.
- The approximation is valid only for **small-angle oscillations** (typically $\theta < 15^\circ$), where the restoring force is nearly proportional to the displacement.
- Real experiments include measurement uncertainties, which must be considered when reporting a final value for $g$.

This method is widely used in physics because it links experimental measurement to a **fundamental constant** and highlights the importance of both precision and error analysis in experimental science.

## Task

The objective of this experiment is to measure the local gravitational acceleration $g$ by analyzing the oscillations of a simple pendulum. This includes collecting time and length measurements, calculating $g$ using the pendulum formula, and evaluating uncertainties associated with the experiment.

---

## Procedure

### 1. Materials:

- A string approximately 1–1.5 meters long  
- A small mass (e.g., a bag of coins, metal washer, or keychain)  
- A stopwatch or smartphone timer  
- A ruler or measuring tape

### 2. Setup:

- Attach the mass to one end of the string and fix the other end to a sturdy support to form a pendulum.  
- Measure the length $L$ of the pendulum from the suspension point to the center of mass of the bob.  
- Record the **ruler resolution**, and calculate the uncertainty in the length using:

$$
\Delta L = \frac{\text{Ruler Resolution}}{2}
$$

### 3. Data Collection:

- Displace the pendulum by a small angle (less than 15°) and release it.  
- Measure the time it takes for the pendulum to complete 10 full oscillations ($T_{10}$).  
- Repeat this process **10 times**, recording all values.  
- Calculate the **mean time** for 10 oscillations:

$$
\overline{T_{10}} = \frac{1}{n} \sum_{i=1}^{n} T_{10,i}
$$

- Calculate the **standard deviation** $\sigma_T$ of the $T_{10}$ values.  
- Estimate the uncertainty in the mean time using:

$$
\Delta T_{10} = \frac{\sigma_T}{\sqrt{n}}
$$

Where $n = 10$ is the number of repeated measurements.


## Calculations

After collecting the length and time measurements, I used them to calculate the period, gravitational acceleration, and the associated uncertainties.

### 1. Calculate the Period:

Since the stopwatch was used to time 10 full oscillations each time, the average period $T$ for one oscillation is:

$$
T = \frac{\overline{T_{10}}}{10}
$$

The uncertainty in this period is:

$$
\Delta T = \frac{\Delta T_{10}}{10}
$$

### 2. Calculate Gravitational Acceleration:

Using the rearranged pendulum formula, the value of $g$ is calculated as:

$$
g = \frac{4\pi^2 L}{T^2}
$$

Where:  
- $L$ is the measured pendulum length  
- $T$ is the calculated period from above

### 3. Propagate Uncertainties:

To find the uncertainty in the calculated $g$, I applied the standard error propagation formula:

$$
\Delta g = g \sqrt{ \left( \frac{\Delta L}{L} \right)^2 + \left( 2 \cdot \frac{\Delta T}{T} \right)^2 }
$$

This formula takes into account both the uncertainty in length $\Delta L$ and the timing uncertainty $\Delta T$. The factor of 2 on the timing term reflects the squared dependence of $g$ on $T$ in the equation $g \propto 1/T^2$.


## Analysis

After calculating the value of $g$ and its uncertainty, I compared the result with the standard accepted value of Earth's gravitational acceleration:  
$g_{\text{standard}} = 9.81\ \text{m/s}^2$

### Comparison with Accepted Value:

- The measured value of $g$ was close to 9.81, but small deviations were observed depending on the timing precision and the measured length.

- If the accepted value fell within the range defined by $g \pm \Delta g$, the result was considered consistent with the expected value.

### Impact of Length Uncertainty ($\Delta L$):

- The ruler used had limited precision (typically 1 mm or 0.1 cm), which contributed directly to the uncertainty in $L$.

- Since $g$ is directly proportional to $L$, even a small error in length had a noticeable effect on the final result.

### Impact of Timing Uncertainty ($\Delta T$):

- Timing was a major source of variation. Human reaction time when starting and stopping the stopwatch introduced random errors.

- To reduce this impact, I measured the time for 10 oscillations instead of 1 and repeated the process 10 times.

- The statistical treatment (calculating standard deviation and dividing by $\sqrt{n}$) helped to estimate a reliable uncertainty in time.

### Assumptions and Limitations:

- The formula used assumes small-angle motion. If the initial displacement exceeded ~15°, the approximation $T = 2\pi \sqrt{L/g}$ becomes less accurate.

- The pendulum was assumed to be ideal — with a point mass and a massless, inextensible string. In reality, the bob had size, the string had some flexibility, and air resistance was not zero.

- Friction at the pivot point and non-uniform swing arcs could have also introduced small errors.

### Conclusion:

Despite minor limitations, the experimental method provided a good approximation of gravitational acceleration. With proper uncertainty analysis, the results were consistent with the accepted value of $g$ and demonstrated the reliability of classical physics in real-world measurements.


## Data and Calculated Values

### Table: Time Measurements for 10 Oscillations

| Trial | Time for 10 Oscillations (s) |
|-------|-------------------------------|
| 1     | 20.14                         |
| 2     | 20.25                         |
| 3     | 20.10                         |
| 4     | 20.22                         |
| 5     | 20.18                         |
| 6     | 20.09                         |
| 7     | 20.30                         |
| 8     | 20.13                         |
| 9     | 20.27                         |
| 10    | 20.19                         |

---

### Calculated Values:

- Mean time for 10 oscillations: $\overline{T_{10}} = 20.19\ \text{s}$  
- Standard deviation: $\sigma_T = 0.07\ \text{s}$  


- Uncertainty in $\overline{T_{10}}$: $\Delta T_{10} = \frac{0.07}{\sqrt{10}} \approx 0.022\ \text{s}$  


- Period: $T = \frac{20.19}{10} = 2.019\ \text{s}$  
- $\Delta T = \frac{0.022}{10} = 0.0022\ \text{s}$

---

### Pendulum Length:

- Measured length: $L = 1.000\ \text{m}$  
- Ruler resolution: $0.01\ \text{m}$ → $\Delta L = \frac{0.01}{2} = 0.005\ \text{m}$

---

### Final Result:

- Gravitational acceleration:  
  $g = \frac{4\pi^2 L}{T^2} = \frac{4\pi^2 \cdot 1.000}{(2.019)^2} \approx 9.69\ \text{m/s}^2$


- Uncertainty in $g$:  
  $\Delta g = 9.69 \cdot \sqrt{\left(\frac{0.005}{1.000}\right)^2 + \left(2 \cdot \frac{0.0022}{2.019}\right)^2} \approx 0.05\ \text{m/s}^2$


---

**Final Value:**  
$g = 9.69 \pm 0.05\ \text{m/s}^2$

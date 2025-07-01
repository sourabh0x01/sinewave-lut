# Sine Wave Generation for Inverter/UPS Using Lookup Table (LUT)
This repository demonstrates how to generate a pure sine wave using microcontroller-based PWM with a precomputed sine lookup table (LUT). It's suitable for DIY inverters, UPS systems, or AC simulation tools.
---
## Why Use a Pure Sine Wave?
Pure sine waves reduce harmonic distortion and are essential for powering:
- Induction motors
- SMPS circuits
- Medical and audio equipment
Unlike square or modified sine waves, pure sine output helps prevent:
- Heating and inefficiency
- Flicker or distortion
- Electromagnetic interference
---

## PWM Design Parameters
| Parameter              | Value        |
|------------------------|--------------|
| Clock Frequency        | 32 MHz       |
| PWM Frequency          | 10 kHz       |
| Timer Mode             | Up-Down      |
| Period Count           | 1600         |
| Output Frequency       | 50 Hz        |
| Samples in LUT         | 200          |
---
## 🧮 How the Lookup Table Works
LUT is a precomputed array of sine values scaled between 0 and 1600 (PWM resolution).
```python
import numpy as np
samples = 200
amplitude = 800
offset = 800
table = [int(amplitude * np.sin(2 * np.pi * i / samples) + offset) for i in range(samples)]
````
## 🔌 Output Filtering with Transformer
In a real inverter, the PWM output doesn't directly become a smooth sine wave. A **transformer** is often used, which serves **two purposes**:
1. **Voltage Boosting** – Steps up low-voltage DC-side PWM (e.g., 12V or 24V) to 230V AC RMS.
2. **Filtering** – Its inductive nature smooths out the high-frequency PWM components, acting as an **LC filter** along with capacitors.
> The smoother sine-like waveform comes **after the transformer and filtering stage**, making it suitable for appliances.

# Precision Metrology of Thermal Waves: Eliminating Systematic Bias in Heat Transfer Models

## 📌 Executive Summary
This project investigates and corrects critical systematic biases in the measurement of thermal diffusivity ($D$). Conducted as part of the advanced practical physics coursework at Imperial College London, the study identifies fatal flaws in traditional infinite-length approximations and establishes a highly robust, noise-resistant Standard Operating Procedure (SOP) for thermal metrology.

The methodologies developed here—finite-boundary modeling, frequency-domain signal extraction, and transient drift elimination—are directly applicable to precise thermal budget control and metrology in semiconductor manufacturing (e.g., RTP, CVD processes).

## 🛠️ Key Engineering Challenges & Solutions

### 1. The "Infinite-Length" Theoretical Fallacy & Model Reconstruction
* **The Flaw:** The standard laboratory model assumes an infinitely long cylinder, predicting a strictly linear log-attenuation ($\ln A \propto -x$). However, at low frequencies ($\tau = 60s$), the extended thermal diffusion length causes strong wave reflection at the top boundary. Forcing a linear fit resulted in a catastrophic **>20x overestimation** of $D$.
* **My Solution:** Discarded the upward-only approximation. Analytically solved the 1D heat equation for a finite cylinder with an adiabatic top boundary ($\partial T / \partial x = 0$ at $x=L$). 
* **Result:** Derived and implemented a finite-length amplitude model (the `cosh` model), which perfectly captures the non-linear standing wave curvature and strictly restored the extracted $D$ value to the correct physical magnitude ($\sim 10^{-5} m^2/s$).
<img width="640" height="416" alt="image" src="https://github.com/user-attachments/assets/4c16f5de-5527-4c42-b50b-24627faac9c1" />

<img width="656" height="433" alt="image" src="https://github.com/user-attachments/assets/1310ccc6-6065-426e-8d78-ca820d82b27d" />

*Figure 1: Comparison between the flawed infinite-length linear assumption (up) and the corrected finite-length adiabatic `cosh` model (down).*

### 2. Hardware Asymmetry & Harmonic Distortion Filtering
* **The Flaw:** Peltier heat pumps exhibit asymmetrical heating and cooling rates, injecting non-sinusoidal harmonic distortion into the thermal waves (Total Harmonic Distortion, THD $\approx 5.7\%$). Naive sine-fitting forces a mathematical compromise with these harmonics, causing a $+0.68\%$ systematic error.
* **My Solution:** Abandoned time-domain curve fitting. Adopted global Fourier extraction ($f_1$ fundamental frequency isolation) to mathematically filter out all hardware-induced harmonic distortion.

### 3. Eliminating Transient Thermal Drift via Strict SOP
* **The Flaw:** Extracting data during the early heating phases captures transient thermal drift, causing a $+3.0\%$ systematic overestimate in $D$ and inflating data variance (STD) by $\sim 7x$.
* **My Solution:** Established a strict steady-state data acquisition SOP. All data processing is strictly gated until after 10 full thermal cycles, ensuring true thermal equilibrium and massively improving Signal-to-Noise Ratio (SNR) and repeatability.

<img width="504" height="392" alt="image_1775762513909" src="https://github.com/user-attachments/assets/5a3427cf-fae5-4a87-8da8-d68b918d807b" />

*Figure 2: Quantifying the $+3.0\%$ systematic bias and massive variance explosion caused by transient thermal drift in early cycles.*

## 📊 Final Corrected Results
By applying the updated finite-boundary `cosh` model, Fourier signal extraction, and steady-state gating, the thermal diffusivity for standard materials was accurately measured with high confidence:
* **Aluminium:** $7.26 \pm 0.05 \times 10^{-5} m^2/s$ (Optimized at $\tau = 15s-30s$)
* **Brass:** $3.23 \pm 0.02 \times 10^{-5} m^2/s$ (Optimized at $\tau = 30s-45s$)

## 📁 Repository Contents
* `# Precision Metrology of Thermal Waves: Eliminating Systematic Bias in Heat Transfer Models

## 📌 Executive Summary
This project investigates and corrects critical systematic biases in the measurement of thermal diffusivity ($D$). Conducted as part of the advanced practical physics coursework at Imperial College London, the study identifies fatal flaws in traditional infinite-length approximations and establishes a highly robust, noise-resistant Standard Operating Procedure (SOP) for thermal metrology.

The methodologies developed here—finite-boundary modeling, frequency-domain signal extraction, and transient drift elimination—are directly applicable to precise thermal budget control and metrology in semiconductor manufacturing (e.g., RTP, CVD processes).

## 🛠️ Key Engineering Challenges & Solutions

### 1. The "Infinite-Length" Theoretical Fallacy & Model Reconstruction
* **The Flaw:** The standard laboratory model assumes an infinitely long cylinder, predicting a strictly linear log-attenuation ($\ln A \propto -x$). However, at low frequencies ($\tau = 60s$), the extended thermal diffusion length causes strong wave reflection at the top boundary. Forcing a linear fit resulted in a catastrophic **>20x overestimation** of $D$.
* **My Solution:** Discarded the upward-only approximation. Analytically solved the 1D heat equation for a finite cylinder with an adiabatic top boundary ($\partial T / \partial x = 0$ at $x=L$). 
* **Result:** Derived and implemented a finite-length amplitude model (the `cosh` model), which perfectly captures the non-linear standing wave curvature and strictly restored the extracted $D$ value to the correct physical magnitude ($\sim 10^{-5} m^2/s$).

*(👉 大实话提示：在这里把 PPT 第 6 页【直线拟合失败的图】和第 7 页【cosh 完美拟合的曲线图】拼成一张图拖进来，并在下面写上图注)*
![Put your comparison graph here: Linear Fit Failure vs. Cosh Fit Success]()
*Figure 1: Comparison between the flawed infinite-length linear assumption (left) and the corrected finite-length adiabatic `cosh` model (right).*

### 2. Hardware Asymmetry & Harmonic Distortion Filtering
* **The Flaw:** Peltier heat pumps exhibit asymmetrical heating and cooling rates, injecting non-sinusoidal harmonic distortion into the thermal waves (Total Harmonic Distortion, THD $\approx 5.7\%$). Naive sine-fitting forces a mathematical compromise with these harmonics, causing a $+0.68\%$ systematic error.
* **My Solution:** Abandoned time-domain curve fitting. Adopted global Fourier extraction ($f_1$ fundamental frequency isolation) to mathematically filter out all hardware-induced harmonic distortion.

### 3. Eliminating Transient Thermal Drift via Strict SOP
* **The Flaw:** Extracting data during the early heating phases captures transient thermal drift, causing a $+3.0\%$ systematic overestimate in $D$ and inflating data variance (STD) by $\sim 7x$.
* **My Solution:** Established a strict steady-state data acquisition SOP. All data processing is strictly gated until after 10 full thermal cycles, ensuring true thermal equilibrium and massively improving Signal-to-Noise Ratio (SNR) and repeatability.

*(👉 大实话提示：在这里把 PPT 第 2 页【Transient bias test 柱状图】截下来拖进去)*
![Put your transient bias bar chart here]()
*Figure 2: Quantifying the $+3.0\%$ systematic bias and massive variance explosion caused by transient thermal drift in early cycles.*

## 📊 Final Corrected Results
By applying the updated finite-boundary `cosh` model, Fourier signal extraction, and steady-state gating, the thermal diffusivity for standard materials was accurately measured with high confidence:
* **Aluminium:** $7.26 \pm 0.05 \times 10^{-5} m^2/s$ (Optimized at $\tau = 15s-30s$)
* **Brass:** $3.23 \pm 0.02 \times 10^{-5} m^2/s$ (Optimized at $\tau = 30s-45s$)

## 📁 Repository Contents
* 
: The full technical presentation detailing the mathematical derivations, boundary condition proofs, and error analysis.
* `thermal_wave_analysis.py` / `.ipynb`: (Optional) Python scripts used for Fourier extraction, `cosh` curve fitting, and data visualization.











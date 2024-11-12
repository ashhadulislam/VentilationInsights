# VentilationInsights

## Week 1.5

This week, I reviewed the work by Graßhoff et al. [^3], where the researchers establish linear relationship between **surface EMG (sEMG)** and **muscle pressure ($P_{mus}$)**.

### Previous Studies

Previous studies have shown that **diaphragm electrical activity (EAdi)** correlates with $P_{mus}$. However, measuring EAdi is invasive. This study instead shows that **transcutaneous EMG (sEMG)**, a fully non-invasive measure, also correlates with $P_{mus}$.

### Focus of This Paper

1.  **sEMG correlates with $P_{mus}$ and transdiaphragmatic pressure ($P_{di}$)**.

### What was done

1. **Estimating Respiratory Effort**: The researchers used the **EMG-Time Product (ETP)** method, calculating the area under the sEMG curve to measure respiratory effort.
2. They then found a relationship between ETP and $P_{mus}$ using a **conversion factor**.
3. They considered two sEMG signals, from the **diaphragm** and **intercostal muscles**, selecting the signal with the higher **signal-to-noise ratio (SNR)** dynamically.

### Detailed Methodology

#### Data Preprocessing

- **On one hand researchers were measuring Pressure** ($P_{es}$ and $P_{ga}$):
   1. Use **occlusion maneuvers** to calculate a scaling factor, ensuring $P_{es}$ is measured accurately.
   2. Remove **heartbeat-related artifacts** from $P_{es}$ and $P_{ga}$.
   3. Calculate:
      - **Transdiaphragmatic pressure ($P_{di}$)** as $P_{ga} - P_{es}$
      - **Respiratory muscle pressure ($P_{mus}$)** as $P_{es} - (\text{Elastic recoil of chest wall})$

- **On the other hand the researchers were measuring sEMG Signals**:
   1. Remove **heartbeat noise** from the sEMG signals.
   2. Smooth the sEMG signals with a **250 ms root mean square (RMS) filter**.
   3. Measure **background noise** during passive phases of the patient (e.g., exhalation) and subtract it from the sEMG to ensure readings start from zero.

#### Focus on Inspiratory Effort for Pressure and sEMG

1. Calculate **PTP** values:
   - **PTP$_{mus}$** and **PTP$_{di}$** are calculated for $P_{mus}$ and $P_{di}$ signals, respectively.
   - Outlier breaths with pressure > 20 cm H$_2$O·s were excluded to focus on normal inspiratory efforts.
   - A threshold-based method was used to detect the beginning and end of each inspiratory phase.
   - **PTP values** are the areas under the $P_{mus}$ and $P_{di}$ curves.

2. Calculate **ETP values**:
   - **ETP$_{di}$** and **ETP$_{interc}$** represent the total electrical activity (in µVs) for the diaphragm and intercostal muscles, respectively.
   - The signal with the higher SNR was chosen for analysis.
   - Both are area under the curves

#### Establishing the Relationship Between $P_{mus}$ and sEMG

- Previous research showed that **EAdi and $P_{di}$** have a linear relationship in ventilated patients.
- Assuming similar linearity, the researchers introduced a **conversion factor $K_{\text{EMG}}$**, a **neuromechanical conversion factor**, to convert ETP to PTP via the linear regression:

```math
\text{PTP}_{mus} = K_{\text{EMG}} \cdot \text{ETP} + P_{\text{bias}} \cdot T_i
```

where:
- $T_i$ is the duration of the inspiratory effort.
- $P_{\text{bias}}$ is a constant bias term used to adjust for systematic offsets.

#### Occlusion Maneuver for Baseline Calibration

During occlusions, where the airway is closed:
- The airway pressure ($P_{\text{aw}}$) equals $P_{es}$, meaning there’s no need for an esophageal catheter to measure $P_{es}$.
- No air moves, so the diaphragm contracts isometrically (no length change), producing a pure muscle-generated pressure. This configuration isolates the diaphragm-generated pressure alone.

The researchers used this setup to calculate a **baseline conversion factor** as follows:

```math
$$P_{mus,\text{EMG}} = \alpha \cdot K_{\text{occl,EMG}} \cdot (\text{EMG}_{\text{sel}} - \text{EMG}_{\text{sel,0}})$$
```


where:
- $\text{EMG}_{\text{sel,0}}$ represents the baseline EMG signal when there was no inspiratory effort.
- $\alpha$ is a correction factor adjusting for overestimation during occlusions due to isometric contraction.

Using this factor, they estimated the pressure-time product for $P_{mus}$:

```math
$$\text{PTP}_{mus,\text{EMG}} = \int P_{mus,\text{EMG}} \, dt = \alpha \cdot K_{\text{occl,EMG}} \cdot \text{ETP}_{\text{sel}}$$
```



## Week 1

This week, I focused on studying the nuances of lung and diaphragm protection during ventilation. I reviewed the Goligher 2020 paper [^1] and gathered several key insights:

### A. Metrics – Measuring Ventilation Effects on the Lungs

- **Compliance**: $\frac{\Delta V_t}{\Delta P_{aw}}$
- **Transpulmonary Pressure** ($P_L$): Airway pressure - pleural pressure
- **Muscle Pressure** ($P_{mus}$) derived from esophageal pressure ($P_{es}$)
- **Diaphragm Electrical Activity** (EAdi)
- **Airway Occlusion Pressure** ($P_{0.1}$)
- **Maximum Airway Pressure Occlusion During Breath Occlusion** ($\Delta P_{occ}$)
- **Ultrasound**

Static airway pressure (i) isn’t ideal for measuring lung stress as it reflects contributions from both the lung and chest. Instead, using **Transpulmonary Pressure** ($P_L$) (ii) or **Muscle Pressure** ($P_{mus}$) (iii) is better, where pleural/esophageal pressure is measured with an esophageal sensor. However, this is more common in research than clinical practice due to invasiveness and technical challenges [^2].

Alternatively, **EAdi** [^3], though also invasive, represents the neural drive or brain signal to control the diaphragm. It has been shown that EAdi can estimate $P_{mus}$. I have started reviewing Graßhoff’s 2021 paper [^3] to explore this in more depth.

### B. Preventive Methods from the Goligher 2020 Paper [^1]:

1. Inspiratory and Expiratory ventilator settings
2. Monitoring for dyssynchrony
3. Prone positioning instead of supine
4. Extracorporeal CO₂ removal
5. Partial neuromuscular blockade
6. Neuromuscular stimulation (Pacing)

The third paper on general Lung and Diaphragm-Protective Ventilation [^4] has been valuable for understanding terminologies and definitions and serves as a useful reference.

#### To-do:
1. Understand the data and equations in the Graßhoff’s 2021 paper [^3]
2. Complete reading the Birds breathing paper [^5]

---

[^1]: Goligher, E. C., Jonkman, A. H., Dianti, J., Vaporidi, K., Beitler, J. R., Patel, B. K., ... & Heunks, L. (2020). Clinical strategies for implementing lung and diaphragm-protective ventilation: avoiding insufficient and excessive effort. *Intensive Care Medicine*, 46(12), 2314-2326.

[^2]: Doorduin, J., Van Hees, H. W., Van Der Hoeven, J. G., & Heunks, L. M. (2013). Monitoring of the respiratory muscles in the critically ill. *American Journal of Respiratory and Critical Care Medicine*, 187(1), 20-27.

[^3]: Graßhoff, J., Petersen, E., Farquharson, F., Kustermann, M., Kabitz, H. J., Rostalski, P., & Walterspacher, S. (2021). Surface EMG-based quantification of inspiratory effort: a quantitative comparison with $P_{es}$. *Critical Care*, 25, 1-12.

[^4]: Goligher, E. C., Dres, M., Patel, B. K., Sahetya, S. K., Beitler, J. R., Telias, I., ... & Brochard, L. (2020). Lung-and diaphragm-protective ventilation. *American Journal of Respiratory and Critical Care Medicine*, 202(7), 950-961.

[^5]: Fainstein, F., Geli, S. M., Amador, A., Goller, F., & Mindlin, G. B. (2021). Birds breathe at an aerodynamic resonance. *Chaos: An Interdisciplinary Journal of Nonlinear Science*, 31(12).


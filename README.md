<img width="1710" height="1170" alt="download (1)" src="https://github.com/user-attachments/assets/47e57ca4-d5ff-48aa-95f2-c4786ee72d74" /># Hybrid Reinforcement Learning and Forecast-Based Solar Battery Scheduling  
**Team:** Solaris Nexus: where solar energy meets global sustainability  
**Team Members:** Rishith S., Favour T., Yelyzaveta M., Aaditya K., Jianxin Y., Hridhaan B.  
**Challenge:** NYAS Junior Academy – Renewable Energy Innovation (2025)

---

## Overview
This project implements and evaluates a hybrid Reinforcement Learning (RL) and Linear Regression (LR) forecast-based controller for solar battery scheduling.  
The goal is to improve solar energy utilization and minimize grid energy dependence in solar-plus-storage systems using real-world data from an operational solar plant in India.  

---

## Dataset
**Source:** [Solar Power Generation Data – Kaggle](https://www.kaggle.com/datasets/anikannal/solar-power-generation-data)  
**Plant Used:** Plant 1  
**Duration:** 34 days  
**Features:**  
- Irradiation  
- Ambient temperature  
- Module temperature  
- DC and AC power generation  

The dataset combines inverter-level generation data with weather sensor readings. Data was cleaned, merged, and resampled into a consistent 15-minute interval format for model training and testing.

---

## Methodology
1. **Data Preparation:**  
   - Aggregation of inverter-level generation data.  
   - Merging with plant-level weather readings.  
   - Creation of a time-series dataset with PV power and synthetic household load profiles.

2. **Forecasting Model (Linear Regression):**  
   - Predicts short-term solar generation based on weather and time features.  
   - Achieved R² ≈ 0.99 and MAE ≈ 0.08 kW, suitable for short-term PV forecasting.

3. **Reinforcement Learning Environment:**  
   - Simulates battery state-of-charge (SoC) dynamics and grid import/export behavior.  
   - Rule-based baseline and hybrid RL controller compared for performance.

4. **Hybrid RL + Forecast Controller:**  
   - Integrates the forecasted PV output into the RL state representation.  
   - Learns to schedule charge-discharge actions adaptively for minimal grid usage.

---

## Results
| Controller Type | Grid Import (kWh) | Equivalent Battery Cycles |
|------------------|------------------:|---------------------------:|
| Rule-based       | ≈ 300 kWh        | 6.6 cycles |
| Hybrid RL + Forecast | ≈ 11 kWh | 35.5 cycles |

**Findings:**  
- Approximately 96 percent reduction in grid import relative to the baseline.  
- Increased battery cycling observed, highlighting the trade-off between energy independence and battery longevity.

Figures:
- PV Forecast vs. Actual Output
<img width="2370" height="1020" alt="download (2)" src="https://github.com/user-attachments/assets/ab0f8887-f3ef-400e-ad8f-75e08c4fb449" />
- Grid Energy Import Comparison

<img width="1710" height="1170" alt="download" src="https://github.com/user-attachments/assets/8277bbf5-71bc-4433-bfce-9aa0a4a07c0b" />

- Battery Cycling Comparison
<img width="1710" height="1170" alt="download (1)" src="https://github.com/user-attachments/assets/900ddd06-45a8-4ee3-aa0f-8eeb52da7f77" />



---

## Lessons Learned
- Optimization in energy systems inherently involves trade-offs between autonomy, efficiency, and hardware wear.  
- Accurate forecasts are critical, as small prediction errors can lead to suboptimal control decisions.  
- A larger dataset (both plants and longer time periods) would improve generalization and robustness.  

---

## Next Steps
The next step is to refine the reward function to balance multiple objectives, including reduced grid import, stable battery health, and minimized cycling.  
Future iterations may integrate LSTM-based forecasting or weather API inputs for dynamic prediction accuracy.  
A differential-equation-based formulation of battery behavior may also be explored to model continuous charge–discharge dynamics and compare analytical behavior with the learned RL policy.  
Building on current results, further testing will include both solar plants and longer datasets, with applications in microgrid simulations and classroom demonstrations to support educational impact.  

---

## Requirements
Python ≥ 3.10
pandas
numpy
matplotlib
scikit-learn

© 2025 Solaris Nexus Team (Aaditya L. Kachhadiya and collaborators)
MIT License

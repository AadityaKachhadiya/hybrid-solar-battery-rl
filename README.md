# Hybrid Reinforcement Learning and Forecast-Based Solar Battery Scheduling  
**Team:** Solaris Nexus: where solar energy meets global sustainability  
**Team Members:** Rishith S., Favour T., Yelyzaveta M., Aaditya K., Jianxin Y., Hridhaan B.  
**Challenge:** NYAS Junior Academy – Energy Infrastructure: Solar Power (2025)

---

# Milestone 3 (Summary)

Milestone 3 delivered the first fully working prototype: a cleaned dataset, a short-term solar forecasting model, a reinforcement learning environment for battery scheduling, and the first hybrid RL + forecast controller. This provided the foundation for full-scale experimentation.

---

# Changelog

### Milestone 3 -> Milestone 4 Progress
- Upgraded from a single Linear Regression forecast to multiple models (Linear Regression, Random Forest, XGBoost).  
- Built a complete forecasting + control pipeline.  
- Added a realistic battery simulation with charge/discharge limits and efficiency modeling.  
- Introduced hybrid controllers for each forecast model.  
- Conducted extensive evaluations: forecasting accuracy, control performance, ablations, robustness to noise, and cross-site generalization.  
- Developed a full research paper with methodology, tables, and results.
- Figures avialable in the code & paper.

---

# Milestone 4 (Full Project)

## Overview
This project implements and evaluates hybrid Reinforcement Learning (RL) and forecast-based controllers for intelligent scheduling of solar battery systems.  
The goal is to minimize grid energy dependence and improve solar energy utilization using real-world PV generation data from two solar plants. 

---

## Dataset
**Source:** Solar Power Generation Data – Kaggle  
**URL:** https://www.kaggle.com/datasets/anikannal/solar-power-generation-data  
**Plants Used:** Plant 1 and Plant 2  
**Duration:** 34 days per plant  

Key features:
- Irradiation  
- Ambient temperature  
- Module temperature  
- AC and DC power  
- Hour-of-day and day-of-year  

Data was cleaned, aligned by timestamps, merged across files, and resampled to a uniform 15-minute interval.  
A synthetic household load profile was generated for control experiments.

---

## Methodology

### 1. Data Preparation
- Combined inverter-level PV generation with plant-level weather station data.  
- Converted all timestamps to a consistent format and sorted chronologically.  
- Unified the dataset into a 15-minute resolution.  
- Added a synthetic residential load curve shaped by morning and evening usage peaks.

### 2. Forecasting Models
- Persistence  
- Linear Regression  
- Random Forest (200 trees)  
- XGBoost (300 estimators, depth 5)  

These models were trained on Plant 1 using a chronological split to avoid leakage.

### 3. Reinforcement Learning Environment
- Battery capacity: 10 kWh  
- Power limits: ±3 kW  
- Round-trip efficiency: 95 percent  
- Reward penalizes grid import and excessive battery cycling  
- 15-minute decision intervals

### 4. Hybrid RL + Forecast Controllers
Hybrid controllers incorporate the one-step-ahead solar forecast into the RL state representation.  
This gives anticipatory behavior: the agent can act based on predicted sunlight, not just current conditions.

---

## Results

### Plant 1 Control Results
| Controller Type | Grid Import (kWh) | Battery Cycles |
|-----------------|------------------:|----------------:|
| Rule-based      | 188.41            | 131.63          |
| RL-only         | 15.92             | 697.50          |
| Hybrid LR       | 10.97             | 701.25          |
| Hybrid RF       | 14.53             | 694.88          |
| Hybrid XGB      | 10.13             | 616.50          |

**Summary:**  
Hybrid controllers reduce grid import by more than 90 percent compared to rule-based control.  
The hybrid XGBoost controller achieves the lowest import with significantly lower cycling than RL-only.

---

### Cross-Site Generalization (Train: Plant 1 → Test: Plant 2)
| Controller Type | Import (kWh) | Cycles |
|-----------------|-------------:|-------:|
| Rule-based      | 209.06       | 131.63 |
| RL-only         | 30.47        | 711.75 |
| Hybrid LR       | 12.71        | 719.63 |
| Hybrid RF       | 15.42        | 709.88 |
| Hybrid XGB      | 12.69        | 651.00 |

**Summary:**  
Hybrid controllers generalize effectively to Plant 2 despite different irradiance variability.  
Performance remains close to Plant 1 numbers without retraining.

---

## Ablation Studies

### 1. Removing Time-of-Day Features
- Hybrid controller performance changes only slightly.  
- Indicates that weather features (irradiation and temperature) dominate predictive power.  

### 2. Removing Battery SoC Regularization
- Battery cycling increases dramatically (well beyond 150 cycles).  
- Proves the SoC penalty is essential for preventing harmful overuse of the battery.

### 3. Forecast Noise Robustness
- Injected up to 30 percent multiplicative noise into solar forecasts.  
- Hybrid controller remained stable and grid import increased only slightly at high noise levels.  
- Confirms robustness to imperfect forecasts.

---

## Lessons Learned
- Incorporating forecasts into RL significantly improves control quality.  
- Battery cycling increases when the agent aggressively minimizes grid import, showing a fundamental trade-off.  
- A larger, longer-term dataset would enable more reliable policies and better generalization.  
- Cross-site validation shows that the hybrid controller learns structural decision rules, not plant-specific patterns.

---

## Next Steps
- Implement multi-step forecast horizon models.  
- Explore continuous-action RL algorithms (e.g., DDPG, SAC).  
- Integrate real weather APIs for adaptive online control.  
- Expand to multi-battery microgrid simulations.  
- Prepare hardware deployment prototype on Raspberry Pi.

---

## Requirements
- Python >= 3.10  
- pandas  
- numpy  
- matplotlib  
- scikit-learn  
- xgboost  

---

© 2025 Solaris Nexus Team (Aaditya L. Kachhadiya and collaborators)  
MIT License

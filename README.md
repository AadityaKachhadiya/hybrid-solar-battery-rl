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
- Built complete forecasting + control pipeline.  
- Added battery simulation with realistic constraints.  
- Introduced hybrid controllers for each forecast model.  
- Conducted extensive evaluations: forecasting accuracy, control performance, ablations, robustness to noise, and cross-site generalization.  
- Developed full research paper with figures, methodology, and results.  

---

# Milestone 4 (Full Project)

## Overview
This project implements and evaluates hybrid Reinforcement Learning (RL) and forecast-based controllers for intelligent scheduling of solar battery systems.  
The goal is to minimize grid energy dependence and improve solar energy utilization using real-world PV generation data.

---

## Dataset
**Source:** Solar Power Generation Data – Kaggle (https://www.kaggle.com/datasets/anikannal/solar-power-generation-data)
**Plant Used:** Plant 1 and Plant 2  
**Duration:** 34 days per plant  

Features include:
- Irradiation  
- Ambient temperature  
- Module temperature  
- AC and DC generation  
- Hour-of-day and day-of-year features  

Data was cleaned, merged, and resampled to a uniform 15-minute interval. Synthetic household load was generated for control experiments.

---

## Methodology

### 1. Data Preparation
- Combined inverter-level generation with plant weather data.  
- Created a consistent time-series dataset.  
- Generated synthetic residential load.  

### 2. Forecasting Models
- Persistence  
- Linear Regression  
- Random Forest (200 trees)  
- XGBoost (300 estimators, depth 5)  

### 3. Reinforcement Learning Environment
- 10 kWh battery  
- ±3 kW action space  
- 95% round-trip efficiency  
- Reward penalizes grid import and excessive cycling  

### 4. Hybrid RL + Forecast Controllers
Hybrid controllers incorporate solar forecast into the RL state representation, enabling anticipatory charging and discharging.

---

## Results

### Plant 1 Results
| Controller Type | Grid Import (kWh) | Battery Cycles |
|-----------------|------------------:|----------------:|
| Rule-based      | 188.41            | 131.63          |
| RL-only         | 15.92             | 697.50          |
| Hybrid LR       | 10.97             | 701.25          |
| Hybrid RF       | 14.53             | 694.88          |
| Hybrid XGB      | 10.13             | 616.50          |

### Cross-Site Generalization (Train: P1 → Test: P2)
| Controller Type | Import (kWh) | Cycles |
|-----------------|-------------:|-------:|
| Rule-based      | 209.06       | 131.63 |
| RL-only         | 30.47        | 711.75 |
| Hybrid LR       | 12.71        | 719.63 |
| Hybrid RF       | 15.42        | 709.88 |
| Hybrid XGB      | 12.69        | 651.00 |

---

## Figures

*(Insert your plots here)*

- PV Forecast vs Actual Output  
- Grid Energy Import Comparison  
- Battery Cycling Comparison  
- Energy–Wear Trade-off  
- Ablation Studies  
- Cross-Site Generalization  

---

## Lessons Learned
- Integrating forecasts into RL dramatically improves performance.  
- Forecasting accuracy directly affects controller stability.  
- There is a natural trade-off between reduced grid import and increased cycling.  
- Cross-site generalization validates the robustness of the hybrid strategy.  

---

## Next Steps
- Multi-step forecasting  
- Continuous RL algorithms  
- Realistic load profiles  
- Multi-battery microgrid simulations  
- Deployment on Raspberry Pi or equivalent hardware  

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

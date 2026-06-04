# 🏞️ Hydrological Modeling with HBV Model (Python/LuMod)

This repository contains an implementation of the conceptual hydrological **HBV** (Hydrologiska Byråns Vattenbalansavdelning) model using Python. The model is used for streamflow simulation and calibration for various catchment areas.

## 📁 Repository Structure
├── data/ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; # Meteorological and hydrological data<br>
└── results/&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; # Output alibration results
---

## 🌀 HBV Model Implementation with LuMod (Python)

The notebook `kaz_hbv_optuna.ipynb` demonstrates the complete workflow of data preparation, hydrological modeling with the HBV model, and hyperparameter optimization using Optuna:

- Reading meteorological data (precipitation and temperature) from Excel files
- Reading discharge observations for gauge stations
- Data transformation and cleaning (handling missing values, date formatting)
- HBV model setup using the [LuMod](https://github.com/hydrogo/lumod) library
- Definition of parameter ranges for calibration (snow parameters, recession coefficients, soil storage parameters, etc.)
- Automated model calibration using **Optuna** with **TPE (Tree-structured Parzen Estimator)** and **CMA** sampler
- Multi-objective optimization with RMSE as the primary metric
- Early stopping callback to prevent unnecessary trials
- MLflow integration for experiment tracking and logging
- Model performance evaluation with multiple metrics:
  - **NSE** (Nash-Sutcliffe Efficiency)
  - **KGE** (Kling-Gupta Efficiency)
  - **RMSE** (Root Mean Square Error)
  - **MAE** (Mean Absolute Error)
- Visualization of observed vs. simulated streamflow (annual comparison plots)
- Export of calibration results to Excel files

## 📊 HBV Model Parameters Calibrated

The following HBV parameters are optimized during the calibration process:

| Parameter | Description | Range |
|-----------|-------------|-------|
| `tthres` | Snowmelt threshold temperature (°C) | -2 to 5 |
| `dd` | Degree-day factor (mm/°C/day) | 1 to 6 |
| `beta` | Shape coefficient for runoff response | 1 to 6 |
| `fc` | Field capacity (mm) | 10 to 1000 |
| `k0` | Upper zone recession coefficient (1/day) | 0.01 to 9 |
| `k1` | Middle zone recession coefficient (1/day) | 0.001 to 2 |
| `k2` | Lower zone recession coefficient (1/day) | 0.0001 to 0.01 |
| `kp` | Percolation coefficient (1/day) | 0 to 2 |
| `snow0` | Initial snow storage (mm water equivalent) | -10 to 100 |
| `w01` | Initial upper zone storage (mm) | 10 to 900 |
| `w02` | Initial lower zone storage (mm) | 10 to 500 |

## 🔧 Technologies Used

- **Python 3.12** - Core programming language
- **LuMod** - HBV model implementation
- **Optuna** - Hyperparameter optimization framework
- **TPESampler** - Bayesian optimization algorithm
- **MLflow** - Experiment tracking and logging
- **pandas, numpy** - Data manipulation
- **scikit-learn** - Performance metrics (RMSE, MAE)
- **hydroeval** - Hydrological evaluation metrics (NSE, KGE)
- **matplotlib** - Visualization

## 📈 Key Features

- **Automated Calibration**: Uses Optuna with TPE sampler for efficient parameter search
- **Early Stopping**: Prevents unnecessary trials when no improvement is observed
- **Parallel Execution**: Supports multi-trial parallel processing (n_jobs parameter)
- **Experiment Tracking**: All parameters and metrics are logged to MLflow
- **Warm-up Period**: First year of simulation is excluded from evaluation
- **Multi-metric Evaluation**: Comprehensive model performance assessment

## 📝 Usage

1. Place meteorological and discharge data in the `data/` directory
2. Configure the gauge station ID in the notebook
3. Set the calibration period (start and end dates) and method(CMA or TPE)
4. Run the Optuna optimization to find optimal parameters
5. Evaluate results using performance metrics and visualization plots

## 🔗 Reference

- [LuMod Documentation](https://github.com/hydrogo/lumod)
- [Optuna Documentation](https://optuna.org/)
- [HBV Model Literature]([https://www.smhi.se/en/research/research-departments/hydrology/hbv-model-1.156574](https://www.geo.uzh.ch/dam/jcr:fb0a59f7-c54d-43ce-b3b3-e33ade4679eb/HBV_intro_lecture.pdf))

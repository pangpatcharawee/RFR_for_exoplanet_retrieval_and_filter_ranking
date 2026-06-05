# A Machine Learning Approach to Exoplanet Atmospheric Retrieval: Application to Optical Filter Ranking

This repository contains the Python code, Jupyter Notebooks, and synthetic transmission data used in the paper: **"A Machine Learning Approach to Exoplanet Atmospheric Retrieval: Application to Optical Filter Ranking"** (Accepted for publication in *The Astronomical Journal*).

## Authors
* Patcharawee Munsaket (Corresponding Author)
* Supachai Awiphan
* Poemwai Chainakun
* Eamonn Kerins
* Napaporn A-thano

## Repository Contents

### Jupyter Notebooks
* `Gen_spectrum_stage2.ipynb`: Simulates the synthetic exoplanet transmission spectra using the TauREx3 framework to generate the training, validation and testing datasets.
* `Zero-out_vs_Standardisation.ipynb`: Compares preprocessing methodologies (Zero-out vs. Min-Max Standardisation) to demonstrate how standardisation bounds variance across narrow planetary radius bins without distorting physical spectral features.
* `Prep_Trian_Predict.ipynb`: Handles the core machine learning pipeline. It loads the synthetic spectra, applies preprocessing, and performs a Grid Search to train the Random Forest Regressor (RFR) model.
* `Plot_rfr_vs_nestle.ipynb`: Evaluates the retrieval performance by comparing the RFR predictions against traditional Bayesian nested sampling methods (generating corner plots and 1-to-1 predicted vs. true plots).
* `Filter_ranking.ipynb`: Calculates feature importance to determine the optimal subset of photometric filters (Johnson-Cousins and SDSS) required for accurate atmospheric parameter estimation.

### Data Structure & Contents
The `data/` directory contains the synthetic transmission spectra generated via TauREx3, which act as the foundational dataset for our machine learning models. Because our methodology partitions data by planetary radius ranges (the "first stage" of our pipeline), it is organised into corresponding sub-directories (e.g., `Syn_transmission_spectra_bin_1_08-1Rj/` for $0.8 - 1.0 R_J$, up through bin 5).

Inside each folder are serialised `.pickle` files (e.g., `Syn93_mrt_1.pickle`). When loaded into Python (e.g., via `pandas.read_pickle`), each file contains a list of dictionaries. Each dictionary represents a single simulated exoplanet and contains the following key-value pairs:

**1. Ground Truth Parameters (Targets):**
These are the input parameters used to configure the TauREx3 forward model.
* `pl_radj`: Planetary Radius ($R_J$)
* `pl_eqt`: Equilibrium Temperature (K)
* `MR_TiO`: Log mixing ratio of Titanium Oxide
* `MR_VO`: Log mixing ratio of Vanadium Oxide
* *(Also includes stellar/orbital configurations such as `st_teff`, `st_rad`, `pl_orbsmax`, etc.)*

**2. Photometric Features (Inputs):**
These represent the simulated observable data after integrating the high-resolution spectra across the broadband filters.
* `U, B, V, R, I`: Binned transit depths for the Johnson-Cousins filters.
* `u', g', r', i', z'`: Binned transit depths for the SDSS filters.
* `[Band]_bw`: The central wavelength for the respective filter (in microns).
* `[Band]_err`: The calculated theoretical error margin for the respective transit depth.

These datasets are directly ingested by `Prep_Trian_Predict.ipynb` and `Filter_ranking.ipynb` for model training and feature evaluation.

## System Requirements and Dependencies
To run these notebooks, you will need Python 3.x and the following core libraries installed:
* `taurex` (Tau Retrieval for Exoplanets)
* `scikit-learn`
* `pandas`
* `numpy`
* `scipy`
* `matplotlib`
* `PyAstronomy`
* `joblib`

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

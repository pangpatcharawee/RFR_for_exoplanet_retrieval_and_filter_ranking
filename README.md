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

### Data
* `Syn93_mrt_*.pickle` (and related data files): The synthetic transmission data generated using TauREx3, used for training and testing the Random Forest model. *(Note: Large datasets may be hosted via Zenodo; see the DOI link in the published paper for the full data archive).*

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

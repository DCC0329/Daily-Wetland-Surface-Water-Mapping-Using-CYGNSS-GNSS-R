# 🌎 Daily Wetland Surface Water Mapping Using CYGNSS GNSS-R
*A workflow for deriving daily surface-water fraction using CYGNSS, Sentinel-1, ERA5, and auxiliary datasets.*

---

## Overview

This repository provides a complete workflow for generating **daily surface-water fraction** from CYGNSS GNSS-R observations.  
It integrates:

- CYGNSS Level-1 DDM SNR  
- Sentinel-1 GRD backscatter (via Google Earth Engine)  
- ERA5 climate variables  
- Global Surface Water  
- DEM, slope, and land-cover datasets  

The workflow covers data downloading → preprocessing → water-fraction computation → visualization → machine-learning modeling.

The goal is to build a **daily wetland mapping system** powered by multi-sensor satellite data and data-driven prediction models.

---

## Module Descriptions

### `download/`
Scripts for downloading raw datasets:
- CYGNSS L1 (DDM SNR)
- ERA5 climate data
- Global Surface Water
- Utility tools for inspecting `.nc` files

### `preprocessing/`
Feature-engineering and data-cleaning notebooks:
- Add water fraction from GSW
- Add DEM, slope, and land-cover
- Merge per-day CSVs
- Compress and filter datasets for modeling

### `utils/`
Small helper utilities:
- Code debugging  
- ERA5 unzip tool  
- Intermediate data inspection  

### `WaterFractionCalculation.ipynb`
Batch script that computes **Sentinel-1–derived water fraction** for each CYGNSS footprint using Google Earth Engine:
- Robust Sentinel-1 search  
- Histogram-based thresholding (Otsu + fallback rules)  
- Slope masking (≤5°)  
- Polygon reduction to compute mean water fraction  

### `Data_view.ipynb`
Exploratory visualization notebook:
- Histograms of water fraction and DDM SNR  
- Spatial distribution plots of CYGNSS footprints  
- Data cleaning and distribution diagnostics  

### `Best_Model.ipynb`
GPU-accelerated XGBoost workflow for predicting water fraction:
- Feature preprocessing  
- Stratified split + quantile weighting  
- Isotonic regression calibration  
- Model evaluation (R, R², MAE, RMSE)  
- SHAP explainability  

---




# Commuting Flow Prediction using OpenStreetMap Data

**Official implementation of the paper:**

> **Commuting Flow Prediction using OpenStreetMap Data**, *Computational Urban Science, Springer*, 2025
> 
> **Authors:** Kuldip Singh Atwal, Taylor Anderson, Dieter Pfoser, & Andreas Züfle (George Mason University, Emory University)
---

## Abstract

This repository contains the official implementation of the study **"Commuting flow prediction using OpenStreetMap data."** We propose a method to broaden the utility of state-of-the-art commuting flow prediction models by using globally available OpenStreetMap (OSM) data. While existing high-performing models often rely on location-specific proprietary datasets, limiting transferability, this approach leverages building types—specifically **residential** and **non-residential** classifications—derived from OSM to predict commuting flows. Our experiments demonstrate that models using these OSM-derived features achieve prediction accuracy comparable to those using region-specific data, while enabling application in data-poor regions through transfer learning.

---

## Key Features

- **OSM-Only Dependency:** The model features are derived exclusively from OpenStreetMap (building types, road networks) and basic census data (population), eliminating the need for proprietary datasets like PLUTO.

- **Building Type Indicator:** Incorporates the count, density, and area of residential and non-residential buildings as key indicators for commuting mobility, which significantly improves prediction accuracy over standard OSM features.

- **Transfer Learning Capability:** The approach allows a model trained in one region (e.g., NYC) to be successfully transferred to another (e.g., Fairfax County) where ground truth commuting data may be unavailable, explaining up to 62.1% of flow variation.

- **Model Benchmarking:** Includes implementations comparing the proposed **GMEL-OSM** approach against Deep Gravity, XGBoost, and Random Forest models.

---

## Methodology

### 1. Data Preprocessing and Building Classification

The pipeline begins by processing OSM data to extract building footprints.

- **Building Classification:** A machine learning approach is used to classify OSM building footprints into **Residential** and **Non-residential** types based on their geometric and topological features.

- **Feature Generation:** We derive nine specific input features for flow prediction:
  * Count, density, and area of residential buildings
  * Count, density, and area of non-residential buildings
  * Region population and population density
  * Distance between census tracts calculated via Open Source Routing Machine (OSRM)
  
---

### 2. Flow Prediction Models

This repository supports the evaluation of several models using the generated features:

- **GMEL (Graph Attention Networks):** A geo-contextual multitask embedding learner that captures spatial dependencies between origin and destination regions.
- **Deep Gravity:** A deep neural network approach inspired by the classic gravity model.
- **Baseline Models:** XGBoost (Regression tree gradient boosting) and Random Forest.

*Note: The original repositories for the key models used in this study can be found here:*
- *GMEL: https://github.com/jackmiemie/GMEL*
- *Deep Gravity: https://github.com/scikit-mobility/DeepGravity*

---

### 3. Evaluation

The models are evaluated using standard metrics including Root Mean Square Error (RMSE), Coefficient of Determination (R<sup>2</sup>), and Common Part of Commuters (CPC). The repository also includes notebooks for visualizing:

- **Choropleth Maps:** Visualizing relative prediction errors for inflows and outflows across census tracts.
- **Scatter Plots:** Comparing ground truth vs. predicted commuters (log-log scale).
- **Histograms:** Analyzing the distribution of relative prediction errors.

---

## Dataset

The model is trained and validated on two distinct study areas:
1. **New York City (NYC), USA:** An urban environment with high transit density.
2. **Fairfax County, Virginia, USA:** A suburban environment used to test transferability.
   
**Data Sources**:
- **Input Data:** OpenStreetMap (OSM) and U.S. Census TIGER/Line shapefiles.
- **Ground Truth**: Longitudinal Employer-Household Dynamics (LODES) Origin-Destination Employment Statistics (2015).

---

The main Jupyter notebook, `Flow_Prediction.ipynb`,  contains the pipeline for:
- Processing ground truth flows from LODES
- Analyzing predictions using standard OSM features
- Analyzing predictions using GMEL/Building Type features
- Generating visualization metrics (bins, deltas) and plots (histograms, scatter plots, maps)

---

## Citation

If you use this code, methodology, or data in your research, please cite:

```bibtex
@article{atwal2025commuting,
  title={Commuting flow prediction using OpenStreetMap data},
  author={Atwal, Kuldip Singh and Anderson, Taylor and Pfoser, Dieter and Z{\"u}fle, Andreas},
  journal={Computational Urban Science},
  volume={5},
  number={1},
  pages={2},
  year={2025},
  publisher={Springer}
}
```

---

## Acknowledgements

This work is supported by the National Science Foundation Grant No. 2109647 titled “Data-Driven Modeling to Improve Understanding of Human Behavior, Mobility, and Disease Spread”.

Computing resources were provided by the Office of Research Computing at George Mason University.

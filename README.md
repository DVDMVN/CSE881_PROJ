
# Machine Learning Guided Discovery: Automated Pattern Extraction for Interpretable Models

## Abstract

This project demonstrates how machine learning can guide statistical model specification and bridge the interpretability issue. This project utilizes tree-based algorithms (Random Forest, XGBoost, LightGBM) as knowledge discovery tools for mining complex patterns from NHANES 2017-2020 data (10,439 records, 2000+ features). While mean-SHAP analysis provides global average magnitude, healthcare policy requires explicit mathematical formulas specifying exact relationships and interactions. We bridge this gap by extracting machine learning-discovered patterns (non-linearities, natural bins, and interactions) to construct policy-ready GLMs that achieve at most 5% of normalized error relative to ML models, while providing the executable formulas required for regulatory compliance and stakeholder communication.
## Environment Setup

⚙️`requirements.txt` file holds all package dependencies. If using conda, create a new environment and use command(s):

```bash
conda activate [your_env_name]
conda install --file requirements.txt
```
## File Documentation

This project was built largely using Jupyter Notebooks (`.ipynb`) and Microsoft Excel Spreadsheets.

Each notebook acts as a separate step in our pipeline:

- 📓`A_HARVEST_DATA.ipynb` - Data collection pipeline, performs collection of raw data files and codebooks from the NHANES root website. Populates 📁`RAW`.
- 📓`B_MERGE_DATA.ipynb` - Performs merge onto `P_GHB.xpt`, a laboratory data file containing the main target variable (A1c / blood sugar level). 
    - Saves result to 📁`PROCESSED/DATA/` as 📄`merged.parquet`.
- 📓`C_HANDLE_MISSINGNESS.ipynb` - Transforms NHANES numerical missing codes, performs rudimentary 30% missingness drop + granular screening drop, encodes measures, renames features. 
    - Saves result to 📁`PROCESSED/DATA/` as 📄`merged_and_dropped.parquet`.
- 📓`D_SPLIT_IMPUTE.ipynb` - Encodes target, drops leakage columns, performs train-test split (80 | 20), and performs imputation. 
    - Saves resulting data splits to 📁`INPUTS/TRAIN/` and 📁`INPUTS/TEST/` as 📄`*.parquet` files.
- 📓`E_BASELINE_MODELS.ipynb` - Training, tuning, evaluation, and SHAP importance mining for baseline tree-ensemble models.
    - Saves best hyperparameters to 📁`RESULTS/BASELINES/PARAMETERS/`
    - Saves performance metrics to 📁`RESULTS/BASELINES/PERFORMANCE/`
    - Saves test probabilities to 📁`RESULTS/BASELINES/PROBABILITIES/`
    - Saves SHAP importances to 📁`RESULTS/BASELINES/SHAP/`
- 📓`F_SAMPLING.ipynb` - Weighted K-means Clustering file compression (SHAP interaction runtime reduction), SHAP interaction mining for GLM interaction terms feature engineering.
- 📓`G_GLM.ipynb` - GLM training, tuning (feature selection via XGB SHAP, p-drops, stepwise selection, VIF-LRT drops + justification, interaction terms), model evaluation.


## Authors

- [@Victor Pietono](https://github.com/pietonov)
- [@Diego Gomez](https://github.com/diegopiraquive)
- [@Alex Chen](https://github.com/DVDMVN)


## Acknowledgements

This project was built as a course project for the Fall 2025 CSE881 Data Mining course at MSU. Please reference our report for additional details: [LINK](https://cse881-ml-guided-discovery-final-report.tiiny.site)

# Cell2Cell Churn Prediction and Retention Strategy

This project analyzes the classic Cell2Cell telecom dataset to predict customer churn, segment customers by customer lifetime value (CLV), and evaluate retention campaign strategies.

The work is organized as a notebook-driven pipeline:

- `01_data_cleaning.ipynb`: raw data cleaning, feature preparation, and exploratory analysis
- `02_modeling.ipynb`: CLV segmentation, churn modeling, ROI simulation, SHAP explainability, and holdout scoring
- `03_figures.ipynb`: publication-ready visual outputs saved into `figures/`

Rendered HTML versions of all three notebooks are included for quick review without opening Jupyter.

## Project Goals

- Understand which customer behaviors and account attributes are associated with churn
- Build a predictive churn model on the training data
- Identify high-value customers using CLV-based clustering
- Compare retention strategies using a business ROI lens
- Score a holdout dataset for out-of-sample churn risk

## Data Files

- `cell2celltrain.csv`: primary training dataset
- `cell2cellholdout.csv`: unseen holdout dataset used for scoring
- `clean_train.csv`: cleaned training export used during analysis
- `payload.pkl`: serialized intermediate objects from the notebook workflow

Note: `payload.pkl` is intentionally excluded from git because it is larger than GitHub's file size limit.

## Workflow Summary

### 1. Data Cleaning and EDA

The first notebook loads the Cell2Cell training data, handles missing and mixed-type fields, explores churn balance, and inspects how important variables differ between churners and non-churners.

Examples of explored patterns include:

- churn distribution
- monthly revenue by churn outcome
- months in service by churn outcome
- customer care and retention call behavior
- overage usage and other account characteristics

### 2. Modeling and Customer Segmentation

The second notebook combines two business questions:

1. Which customers are likely to churn?
2. Which churn risks matter most financially?

To answer that, the notebook:

- computes CLV-oriented features
- clusters customers into `Low CLV`, `Mid CLV`, and `High CLV` groups using `KMeans`
- trains an `XGBoost` classifier for churn prediction
- generates predicted churn probabilities
- evaluates a holdout set
- explains predictions using SHAP

### 3. Business Decision Layer

Instead of stopping at classification, the project compares retention policies.

The ROI section contrasts:

- a naive strategy: target every predicted churner with a retention offer
- a smart strategy: target higher-value predicted churners first

This framing helps connect model output to customer value and campaign cost.

## Key Outputs

The `figures/` folder contains the main visual deliverables:

- `fig1_eda_overview.png`: churn and feature-pattern overview
- `fig2_clv_clustering.png`: CLV segmentation and cluster interpretation
- `fig3_model_evaluation.png`: model behavior, performance, and feature importance
- `fig4_shap_explainability.png`: SHAP-based explanation of churn drivers
- `fig5_retention_roi.png`: retention matrix and ROI comparison
- `fig6_customer_deep_dive.png`: single-customer decision/explanation view
- `fig7_holdout_validation.png`: holdout scoring and risk distribution

## Notable Findings

Based on the notebook outputs currently stored in the repository:

- customers are segmented into three CLV tiers for prioritization
- the holdout scoring step flags an estimated churn rate of about `44.7%`
- the ROI simulation shows that campaign design materially changes financial outcome
- the analysis notes that a large share of predicted churners are low-CLV customers, which is important when deciding whom to target

One especially useful takeaway is that churn prediction alone is not enough. The project shows why combining churn risk with CLV leads to better retention decisions than treating all predicted churners the same way.

## Tools and Libraries

The notebooks reference the following Python ecosystem tools:

- `pandas`
- `numpy`
- `matplotlib`
- `seaborn`
- `scikit-learn`
- `xgboost`
- `shap`
- `pickle`

## Running the Project

Open the notebooks in order:

1. `01_data_cleaning.ipynb`
2. `02_modeling.ipynb`
3. `03_figures.ipynb`

If you want to rerun the full workflow, make sure the Python environment includes the libraries listed above and that the CSV files are present in the project root.

## Repository Structure

```text
cell2cell_project/
├── 01_data_cleaning.ipynb
├── 01_data_cleaning.html
├── 02_modeling.ipynb
├── 02_modeling.html
├── 03_figures.ipynb
├── 03_figures.html
├── cell2celltrain.csv
├── cell2cellholdout.csv
├── clean_train.csv
├── figures/
├── payload.pkl
└── README.md
```

## Why This Project Matters

This repository is more than a churn model. It is a compact business analytics project that connects:

- data cleaning
- predictive modeling
- customer segmentation
- explainability
- retention economics

That makes it useful both as a machine learning portfolio project and as a practical example of decision-focused analytics.

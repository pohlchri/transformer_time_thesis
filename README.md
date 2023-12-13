# Potential of transformer time series models for the energy sector

**Type:** Master's Thesis

**Author:** Christin Pohl

**1st Examiner:** Prof. Dr. Stefan Lessmann

**2nd Examiner:** Prof. Dr. Benjamin Fabian

## Table of Content

- [Summary](#summary)
- [Working with the repo](#Working-with-the-repo)
    - [Dependencies](#Dependencies)
    - [Setup](#Setup)
- [Reproducing results](#Reproducing-results)
    - [Training code](#Training-code)
    - [Evaluation code](#Evaluation-code)
- [Results](#Results)
- [Project structure](-Project-structure)

## Summary

**Keywords**: transformers, time series, renewable energy forecasting, load forecasting, Germany

**Abstract**: The contribution of renewables such as wind and solar energy to fulfill the electricity
demand is increasing. Incorporating renewable energies leads to more volatility within the grid. Therefore, it is necessary to forecast wind and solar energy production and the demand for electricity from all consumers (load). Accurate predictions lead to economic and environmental benefits. Models with transformer architecture have recently been applied to this problem with initially promising results. However, there is a gap in comparing different transformer time series models with each other as well as with baseline models on load, wind, and solar energy forecasting. Therefore, the primary objective of this work is to quantify the distinction in accuracy between different transformer time series models and the selected baseline methods. We run experiments on three univariate and three multivariate datasets from Germany for four prediction lengths. Per dataset, three baselines and three transformer time series models were tested to forecast load, wind, and solar energy.

As a result of statistical testing, it becomes apparent that all models perform better than a naive forecast. Overall, Informer is the best-performing model in terms of RMSE. It is significantly better than all models except for DLinear. Given that hyperparameter experiments on tuning a transformer model significantly improved the results, further performance increases on Informer with more hyperparameter tuning possibilities are expected. There are significant performance differences between transformer time series models. Namely, Informer is significantly better than Autoformer, and Autoformer is significantly better than Temporal Fusion Transformer. While transformer time series models perform very strongly in the univariate case, a simple Vector Autoregressive model is often more accurate in the multivariate case. This thesis manifests that transformer time series models are very relevant in the energy forecasting space but need to be compared with baseline models for performance evaluation. In addition, future research is necessary to estimate the concrete CO2 and cost-saving potential from more accurate forecasts.  

## Setup

1. Clone this repository

2. Create a virtual environment and activate it. Please ensure to use Python 3.10
```bash
python -m venv env
source env/bin/activate
```
3. Install requirements
```bash
pip install --upgrade pip
pip install -r 06_requirements.txt
```
4. Datasets 
The original data can be loaded from [Open Power System Data] (https://data.open-power-system-data.org/time_series/2020-10-06). After this, please put the dataset in the 01_datasets folder. Then execute the 02_data_set_prep.ipynb. This will result in three new datasets within the 01_datasets folder that are required for the experiments.

## Reproducing results

### Training code

All training code for the models are in the repository. There are three notebooks relevant to training.
1. To train the simple baseline models (naive model, ARIMA model and VAR model) execute 03_baseline_models/baseline_models.ipynb. 

2. For Informer, Autoformer, and DLinear execute 04_transformer_models/Informer_Autoformer_DLinear/01_Experiments/Informer_Autoformer_DLinear.ipynb.

3. For Temporal Fusion Transformer execute the three notebooks under 04_transformer_models/TFT. Two notebooks are for the univariate case (with and without) hyperparameter tuning. One notebook is for the multivariate case. 

### Evaluation code

After training, each notebook also contains code to calculate the performance of the models (in the same notebooks as outlined above). If you require the pre-trained models and prediction results please write me an e-mail. They are too large to put them all on GitHub.

## Results

After model training, we test whether the models differ significantly from each other. The result plots show any critical differences between models. A critical difference between models is visually larger than one of the black lines. For instance, there is a critical difference between all models and the naive model. There is no critical difference between Informer and DLinear. Informer is critically different than all other models except for DLinear. The three transformer models Informer, Autoformer, and Temporal Fusion Transformer are all critically different.

![results](/critical_difference_diagram.png)

## Project structure
This only contains the folder structure and the ipynb notebooks. Further files, such as results files or model saving folders, are created during training. 

```bash
├── README.md
├── 01_datasets                                                       -- After downloading the data from the link above, put it here
├── 02_data_set_prep.ipynb                                            -- Prepares three datasets and analyzes the data 
├── 03_baseline_models                                                -- Baseline models: Naive model, ARIMA, VAR
    ├── baseline_models.ipynb
├── 04_transformer_models
    ├── Informer_Autoformer_DLinear                                   -- Contains everything related to Informer, Autoformer and DLinear
        ├── 01_Experiments
            ├── Informer_Autoformer_DLinear.ipynb
    ├── TFT                                                           -- Contains everything related to Temporal Fusion Transformer
            ├── Seasonal_plot.ipynb
            ├── TFT_multivariate.ipynb
            ├── TFT_univariate_with_hyperparameters.ipynb
            ├── TFT_univariate.ipynb
├── 05_result_comparison.ipynb                                        -- Friedman Test and Post-Hoc Test to access model differences
├── critical_difference_diagram.png

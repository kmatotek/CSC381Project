# Predicting Global Video Game Sales from Game Metadata

---

## 1. Project Overview

This project will examine whether metadata about a video game can be used to predict its global sales. The dataset includes variables such as platform, genre, publisher, developer, critic score, release date, and regional sales. The main goal is to estimate `total_sales`, measured in millions of copies.

This problem is interesting because it has practical value for market analysis. It involves structured data, missing values, categorical variables, and a continuous target, making it well suited for model comparison and analysis.

The task will be treated as regression.

## 2. Problem Definition

The project objective is to predict global video game sales from game metadata.

- Target variable: `total_sales`
- Objective: predict a continuous numeric value
- Task type: Regression

#### Hypothesis

Game metadata should contain useful predictive information about sales. Variables such as `console`, `genre`, `publisher`, `developer`, release timing, and `critic_score` are expected to be related to `total_sales`. A simple linear model should provide a reasonable baseline, but more flexible models such as Support Vector Regression and a neural network are expected to perform better because the relationships are likely non-linear.

## 3. Dataset Description

- Source: https://www.kaggle.com/datasets/siddharth0935/video-game-sales
- Size: 64,016 rows and 14 columns

#### Key Variables

- Predictors: `console`, `genre`, `publisher`, `developer`, `critic_score`, `release_date`
- Target: `total_sales`
- Regional sales fields: `na_sales`, `jp_sales`, `pal_sales`, `other_sales`

#### Expected Challenges

- many missing values, especially in `critic_score`
- missing target values, which reduce the usable regression subset
- high-cardinality categorical variables such as `publisher` and `developer`
- possible target leakage if regional sales are used to predict total sales
- a right-skewed target distribution with outliers

## 4. Planned Analysis

The project will use a regression workflow.

#### Models

- Baseline: `Linear Regression`
- Additional model: `SVR`
- Additional model: `MLPRegressor`

#### Model Rationale

- `Linear Regression` provides a simple, interpretable baseline.
- `SVR` is appropriate because it can capture non-linear structure with kernel methods.
- `MLPRegressor` is appropriate because a neural network can learn more complex interactions between features.

#### Evaluation Plan

Performance will be measured with `RMSE`, `MAE`, and `R^2`

The project will use:

- a train/test split for final evaluation
- cross-validation on the training data for limited hyperparameter tuning
- consistent preprocessing across models for fair comparison

Results will be summarized with tables and plots such as actual-vs-predicted graphs, metric comparison charts, and residual analysis.

## 5. Feasibility and Timeline

The project is feasible because the dataset is already available and all planned models are available in `scikit-learn`.

#### Planned Milestones

1. Clean the data and engineer useful features.
2. Train a Linear Regression baseline.
3. Train and tune `SVR` and `MLPRegressor`.
4. Compare models using `RMSE`, `MAE`, and `R^2`.
5. Analyze overfitting, underfitting, and major prediction errors.
6. Write the final report.

#### Anticipated Challenges

- handling missing values without introducing bias
- preventing leakage from regional sales variables
- managing high-cardinality categorical features
- predicting rare blockbuster games accurately

## 6. Data Preprocessing Plan

Planned preprocessing steps include:

- remove rows without `total_sales`
- exclude leakage variables such as `na_sales`, `jp_sales`, `pal_sales`, and `other_sales`
- convert `release_date` into features such as release year and release month
- impute missing numeric values, especially `critic_score`
- handle missing categorical values with an `Unknown` category or similar strategy
- encode categorical variables and scale numeric features for models such as `SVR` and `MLPRegressor`
- inspect outliers and consider a justified transformation if target skew is severe

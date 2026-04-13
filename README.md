# Reliability Analysis of Mechanical Springs

## Project Overview
This repository contains a statistical survival analysis of mechanical springs to evaluate the impact of operational stress and manufacturing parameters on their operational life. The study identifies the primary drivers of "Cycles to Failure" using non-parametric and semi-parametric modeling techniques.

## Dataset
* **Source**: `NewSpring.csv` from Meeker et al., *Statistical Methods for Reliability Data*.
* **Design**: 108-unit full factorial experiment with 9 replicates per factor combination.
* **Variables**:
    * `A.Stroke`: Mechanical displacement (50, 60, 70 mils).
    * `B.ProcessTpt`: Processing temperature (500, 1000 °F).
    * `C.Method`: Manufacturing technique (New vs. Old).
    * `Cycles`: The time-to-event response variable.
    * `Censoring`: Right-censoring indicator (1 = failure, 0 = survived 5,000 cycles).

## Analysis Pipeline
The R analysis follows a structured statistical workflow:
1. **Exploratory Data Analysis (EDA)**: Visualization of data distributions.
2. **Non-Parametric Modeling**:
    * Kaplan-Meier (KM) survival curves.
    * Stratified Log-Rank tests to isolate factor effects.
    * Hazard estimation using the Nelson-Aalen method and kernel-smoothed hazard plots.
3. **Semi-Parametric Modeling**:
    * Cox Proportional Hazards (CPH) modeling.
    * Automated stepwise model selection using the Akaike Information Criterion (AIC).
4. **Model Diagnostics**:
    * Verification of Proportional Hazards (PH) using Schoenfeld residuals and log-log survival curves.
    * Martingale residuals.
    * Influence analysis using DFBETAS to detect outliers.

## Key Results
* **Manufacturing Method**: The "New" method is the most effective factor for extending reliability, reducing failure hazard by approximately 89% (HR ≈ 0.11).
* **Mechanical Stress**: Stroke length is the dominant stressor; every 1-mil increase raises the risk of failure by ~17% (HR ≈ 1.17).
* **Optimal Model**: The final model includes all three main effects: `Surv(Cycles, Censoring) ~ A.Stroke + B.ProcessTpt + C.Method`.

## Dependencies
The analysis requires R and the following libraries:
* `tidyverse`, `survival`, `survminer`, `muhaz`, `gtsummary`, `ggfortify`, `ggsurvfit`.

## Author
Samd Guizani

# Predicting Progress Toward SDG 4: A Global Education Classification Model

![SDG 4 Logo](https://www.un.org/sustainabledevelopment/wp-content/uploads/2019/08/E_SDG_Icons-04.jpg)

## Overview
This project focuses on predicting whether countries are on track to meet **Sustainable Development Goal 4 (SDG 4)**, which aims to ensure inclusive and equitable quality education for all. Using machine learning classification techniques, we analyze global education indicators from the **United Nations SDG Global Database** to identify countries at risk of not achieving SDG 4 targets. The project follows an iterative modeling approach, employing logistic regression, decision trees, and random forests to predict educational outcomes based on features like proficiency levels, education level, gender, and geographic area.

The analysis is intended for **global education organizations** such as UNESCO, UNICEF, and the World Bank, providing insights to guide resource allocation and policy interventions.

## Business and Data Understanding

### Stakeholder
The primary stakeholders are **global education organizations** (e.g., UNESCO, UNICEF, World Bank) responsible for monitoring and supporting global education progress. These organizations need data-driven insights to prioritize funding and interventions in countries struggling to meet SDG 4 targets.

### Business Problem
The core question addressed is:  
**Can we predict whether a country is "on track" or "off track" to meet SDG 4 based on publicly available education and development indicators?**  
By classifying countries based on their educational performance, stakeholders can identify at-risk regions and allocate resources effectively to improve outcomes.

### Dataset Choice
The dataset is sourced from the **United Nations SDG Global Database**, specifically the `Goal4` sheet, which includes indicators such as:
- Proportion of children achieving minimum proficiency in reading and mathematics
- Education levels (e.g., primary, secondary)
- Demographic breakdowns (e.g., sex, age group)
- Country-level data and time series

![Dataset Snapshot](images/dataset_snapshot.png)

The dataset is maintained by the UN Statistics Division and aggregates data from national statistical offices and international agencies like UNESCO. It was chosen for its comprehensive coverage of SDG 4 indicators and its relevance to global education policy.

## Modeling
The project employs an **iterative modeling approach** to predict whether a country is on track to meet SDG 4 targets, defined by a threshold (e.g., 75% proficiency in foundational skills). Key steps include:

1. **Data Preprocessing**:
   - Handled missing values using imputation (e.g., SimpleImputer for numerical data).
   - Encoded categorical variables (e.g., education level, sex, country) using LabelEncoder.
   - Scaled numerical features (e.g., proficiency values) with StandardScaler to support distance-based models like logistic regression.
   - Created a binary classification target ("on track" vs. "off track") based on proficiency thresholds.

2. **Models Built**:
   - **Baseline Model**: Logistic Regression (interpretable, simple model to establish a performance baseline).
   - **Tuned Baseline Model**: Logistic Regression with hyperparameter tuning (e.g., adjusting regularization strength via GridSearchCV).
   - **Decision Tree**: Explored to capture non-linear relationships in the data.
   - **Random Forest**: An ensemble model to improve predictive performance and assess feature importance.

3. **Feature Engineering**:
   - Focused on key indicators like proficiency in math and reading, education level, gender, and geographic area (GeoAreaName).
   - Ensured no data leakage by fitting transformers (e.g., StandardScaler, LabelEncoder) on training data only and applying transformations to both train and test sets.

4. **Evaluation Metrics**:
   - Used **accuracy**, **precision**, **recall**, and **F1-score** to evaluate model performance, with a focus on **recall** to prioritize identifying countries "off track" (to minimize false negatives for at-risk countries).
   - Evaluated models on both training and test datasets to ensure generalizability.

## Evaluation
- **Model Performance**: 
  - The Random Forest model outperformed the baseline logistic regression and decision tree models, achieving higher recall and F1-scores on the test set.
  - However, no country consistently met the "on track" threshold across all records, indicating widespread challenges in achieving SDG 4 targets.
- **Feature Importance**:
  - The Random Forest model highlighted **type of skill** (math vs. reading), **education level**, and **country (GeoAreaName)** as the most influential predictors.
  - These findings suggest that geographic disparities and specific skill deficits (e.g., math proficiency) are critical factors in educational outcomes.

![Feature Importance Plot](images/feature_importance.png)

- **Limitations**:
  - Sparse or outdated data for some countries may skew predictions.
  - The binary threshold (e.g., 75% proficiency) may oversimplify complex educational progress.
  - The model may not capture recent improvements due to dataset limitations.

![Confusion Matrix](images/confusion_matrix.png)

## Conclusion
This project demonstrates that machine learning can effectively identify countries at risk of not meeting SDG 4 targets, enabling stakeholders to prioritize interventions. Key findings include:
- **Persistent Gaps**: Most countries in the dataset fall short of the 75% proficiency benchmark in foundational skills.
- **Geographic and Skill Disparities**: Country-specific factors and skill type (math vs. reading) significantly influence outcomes.
- **Actionable Insights**: Stakeholders should focus on:
  - Strengthening foundational skill training, particularly in primary education.
  - Tailoring interventions by region and skill type (e.g., math-focused programs in underperforming areas).
  - Improving data collection to ensure more comprehensive and recent datasets.

### Recommendations for Stakeholders
1. **Policy Focus**: Invest in primary education programs to address deficits in math and reading proficiency.
2. **Targeted Interventions**: Prioritize regions and demographics with consistently low performance, as identified by the model.
3. **Enhanced Data Collection**: Advocate for more frequent and complete reporting to the UN SDG Database to improve prediction accuracy.
4. **Monitoring Tool**: Deploy this model as an early warning system to track progress and flag at-risk countries in real-time with updated data.

This repository contains the Jupyter Notebook (`notebook.ipynb`), dataset (`data.xlsx`), and a non-technical presentation (to be submitted separately in PDF format). The code is well-documented, and the analysis is reproducible for further exploration or updates with new data.

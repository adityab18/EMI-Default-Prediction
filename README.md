# EMI Default Prediction Project

## 1. Project Overview

This project aims to predict the likelihood of a customer defaulting on their Equated Monthly Installment (EMI) payments. Using a real-world, noisy dataset from an Indian bank, this project performs data cleaning, preprocessing, and employs machine learning models to make predictions.

The primary goal is to build a reliable classification model that can help financial institutions mitigate risks associated with lending in Tier 3 towns and suburbs.

**Target Variable:** `Target_Flag` (1 indicates a default, 0 indicates no default).

---

## 2. Dataset

* **Source:** A real-world dataset from an Indian bank.
* **Description:** The dataset contains customer information related to their financial behavior and demographics. It is characterized by a significant class imbalance, with approximately 88% of customers belonging to the non-defaulting class. It also contains numerous columns with missing (null) values and some inconsistencies.

---

## 3. Project Workflow

The project follows a standard data science pipeline:

1.  **Data Loading & Initial Analysis:** Loading the raw data and performing an initial assessment to understand its structure, features, and quality.
2.  **Exploratory Data Analysis (EDA):** Identifying missing values, data inconsistencies (e.g., negative values in `N_Family_Member`), and understanding the relationships between different features using a correlation matrix.
3.  **Data Preprocessing & Cleaning:**
    * Dropping irrelevant columns and those with a high percentage (>65%) of missing data.
    * Converting categorical features to a numerical format.
    * Correcting invalid data entries.
    * Imputing missing values using domain knowledge and advanced techniques like KNN imputation.
4.  **Model Training & Evaluation:**
    * Splitting the data into training and testing sets.
    * Training multiple classification models (Random Forest, Logistic Regression, XGBoost).
    * Evaluating model performance using key metrics like Accuracy, Precision, Recall, and ROC-AUC score.
5.  **Prediction:** Generating a final submission file with customer predictions.

---

## 4. Data Preprocessing in Detail

A significant portion of this project involves preparing the noisy data for modeling.

* **Column Removal:** The following columns were dropped due to high null counts or irrelevance: `CoAp_Income`, `Max_Ratio_OC_Pending_POS`, `Total_Field_Trails`, `Total_Resolved`, `Customer_No`, `Branch_Code`, and `Birth_Year`.
* **Handling Inconsistencies:**
    * Negative values in `N_Family_Member` and `N_WorkEx_Yr` were corrected by taking their absolute values or imputing them based on customer age.
    * The `Ever_Default_L12M` column was converted from 'Yes'/'No' to a binary 1/0 format.
* **Missing Value Imputation:**
    * A **KNN (K-Nearest Neighbors) Imputer** with `n_neighbors=7` was used to fill in missing values for key financial columns. This method was chosen because it can provide more accurate imputations than simple mean/median by considering the "similarity" between data points based on other features.

---

## 5. Modeling and Results

* **Model Selection:** The following classification algorithms were implemented to tackle this prediction task:
    * Logistic Regression
    * Random Forest Classifier
    * XGBoost Classifier
* **Class Imbalance:** Given the 88% majority class, techniques to handle class imbalance (like SMOTE or using `class_weight` parameters in models) should be considered to avoid a biased model.
* **Evaluation:** Models were evaluated based on their ability to correctly identify defaulters (Recall) while maintaining a good overall accuracy and ROC-AUC score.

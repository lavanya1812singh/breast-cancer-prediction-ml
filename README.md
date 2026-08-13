# PREDICTING THE MALIGNANCY OF BREAST CANCER USING PCA AND MACHINE LEARNING MODELS

## Overview

This project investigates the use of Principal Component Analysis (PCA) and machine learning classification models to predict the malignancy of breast cancer cases.

The analysis explores relationships between diagnostic features, reduces dimensionality using PCA, trains multiple machine learning models, and evaluates the effect of outlier removal on model performance and PCA explained variance.

## Dataset

The dataset contains **569 observations and 32 columns**, including the diagnosis label and numerical diagnostic features such as:

* Radius
* Texture
* Perimeter
* Area
* Smoothness
* Compactness
* Concavity
* Concave points
* Symmetry
* Fractal dimension

The `diagnosis` variable is converted into a binary target:

* `0` → Benign
* `1` → Malignant

The notebook also checks for missing values and finds no missing values in the dataset.

## Project Workflow

### 1. Data Preparation

The project begins by importing the required Python libraries and loading the breast cancer dataset.

The data is inspected for missing values, and the categorical diagnosis values are converted into binary labels.

### 2. Correlation Analysis

A correlation matrix is generated to investigate the relationships between the diagnostic parameters and malignancy.

The analysis identifies several features with relatively strong correlations with the diagnosis, including:

* `concave_points_worst`
* `perimeter_worst`
* `concave_points_mean`
* `radius_worst`
* `perimeter_mean`
* `area_worst`
* `radius_mean`

A correlation heatmap and diagnosis distribution plot are also used for exploratory analysis.

### 3. PCA

Principal Component Analysis is applied after splitting the data into training and testing sets and standardizing the features.

The project reduces the feature representation to **two principal components** and visualizes the transformed training data using the first and second principal components.

Before removing outliers:

* **PC1 explained variance:** 45.71%
* **PC2 explained variance:** 17.84%

After removing outliers:

* **PC1 explained variance:** 42.63%
* **PC2 explained variance:** 20.86%

### 4. Machine Learning Models

Three classification models are implemented and evaluated:

* Logistic Regression
* Random Forest
* Decision Tree

The models are evaluated using:

* Accuracy
* F1-score
* Precision
* Recall
* Mean Absolute Error (MAE)
* Mean Squared Error (MSE)

Confusion matrices are also generated to examine classification results.

## Model Performance

### Before Outlier Removal

| Model               | Accuracy | F1-score | Precision | Recall |
| ------------------- | -------: | -------: | --------: | -----: |
| Logistic Regression |   90.06% |   86.82% |    84.85% | 88.89% |
| Random Forest       |   87.13% |   83.33% |    79.71% | 87.30% |
| Decision Tree       |   85.96% |   82.09% |    77.46% | 87.30% |

The results above are taken from the model comparison performed in the notebook.

### After Outlier Removal

The notebook uses boxplots to investigate outliers and applies feature-wise limits based on the mean and standard deviation before creating a dataset without outliers.

| Model               | Accuracy | F1-score | Precision | Recall |
| ------------------- | -------: | -------: | --------: | -----: |
| Logistic Regression |   89.93% |   83.52% |    86.36% | 80.85% |
| Random Forest       |   89.93% |   83.52% |    86.36% | 80.85% |
| Decision Tree       |   90.60% |   84.78% |    86.67% | 82.98% |

The Decision Tree achieved the highest accuracy in the reported results after outlier removal at **90.60%**, with an F1-score of **84.78%**.

## Outlier Analysis

A major part of the project is comparing the analysis before and after removing outliers.

The notebook investigates outliers using boxplots and calculates feature-specific upper and lower limits using the mean and standard deviation. The resulting dataset contains **495 rows and 32 columns** after the outlier-removal process.

The comparison shows that removing outliers changes the distribution of variance captured by the principal components:

|                        |    PC1 |    PC2 |
| ---------------------- | -----: | -----: |
| Before Outlier Removal | 45.71% | 17.84% |
| After Outlier Removal  | 42.63% | 20.86% |

The notebook discusses this as a trade-off: removing outliers reduces some variability captured by PC1 while increasing the variance captured by PC2.

## Key Findings

* The diagnostic features show different levels of correlation with malignancy.
* PCA provides a lower-dimensional representation of the standardized feature space.
* Logistic Regression performs best among the models evaluated before outlier removal, with approximately **90.06% accuracy**.
* After outlier removal, the Decision Tree achieves the highest reported accuracy at approximately **90.60%**.
* Outlier removal changes the distribution of variance between the first two principal components.
* Comparing models with and without outliers provides insight into how preprocessing choices can affect classification performance.

## Technologies Used

* **Python**
* **Jupyter Notebook**
* **Pandas**
* **NumPy**
* **Matplotlib**
* **Seaborn**
* **Scikit-learn**
* **StandardScaler**
* **PCA**
* **Logistic Regression**
* **Random Forest**
* **Decision Tree**

## Repository Contents

* `Breast_Cancer_Prediction_PCA.ipynb` — Complete Jupyter Notebook containing data preprocessing, exploratory analysis, PCA, machine learning models, outlier analysis, and evaluation.
* `Breast_Cancer_Prediction_Presentation.pptx` — Project presentation summarizing the methodology and findings.

## Conclusion

This project demonstrates an end-to-end machine learning workflow for breast cancer malignancy classification, combining exploratory data analysis, feature standardization, PCA-based dimensionality reduction, classification models, and outlier analysis.

The comparison between models trained before and after outlier removal highlights how preprocessing decisions can influence both model performance and the structure of the transformed feature space.

> **Disclaimer:** This project is for educational and machine learning demonstration purposes only. It is not a medical diagnostic system and should not be used to make clinical decisions.

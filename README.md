# Task 3: Multiple Linear Regression for House Price Prediction

### Objective
The primary objective was to implement a **Multiple Linear Regression** model to predict house prices, focusing on validating model assumptions, transforming skewed features, and interpreting feature coefficients.

### Dataset & Key Challenge
* **Dataset:** Housing Price Prediction Dataset (545 entries, India).
* **Challenge:** Initial EDA confirmed the target variable, `price`, and the primary numerical feature, `area`, were **highly right-skewed** (Mean > Median), violating the Normality assumption of Linear Regression.

---

### Methodology: Data Transformation & Scaling (L.I.N.E. Validation)

The pipeline was strictly executed to stabilize the data and ensure adherence to the key Linear Regression assumptions:

1.  **Categorical Encoding:** All object columns (including binary features like `mainroad` and multi-category features like `furnishingstatus`) were converted to numerical values using **Label Encoding** and **One-Hot Encoding**.
2.  **Skewness Correction (Transformation):** A **natural logarithmic transformation** ($\text{price}_{\text{log}} = \ln(\text{price})$) was applied to the target variable (`price`) and the main predictor (`area_log`). This critical step minimizes skewness and normalizes the distribution, satisfying the model's **Normality** assumption.
3.  **Feature Scaling:** All predictor features (X) were standardized using **`StandardScaler`**. This is necessary to equalize feature variance, allowing the Linear Regression algorithm (**Gradient Descent**) to converge efficiently and ensuring the resulting coefficients accurately reflect **relative feature importance**.

---

### Model Evaluation (Multiple Linear Regression)

| Metric | Value | Interpretation |
| :--- | :--- | :--- |
| **$R^2$ Score** | **0.6782** | The model explains **67.82%** of the variance in the log-price, indicating good fit. |
| **MAE (Mean Absolute Error)** | **0.1997** | The average magnitude of error in predicting the log-price. |
| **MSE (Mean Squared Error)** | **0.0621** | Measures the average squared error, penalizing larger mistakes. |

#### Plot Interpretation (Actual vs. Predicted)

The scatter plot compares the **Actual Log-Prices** ($Y_{test}$) against the **Predicted Log-Prices** ($Y_{pred}$). The red dashed line represents the **ideal prediction line** ($\text{Predicted} = \text{Actual}$). The tight clustering of the scatter points around this ideal line visually confirms the high $R^2$ score and the model's strong predictive capability.

---

### Coefficient Analysis (Feature Importance)

The coefficients, derived from the **standardized** features, show the relative impact of each variable on the house price:

| Feature | Coefficient Value | Impact on Price |
| :--- | :--- | :--- |
| **area_log** | 0.1177 | **Strongest Positive Predictor** (e.g., more likely to increase price). |
| **bathrooms** | 0.0882 | Second strongest positive predictor. |
| **furnishingstatus_unfurnished** | -0.0533 | **Strongest Negative Predictor** (e.g., most likely to decrease price). |
| **furniturestatus_semi_furnished** | -0.0025 | Second strongest negative predictor. |

**Key Insight:** The coefficient analysis confirms that **'Log-Area' and 'Bathrooms' are the most significant drivers of price.**


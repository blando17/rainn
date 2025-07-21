#  Rainfall Prediction 

This project predicts the likelihood of rainfall based on meteorological features using various state-of-the-art classification models. It includes data preprocessing, visualization, handling of class imbalance, and evaluation using ROC-AUC and classification metrics.

---

##  Dataset

- The dataset contains **366 days of weather data**, including:
  - Atmospheric pressure, temperature (max, min, avg), dew point
  - Humidity, cloud coverage, sunshine hours, wind direction/speed
  - Binary rainfall indicator (`yes`/`no`, later converted to `1`/`0`)

---

##  Data Preprocessing

- **Handled missing values** in `winddirection` and `windspeed` using column means.
- **Removed extra whitespaces** in column names.
- **Encoded categorical column**: `rainfall` → `1` for rain, `0` for no rain.
- **Scaled numerical features** using `StandardScaler`.
- **Balanced the dataset** using `RandomOverSampler` to oversample the minority class (rain days).

---

##  Exploratory Data Analysis (EDA)

- **Pie chart** to visualize class imbalance between rainy and non-rainy days.
- **Distribution plots** to observe the spread and skewness of each feature.
- **Box plots** to detect potential outliers in continuous features.

---

##  Models Used

We implemented and compared three classification models:

### 1. Logistic Regression
- Linear baseline model.
- Lightweight and interpretable.
- Good for linearly separable data.

### 2. XGBoost Classifier
- Gradient Boosting Tree model.
- Captures non-linear patterns.
- Can handle missing data natively.
- May overfit on small datasets if not tuned.

### 3. Support Vector Classifier (SVC)
- Kernelized classifier using RBF.
- Effective in high-dimensional and non-linear data.
- `probability=True` enabled to support ROC-AUC calculation.

---

##  Model Evaluation

Each model was trained on the **balanced training set** and tested on the **original (imbalanced) validation set** using **ROC-AUC score**.

| Model               | Training AUC | Validation AUC |
|--------------------|--------------|----------------|
| Logistic Regression| 0.8893       | 0.8967         |
| XGBoost Classifier | 1.0000       | 0.8392         |
| SVC (RBF Kernel)   | 0.9026       | 0.8858         |

>  **Logistic Regression and SVC** generalized well.  
>  **XGBoost** showed signs of overfitting.


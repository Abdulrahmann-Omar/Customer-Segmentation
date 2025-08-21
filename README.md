# 📊 Customer Segmentation Pipeline

A robust Python pipeline for generating synthetic telecom customer data, performing exploratory data analysis (EDA), and applying thorough data cleaning & preprocessing. This project simulates real-world telecom data challenges such as missing values, outliers, and inconsistencies—laying the foundation for effective customer segmentation (e.g., for operators like Vodafone).

---

## 🚦 Project Structure

The pipeline consists of three main stages:

1. **Synthetic Data Generation**  
   Create realistic telecom customer datasets with built-in data "dirtiness" for ML-ready workflows.

2. **Exploratory Data Analysis (EDA)**  
   Profile, visualize, and detect anomalies in the raw dataset.

3. **Data Cleaning & Preprocessing**  
   Clean, impute, and engineer features for downstream analytics or ML.

---

## 🏗️ Key Technologies

- **Core Libraries:** `pandas`, `numpy`, `random`, `faker`, `datetime`
- **Visualization:** `matplotlib`, `seaborn`
- **Preprocessing:** `sklearn.preprocessing`

---

## 1️⃣ Synthetic Data Generation

- **Function:** `generate_customer_data`
- **Purpose:** Generates a dataset with 28 attributes (demographics, service usage, telecom features).
- **Inputs:**  
  - `num_records` (int, default=1000): Number of customers to simulate.
- **Outputs:**  
  - `customer_segmentation_dirty_data.csv`

**Features:**

- **Realistic Profiles:** Names from `faker`, randomized service attributes.
- **Telecom-Specific Columns:** Demographics, package type, tenure, spend, device, etc.
- **Behavior Simulation:** Postpaid users show higher spend & tenure vs. Prepaid.
- **Data Dirtiness:**
  - *Missing Values:* Age (5%), Location (3%), AvgMonthlyDataGB (7%), PlanType (2%), VodafoneCashUsage (10%)
  - *Outliers:* Spend (1%), Data usage (0.5%)
  - *Inconsistencies:* Device flags (2%), tenure anomalies (1%)

---

## 2️⃣ Exploratory Data Analysis (EDA)

- **Input:** `customer_segmentation_dirty_data.csv`
- **Outputs:**  
  - Console logs (info, stats, missing/outlier/inconsistency reports)
  - PNG plots:
    - `age_distribution_dirty.png`
    - `spend_by_plan_type_dirty.png`
    - `correlation_matrix_dirty.png`
    - `churn_status_distribution_dirty.png`
    - `payment_method_distribution_dirty.png`

**Key Steps:**

- **Profiling:** Shape, columns, descriptive stats.
- **Missing Value Analysis:** Count & percent per column.
- **Outlier Detection:** IQR method (1.5 × IQR rule).
- **Inconsistency Checks:** Device capability mismatches, tenure anomalies.
- **Visualization:** Histograms, boxplots, heatmaps, count plots.

---

## 3️⃣ Data Cleaning & Preprocessing

- **Function:** `preprocess_customer_data`
- **Input:** `customer_segmentation_dirty_data.csv`
- **Output:** `customer_segmentation_cleaned_data.csv`

**Cleaning Logic:**

- **Missing Values:**
  - *Age, AvgMonthlyDataGB:* Median imputation
  - *Location, PlanType:* Mode imputation
  - *VodafoneCashUsage:* Imputed as 0
  - *InterconnectedRelativePackage:* Imputed as "None"
- **Outliers:** Capped using IQR bounds.
- **Inconsistencies:**
  - Align phone models with correct 4G/5G capabilities
  - Cap Prepaid tenure at 60 months
  - Enforce Postpaid tenure ≥ 12 months
- **Feature Engineering:** Convert `DevicePurchaseDate` to `datetime`
- **(Optional):** One-hot encoding & scaling (commented for flexibility)
- **Validation:** Prints missing stats before & after cleaning

---

## ⚙️ Key Parameters & Configurations

- **Phone Models Dictionary:** Maps devices to valid 4G/5G
- **Predefined Categories:** Locations, package types, payment methods
- **Data Dirtiness:** Missing/outlier rates are tunable in `generate_customer_data`
- **Adjustable:**  
  - `num_records` (dataset size)
  - Outlier detection IQR bounds

---

## 🚀 Usage

**Install Dependencies:**
```sh
pip install pandas numpy faker matplotlib seaborn scikit-learn
```

**Run Pipeline (in order):**
```sh
python generate_data.py       # Step 1: Generate synthetic dirty data
python analyze_data.py        # Step 2: EDA & anomaly detection
python preprocess_data.py     # Step 3: Clean & preprocess data
```

**Generated Outputs:**
- `customer_segmentation_dirty_data.csv`
- `customer_segmentation_cleaned_data.csv`
- EDA plots:  
  - `age_distribution_dirty.png`  
  - `spend_by_plan_type_dirty.png`  
  - `correlation_matrix_dirty.png`  
  - `churn_status_distribution_dirty.png`  
  - `payment_method_distribution_dirty.png`

---

## 📌 Assumptions & Limitations

**Assumptions**
- Synthetic data mimics typical telecom patterns (e.g., postpaid → higher spend & tenure).
- Distributions approximate real-world customer behavior.

**Limitations**
- Synthetic data may not cover all real-world customer nuances.
- Basic visualizations; extend for advanced analytics as needed.

---

## 🤝 Contributions

Contributions and suggestions are welcome! Please open an issue or submit a pull request.

---

## 📄 License

Distributed under the MIT License.

Customer Segmentation Code Documentation
📌 Overview

This project provides a Python-based pipeline for generating synthetic telecom customer data, performing exploratory data analysis (EDA), and applying data cleaning techniques.

The goal is to build a customer segmentation system for a telecom operator (e.g., Vodafone), simulating real-world data challenges such as missing values, outliers, and inconsistencies.

The project is divided into three main components:

Synthetic Data Generation

Exploratory Data Analysis (EDA)

Data Cleaning & Preprocessing

Key Libraries: pandas, numpy, random, faker, datetime, matplotlib, seaborn, sklearn.preprocessing

🔹 1. Synthetic Data Generation
Functionality

The generate_customer_data function creates a dataset with 28 attributes for a given number of customer records (default: 1000). The dataset simulates demographics, service usage, and telecom-specific features.

Inputs

num_records (int): Number of records to generate (default = 1000).

Outputs

CSV file: customer_segmentation_dirty_data.csv

Key Features

Realistic Data: Uses faker for customer names and random for service attributes.

Telecom-Specific Attributes: Includes demographics, package type, tenure, spend, device type, etc.

Plan-Based Behavior: Postpaid users generally have higher spend and longer tenure than Prepaid.

Data Dirtiness:

Missing Values: Age (5%), Location (3%), AvgMonthlyDataGB (7%), PlanType (2%), VodafoneCashUsage (10%).

Outliers: Spend (1%), Data usage (0.5%).

Inconsistencies: Incorrect 4G/5G flags (2%), unusual tenure values (1%).

🔹 2. Exploratory Data Analysis (EDA)
Functionality

Analyzes the raw dataset (customer_segmentation_dirty_data.csv) to detect missing values, outliers, and inconsistencies, while generating insights through visualizations.

Inputs

customer_segmentation_dirty_data.csv

Outputs

Console Logs: Dataset info, descriptive stats, missing values summary, outlier counts, inconsistency reports.

Visualizations (PNG files):

age_distribution_dirty.png

spend_by_plan_type_dirty.png

correlation_matrix_dirty.png

churn_status_distribution_dirty.png

payment_method_distribution_dirty.png

Key Features

Data Profiling: Shape, column info, summary statistics.

Missing Value Report: Counts and percentages.

Outlier Detection: IQR method (1.5 * IQR).

Inconsistency Detection: Device capability mismatches, tenure anomalies.

Visualization: Histograms, boxplots, heatmaps, and count plots.

🔹 3. Data Cleaning & Preprocessing
Functionality

The preprocess_customer_data function cleans the dataset by handling missing values, outliers, and inconsistencies.

Inputs

Raw dirty dataset (customer_segmentation_dirty_data.csv)

Outputs

CSV file: customer_segmentation_cleaned_data.csv

Key Features

Missing Value Handling:

Age, AvgMonthlyDataGB → Median imputation

Location, PlanType → Mode imputation

VodafoneCashUsage → Replaced with 0

InterconnectedRelativePackage → "None"

Outlier Capping: IQR-based capping.

Inconsistency Fixes:

Aligns phone models with true 4G/5G capability.

Caps Prepaid tenure at 60 months.

Ensures Postpaid tenure ≥ 12 months.

Feature Engineering: Converts DevicePurchaseDate to datetime.

Optional Preprocessing: One-hot encoding & scaling (commented for flexibility).

Validation: Prints missing value stats before & after cleaning.

⚙️ Key Parameters & Configurations

Phone Models Dictionary: Maps devices to valid 4G/5G capabilities.

Predefined Categories: Locations, package types, payment methods.

Data Dirtiness Probability: Tunable missing/outlier rates in generate_customer_data.

Adjustable Parameters:

num_records (dataset size).

Outlier detection IQR bounds.

🚀 Usage

Install Dependencies:

pip install pandas numpy faker matplotlib seaborn scikit-learn


Run Scripts in Order:

python generate_data.py      # Generate dirty dataset
python analyze_data.py       # Perform EDA
python preprocess_data.py    # Clean dataset


Generated Output Files:

customer_segmentation_dirty_data.csv

customer_segmentation_cleaned_data.csv

EDA plots (.png files listed above)

📌 Assumptions & Limitations
Assumptions

Synthetic data mimics typical telecom patterns (e.g., Postpaid → higher spend & tenure).

Predefined distributions approximate real-world telecom behavior.

Limitations

Synthetic data may not capture all real-world customer nuances.

Preprocessing steps like one-hot encoding/scaling are optional (commented).

Visualizations are basic and can be extended for advanced analysis.

# Task 1: Data Cleaning and Preprocessing

## 📊 Dataset
**Source:** Customer Personality Analysis (Kaggle)
**File:** `marketing_campaign.csv`

## 🔍 Raw Data Issues Found
Upon initial inspection, the following issues were identified:
1. **Missing Values:** 24 missing values in the `Income` column.
2. **Inconsistent Text:** `Marital_Status` contained erroneous categories like "Alone", "YOLO", and "Absurd". Text capitalization was inconsistent across columns.
3. **Date Formats:** `Dt_Customer` was stored as an object string (`dd-mm-yyyy`) instead of a recognized datetime type.
4. **Data Types & Outliers:** `Year_Birth` contained impossible years (1893, 1899, 1900), resulting in ages > 120. `Income` contained extreme outliers (e.g., 666,666).
5. **Useless Columns:** `Z_CostContact` and `Z_Revenue` contained constant values and provided zero analytical value.

## 🛠️ Cleaning Steps Performed
1. **Headers:** Standardized all column names to lowercase and replaced spaces with underscores.
2. **Constant Columns:** Dropped `Z_CostContact` and `Z_Revenue`.
3. **Missing Values:** Filled the 24 missing `Income` values using the **median income grouped by Education**. This preserves the natural distribution better than a global median.
4. **Date Parsing:** Converted `Dt_Customer` to a proper `datetime64` object using `dayfirst=True`. Derived `customer_year` and `customer_month`.
5. **Impossible Years:** Filtered out 3 rows where `Year_Birth` was before 1900. Calculated a new `age` column based on the dataset reference year (2014).
6. **Text Standardization:** Applied `Title Case` to `Education` and `Marital_Status`. Merged sparse categories: "Alone", "Absurd", and "YOLO" were consolidated into "Single".
7. **Duplicates:** Ran `drop_duplicates()`. (Note: 0 rows were removed as the dataset uses a unique ID per row).
8. **Outliers:** Used the IQR method on `Income`. Instead of deleting rows, created a new column `income_capped` to clip extreme values at the upper bound (Q3 + 1.5*IQR).

## 📈 Final Shape
* **Before:** 2240 rows, 29 columns
* **After:** 2237 rows, 32 columns

## 📁 Files in this Repository
* `cleaning_script.py` - The Python script used for the cleaning process.
* `marketing_campaign.csv` - The original raw dataset.
* `cleaned_marketing_campaign.csv` - The final cleaned dataset.

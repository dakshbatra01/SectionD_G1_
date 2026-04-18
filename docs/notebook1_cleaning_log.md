# Notebook 01 – Data Extraction & Initial Cleaning Log

##  Dataset Information
- Dataset Name: Loan_Default_Raw.csv
- Total Rows (Initial): 15,000
- Total Columns: 34

---

##  Step 1: Data Loading
- Loaded dataset using pandas
- Verified structure using:
  - head()
  - info()
  - describe()

---

##  Step 2: Missing Value Handling
- Checked null values using `isnull().sum()`
- Applied:
  - Median imputation for numerical columns
  - Mode imputation for categorical columns
- Result:
  - Missing values reduced to 0 (or near 0)

---

##  Step 3: Duplicate Removal
- Removed duplicate rows using `drop_duplicates()`
- Ensured dataset uniqueness

---

## Step 4: Column Standardization
- Converted all column names to lowercase
- Removed extra spaces
- Example:
  - `Loan_Amount` → `loan_amount`

---

##  Step 5: Text Cleaning
- Converted all categorical values to lowercase
- Removed leading/trailing spaces
- Ensured consistency in categorical data

---

##  Output
- Cleaned dataset saved as:
  - `loan_stage1_cleaned.csv`

---

##  Summary
This notebook focused on:
- Data extraction
- Handling missing values
- Removing duplicates
- Standardizing structure

The dataset is now clean and ready for transformation.

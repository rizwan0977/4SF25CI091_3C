# Skill Lab – CIE 1 (Milestone 1): Retail & E-Commerce Sales Data Analysis

## Overview
This repository contains the submission for **Skill Lab – CIE 1 (Milestone 1): Data Transformation, Null Value Handling, Insight Generation, and Visualization**. The project analyzes a retail and e-commerce dataset (`sales_data.csv`) containing **2,500 transaction records** across calendar year 2025 using **Python**, **Pandas**, **NumPy**, **Matplotlib**, and **Seaborn**.

## Repository Contents
| File Name | Description |
| :--- | :--- |
| `CIE1_Milestone1_Analysis.ipynb` | Executed Jupyter Notebook implementing data loading, exploratory understanding, data transformation, mean imputation for null values, insight generation, and visualizations |
| `sales_data.csv` | Raw CSV dataset (2,500 rows × 15 columns) containing retail order records, pricing, customer ratings, regional details, and missing values for imputation |
| `README.md` | Project overview, dataset schema, methodology summary, key findings, and execution instructions |

## Dataset Description (`sales_data.csv`)
The dataset consists of **2,500 retail transactions** spanning **January 2025 to December 2025** across five geographic regions (`South`, `West`, `North`, `East`, `Central`) and six product categories (`Electronics`, `Home & Kitchen`, `Apparel`, `Sports & Outdoors`, `Beauty & Personal Care`, `Books & Media`).

| Column Name | Data Type (Raw) | Description | Null Values (Raw) |
| :--- | :--- | :--- | :--- |
| `Order_ID` | `object` (String) | Unique identifier for each order (`ORD-100001` to `ORD-102500`) | 0 |
| `Order_Date` | `object` (String) | Transaction date in `YYYY-MM-DD` format | 0 |
| `Customer_ID` | `object` (String) | Unique identifier for the customer | 0 |
| `Customer_Segment` | `object` (String) | Buyer segment (`Consumer`, `Corporate`, `Home Office`) | 0 |
| `Region` | `object` (String) | Geographic region (`South`, `West`, `North`, `East`, `Central`) | 0 |
| `Category` | `object` (String) | Product category (6 categories) | 0 |
| `Product_Name` | `object` (String) | Specific item purchased | 0 |
| `Payment_Method` | `object` (String) | Payment channel (`UPI`, `Credit Card`, `Debit Card`, `Net Banking`, `Cash on Delivery`) | 0 |
| `Quantity` | `float64` | Number of units purchased in the order | 80 (3.20%) |
| `Unit_Price` | `float64` | Price per unit (in ₹) | 120 (4.80%) |
| `Discount_Percent` | `float64` | Promotional discount applied (`0%` to `25%`) | 140 (5.60%) |
| `Shipping_Cost` | `float64` | Delivery charge for the order (in ₹) | 100 (4.00%) |
| `Customer_Rating` | `float64` | Post-purchase customer rating (`1.5` to `5.0`) | 160 (6.40%) |
| `Internal_Audit_Code` | `object` (String) | Redundant administrative code dropped during transformation | 0 |
| `Legacy_System_Ref` | `object` (String) | Legacy system tag dropped during transformation | 0 |

## Methodology & Workflow

### 1. Dataset Selection and Reading
- Loaded `sales_data.csv` into a Pandas DataFrame using `pd.read_csv("sales_data.csv")` and verified its initial shape (`2500 rows × 15 columns`).

### 2. Data Understanding
- Inspected first and last records via `df.head()` and `df.tail()`.
- Examined schema, non-null counts, and column types using `df.info()`.
- Computed summary statistics for numerical and categorical features via `df.describe()` and `df.describe(include='object')`.

### 3. Data Transformation
- **Dropped Unnecessary Columns**: Removed `Internal_Audit_Code` and `Legacy_System_Ref` using `df.drop()`.
- **Changed Data Types**: Converted `Order_Date` from `object` to `datetime64[ns]` using `pd.to_datetime()`.
- **Added Derived Columns**: Extracted temporal features (`Order_Year`, `Order_Month`, `Order_Month_Name`, `Order_Quarter`, `Day_of_Week`) and computed revenue metrics (`Gross_Sales`, `Discount_Amount`, `Net_Revenue`, `Total_Billed_Amount`, and `Order_Value_Tier`).

### 4. Handling Null Values (Mean Imputation)
- Identified **600 total missing values** distributed across five numerical columns.
- Imputed missing entries in each numerical column using **Mean Imputation** (`df[col].fillna(round(df[col].mean(), 2))`):
  - `Quantity`: Imputed 80 missing values with the column mean (`2.28`).
  - `Unit_Price`: Imputed 120 missing values with the column mean (`₹2,163.84`).
  - `Discount_Percent`: Imputed 140 missing values with the column mean (`9.09%`).
  - `Shipping_Cost`: Imputed 100 missing values with the column mean (`₹145.45`).
  - `Customer_Rating`: Imputed 160 missing values with the column mean (`4.13`).
- Verified that `df.isnull().sum().sum()` equals `0` after imputation.

### 5. Key Insights Generated
| Analytical Dimension | Key Finding | Metric / Value |
| :--- | :--- | :--- |
| **Overall Revenue** | Total net revenue across 2,500 orders in 2025 | **₹1,10,55,166.47** (~₹110.55 Lakhs) |
| **Peak Sales Period** | Highest monthly net revenue recorded in **November 2025** (273 orders) | **₹12.40 Lakhs** (Avg Order Value: ₹4,542.58) |
| **Top Region** | **South** leads all regions in order volume (729 orders) and net revenue | **₹34.91 Lakhs** (**31.58%** of total revenue) |
| **Second-Largest Region** | **West** ranks second in regional revenue contribution | **₹27.85 Lakhs** (**25.19%** of total revenue) |
| **Top Product Category** | **Electronics** generates the largest share of net revenue (626 orders) | **₹44.42 Lakhs** (**40.18%** of total revenue) |
| **Second-Largest Category** | **Home & Kitchen** ranks second in category revenue | **₹27.08 Lakhs** (**24.50%** of total revenue) |
| **Payment Preference** | Digital payments (**UPI**, **Credit Card**, **Debit Card**) dominate checkout | **82.0%** of all transactions (UPI leads at ~42%) |

### 6. Data Visualizations Included in the Notebook
1. **Monthly Net Revenue Trend (Line Chart)**: Illustrates month-over-month revenue trajectory and Q4 festive surge across 2025.
2. **Region-Wise Net Revenue Comparison (Bar Chart)**: Displays total net revenue (in ₹ Lakhs) and percentage share across all 5 regions.
3. **Product Category Revenue Ranking (Horizontal Bar Chart)**: Ranks all 6 product categories by net revenue contribution.
4. **Category vs. Region Net Revenue Matrix (Heatmap)**: Visualizes cross-regional performance for every product category.
5. **Customer Segment Revenue & Payment Method Share (Dual Plot)**: Compares revenue across `Consumer`, `Corporate`, and `Home Office` segments alongside a pie chart of payment channels.
6. **Correlation Matrix Heatmap**: Displays pairwise Pearson correlations among numerical features post-mean imputation.

## How to Run Locally
1. Clone your repository (`USN_SECTION`, e.g., `4SF35CI223_3C`):
   ```bash
   git clone https://github.com/<your-username>/<USN_SECTION>.git
   cd <USN_SECTION>
   ```
2. Install the required Python libraries:
   ```bash
   pip install pandas numpy matplotlib seaborn jupyter
   ```
3. Launch Jupyter Notebook and open `CIE1_Milestone1_Analysis.ipynb`:
   ```bash
   jupyter notebook CIE1_Milestone1_Analysis.ipynb
   ```
   *(Ensure `sales_data.csv` is in the same directory as `CIE1_Milestone1_Analysis.ipynb`.)*

# SmartCart Customer Segmentation – Data Dictionary

## 1. Dataset Overview

The SmartCart dataset contains customer demographic information, household details, purchasing behavior and marketing campaign response information.

| Attribute | Value |
|---|---|
| Dataset file | smartcart_customers.csv |
| Format | CSV |
| Total records | 2,240 |
| Total columns | 22 |
| Numerical columns | 20 |
| Categorical columns | 2 |

*Note: Numerical and categorical counts above are based on the pandas data types observed in the raw CSV.*

## 2. Column Descriptions

### A. Customer Identification and Demographics

| Column | Data Type | Description |
|---|---|---|
| ID | Integer | Unique customer identifier |
| Year_Birth | Integer | Customer's birth year |
| Education | Object | Customer's education level |
| Marital_Status | Object | Customer's marital status |
| Income | Float | Customer's annual income |

### B. Household Information

| Column | Data Type | Description |
|---|---|---|
| Kidhome | Integer | Number of children in the household |
| Teenhome | Integer | Number of teenagers in the household |
| Dt_Customer | Object | Date when the customer registered or joined |

### C. Customer Purchasing Behavior

| Column | Data Type | Description |
|---|---|---|
| Recency | Integer | Number of days since the customer's last purchase |
| MntWines | Integer | Amount spent on wine products |
| MntFruits | Integer | Amount spent on fruit products |
| MntMeatProducts | Integer | Amount spent on meat products |
| MntFishProducts | Integer | Amount spent on fish products |
| MntSweetProducts | Integer | Amount spent on sweet products |
| MntGoldProds | Integer | Amount spent on gold products |

### D. Purchase Channel Information

| Column | Data Type | Description |
|---|---|---|
| NumDealsPurchases | Integer | Number of purchases made using discounts or deals |
| NumWebPurchases | Integer | Number of purchases made through the website |
| NumCatalogPurchases | Integer | Number of purchases made through the catalog |
| NumStorePurchases | Integer | Number of purchases made directly in stores |
| NumWebVisitsMonth | Integer | Number of website visits during the month |

### E. Marketing Campaign Information

| Column | Data Type | Description |
|---|---|---|
| Complain | Integer | Indicates whether the customer registered a complaint |
| Response | Integer | Indicates whether the customer responded to a marketing campaign |

## 3. Data Type Summary

The dataset contains the following data types:

- Integer (int64): Customer identifiers, demographic values, purchase counts and campaign indicators.
- Float (float64): Income.
- Object: Education, Marital_Status and Dt_Customer.

Note: The actual pandas output identifies three object columns, not two. These are categorical or date-like fields.

## 4. Dataset Usage in Machine Learning

The dataset provides information that can be used for customer segmentation.

Important feature groups include:

1. Demographic features – Age, Education, Marital Status and Income.
2. Household features – Kidhome and Teenhome.
3. Spending features – Product-wise spending amounts.
4. Purchase behavior – Deals, web, catalog and store purchases.
5. Customer engagement – Recency, website visits and campaign response.

## 5. Data Preparation Considerations

Before applying machine learning algorithms, the dataset may require:

- Handling missing values.
- Converting date columns into appropriate formats.
- Feature engineering.
- Handling outliers.
- Encoding categorical variables.
- Feature scaling.

The actual preprocessing steps are documented separately in METHODOLOGY.md.

## 6. Dataset Limitations

- The dataset represents customer information at a particular point in time.
- Customer segmentation depends on the selected features.
- Some columns may require transformation before clustering.
- The dataset's monetary units and original collection methodology should be verified from its original source.


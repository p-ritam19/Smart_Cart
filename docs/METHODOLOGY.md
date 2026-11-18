# SmartCart Customer Segmentation – Methodology

## 1. Introduction

This document explains the data preprocessing, feature engineering, dimensionality reduction and clustering techniques implemented in the SmartCart Customer Segmentation project.

The project uses unsupervised machine learning to identify customer groups based on demographic characteristics and purchasing behavior.

## 2. Data Preprocessing

### 2.1 Dataset Loading

The customer dataset is loaded from a CSV file using Pandas.

### 2.2 Missing Value Handling

The dataset initially contains 24 missing values in the Income column.

These missing values are handled using median imputation.

```python
df["Income"] = df["Income"].fillna(df["Income"].median())
```

Median imputation is used to replace missing income values without removing customer records.

## 3. Feature Engineering

New features are created to provide additional information about customer behavior.

### 3.1 Age

Customer age is calculated using the birth year.

```python
df["Age"] = 2026 - df["Year_Birth"]
```

### 3.2 Customer Tenure

Customer joining dates are converted into datetime format.

Customer tenure is calculated as the difference between the latest joining date in the dataset and each customer's joining date.

```python
df["Dt_Customer"] = pd.to_datetime(
    df["Dt_Customer"], dayfirst=True
)

reference_date = df["Dt_Customer"].max()

df["Customer_Tenure_Days"] = (
    reference_date - df["Dt_Customer"]
).dt.days
```

### 3.3 Total Spending

Total customer spending is calculated by combining spending across six product categories:

- Wines
- Fruits
- Meat products
- Fish products
- Sweet products
- Gold products

```python
df["Total_Spending"] = (
    df["MntWines"] +
    df["MntFruits"] +
    df["MntMeatProducts"] +
    df["MntFishProducts"] +
    df["MntSweetProducts"] +
    df["MntGoldProds"]
)
```

### 3.4 Total Children

The total number of children and teenagers in the household is calculated.

```python
df["Total_Children"] = (
    df["Kidhome"] + df["Teenhome"]
)
```

### 3.5 Education Transformation

Education categories are grouped into broader educational levels:

- Basic and 2n Cycle → Undergraduate
- Graduation → Graduate
- Master and PhD → Postgraduate

### 3.6 Living Status Transformation

Marital status categories are transformed into two groups:

- Partner
- Alone

This creates a simplified household living-status feature.

## 4. Feature Selection

The following original columns are removed:

- ID
- Year_Birth
- Marital_Status
- Kidhome
- Teenhome
- Dt_Customer
- Original product-wise spending columns

These columns are removed after creating the relevant engineered features.

The resulting cleaned dataset contains 15 columns before categorical encoding.

## 5. Outlier Handling

Pair plots are used to explore relationships and distributions among selected numerical features.

The following filtering conditions are applied:

```python
df_cleaned = df_cleaned[
    df_cleaned["Age"] < 90
]

df_cleaned = df_cleaned[
    df_cleaned["Income"] < 600000
]
```

After filtering, the dataset contains 2,236 customer records, compared with the original 2,240 records.

## 6. Exploratory Data Analysis

A correlation heatmap is generated to examine relationships between numerical features.

This helps understand the relationships between income, spending, customer engagement and other numerical attributes.

## 7. Categorical Encoding

One-Hot Encoding is applied to the following categorical features:

- Education
- Living_With

The encoded columns are combined with the numerical features to create the final feature matrix.

After encoding, the dataset contains:

- 2,236 customer records
- 18 features

## 8. Feature Scaling

StandardScaler is applied to standardize the feature values.

```python
scaler = StandardScaler()

X_scaled = scaler.fit_transform(X)
```

Scaling ensures that features with larger numerical ranges do not dominate the distance-based clustering algorithms.

## 9. Dimensionality Reduction Using PCA

Principal Component Analysis (PCA) is used to reduce the feature space to three principal components.

```python
pca = PCA(n_components=3)

X_pca = pca.fit_transform(X_scaled)
```

The explained variance ratios obtained are:

| Component | Explained Variance |
|---|---:|
| PCA 1 | 23.16% |
| PCA 2 | 11.39% |
| PCA 3 | 10.41% |
| **Total** | **44.95%** |

A three-dimensional scatter plot is generated to visualize the reduced feature space.

## 10. Optimal Cluster Selection

### 10.1 Elbow Method

The Elbow Method is used to analyze the Within-Cluster Sum of Squares (WCSS).

K-Means is evaluated for cluster counts ranging from 1 to 10.

KneeLocator is used to identify the elbow point.

The notebook identifies four clusters as the elbow point.

### 10.2 Silhouette Score

Silhouette scores are calculated for K-Means clustering with cluster counts ranging from 2 to 10.

This metric helps evaluate how well-separated the resulting clusters are.

The notebook calculates and plots the scores to support cluster selection.

## 11. Clustering Algorithms

### 11.1 K-Means Clustering

K-Means is implemented using four clusters and a random state of 42.

```python
kmeans = KMeans(
    n_clusters=4,
    random_state=42
)

labels_kmeans = kmeans.fit_predict(X_pca)
```

A 3D scatter plot is generated to visualize the resulting customer clusters.

### 11.2 Agglomerative Clustering

Agglomerative Clustering is also implemented using four clusters and Ward linkage.

```python
agg_clf = AgglomerativeClustering(
    n_clusters=4,
    linkage="ward"
)

labels_agg = agg_clf.fit_predict(X_pca)
```

A separate 3D visualization is generated for the resulting clusters.

## 12. Cluster Characterization

The notebook uses the Agglomerative Clustering labels for cluster characterization.

A cluster column is added to the feature dataset.

Customer groups are analyzed using:

- Cluster distribution.
- Income patterns.
- Total spending patterns.
- Customer purchasing behavior.
- Demographic and household features.

A cluster summary is generated using group-wise mean values.

## 13. Final Outcome

The project demonstrates how customer information can be transformed into meaningful features and analyzed using unsupervised learning.

K-Means and Agglomerative Clustering are both explored to identify customer segments.

PCA provides a three-dimensional representation of the processed feature space for visualization and clustering.

## 14. Implementation Notes and Limitations

- The age calculation currently uses a fixed reference year of 2026.
- Customer tenure uses the maximum joining date in the dataset as its reference date.
- PCA retains approximately 44.95% of the total variance in the three selected components.
- Four clusters are selected using the elbow point.
- Silhouette scores are calculated, but the notebook does not print a numerical comparison of the scores.
- The cluster characterization section uses Agglomerative Clustering labels.


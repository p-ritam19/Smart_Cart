# SmartCart Customer Segmentation — Results

## 1. Dataset Overview

- Original records: 2,240 customers
- Original features: 22 columns
- Missing values: 24 in the Income column
- Missing Income values were filled using median imputation.
- Records after outlier filtering: 2,236 customers.

## 2. Feature Engineering and Preprocessing

The following features were engineered:

- Age: Calculated using 2026 minus birth year.
- Customer_Tenure_Days: Customer registration tenure.
- Total_Spending: Sum of spending across six product categories.
- Total_Children: Sum of children and teenagers in the household.

Categorical features were transformed using one-hot encoding.

- Processed customer records: 2,236
- Features after encoding: 18
- StandardScaler was used for feature scaling.

## 3. Principal Component Analysis (PCA)

PCA was applied to reduce the scaled dataset to three components.

| Component | Explained Variance |
|---|---:|
| PCA 1 | 23.16% |
| PCA 2 | 11.39% |
| PCA 3 | 10.41% |
| Total | 44.95% |

The three components retain approximately 44.95% of the original variance.

## 4. Clustering Algorithms

### K-Means Clustering

- Number of clusters: 4
- Random state: 42
- Input: Three PCA components
- Elbow Method and Silhouette Score were explored.

### Agglomerative Clustering

- Number of clusters: 4
- Linkage method: Ward
- Input: Three PCA components

Both algorithms were visualized using PCA projections.

## 5. Customer Segment Analysis

The customer profile summary was generated using Agglomerative Clustering labels.

| Cluster | Avg. Income | Avg. Spending | Avg. Age | Avg. Response |
|---|---:|---:|---:|---:|
| 0 | 39,681 | 222 | 55.67 | 7.62% |
| 1 | 72,808 | 1,237 | 59.49 | 16.67% |
| 2 | 36,960 | 166 | 55.69 | 14.19% |
| 3 | 70,723 | 1,190 | 58.93 | 32.01% |

Note: Income and spending values are expressed in the dataset's original units.

### Cluster Observations

**Cluster 0 — Lower-Income, Lower-Spending Customers**

- Average income: 39,681
- Average spending: 222
- Average campaign response: 7.62%

**Cluster 1 — Higher-Income, Higher-Spending Customers**

- Average income: 72,808
- Average spending: 1,237
- Average campaign response: 16.67%

**Cluster 2 — Lower-Income, Lower-Spending Customers**

- Average income: 36,960
- Average spending: 166
- Average campaign response: 14.19%

**Cluster 3 — Higher-Income, Higher-Spending Customers**

- Average income: 70,723
- Average spending: 1,190
- Average campaign response: 32.01%

## 6. Key Business Insights

1. Higher-income customer segments show substantially higher average spending.
2. Clusters 1 and 3 have higher purchasing activity than clusters 0 and 2.
3. Cluster 3 has the highest average campaign response rate.
4. Clusters 0 and 2 may offer opportunities for targeted promotions.
5. Household composition differs across the generated customer segments.

## 7. Limitations

- The first three PCA components explain approximately 44.95% of the variance.
- Four clusters were selected for the final clustering models.
- Cluster labels are algorithm-generated identifiers.
- The project does not include real-time segmentation or deployment.

## 8. Future Improvements

- Evaluate clustering with additional metrics.
- Explore alternative dimensionality reduction techniques.
- Experiment with other clustering algorithms.
- Build an interactive customer segmentation dashboard.
- Deploy the project using Flask or Django.

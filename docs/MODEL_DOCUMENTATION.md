# SmartCart – Machine Learning Model Documentation

## 1. Overview

This document describes the machine learning techniques implemented in the SmartCart Customer Segmentation project.

The project uses unsupervised learning to discover customer groups based on demographic information and purchasing behavior.

The following techniques are implemented:

- Principal Component Analysis (PCA)
- K-Means Clustering
- Agglomerative Clustering

## 2. Principal Component Analysis (PCA)

### Purpose

PCA is a dimensionality reduction technique used to transform the original feature space into a smaller number of principal components.

In this project, PCA reduces the processed feature matrix to three components.

### Implementation

```python
from sklearn.decomposition import PCA

pca = PCA(n_components=3)
X_pca = pca.fit_transform(X_scaled)
```

### Explained Variance

The three principal components collectively explain approximately 44.95% of the variance in the scaled dataset.

PCA is also used to visualize customer data in three dimensions.

## 3. K-Means Clustering

### Purpose

K-Means is an unsupervised learning algorithm that groups data points into a predefined number of clusters based on their distances from cluster centroids.

### Implementation

```python
from sklearn.cluster import KMeans

kmeans = KMeans(
    n_clusters=4,
    random_state=42
)

labels_kmeans = kmeans.fit_predict(X_pca)
```

### Cluster Selection

The Elbow Method is used to examine the Within-Cluster Sum of Squares (WCSS) for different cluster counts.

The notebook also calculates silhouette scores for different values of K.

The elbow analysis identifies four clusters, which are used in the final K-Means implementation.

### Visualization

A three-dimensional scatter plot is generated using the PCA components, with points colored according to their assigned cluster.

## 4. Agglomerative Clustering

### Purpose

Agglomerative Clustering is a hierarchical clustering algorithm.

It begins with individual observations and progressively merges similar groups until the required number of clusters is reached.

### Implementation

```python
from sklearn.cluster import AgglomerativeClustering

agg_clf = AgglomerativeClustering(
    n_clusters=4,
    linkage="ward"
)

labels_agg = agg_clf.fit_predict(X_pca)
```

### Linkage Method

Ward linkage is used to determine which clusters should be merged.

It aims to minimize the increase in within-cluster variance during the merging process.

### Visualization

A separate three-dimensional scatter plot is generated to visualize the Agglomerative Clustering results.

## 5. Cluster Characterization

The project uses the Agglomerative Clustering labels for further customer analysis.

The cluster labels are added to the processed feature dataset.

The following analyses are performed:

- Customer count in each cluster.
- Relationship between customer income and spending.
- Average numerical feature values for each cluster.

A group-wise mean summary is generated to understand the characteristics of each customer segment.

## 6. Model Comparison

| Aspect | K-Means | Agglomerative |
|---|---|---|
| Learning type | Unsupervised | Unsupervised |
| Approach | Centroid-based | Hierarchical |
| Number of clusters | 4 | 4 |
| Distance strategy | Euclidean distance by default | Ward linkage |
| Output | Cluster labels | Cluster labels |

Both algorithms are applied to the same PCA-transformed feature matrix.

The notebook visualizes both clustering results separately.

A numerical comparison of clustering quality has not yet been implemented.

## 7. Limitations

- PCA with three components retains approximately 44.95% of the original variance.
- The final cluster count is fixed at four.
- Cluster quality should be evaluated using additional metrics.
- Cluster labels do not automatically represent meaningful business categories.
- Agglomerative Clustering is used for the final cluster characterization.

## 8. Future Improvements

- Compare clustering quality using silhouette scores for both algorithms.
- Evaluate Davies-Bouldin and Calinski-Harabasz scores.
- Experiment with different PCA component counts.
- Analyze cluster stability.
- Develop customer segment profiles.
- Build an interactive customer segmentation dashboard.


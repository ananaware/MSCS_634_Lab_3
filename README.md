# MSCS 634 - Lab 3: Clustering Analysis Using K-Means and K-Medoids

## Purpose
This lab compares K-Means and K-Medoids clustering on the Wine dataset from scikit-learn (178 wines, 13 features, 3 classes). I standardized the data with z-scores, clustered it with k = 3, and judged the results with the Silhouette Score and the Adjusted Rand Index (ARI).

## Results

| Algorithm | Silhouette Score | ARI | Wines in the wrong cluster |
|---|---|---|---|
| K-Means | 0.2849 | 0.8975 | 6 |
| K-Medoids | 0.2676 | 0.7411 | 16 |

## Key Insights
- K-Means did better. Its ARI was much higher, so its clusters matched the real wine classes more closely. The silhouette scores were close, so both give clusters that are only moderately separated.
- The two methods agree on one group and differ on the other two. K-Medoids made one group bigger by taking in 12 wines that K-Means placed in a different group.
- K-Means fits this data well because it is clean, standardized, and has no big outliers. K-Medoids would be a better choice when there are outliers, or when each cluster center needs to be a real data point.

## Challenges and Decisions
- **Scaling:** I standardized all features first, because both methods use distances and large-valued features like proline would otherwise dominate.
- **K-Medoids library:** The usual `scikit-learn-extra` package failed to import because of a NumPy version problem, so I used the `kmedoids` package with the PAM method instead. PAM gave the same result every time I ran it.
- **Data type error:** The package returned labels as an unsigned integer type, which caused an error in `np.bincount`. I fixed it by converting the labels to regular integers.
- **Plotting:** The data has 13 features, so I used PCA to draw it in 2D. The two axes keep about 55% of the information, so the clusters look more overlapped than they really are. I also matched the cluster colors between the two plots so they are easy to compare.

## Files
- `MSCS_634_Lab_3.ipynb` - notebook with all code, plots, and explanations
- `README.md` - this file

# Feature Selection for Clustering: A Review

number of synsets will be reduced.. Finally, FTS will be applied to these documents that contain the synsets.

These two proposed algorithms (i.e., FTS and FTMS) were empirically proved to be superior to other algorithms, as such bisect k-means and hierarchical item-based clustering. Yet, FTMS is more capable of capturing precise clustering topics than FTS. This is due to using the terms synsets instead of just the word itself.

There are several clustering techniques based on frequent term sets besides the notions in this chapter [19, 61, 77, 4, 47]. However, they all follow the notion of reducing dimensionality by finding the frequent term sets. They differ in the parameters or the underlying utilized methods. For example, the number of terms in the frequent set may be set to a specific number or undefined. Hence, the maximum number will be found. They also differ in the final cluster smoothed or merged.

# 2.2.3 Algorithms for Streaming Data

Streaming Data are continuous and rapid data. Formally defined as a set of multi-records X1,...,Xn, that come in time sets T1,...,Tn. Each record Xi is multidimensional. These usually have a huge dimensionality and arrive very fast. They require scalable and efficient algorithms. Also, the underlying structure is changing, so we need to capture this and keep selected features up to date. In this section, we introduce what we believe to be required characteristics of a good algorithm that handles streaming data:

+   - **Adaptivity**: The algorithm should be able to adjust features' weights or reselect the features, so it is able to handle the data drift, aka dataset shift.

+   - **Single scan**: The algorithm should be able to cluster the incoming stream in one scan, since another scan is usually impossible or at least costly.

The following algorithms represent the literature of feature selection for data stream clustering. In fact, this area still needs great attention from the researchers due to the lack of work in this area.

# 2.2.3.1 Text Streaming Based on Adaptive Feature Selection (TSC-AFS)

It is natural for clusters and data categories to evolve over time. For example, the breaking news dominates the world today may change dramatically. Therefore, using the same set of features to process and cluster data stream may lead to unsatisfactory learning results over time. Gop et al in [20] propose using the cluster quality γ to test the quality of newly arrived samples' clustering respect to old clusters. TSC-AFS starts by applying feature selection on training data D. Then, it clusters the samples of D with the selected features only.

After that, it tracks data streams and assigns to the closest cluster. TSC-AFS evaluates a validity index p for each cluster the Davies-Bouldin B index. If j is less than p, then TSC-AFS will reselect the set of features. Otherwise, the algorithm keeps the feature set and clusters based on them and accepts new streams to come. Otherwise, TSC-AFS will reevaluate p while considering the new data stream being added the closest cluster. If the validity index cannot satisfy the thresholds, a tolerance kappa is set to allow the cluster to be closed and initialize the algorithm again. kappa and γ are simply determined by the cross-validation approach.

This algorithm utilizes a order variance-based method for feature selection since the domain in [20] is text stream. However, any appropriate algorithm may be used. In addition, k-means is used as a clustering method. Algorithm 8 shows the pseudocode for TSC-AFS. TSC-AFS, shown in Algorithm 8, is argues in terms of performance and applicability in the
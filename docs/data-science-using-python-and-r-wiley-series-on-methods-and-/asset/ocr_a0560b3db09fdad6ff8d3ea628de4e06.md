straightforward and effective algorithm for finding clusters in data. The algorithm proceeds as follows:

+   - Step 1: Ask the user how many clusters k the data set should be partitioned into.
+   - Step 2: Randomly assign k records to be the initial cluster center locations.
+   - Step 3: For each record, find the nearest cluster center. Thus, in a sense, each cluster center "owns" a subset of the records, thereby representing a partition of the data set. We therefore have k clusters, C1, C2, ..., Ck.
+   - Step 4: For each of the k clusters, find the cluster centroid and update the location of each cluster center to the new value of the centroid.
+   - Step 5: Repeat steps 3–5 until convergence or termination.

The "nearest" criterion in step 3 is usually Euclidean distance, although other criteria may be applied as well. The cluster centroid in step 4 is found as follows. Suppose that we have n data points (a1, b1, c1), (a2, b2, c2), ..., (an, bn, cn), the centroid of these points is the center of gravity of these points and is located at point (Σa/n, Σb/n, Σc/n). For example, the points (1,1,1), (1,2,1), (1,3,1), and (2,1,1) would have centroid

\(\left( \frac{1+1+1+2}{4}, \frac{1+2+3+1}{4}, \frac{1+1+1+1}{4} \right) = (1.25, 1.75, 1.00)\)

The algorithm terminates when the centroids no longer change. In other words, the algorithm terminates when for all clusters C1, C2, ..., Ck, all the records "owned" by each cluster center remain in that cluster. For much more on k-means clustering, see Data Mining and Predictive Analytics.

# 10.3 AN APPLICATION OF K-MEANS CLUSTERING

We apply the k-means clustering algorithm to the white_wine_training and the white_wine_test data sets. These data sets are adapted from the Wine Quality data set at UCI.3 The data consist of chemical and quality characteristics of a collection of Portuguese white wines. The predictors are alcohol and sugar. The target variable is quality, a measure of how good the wine is, according to a professional taster. When constructing clusters, it is important to not include the target variable as an input to the clustering algorithm. Doing so would bias the results if we later use the clusters to predict the target. It is also important to standardize or normalize all the predictors, so that the greater variability of one predictor does not dominate the cluster construction process.

Now, the k-means algorithm requires the analyst to specify the desired number of clusters. For simplicity, we specify k = 2 clusters and proceed to apply

3https://archive.ics.uci.edu/ml/datasets/wine+quality. Also P. Cortez, A. Cerdeira, F. Almeida, T. Matos, and J. Reis. Modeling wine preferences by data mining from physicochemical properties. Decision Support Systems, Elsevier, 47(4), 547-553. 2009.
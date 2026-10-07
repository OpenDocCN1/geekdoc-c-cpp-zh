# Clustering Categorical Data

First level clusters. Categorical similarity is emphasized.

![](bbox=[0.283, 0.083, 0.362, 0.153])

![](bbox=[0.453, 0.083, 0.532, 0.153])

![](bbox=[0.583, 0.083, 0.662, 0.153])

![](bbox=[0.713, 0.083, 0.822, 0.153])

Second level clusters consist of subclusters. Numerical similarity is emphasized.

![](bbox=[0.283, 0.199, 0.362, 0.269])

![](bbox=[0.453, 0.199, 0.532, 0.269])

![](bbox=[0.583, 0.199, 0.662, 0.269])

![](bbox=[0.713, 0.199, 0.822, 0.269])

FIGURE 12.8: Overview of the BILCOM clustering process.

tion, age and weight are numerical attributes modeled with a normal (Gaussian) distribution. At each loop, AutoClass changes the classifications of objects in clusters, so that each object is assigned to the cluster with the attribute probability distributions (considering the current means and variances) that give the highest probability of observing the object' values. Additionally, AutoClass iteratively examines different number of clusters, which are not user-specified. Then, AutoClass changes the means and variances of the probability distributions for the attributes in cluster. The iteration continues until the clusters and the attributes' probability distributions stabilize. The AutoClass output is a mixture of several likely clusters, where a clustering classifies each object into the most likely cluster on the basis of the attributes' probability distributions.

Drawbacks of AutoClass include that users have to specify the model spaces to be searched and in wrong models may produce wrong results. Also, AutoClass can be slow to converge to a clustering result on some datasets.

# 12.4.4.3 SVM (Mixed Categorical and Numerical)

Support Vector Machines (SVMs) provide a method for supervised learning. SVMs construct a separating hyperplane using a training of data, as shown in Figure 12.9. Despite their superiority, SVMs have been applied to categorical data to find clusters in an unsupervised manner. The approach involves randomly assigning objects to pairs of clusters and recomputing the separating hyperplane, until there is a convergence of object assignment and the hyperplane.

Previously, SVM-Internal (usually referred to as a one-class SVM) used internal of Support Vector Machines to find the closest sphere in data. The internal approach to SVM clustering lacked robustness and is biased towards clusters with a spherical shape feature. In the case of real-world problems, the SVM-Internal algorithm could only detect the relatively small cluster cores.

To remedy this, an external-SVM algorithm was introduced to clusters data with no prior knowledge of each object's classification. Initially, every object in the dataset is densely labeled and a binary SVM is trained. After the initial convergence is achieved, the sensitivity + specificity will be low, likely near 1. The algorithm improves this result by iteratively relabeling only those misclassified objects, which have confidence factors beyond some threshold, followed by rerunning the SVM on the newly labeled dataset. The lowest confidence classifications, those objects with confidence values beyond some threshold, repeatedly
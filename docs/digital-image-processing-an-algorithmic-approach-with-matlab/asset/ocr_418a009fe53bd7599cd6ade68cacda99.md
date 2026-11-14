![](bbox=[0.1, 0.08, 0.93, 0.56])

FIGURE 12.3 (See color insert following Page 204.) Application of nearest neighbor algorithm to classify the given image into its classes. (a) Sample image. (b) selected areas as training classes, (c) segmented image, (d) class boundaries.

classifier is a more “informed” algorithm as the frequencies of occurrence of the features of interest are used to aid the classification process. Without this information, the minimum (mean) distance classifier can yield biased classifications. This can be best combated by applying training patterns at the natural rates at which they arise in the raw training set.

# 12.5 UNSUPERVISED CLASSIFICATION

The second method employed for this classification is called unsupervised segmentation. In general, unsupervised clustering techniques are used less frequently, as the computation time required for the algorithm to learn
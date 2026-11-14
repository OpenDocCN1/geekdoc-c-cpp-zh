![](bbox=[0.05, 0.08, 0.46, 0.34])

![](bbox=[0.49, 0.08, 0.9, 0.34])

![](bbox=[0.27, 0.36, 0.68, 0.63])

FIGURE 12.1 (See color insert following Page 204.) Image classification using the grayscale ranges only: (a) Original RGB image, (b) grayscale version of (a), (c) segmented image.

# 12.4 NEAREST NEIGHBOR CLASSIFIER

A convenient way of building a parametric description of the kind mentioned in the previous section is by using a feature vector \([\theta_1, \theta_2, \cdots, \theta_n]\), where \(n\) is the number of attributes that describe each image feature and training class. This representation allows us to consider each image feature as occupying a point, and each training class as occupying a subspace (i.e., a representative point surrounded by some spread, or deviation) within the \(n\)-dimensional classification
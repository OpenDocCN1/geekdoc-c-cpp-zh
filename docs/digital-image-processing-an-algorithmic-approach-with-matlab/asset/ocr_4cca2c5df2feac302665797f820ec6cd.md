![](bbox=[0.28, 0.07, 0.84, 0.35])

FIGURE 12.2 Feature space: + represents color #, o represents texture degree.

space. Viewed as such, the classification problem is that of determining to which subspace class each feature vector belongs.

For example, consider an application in which we must distinguish between two different types of objects (e.g., apples and oranges) based on a set of two attribute classes (e.g., color and texture). If we assume that we have a vision system capable of extracting these features from a set of training images, we can plot the result in the 2D feature space shown in Figure 12.2.

However, usually the situation is not so simple for isolating the data into various groups. At this point, we must decide how to numerically partition the feature space so that if we are given the feature vector of a test object, we can determine, quantitatively, to which of the two classes it belongs. One of the simplest (although not the most computationally efficient) techniques is to employ a supervised, distribution-free approach known as the minimum (mean) distance classifier or nearest neighbor classifier. This technique is now described.

Minimum (mean) distance classifier. Among the various methods of supervised statistical pattern recognition, the nearest neighbor rule achieves consistently high performance, without a priori assumptions about the distributions from which the training examples are drawn. It involves a training set of both positive and negative cases. A new sample is classified by calculating the distance to the nearest training case; the sign of that point then determines the classification of the sample. The k-NN classifier extends
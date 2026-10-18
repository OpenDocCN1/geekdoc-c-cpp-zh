of the two selected winning prototypes w_jq and w_kp, ensuring that the two winning prototypes are close to the boundary between the two competing categories. The LVQ2 update is as follows:

w_jq(t) = w_jq(t − 1) − η(t)(x − w_jq)   for the first winner but incorrect category   (8.37)
w_kq(t) = w_kq(t − 1) + η(t)(x − w_kq)   for the second winner and correct category   (8.38)

LVQ2 training selects and updates the two winning prototypes, whenever misclassification occurs and when these prototypes are directly competing. This is slightly similar to the multi-class perceptron model except that the goal of the LVQ2 is to minimize the distance to the correct prototype while the perceptron minimizes the dot product between the input and the weights.

LVQ can be seen as a supervised extension of vector quantization (VQ), Self-Organization Map (SOM) [76], or k-means clustering. Those algorithms compress data into a set of representative prototypes and generate clusters of data centered at prototypes. These unsupervised techniques are generally used as a starting point for LVQ training, which is then used to readjust the clusters, boundaries based on the data labels. Clustering can generate initial prototypes using the entire data set but it is more effective to perform clustering within each category, thus generating initial prototypes per category, and then use LVQ competitive training to readjust the boundaries [93].

# 8.3.3.3 Application and Limitations

LVQ inherits the benefits of prototype-based learning algorithms in terms of theoretically proven generalization ability for high dimensional data and are characterized by dimensionality independent large-margin generalization bounds [30]. LVQ has been successfully applied to a wide range of data classification tasks. In particular, an LVQ system was able to achieve similar performance as a more complex neural network in a speech sounds classification task [93]. However, the original LVQ formulation suffers from several drawbacks. One drawback is the lack of an objective function being optimized; LVQ training was derived intuitively and used heuristics that may lead to instability or sensitivity to learning parameters [13]. Another drawback is the use of the Euclidean distance, which limits the performance capabilities of the system.

Various generalizations of LVQ have been proposed to overcome some of these issues. The generalized LVQ (GLVQ) [119] proposes an objective function that quantifies the difference between the closest but wrong category and the second closest but correct category. Minimization, based on gradient descent techniques, is more stable than the original LVQ version. Similarly, LVQ can be seen as a particular instance of the prototype-based minimum classification error (PBMEC) [94, 106]. PBMEC implements an Lp-norm of distances to prototypes with a discriminative objective function whose optimization yields an update similar to LVQ2. Also, alternative distance measures have been used, including the Mahalanobis distance, and the use of kernels with better success [50, 121]

# 8.4 Kernel Neural Network

We used the term kernel-based neural network for a class of neural network that use a kernel within their architecture. The most prominent example of this type is the Radial Basis Function Network, which is the focus of this section.

# 8.4.1 Radial Basis Function Network

A radial basis function network (RBFN) [108] implements a two-layer architecture, featuring kernel units in the hidden layer and linear units in the output layer. Although RBFNs were derived
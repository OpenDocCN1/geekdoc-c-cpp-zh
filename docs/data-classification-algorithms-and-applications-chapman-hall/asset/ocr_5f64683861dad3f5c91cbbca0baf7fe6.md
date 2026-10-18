function is computed at the instance using these centers. The combination of functions computed from each of these centers is computed with the use of a neural network. Radial basis functions can be considered three-layer feed-forward networks, in which each hidden unit computes a function of the form:

```
$$f_i(x) = e^{-\|x - x_i\|^2 / 2 \sigma_i^2}. \tag{6.17}$$
```

Here $\sigma_i^2$ represents the local variance at center $x_i$. Note that the function $f_i(x)$ has a very similar form to that commonly used in kernel density estimation. For ease in discussion, we assume that this is a binary classification problem, with labels drawn from $\{+1, -1\}$, though this general approach extends much further, even to the extent of regression modeling. The final function is a weighted combination of these values with weights $c_i$.

```
$$f^*(x) = \sum_{i=1}^{N} w_i \cdot f_i(x). \tag{6.18}$$
```

Here $x_1 \dots x_N$ represent the $N$ different centers, and $w_i$ denotes the weight of center $i$, which is learned in the neural network. In classical instance-based methods, each data point $x_i$ is an individual training instance, and the weight $w_i$ is set to $+1$ or $-1$, depending upon its label. However, in RBF methods, the weights are learned with a neural network approach, since the centers are derived from the underlying training data, and do not have a label directly attached to them.

The $N$ centers $x_1 \dots x_N$ are typically constructed with the use of an unsupervised approach [19, 37, 46], though some recent methods also use supervised techniques for constructing the centers [71]. The unsupervised methods [19, 37, 46] typically use a clustering algorithm in order to generate the different centers. A smaller number of centers typically results in smaller complexity, and greater efficiency of the classification process. Radial-basis function networks are related to sigmoidal function networks (SGF), which have one unit for each instance in the training data. In this sense sigmoidal networks are somewhat closer to classical instance-based methods, since they do not have a first phase of cluster-based summarization. While radial-basis function networks are generally more efficient, the points at the different cluster boundaries may often be misclassified. It has been shown in [52] that RBF networks may sometimes require ten times as much training data as SGF in order to achieve the same level of accuracy. Some recent work [71] has shown how supervised methods even at the stage of center determination can significantly improve the accuracy of these classifiers. Radial-basis function networks can therefore be considered an evolution of nearest neighbor classifiers, where more sophisticated (clustering) methods are used for prototype selection (or re-construction in the form of cluster centers), and neural network methods are used for combining the density values obtained from each of the centers.

# 6.10 Lazy Methods for Diagnostic and Visual Classification

Instance-centered methods are particularly useful for diagnostic and visual classification, since the role of a diagnostic method is to find diagnostic characteristics that are specific to that test-instance. When an eager model is fully constructed as a pre-processing step, it is often not optimized to finding the best diagnostic characteristics that are specific to a particular test instance. Therefore, instance-centered methods are a natural approach in such scenarios. The subspace decision path method [6] can be considered a lazy and interactive version of the decision tree, which provides insights into the specific characteristics of a particular test instance.

Kernel density estimation is used in order to create a visual profile of the underlying data. It is assumed that the data set $\mathcal{D}$ contains $N$ points and $d$ dimensions. The set of points in $\mathcal{D}$ are denoted
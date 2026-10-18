
restricted to a strict hierarchical partitioning of the data. This is most evident from the relative performance of these methods in some sparse high dimensional domains such as text. For example, while many rule-based methods such as RIPPER are frequently used for the text domain, decision trees are used rarely for text. Another advantage of these methods is that they are relatively easy to generalize to different data types such as sequences, XML or graph data [14,93]. In such cases, the left-hand side of the rule needs to be defined in a way that is specific for that data domain. For example, for a sequence classification problem [14], the left-hand side of the rule corresponds to a sequence of symbols. For a graph-classification problem, the left-hand side of the rule corresponds to a frequent structure [93]. Therefore, while rule-based methods are related to decision trees, they have significantly greater expressive power. Rule-based methods are discussed in detail in Chapter 5.

### 1.2.5 Instance-Based Learning

In instance-based learning, the first phase of constructing the training model is often dispensed with. The test instance is directly related to the training instances in order to create a classification model. Such methods are referred to as lazy learning methods, because they wait for knowledge of the test instance in order to create a locally optimized model, which is specific to the test instance. The advantage of such methods is that they can be directly tailored to the particular test instance, and can avoid the information loss associated with the incompleteness of any training model. An overview of instance-based methods may be found in [15,16,89].

An example of a very simple instance-based method is the nearest neighbor classifier. In the nearest neighbor classifier, the top $k$ nearest neighbors in the training data are found to the given test instance. The class label with the largest presence among the $k$ nearest neighbors is reported as the relevant class label. If desired, the approach can be made faster with the use of nearest neighbor index construction. Many variations of the basic instance-based learning algorithm are possible, wherein aggregates of the training instances may be used for classification. For example, small clusters can be created from the instances of each class, and the centroid of each cluster may be used as a new instance. Such an approach is much more efficient and also more robust because of the reduction of noise associated with the clustering phase which aggregates the noisy records into more robust aggregates. Other variations of instance-based learning use different variations on the distance function used for classification. For example, methods that are based on the Mahalanobis distance or Fisher’s discriminant may be used for more accurate results. The problem of distance function design is intimately related to the problem of instance-based learning. Therefore, separate chapters have been devoted in this book to these topics.

A particular form of instance-based learning is one where the nearest neighbor classifier is not explicitly used. This is because the distribution of the class labels may not match with the notion of proximity defined by a particular distance function. Rather, a locally optimized classifier is constructed using the examples in the neighborhood of a test instance. Thus, the neighborhood is used only to define the locality in which the classification model is constructed in a lazy way. Local classifiers are generally more accurate, because of the simplification of the class distribution within the locality of the test instance. This approach is more generally referred to as lazy learning. This is a more general notion of instance-based learning than traditional nearest neighbor classifiers. Methods for instance-based classification are discussed in Chapter 6. Methods for distance-function learning are discussed in Chapter 18.

### 1.2.6 SVM Classifiers

SVM methods use linear conditions in order to separate out the classes from one another. The idea is to use a linear condition that separates the two classes from each other as well as possible. Consider the medical example discussed earlier, where the risk of cardiovascular disease is related to diagnostic features from patients.

![](img/e042be977d84f1032c985f0d70b57c8b_40_0.png)
![](img/e042be977d84f1032c985f0d70b57c8b_40_1.png)

(a) Hard separation

(b) Soft separation

MARGIN

MARGIN

MARGIN VIOLATION WITH PENALTY-BASED SLACK VARIABLES

**FIGURE 1.2:** Hard and soft support vector machines.

$$
\text{CRP} + \text{Cholesterol}/100 \le 4
$$

In such a case, the split condition in the multivariate case may also be used as a stand-alone condition for classification. Thus, an SVM classifier may be considered a single-level decision tree with a very carefully chosen multivariate split condition. Clearly, since the effectiveness of the approach depends only on a single separating hyperplane, it is critical to define this separation carefully.

Support vector machines are generally defined for binary classification problems. Therefore, the class variable $y_i$ for the $i$-th training instance $\overline{X}_i$ is assumed to be drawn from $\{-1, +1\}$. The most important criterion, which is commonly used for SVM classification, is that of the maximum margin hyperplane. In order to understand this point, consider the case of linearly separable data illustrated in Figure 1.2(a). Two possible separating hyperplanes, with their corresponding support vectors and margins have been illustrated in the figure. It is evident that one of the separating hyperplanes has a much larger margin than the other, and is therefore more desirable because of its greater generality for unseen test examples. Therefore, one of the important criteria for support vector machines is to achieve maximum margin separation of the hyperplanes.

In general, it is assumed for $d$-dimensional data that the separating hyperplane is of the form $\overline{W} \cdot \overline{X} + b = 0$. Here $\overline{W}$ is a $d$-dimensional vector representing the coefficients of the hyperplane of separation, and $b$ is a constant. Without loss of generality, it may be assumed (because of appropriate coefficient scaling) that the two symmetric support vectors have the form $\overline{W} \cdot \overline{X} + b = 1$ and $\overline{W} \cdot \overline{X} + b = -1$. The coefficients $\overline{W}$ and $b$ need to be learned from the training data $D$ in order to maximize the margin of separation between these two parallel hyperplanes. It can be shown from elementary linear algebra that the distance between these two hyperplanes is $2 / \|\overline{W}\|$. Maximizing this objective function is equivalent to minimizing $\|\overline{W}\|^2 / 2$. The problem constraints are defined by the fact that the training data points for each class are on one side of the support vector. Therefore, these constraints are as follows:

$$
\overline{W} \cdot \overline{X}_i + b \ge +1 \quad \forall i : y_i = +1 \quad (1.12)
$$

$$
\overline{W} \cdot \overline{X}_i + b \le -1 \quad \forall i : y_i = -1 \quad (1.13)
$$

This is a constrained convex quadratic optimization problem, which can be solved using Lagrangian methods. In practice, an off-the-shelf optimization solver may be used to achieve the same goal.

In practice, the data may not be linearly separable. In such cases, soft-margin methods may be used. A slack variable $\xi_i \ge 0$ is introduced for each training instance, and a training instance is allowed to violate the support vector constraint for a penalty, which is dependent on the slack. This situation is illustrated in Figure 1.2(b). Therefore, the new set of constraints is now as follows:

$$
\overline{W} \cdot \overline{X}_i + b \ge +1 - \xi_i \quad \forall i : y_i = +1 \quad (1.14)
$$

$$
\overline{W} \cdot \overline{X}_i + b \le -1 + \xi_i \quad \forall i : y_i = -1 \quad (1.15)
$$

$$
\xi_i \ge 0 \quad (1.16)
$$

Note that additional non-negativity constraints also need to be imposed on the slack variables. The objective function is now:

$$
\frac{\|\overline{W}\|^2}{2} + C \cdot \sum_{i=1}^{n} \xi_i
$$

The constant $C$ regulates the importance of the margin and the slack requirements. In other words, small values of $C$ make the approach closer to a soft-margin SVM, whereas large values of $C$ make the approach more of a hard-margin SVM. It is also possible to solve this problem using off-the-shelf optimization solvers.

It is also possible to use transformations on the feature variables in order to design non-linear SVM methods. In practice, non-linear SVM methods are learned using kernel methods. The key idea here is that SVM formulations can be solved using only pairwise dot products (similarity values) between objects. In other words, the optimal decision about the class label of a test instance, from the solution to the quadratic optimization problem in this section, can be expressed in terms of the following:

1. Pairwise dot products of different training instances.
2. Pairwise dot products of the test instance and different training instances.

The reader is advised to refer to [84] for the specific details of the solution to the optimization formulation. The dot product between a pair of instances can be viewed as a notion of similarity among them. Therefore, the aforementioned observations imply that it is possible to perform SVM classification, with pairwise similarity information between training data pairs and training-test data pairs. The actual feature values are not required.

This opens the door for using transformations, which are represented by their similarity values. These similarities can be viewed as kernel functions $K(\overline{X},\overline{Y})$, which measure similarities between the points $\overline{X}$ and $\overline{Y}$. Conceptually, the kernel function may be viewed as the dot product between the pair of points in a newly transformed space (denoted by the mapping function $\Phi(\cdot)$). However, this transformation does not need to be explicitly computed, as long as the kernel function (dot product) $K(\overline{X},\overline{Y})$ is already available:

$$
K(\overline{X},\overline{Y}) = \Phi(\overline{X}) \cdot \Phi(\overline{Y}) \quad (1.17)
$$

Therefore, all computations can be performed in the original space using the dot products implied by the kernel function. Some interesting examples of kernel functions include the Gaussian radial basis function, polynomial kernel, and hyperbolic tangent, which are listed below in the same order.

$$
K(\overline{X}_i,\overline{X}_j) = e^{-\|\overline{X}_i - \overline{X}_j\|^2 / 2\sigma^2} \quad (1.18)
$$

$$
K(\overline{X}_i,\overline{X}_j) = (\overline{X}_i \cdot \overline{X}_j + 1)^h \quad (1.19)
$$

$$
K(\overline{X}_i,\overline{X}_j) = \tanh(k \overline{X}_i \cdot \overline{X}_j - \delta) \quad (1.20)
$$

These different functions result in different kinds of nonlinear decision boundaries in the original space, but they correspond to a linear separator in the transformed space. The performance of a classifier can be sensitive to the choice of the kernel used for the transformation. One advantage of kernel methods is that they can also be extended to arbitrary data types, as long as appropriate pairwise similarities can be defined.

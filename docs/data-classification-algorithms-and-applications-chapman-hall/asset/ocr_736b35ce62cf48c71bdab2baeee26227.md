In practice, the data may not be linearly separable. In such cases, soft-margin methods may be used. A slack $\xi_i \geq 0$ is introduced for training instance, and a training instance is allowed to violate the support vector constraint, for a penalty, which is dependent on the slack. This situation is illustrated in Figure 1.2(b). Therefore, the new set of constraints are now as follows:

$\overline{W}\cdot\overline{X}_i+b\geq +1-\xi_i \quad \forall i:y_i=+1$  (1.14)

$\overline{W}\cdot\overline{X}_i+b\leq -1+\xi_i \quad \forall i:y_i=-1$  (1.15)

$\xi_i\geq 0$  (1.16)

Note that additional non-negativity constraints also need to be imposed in the slack variables. The objective function is now $\|\overline{W}\|^2/2+C\cdot\sum_{i=1}^{n}\xi_i$. The constant $C$ regulates the importance of the margin and the slack requirements. In other words, small values of $C$ make the approach closer to soft-margin SVM, whereas large values of $C$ make the approach more of the hard-margin SVM. It is also possible to solve this problem using off-the-shelf optimization solvers.

It is also possible to use transformations on the feature variables in order to design non-linear SVM methods. In practice, non-linear SVM methods are learned using kernel methods. The key idea here is that SVM formulations can be solved using only pairwise dot products (similarity values) between objects. In other words, the optimal decision about the class label of a test instance, from the solution to the quadratic optimization problem in this section, can be expressed in terms of the following:

+   1. Pairwise dot products of different training instances.
+   2. Pairwise dot product of the test instance and different training instances.

The reader is advised to refer to [84] for the specific details of the solution to the optimization formulation. The dot product between a pair of instances can be viewed as notion of similarity among them. Therefore, the aforementioned observations imply that it is possible to perform SVM classification, with pairwise similarity information between training data pairs and training-test data pairs. The actual feature values are not required.

This opens the door for using transformations, which are represented by their similarity values. These similarities can be viewed as kernel functions $K(\overline{X},\overline{Y})$, which measure similarities between the points $\overline{X}$ and $\overline{Y}$. Conceptually, the kernel function may be viewed as dot product between the pair of points in a newly transformed space (denoted by mapping function $\Phi(\cdot)$). However, this transformation does not need to be explicitly computed, as long as the kernel function (dot product) $K(\overline{X},\overline{Y})$ is already available:

$K(\overline{X},\overline{Y})=\Phi(\overline{X})\cdot\Phi(\overline{Y})$  (1.17)

Therefore, all computations can be performed in the original space using the dot products implied by the kernel function. Some interesting examples of kernel functions include the Gaussian radial basis function, polynomial kernel, and hyperbolic tangent, which are listed below in the same order.

$K(\overline{X}_i,\overline{X}_j)=e^{-\|\overline{X}_i-\overline{X}_j\|^2/2\sigma^2}$  (1.18)

$K(\overline{X}_i,\overline{X}_j)=(\overline{X}_i\cdot\overline{X}_j+1)^h$  (1.19)

$K(\overline{X}_i,\overline{X}_j)=\tanh(k\overline{X}_i\cdot\overline{X}_j-\delta)$  (1.20)

These different functions result in different kinds of nonlinear decision boundaries in the original space, but they correspond to a linear separator in the transformed space. The performance of a classifier can be sensitive to the choice of the kernel used for the transformation. One advantage of kernel methods is that they can also be extended to arbitrary data types, as long as appropriate pairwise similarities can be defined.
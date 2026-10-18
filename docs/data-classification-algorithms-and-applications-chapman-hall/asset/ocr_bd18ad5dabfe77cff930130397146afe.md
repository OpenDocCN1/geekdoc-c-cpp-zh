![](bbox=[0.11, 0.15, 0.42, 0.31])

![](bbox=[0.49, 0.13, 0.82, 0.3])

# (a) Hard separation

# (b) Soft separation

# FIGURE 11.1: Hard and soft support vector machines.

X̄ + b = −1. The coefficients W̄ and b need to be learned from the training data D in order to maximize the margin of separation between these two parallel hyperplanes. It can be shown from elementary linear algebra that the distance between these two hyperplanes is 2 / ||W̄||. Maximizing this objective function is equivalent to minimizing ||W̄||² / 2. The constraints are defined by the fact that the training data points for each class are on one side of the support vector. Therefore, these constraints are as follows:

W̄ · X̄_i + b ≥ +1   ∀i : y_i = +1   (11.14)
W̄ · X̄_i + b ≤ −1   ∀i : y_i = −1.   (11.15)

This is a constrained convex quadratic optimization problem, which can be solved using Lagrangian methods. In practice, an off-the-shelf optimization solver may be used to achieve the same goal.

In practice, the data may not be linearly separable. In such cases, soft-margin methods may be used. A slack ξ_i ≥ 0 is introduced for training instance, and a training instance is allowed to violate the support vector constraint, for a penalty, which is dependent on the slack. This situation is illustrated in Figure 1.2(b). Therefore, the new set of constraints are now as follows:

W̄ · X̄ + b ≥ +1 − ξ_i   ∀i : y_i = +1   (11.16)
W̄ · X̄ + b ≤ −1 + ξ_i   ∀i : y_i = −1   (11.17)
ξ_i ≥ 0.   (11.18)

Note that additional non-negativity constraints also need to be imposed in the slack variables. The objective function is now ||W̄||² / 2 + C · Σ_{i=1}^n ξ_i. The constant C regulates the importance of the margin and the slack requirements. In other words, small values of C make the approach closer to soft-margin SVM, whereas large values of C make the approach more of the hard-margin SVM. It is also possible to solve this problem using off-the-shelf optimization solvers.

It is also possible to use transformations on the feature variables in order to design non-linear SVM methods. In practice, non-linear SVM methods are learned using kernel methods. The key idea here is that SVM formulations can be solved using only pairwise dot products (similarity values) between objects. In other words, the optimal decision about the class label of a test instance, from the solution to the quadratic optimization problem in this section, can be expressed in terms of the following:
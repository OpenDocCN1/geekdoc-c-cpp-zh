# # Non-Linear Classification

The chapter begins by deriving the Quadratic Discriminant analysis as the boundary between two normally distributed classes. This is then shown to be a line in a higher dimensional space leading to the kernel trick. Heuristic methods such as $k$ nearest neighbours and decision trees are covered. For the latter impurity is defined and examples such as the Gini Diversity Index are given. Neural networks are explored further as a set of many conditions of the form to the left or right of a line determined by the network parameters. The chapter concludes with boosting and cascades as a way to build strong classifiers from weak ones and taking the cost into account.

# ## 5.1 Quadratic Discriminant Analysis

So far we assumed that the data can be separated by a straight line. However, this assumption of linear classification is very restrictive. Before we go into this, however, we need to recall the subtle difference between two key concepts: *probability* and *likelihood*. Probability answers the question: How probable is it that a sample of class $C_i$ has these features? Likelihood, on the other hand, answers the question: How likely is it that a sample with these features belongs to class $C_i$?

Let the features of samples in class $C_i$ be normally distributed with mean $\mu_i$ and variance $\Sigma_i, i = 0, 1$. Let $\mathbf{v}$ be a feature vector. The probability of $\mathbf{v}$ given that it is in class $C_i$ is:

$p(\mathbf{v}|\mathbf{v} \in C_i) = \frac{1}{\sqrt{(2\pi)^M |\Sigma_i|}} \exp \left( -\frac{1}{2} (\mathbf{v} - \mu_i)^T \Sigma_i^{-1} (\mathbf{v} - \mu_i) \right)$.
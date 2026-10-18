we could have millions of training examples and hundreds of thousands of features. For such applications, it is highly desirable to have a classification algorithm that scales well with respect to both n and d.

To this end, SVMPerf was proposed in [20], whose time complexity is O(ns), where s is the average non-zero feature values per training example. Note that such a time-complexity is very attractive for many real applications where the features are sparse (small s) even though its dimensionality d is high.

The key idea of SVMPerf is to re-formulate the original SVM in Equation (10.1) as the following structural SVM:

```
min_{w, ξ ≥ 0} 1/2 w^T w + C ξ
s.t. ∀c ∈ {0,1}^n : 1/n w^T Σ_{i=1}^n (c_i y_i x_i) ≥ 1/n Σ_{i=1}^n c_i - ξ. (10.2)
```

Compared with the original formulation in Equation (10.1), the above formulation has a much simpler objective function, where we only have a single slack variable ξ. On the other hand, there are 2^n constraints in the structural SVM, each of which corresponds to the sum of a subset of the constraints in the original formulation and such a subset is specified by the vector c = (c1, ..., cn) ∈ {0,1}^n. Thus, the reduction in the number of slack variables is achieved at the expense of having many more constraints. So how is this better?

Despite the fact that we have an exponential number of constraints in Equation (10.2), it turns out we can resort to the cutting-plane algorithm to efficiently solve it. The basic idea is as follows. Instead of working on the entire 2^n constraints directly, we keep an active current work set of constrains W. The algorithm starts with an empty set of constraint set W, and then iteratively (1) solves Equation (10.2) by considering the constraints that are only in the current set W; and (2) expands the current working set W of constraints, based on the current classifier, until a pre-defined precision is reached.

The key component in this algorithm is the approach for expanding the current working set W. The work in [20] suggests using the constraint in Equation (10.2) that requires the biggest ξ to make it feasible. To be specific, if w is the currently learnt weighted vector, we define c as ci = 1 if yi(w^T xi) < 1; and ci = 0 otherwise. Then, we will add this constraint c in the current work set W.

Note that the above algorithm is designed for discrete binary classification. The work in [20] further generalizes it to the ordinal regression for the task of ranking (as opposed to binary classification), where yi ∈ {1, ..., R} indicates an ordinal scale. The algorithm for this case has the complexity of O(s n log(n)).

In SVMPerf, there is a parameter ε that controls the accuracy in the iterative process. The overall time complexity is also related to this parameter. To be specific, the number of required iterations in SVMPerf is O(1/ε^2). This yields an overall complexity of O(ns/ε^2).

# 10.2.3 Pegasos

Note that we still have a linear term with respect to the number of training examples O(n) in SVMPerf. For the applications from big data, this term is often on the order of millions or even billions. In order to further speed up the training process, Pegasos was proposed in [25] based on a stochastic sub-gradient descent method.

Unlike SVMPerf and many other methods, which formulate SVM as a constrained optimization problem, Pegasos relies on the the following un-constrained optimization formulation of SVM:

```
min_w λ/2 w^T w + 1/n Σ_{i=1}^n l(w, (x_i, y_i))
where l(w, (x_i, y_i)) = max{0, 1 - y_i w^T x_i}. (10.3)
```
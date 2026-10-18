subspace, and the vector found in the next iteration is the optimal one from a smaller search space. The process of finding linear discriminants is continued until the class separation, as measured by an objective function, reduces below a given threshold for the vector determined in the current iteration. The power of such a dimensionality reduction approach has been illustrated in [23], in which it has been shown that a simple decision tree classifier can perform much more effectively on this transformed data, as compared to more sophisticated classifiers.

Next, we discuss how the Fisher’s discriminant is actually constructed. First, we will set up the objective function J(\overline{\alpha}), which determines the level of separation of the different classes along a given direction (unit-vector) \overline{\alpha}. This sets up the crisp optimization problem of determining the value of \overline{\alpha}, which maximizes J(\overline{\alpha}). For simplicity, let us assume the case of binary classes. Let D1 and D2 be the two sets of documents belonging to the two classes. Then, the projection of a document \overline{X} \in D1 \cup D2 along \overline{\alpha} is given by \overline{X} \cdot \overline{\alpha}. Therefore, the squared class separation S(D1,D2,\overline{\alpha}) along the direction \overline{\alpha} is given by:

```
S(D1,D2,\overline{\alpha}) = \left( \frac{\sum_{\overline{X} \in D1} \overline{\alpha} \cdot \overline{X}}{|D1|} - \frac{\sum_{\overline{X} \in D2} \overline{\alpha} \cdot \overline{X}}{|D2|} \right)^2. (11.7)
```

In addition, we need to normalize this absolute class separation with the use of the underlying class variances. Let Var(D1,\overline{\alpha}) and Var(D2,\overline{\alpha}) be the individual class variances along the direction \alpha. In other words, we have:

```
Var(D1,\overline{\alpha}) = \frac{\sum_{\overline{X} \in D1} (\overline{X} \cdot \overline{\alpha})^2}{|D1|} - \left( \frac{\sum_{\overline{X} \in D1} \overline{X} \cdot \overline{\alpha}}{|D1|} \right)^2. (11.8)
```

The value of Var(D2,\overline{\alpha}) can be defined in a similar way. Then, the normalized class-separation J(\overline{\alpha}) is defined as follows:

```
J(\overline{\alpha}) = \frac{S(D1,D2,\overline{\alpha})}{Var(D1,\overline{\alpha}) + Var(D2,\overline{\alpha})} (11.9)
```

The optimal value of \alpha needs to be determined subject to the constraint that \overline{\alpha} is a unit vector. Let \mu1 and \mu2 be the means of the two data sets D1 and D2, and C1 and C2 be the corresponding covariance matrices. It can be shown that the optimal (unscaled) direction \overline{\alpha} = \overline{\alpha}^* can be expressed in closed form, and is given by the following:

```
\overline{\alpha}^* = \left( \frac{C1 + C2}{2} \right)^{-1} (\mu1 - \mu2). (11.10)
```

The main difficulty in computing the above equation is that this computation requires the inversion of the covariance matrix, which is sparse and computationally difficult in the high-dimensional text domain. Therefore, a gradient descent approach can be used in order to determine the value of \overline{\alpha} in a more computationally effective way. Details of the approach are presented in [23].

Another related method that attempts to determine projection directions that maximize the topical differences between different classes is the Topical Difference Factor Analysis method proposed in [84]. The problem has been shown to be solvable as a generalized eigenvalue problem. The method was used in conjunction with a k-nearest neighbor classifier, and it was shown that the use of this approach significantly improves the accuracy over a classifier that uses the original set of features.

# 11.2.8 Generalized Singular Value Decomposition

While the method discussed above finds one vector \overline{\alpha}_i at a time in order to determine the relevant dimension transformation, it is possible to be much more direct in finding the optimal subspaces simultaneously by using a generalized version of dimensionality reduction [68,69]. It is important to
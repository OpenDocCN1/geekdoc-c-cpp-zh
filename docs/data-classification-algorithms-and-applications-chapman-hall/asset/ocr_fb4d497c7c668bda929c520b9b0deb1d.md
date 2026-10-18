![](bbox=[0.25, 0.07, 0.65, 0.26])

# (a) Univariate Splits

![](bbox=[0.3, 0.29, 0.65, 0.38])

# (b) Multivariate Splits

# FIGURE 1.1: Illustration of univariate and multivariate splits for decision tree construction.

higher CRP and Cholesterol levels correspond to greater risk, though it is possible to reach more definitive conclusions by combining the two.

An example of a decision tree that constructs the classification model on the basis of the two features is illustrated in Figure 1.1(a). This decision tree uses univariate splits, by first partitioning on the CRP level, and then using a split criterion on the Cholesterol level. Note that the Cholesterol split criteria in the two CRP branches of the tree are different. In principle, different features can be used to split different nodes at the same level of the tree. It is also sometimes possible to use conditions on multiple attributes in order to create more powerful splits at a particular level of the tree. An example is illustrated in Figure 1.1(b), where a linear combination of the two attributes provides a much more powerful split than a single attribute. The split condition is as follows:

```
CRP + Cholestrol/100 ≤ 4
```

Note that a single condition such as this is able to partition the training data very well into the two classes (with a few exceptions). Therefore, the split is more powerful in discriminating between the two classes in a smaller number of levels of the decision tree. Where possible, it is desirable to construct more compact decision trees in order to obtain the most accurate results. Such splits are referred to as multivariate splits. Some of the earliest methods for decision tree construction include C4.5 [72], ID3 [73], and CART [22]. A detailed discussion of decision trees may be found in [22,65,72,73]. Decision trees are discussed in Chapter 4.

# 1.2.4 Rule-Based Methods

Rule-based methods are closely related to decision trees, except that they do not create a strict hierarchical partitioning of the training data. Rather, overlaps are allowed in order to create greater robustness for the training model. Any path in a decision tree may be interpreted as a rule, which
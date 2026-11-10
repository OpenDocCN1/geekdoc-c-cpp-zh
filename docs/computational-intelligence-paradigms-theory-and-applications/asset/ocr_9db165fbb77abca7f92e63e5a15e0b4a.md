![](bbox=[0.15, 0.07, 0.85, 0.38])

FIGURE 9.13: Flowchart of Resubstitution Estimate

tree be allowed to be grown to its maximal size first, and then gradually shrunk by pruning away branches that lead to the smallest decrease in accuracy compared to pruning other branches. The search for the "right-sized" tree starts by pruning or collapsing some of the branches of the largest tree from the bottom up, using the cost complexity parameter and cross validation or an independent test sample to measure the predictive accuracy of the pruned tree.

# 9.5.7 Accuracy Estimation in CART

Almost all classification procedures produce errors, but accuracy is the most important attribute in CART. Breiman proposed three procedures for estimating the accuracy of tree-structured classifiers.

Resubstitution Estimate: The accuracy of the true misclassification rate is estimated as shown in Figure 9.13. The disadvantage of this misclassification estimate is that it is derived from the same data set from which the tree is built; hence, it underestimates the true misclassification rate. The error rate is always low in such cases.
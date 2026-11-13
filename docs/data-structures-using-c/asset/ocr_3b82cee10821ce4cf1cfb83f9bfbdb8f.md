![](bbox=[0.2, 0.1, 0.88, 0.38])

Fig. 10.2 Sample BSTs for keys (25, 10, 35, 27, 35, 22, 20) (a) Sample 1 (b) Sample 2

Note that the left BST in Fig. 10.2(a) requires utmost four comparisons to search the target in the tree, whereas for searching the target in the right tree (Fig. 10.2b), the maximum comparisons needed are five. We can say that the first BST has a better average behaviour than the second.

When the target is at the root (level 0), we need just one comparison; if the target is at level 1, we need two comparisons, and so on. Since the number of comparisons, or in other words iterations, through the search loop determines the cost of search, the cost should be minimum, that is, optimal. Hence, the optimality criteria for a static BST can be stated as minimizing the cost of the BST under a given access sequence. Such a cost can be defined as follows:

```
Cost(T) = \sum_{i=1}^{n} l(a_i) \qquad (10.1)
```

Here, the total number of nodes are n, and l(a) is the length of the i-th key, a.

Here, we assume that all the keys are searched with equal probabilities. However, in reality, the keys are searched with different probabilities, and it should be taken care of while constructing the tree so that the keys searched more often should require less time as compared to those searched rarely. This can be achieved by placing the more frequently searched key nodes closer to the root as compared to those that are searched rarely, to reduce the total number of average searches. A node is said to be closer to the root when its path length is lesser than that of the other nodes.
# 4.3.3 Pruning Strategy

CART uses cost complexity pruning. This is one of the most theoretically sound pruning methods. To remove data and algorithmic bias from the tree growth phase, it uses a different goodness criterion and a different dataset for pruning. Acknowledging that there is still statistical uncertainty about the computations, a standard error statistic is computed, and the smallest tree that is with the error range is chosen.

C4.5 uses pessimistic error pruning with the binomial confidence interval. Quinlan himself acknowledges that C4.5 may be applying statistical concepts loosely [66]. As a heuristic method, however, it works about as well as any other method. Its major advantage is that it does not require a separate dataset for pruning. Moreover, it allows a subtree to be replaced not only by a single node but also by the most commonly selected child.

# 4.3.4 Handling Unknown Values: Induction and Prediction

One real-world complication is that some data items have missing attribute values. Using the notation x = {x1,x2,...,xd}, some of the xi values may be missing (null). Missing values generate three concerns:

+   1. Choosing the Best Split: If a candidate splitting criterion uses attribute Ai but some items have no values for Ai, how should we account for this? How do we select the best criteria, when they have different proportions of missing values?
+   2. Partitioning the Training Set: Once a splitting criteria is selected, to which child node will the incomplete data items be assigned?
+   3. Making Predictions: If making class predictions for items with missing attribute values, how will they proceed down the tree?

Recent studies have compared different techniques for handling missing values in decision trees [18, 67]. CART and C4.5 take very different approaches for addressing these concerns.

CART: CART assumes that missing values are sparse. It calculates and compares splitting criteria using only data that contain values for the relevant attributes. However, if the top scoring splitting criteria is on an attribute with some missing values, then CART selects the best surrogate split that has no missing attribute values. For any splitting rule S, a surrogate rule generates similar partitioning results, and the surrogate S' is the one that is most strongly correlated. For each actual rule selected, CART computes and saves a small ordered list of top surrogate rules. Recall that CART performs binary splits. For dataset Xi, p11 is the fraction of items that is classified by both S and S' as state 1; p00 is the fraction that is classified by both as state 0. The probability that a random item is classified the same by both S and S' is p(S,S') = p11(S,S') + p00(S,S'). This measure is further refined in light of the discriminating power of S. The final predictive measure of association between S and S' is

```
λ(S'|S) = [min(p0(S),p1(S)) - (1 - p(S,S'))] / min(p0(S),p1(S)) . (4.18)
```

The scaling factor min(p0(S),p1(S)) estimates the probability that S correctly classifies an item. Due to the use of surrogates, we need not worry about how to partition items with missing attribute values.

When trying to predict the class of a new item, if a missing attribute is encountered, CART looks for the best surrogate rule for which the data item does have an attribute value. This rule is
rooted at v, and L(v) be the leaf nodes under v. Then,

not pruned: ℰ_pess(T(v)) = Σ_{l∈L(v)} ℰ(l) + |L(v)|/2  (4.16)
if pruned: ℰ_pess(v) = ℰ(v) + 1/2.  (4.17)

Because this adjustment alone might still be too optimistic, the actual rule is that a subtree will be pruned if the decrease in error is larger than the Standard Error.

In C4.5, Quinlan modified pessimistic error pruning to be more pessimistic. The new estimated error is the upper bound of the binomial distribution confidence interval, U_CF(ℰ, |X_i|). C4.5 uses 25% confidence by default. Note that the binomial distribution should not be approximated by the normal distribution, because the approximation is not good for small error rates.

For our [age > 55?] example in Figure 4.2(a), C4.5 would assign the subtree an error score of (5/6)U_CF(0,5) + (1/6)U_CF(0,1) = (0.833)0.242 + (0.166).750 = 0.327. If we prune, then the new root has a score of U_CF(1,6) = 0.390. The original split has a better error score, so we retain the split.

# 6. Additional Pruning Methods

Mansour [52] has computed a different upper bound for pessimistic error pruning, based on the Chernoff bound. The formula is simpler than Quinlan’s but requires setting two parameters. Kearns and Mansour [44] describe an algorithm with good theoretical guarantees for near-optimal tree size. Mehta et al. present an MDL-based method that offers a better combination of tree size and speed than C4.5 or CART on their test data.

Esposito et al. [20] have compared the five earlier pruning techniques. They find that cost-complexity pruning and reduced error pruning tend to overprune, i.e., create smaller but less accurate decision trees. Other methods (error-based pruning, pessimistic error pruning, and minimum error pruning) tend to underprune. However, no method clearly outperforms others on all measures. The wisest strategy for the user seems to be to try several methods, in order to have a choice.

# 4.3 Case Studies with C4.5 and CART

To illustrate how a complete decision tree classifier works, we look at the two most prominent algorithms: CART and C4.5. Interestingly, both are listed among the top 10 algorithms in all of data mining, as chosen at the 2006 International Conference on Data Mining [85].

CART was developed by Breiman, Friedman, Olshen, and Stone, as a research work. The decision tree induction problem and their solution is described in detail in their 1984 book, Classification and Regression Trees [8]. C4.5 gradually evolved out of ID3 during the late 1980s and early 1990s. Both were developed by J. Ross Quinlan. Early on C4.5 was put to industrial use, so there has been a steady stream of enhancements and added features. We focus on the version described in Quinlan’s 1993 book, C4.5: Programs for Machine Learning [66].
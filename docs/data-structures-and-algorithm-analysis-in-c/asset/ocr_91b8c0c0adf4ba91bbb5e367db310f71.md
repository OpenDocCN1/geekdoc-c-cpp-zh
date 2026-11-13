Of course, the implication of this model is that there is only a \(\frac{2}{3}\) chance that the next union will involve the large tree. Another model might say that all unions between any two elements in different trees are equally likely, so a larger tree is more likely to be involved in the next union than a smaller tree. In the example above, there is an \(\frac{1}{11}\) chance that the large tree is involved in the next union, since (ignoring symmetries) there are 6 ways in which to merge two elements in {0, 1, 2, 3}, and 16 ways to merge an element in {4, 5, 6, 7} with an element in {0, 1, 2, 3}. There are still more models and no general agreement on which is the best. The average running time depends on the model: \(\Theta(M)\), \(\Theta(M \log N)\), and \(\Theta(MN)\) bounds have actually been shown for three different models, although the latter bound is thought to be more realistic.

Quadratic running time for a sequence of operations is generally unacceptable. Fortunately, there are several ways of easily ensuring that this running time does not occur.

# 8.4 Smart Union Algorithms

The unions above were performed rather arbitrarily, by making the second tree a subtree of the first. A simple improvement is always to make the smaller tree a subtree of the larger, breaking ties by any method; we call this approach union-by-size. The three unions in the preceding example were all ties, and so we can consider that they were performed by size. If the next operation were union(3, 4), then the forest in Figure 8.10 would form. Had the size heuristic not been used, a deeper tree would have been formed (Fig. 8.11).

We can prove that if unions are done by size, the depth of any node is never more than \(\log N\). To see this, note that a node is initially at depth 0. When its depth increases as a result of a union, it is placed in a tree that is at least twice as large as before. Thus, its depth can be increased at most \(\log N\) times. (We used this argument in the quick-find algorithm at the end of Section 8.2.) This implies that the running time for a find operation is \(O(\log N)\), and a sequence of \(M\) operations takes \(O(M \log N)\). The tree in Figure 8.12 shows the worst case possible after 16 unions and is obtained if all unions are between equal-sized trees (the worst-case trees are binomial trees, discussed in Chapter 6).

To implement this strategy, we need to keep track of the size of each tree. Since we are really just using an array, we can have the array entry of each root contain the negative of

![](bbox=[0.05, 0.7, 0.8, 0.88])

Figure 8.10 Result of union-by-size
The program then updates its knowledge tree to hold the new question and animal. The new tree is shown in Figure 10-16.

![](bbox=[0.143, 0.149, 0.58, 0.403])

**Figure 10-16:** This knowledge tree can now differentiate between cat and giraffe.

# # Expression Evaluation

You can model many situations with trees. You can model mathematical expressions by creating an internal node for each operator and a leaf node for each numeric value.

Mathematical expressions naturally break into subexpressions that you must evaluate before you can evaluate the expression as a whole. For example, consider the expression (6 × 14) + (9 + 12). To evaluate this expression, you must first evaluate 6 × 14 and 9 + 12. You can then divide the results of those calculations to get the final result.

To model this expression as a tree, you build subtrees to represent the subexpressions. You join the subexpressions with a root node that represents the operation that combines the subexpressions—in this case, division.

**Figure 10-17:** The tree representing the expression (6 × 14) + (9 + 12).

![](bbox=[0.143, 0.75, 0.443, 0.883])

**Figure 10-17:** You can use trees to evaluate mathematical expressions.
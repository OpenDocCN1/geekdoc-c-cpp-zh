In the expression tree as in Fig. 7.74, an infix expression is represented by representing the node as an operator, and the left and right subtrees are the left and right operands of that operator.

If we traverse this tree in preorder, we visit the nodes in the order of: / + × AB – CD – CE, and this is a prefix form of the infix expression. On the other hand, if we traverse the tree in postorder, the nodes are visited in the following order: AB × CD – E – I, which is a postfix equivalent of the infix notation.

Example 7.7 represents the postfix equivalent of a given infix notation.

# EXAMPLE 7.7 Represent AB + D × EFAD × / + C + as an expression tree.

Solution Figure 7.75 represents the given expression in the form of a tree.

![](bbox=[0.25, 0.35, 0.8, 0.58])

Fig. 7.75 Expression tree for E = AB + D × EFAD × / + C +

# Construction of Expression Tree

We have studied the binary tree representation of an expression. Let us study how to construct a tree when the infix expression is given. First, the infix expression is converted to a postfix expression. Use Algorithm 7.3 to construct an expression tree.

# ALGORITHM 7.3
(Scan the postfix expression from left to right.)

+   1. Get one token from expression E.

+   2. Create a node say curr for it.
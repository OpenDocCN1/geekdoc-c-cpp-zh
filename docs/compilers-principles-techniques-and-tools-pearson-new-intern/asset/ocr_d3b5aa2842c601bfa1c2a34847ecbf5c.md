Any SDT can be implemented as follows:

+   1. Ignoring the actions, parse the input and produce a parse tree as a result.
+   2. Then, examine each interior node \(N\), say one for production \(A \to \alpha\). Add additional children to \(N\) for the actions in \(\alpha\), so the children of \(N\) from left to right have exactly the symbols and actions of \(\alpha\).
+   3. Perform a preorder traversal (see Section 2.3.4) of the tree, and as soon as a node labeled by an action is visited, perform that action.

For instance, Fig. 5.22 shows the parse tree for expression 3 * 5 + 4 with actions inserted. If we visit the nodes in preorder, we get the prefix form of the expression: + * 3 5 4.

![](bbox=[0.289, 0.389, 0.683, 0.624])

Figure 5.22: Parse tree with actions embedded

# 5.4.4 Eliminating Left Recursion From SDT’s

Since no grammar with left recursion can be parsed deterministically top-down, we examined left-recursion elimination in Section 4.3.3. When the grammar is part of an SDT, we also need to worry about how the actions are handled.

First, consider the simple case, in which the only thing we care about is the order in which the actions in an SDT are performed. For example, if each action simply prints a string, we care only about the order in which the strings are printed. In this case, the following principle can guide us:

+   - When transforming the grammar, treat the actions as if they were terminal symbols.
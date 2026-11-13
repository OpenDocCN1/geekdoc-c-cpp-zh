+   3. If (symbol is operand) then
+   (a) push a node curr onto a stack.

+   4. else if (symbol is operator) then

+   (a) T2 = pop()
+   T1 = pop()
+   Here T1 and T2 are pointers to left trees and right subtrees of the operator,
+   respectively.

+   (b) Attach T1 to left and T2 to the right of curr.

+   (c) Form a tree whose root is the operator and T1 and T2 are left and right children,
+   respectively.

+   (d) Push the node curr having attached left and right subtrees onto a stack.

+   5. Repeat steps 1–4 till the end of expression.

+   6. Pop the node curr from the stack, which is a pointer to the root of expression tree.

Example 7.8 shows the steps to construct an expression tree for a given expression, E.

# EXAMPLE 7.8 Represent E = (a + b x c)/d as an expression tree.

Solution Let us consider the expression E = (a + b x c)/d

Postfix expression = abc x+ dl/

The following steps of operations are performed:

+   1. The operands a, b, c will be pushed onto the stack by forming a one-node tree of each
+   and pushing a pointer to each onto a stack (Fig. 7.76).

![](bbox=[0.3, 0.615, 0.77, 0.745])

Fig. 7.76 Step 1

+   2. When the operator x has been encountered, the top two pointers are popped. A tree is
+   formed with x as a root and the two popped pointers as children. The pointer to the root
+   is pushed onto a stack (Fig. 7.77).
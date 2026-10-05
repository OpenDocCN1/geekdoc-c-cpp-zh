
12. Variable via_branch is True, so follow the left branch to 7 and process node 7.
13. Follow the right thread to 9, and set via_branch to False.
14. Variable via_branch is False, process node 9.
15. Follow the right thread to null, and set via_branch to False.
16. Variable node is not null, and the While loop ends.

This algorithm fills all the nodes, and it visits every node, so its run time O(N). However, it doesn't need to let recursive calls unwind up the child branches, but it saves a bit of time over a normal traversal. It doesn't use recursion, so it doesn't have problems with deep levels of recursion. It doesn't need any extra storage space, unlike a depth-first traversal.

## Specialized Tree Algorithms

Over the years programmers have developed many specialized algorithms to solve specific problems. This chapter cannot possibly describe every algorithm, but the following sections describe four algorithms that are particularly interesting. They demonstrate the useful techniques of updating a tree to include new data, evaluating recursive expressions, and subdividing geometric areas. The final section explains trees, which are well-known in algorithmic studies.

## The Animal Game

In the animal game, the user thinks of an animal, and the program's simple artificial intelligence tries to guess what it is. The program is a learning system, so over time it gets better at guessing the user's animal.

The program stores information about animals in a binary tree. Each internal node holds a yes-or-no question that guides the program down the left or right branch. Leaf nodes represent animals.

The program asks the questions at each node and follows the appropriate branch until it reaches a leaf node where it guesses that node's animal.
If the program is wrong, it asks the user to type a question it can ask to differentiate from the animal it guessed and the correct answer. It adds a new internal node containing the question and gives that leaves holding the correct and incorrect animals.

Figure 10-15 shows a small knowledge tree for the game.
For example, suppose the user is thinking about a snake. Table 10-2 shows the questions the program asks and the answers the user gives.

For another example, suppose the user is thinking about a giraffe. Table 10-3 shows the questions the program asks and the answers the user gives in this example.

![](img/fefa42765c0b410af6705110aea7c0cb_280_0.png)

**Figure 10-15:** This knowledge tree can differentiate among dog, cat, fish, snake, and bird.

**Table 10-2:** The Animal Game Trying to Guess Snake

| THE PROGRAM ASKS: | THE USER ANSWERS: |
|---|---|
| Is it a mammal? | No |
| Does it have scales? | Yes |
| Does it breathe water? | No |
| Is it a snake? | Yes |

**Table 10-3:** The Animal Game Trying to Guess Giraffe

| THE PROGRAM ASKS: | THE USER ANSWERS: |
|---|---|
| Is it a mammal? | Yes |
| Does it a bark? | No |
| Is it a cat? | No |
| What is your animal? | Giraffe |
| What question could I ask to differentiate between a cat and a giraffe? | Does it have a long neck? |
| Is the answer to this question true for a giraffe? | Yes |

The program then updates its knowledge tree to hold the new question and animal. The new tree is shown in Figure 10-16.

![](img/fefa42765c0b410af6705110aea7c0cb_281_0.png)

**Figure 10-16:** This knowledge tree can now differentiate between cat and giraffe.

## Expression Evaluation

You can model many situations with trees. You can model mathematical expressions by creating an internal node for each operator and a leaf node for each numeric value.

Mathematical expressions naturally break into subexpressions that you must evaluate before you can evaluate the expression as a whole. For example, consider the expression (6 × 14) + (9 + 12). To evaluate this expression, you must first evaluate 6 × 14 and 9 + 12. You can then divide the results of those calculations to get the final result.

To model this expression as a tree, you build subtrees to represent the subexpressions. You join the subexpressions with a root node that represents the operation that combines the subexpressions—in this case, division.

**Figure 10-17:** The tree representing the expression (6 × 14) + (9 + 12).

![](img/fefa42765c0b410af6705110aea7c0cb_281_1.png)

**Figure 10-17:** You can use trees to evaluate mathematical expressions.

Each internal node has children representing its operands. For example, binary operators use as + and / have left and right children that the operator must combine.

You can think of the leaf nodes as special operators that convert a text value into a numeric one. In that case the leaf nodes must hold their text.

The only thing missing from the arithmetic class is a method to evaluate the node. That method should examine the type of node and return an appropriate result. For example, if the operator is +, the method should recursively evaluate its operands subexpressions, and then it can add the results.

The following pseudocode creates an enumeration that defines values indicate a node's type:

```
Enumeration Operators
Literal
Plus
Minus
Times
Divide
Negate
End Enumeration
```

This enumeration defines operator types for literal values such as 8, addition, subtraction, multiplication, division and negation as in -5). You can add other operators such as square root, exponentiation, sine, cosine, and others.

The following pseudocode shows an ExpressionNode class that represents a node in a mathematical expression tree:

```
Class ExpressionNode
Operators: Operator
ExpressionNode: LeftOperand, RightOperand
String: LiteralText

// Evaluate the expression.
Float: Evaluate()
Case Operator
Literal:
  Return Float.Parse(LiteralText)
Plus:
  Return LeftOperand.Evaluate() + RightOperand.Evaluate()
Minus:
  Return LeftOperand.Evaluate() - RightOperand.Evaluate()
Times:
  Return LeftOperand.Evaluate() * RightOperand.Evaluate()
Divide:
  Return LeftOperand.Evaluate() / RightOperand.Evaluate()
Negate:
  Return -LeftOperand.Evaluate()
```

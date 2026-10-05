# Chapter 10 | Trees 259

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
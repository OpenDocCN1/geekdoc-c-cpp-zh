# Output 12.3:

```
------------------ (x, y) => x > y ------------------
>   x (Parameter)
>   y (Parameter)
------------------ (x, y) => (x * y) > (x + y) ------------------
>   * (Parameter)
>       y (Parameter)
>   + (Parameter)
>       x (Parameter)
>       y (Parameter)
```

The output of the expression as text is due to conversion from the underlying data of an expression tree—conversion similar to the PrintNode() and NodeTypeToString() functions, only more comprehensive. The important point to note is that an expression tree is a collection of data, and by iterating over the data, it is possible to convert the data to another format. In the PrintNode() method, Listing 12.24 converts the data to a horizontal text interpretation of the data. However, the interpretation could be virtually anything.

Using recursion, the PrintNode() function demonstrates that an expression tree is a tree of zero or more expression trees. The contained expression trees are stored in an Expression’s Body property. In addition, the expression tree includes an ExpressionType property called NodeType where ExpressionType is an enum for each different type of expression. There are numerous types of expressions: BinaryExpression, ConditionaLExpression, LambdaExpression (the root of an expression tree), MethodCallExpression, ParameterExpression, and ConstantExpression are examples. Each type derives from System.Linq.Expressions.Expression. Generally, you can use statement lambdas interchangeably with expression lambdas. However, you cannot convert statement lambdas into expression trees. You can express expression trees only by using expression lambda syntax.
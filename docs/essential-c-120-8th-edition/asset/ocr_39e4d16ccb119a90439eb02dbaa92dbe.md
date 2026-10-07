# Expression Trees 723

```
PrintNode(expression.Left, indent + 1);
PrintSingle(expression, indent);
PrintNode(expression.Right, indent + 1);
}
```

```
private static void PrintSingle(
    Expression expression, int indent) =>
    Console.WriteLine("{0}" + indent * 5 + ""{1}",
    "" + NodeToString(expression));
```

```
private static string NodeToString(Expression expression) =>
{
    // using static ExpressionType
    Multiply => "+",
    Add => "+",
    Divide => "/",
    Subtract => "-",
    GreaterThan => ">",
    LessThan => "<",
    => expression.ToString() +
    "" + (" + expression.NodeType.ToString() + ")";
}
```

Note passing an instance of the expression tree to Console.WriteLine() automatically converts the expression tree to a descriptive string form; the objects generated for expression trees all override ToString() so that you can see the contents of expression tree at a glance when debugging.

In Output 13.5, we see that the Console.WriteLine() statements in Main() print out the body of the expression trees as text.

# Output 13.5

![](bbox=[0.156, 0.677, 0.904, 0.873])
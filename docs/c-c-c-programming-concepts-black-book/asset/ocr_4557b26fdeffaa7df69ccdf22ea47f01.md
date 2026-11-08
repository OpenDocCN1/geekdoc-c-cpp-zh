Listing 19.21 uses the lambda expression, `i => i % 2 != 0`, to build an expression tree:

# Listing 19.21: Building an Expression Tree from a Lambda Expression

```
```csharp
using System;
using System.Linq;
using System.Linq.Expressions;

class Program
{
    public static void Main()
    {
        //Building expression tree from the lambda expression i => i % 2 != 0
        Expression<Func<int, bool>> lambdaExpr = i => i % 2 != 0;

        BinaryExpression binaryExpr
          = (BinaryExpression)lambdaExpr.Body;//holding the expression i%2 != 0
        BinaryExpression parentLeft
          = (BinaryExpression)binaryExpr.Left;//holding the expression i % 2
        ParameterExpression left
          = (ParameterExpression)parentLeft.Left;//holding the parameter i
                                                    //of i%2
        ConstantExpression right
          = (ConstantExpression)parentLeft.Right;//holding the constant of i%2
        ConstantExpression parentRight
          = (ConstantExpression)binaryExpr.Right;//holding 0
        ParameterExpression param
          =(ParameterExpression)lambdaExpr.Parameters[0];//holding
                                                    //the parameter i

        Console.WriteLine("The expression is...");
        //Displaying the lambda expression
        Console.WriteLine("{0} => {1} {2} {3} {4} {5}",
          param.Name,left.Name,parentLeft.NodeType,
          right.Value, binaryExpr.NodeType, parentRight.Value);
    }
}
```
```

In the preceding program, we first got the entire body of the binary expression and then separated its tree elements accordingly. The output of the program is given as follows:

```
```text
The expression is...
i => i Modulo 2 NotEqual 0
```
```

Let’s now learn about the standard LINQ operators.

# Standard LINQ Operators

LINQ provides a collection of the operators that can be used to create an expression similar to a SQL query. These operators are called standard LINQ operators. There are approximately 50 operators that are used to perform query operations over a collection or an array of objects. The `System.Query.Sequence` class, which comes under the `System.Query` namespace, has methods called standard query operators that are used in LINQ queries. Standard query operators are categorized into two groups:

+   - A set of standard query operators that comes under the `IEnumerable<T>` interface
+   - A set of standard query operators that comes under the `IQueryable<T>` interface
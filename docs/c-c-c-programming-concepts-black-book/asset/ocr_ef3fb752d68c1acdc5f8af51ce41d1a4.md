# **Listing 19.20:** Building an Expression Tree for a Lambda Expression

```
```csharp
using System;
using System.Linq;
using System.Linq.Expressions;

class Program
{
    public static void Main()
    {
        //Building expression tree for the lambda expression i => i % 2 != 0
        //Defining the parameter i
        ParameterExpression p = Expression.Parameter(typeof(int), "i");
        //Defining the constant 2
        ConstantExpression c = Expression.Constant(2, typeof(int));
        //Defining the constant 0
        ConstantExpression c1 = Expression.Constant(0, typeof(int));
        //Building the expression i%2
        BinaryExpression modulo = Expression.Modulo(p, c);
        //Building the expression i%2 != 0
        BinaryExpression isEqual = Expression.NotEqual(modulo, c1);

        //Compiler builds the lambda expression i => i % 2 != 0 at this step
        Expression<Func<int, bool>> l1 = Expression.Lambda<Func<int, bool>>(isEqual,
            new ParameterExpression[] { p });

        //Compile the lambda expression
        Func<int, bool> lambda = l1.Compile();

        //Displaying the result of the lambda expression
        Console.WriteLine(lambda(5));
    }
}
```
```

Listing 19.20 is self-explanatory, as it shows the stepwise execution of building an expression tree. Therefore, when run this program, the output will be True.

In an expression tree, the root node is always of type `Expression<DelegateT>`, that is, the root node holds the entire lambda expression. C# also allows us to create an expression tree from an available lambda expression.

Figure 19.21 shows the expression tree for the expression i => i % 2 != 0:

![](bbox=[0.301, 0.626, 0.724, 0.794])

**Figure 19.21:** Showing an Expression Tree
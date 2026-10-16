
```csharp
WriteLine("query started");
Write("cancel?");
string input = ReadLine();
if (input.ToLower().Equals("y"))
{
    // cancel!
    cts.Cancel();
}
```

> NOTE You can read more about cancellation and the CancellationToken in Chapter 21.

## Expression Trees

With LINQ to Objects, the extension methods require a delegate type as parameter; this way, a lambda expression can be assigned to the parameter. Lambda expressions can also be assigned to parameters of type `Expression<T>`. The C# compiler defines different behavior for lambda expressions depending on the type. If the type is `Expression<T>`, the compiler creates an expression tree from the lambda expression and stores it in the assembly. The expression tree can be analyzed during runtime and optimized for querying against the data source.

Let’s turn to a query expression that was used previously (code file `ExpressionTreeSample/Program.cs`):

```csharp
var brazilRacers = from r in racers
    where r.Country == "Brazil"
    orderby r.Wins
    select r;
```

The preceding query expression uses the extension methods `Where`, `OrderBy`, and `Select`. The `Enumerable` class defines the `Where` extension method with the delegate type `Func<T, bool>` as parameter predicate:

```csharp
public static IEnumerable<TSource> Where<TSource>(
    this IEnumerable<TSource> source, Func<TSource, bool> predicate);
```

This way, the lambda expression is assigned to the predicate. Here, the lambda expression is similar to an anonymous method, as explained earlier:

```csharp
Func<Racer, bool> predicate = r => r.Country == "Brazil";
```

The `Enumerable` class is not the only class for defining the `Where` extension method. The `Where` extension method is also defined by the class `Queryable`. This class has a different definition of the `Where` extension method:

```csharp
public static IQueryable<TSource> Where<TSource>(
    this IQueryable<TSource> source,
    Expression<Func<TSource, bool>> predicate);
```

Here, the lambda expression is assigned to the type `Expression<T>`, which behaves differently:

```csharp
Expression<Func<Racer, bool>> predicate = r => r.Country == "Brazil";
```

Instead of using delegates, the compiler emits an expression tree to the assembly. The expression tree can be read during runtime. Expression trees are built from classes derived from the abstract base class `Expression`. The `Expression` class is not the same as `Expression<T>`. Some of the expression classes that inherit from `Expression` include `BinaryExpression`, `ConstantExpression`, `InvocationExpression`, `LambdaExpression`, `NewExpression`, `NewArrayExpression`, `TernaryExpression`, `UnaryExpression`, and more. The compiler creates an expression tree resulting from the lambda expression.

For example, the lambda expression `r.Country == "Brazil"` makes use of `ParameterExpression`, `MemberExpression`, `ConstantExpression`, and `MethodCallExpression` to create a tree and store the tree in the assembly. This tree is then used during runtime to create an optimized query to the underlying data source.

The method `DisplayTree` is implemented to display an expression tree graphically on the console. In the following example, an `Expression` object can be passed, and depending on the expression type some information about the expression is written to the console. Depending on the type of the expression, `DisplayTree` is called recursively:

> NOTE This method does not deal with all expression types, only the types that are used with the following example expression.

```csharp
private static void DisplayTree(int indent, string message, Expression expression)
{
    string output = $"{string.Empty.PadLeft(indent, '>')}{message}" +
        $"! NodeType: {expression.NodeType}; Expr: {expression}";

    indent++;
    switch (expression.NodeType)
    {
        case ExpressionType.Lambda:
            Console.WriteLine(output);
            LambdaExpression lambdaExpr = (LambdaExpression)expression;
            foreach (var parameter in lambdaExpr.Parameters)
            {
                DisplayTree(indent, "Parameter", parameter);
            }
            DisplayTree(indent, "Body", lambdaExpr.Body);
            break;
        case ExpressionType.Constant:
            ConstantExpression constExpr = (ConstantExpression)expression;
            WriteLine($"{output} Const Value: {constExpr.Value}");
            break;
        case ExpressionType.Parameter:
            ParameterExpression paramExpr = (ParameterExpression)expression;
            WriteLine($" {output} Param Type: {paramExpr.Type.Name} ");
            break;
        case ExpressionType.Equal:
        case ExpressionType.AndAlso:
        case ExpressionType.GreaterThan:
            BinaryExpression binExpr = (BinaryExpression)expression;
            if (binExpr.Method != null)
            {
                WriteLine($" {output} Method: {binExpr.Method.Name} ");
            }
            else
            {
                WriteLine(output);
            }
            DisplayTree(indent, "Left", binExpr.Left);
            DisplayTree(indent, "Right", binExpr.Right);
            break;
        case ExpressionType.MemberAccess:
            MemberExpression memberExpr = (MemberExpression)expression;
            WriteLine($" {output} Member Name: {memberExpr.Member.Name}, " +
                $"Type: {memberExpr.Type.Name}");
            DisplayTree(indent, "Member Expr", memberExpr.Expression);
            break;
        default:
            WriteLine();
            WriteLine($" {expression.NodeType} {expression.Type.Name} ");
            break;
    }
}
```

The expression that is used for showing the tree is already well known. It’s a lambda expression with a `Racer` parameter, and the body of the expression takes racers from Brazil only if they have won more than six races:

```csharp
Expression<Func<Racer, bool>> expression =
    r => r.Country == "Brazil" && r.Wins > 6;

DisplayTree(0, "Lambda", expression);
```

Looking at the tree result, you can see from the output that the lambda expression consists of a Parameter and an AndAlso node type. The AndAlso node type has an Equal node type to the left and a GreaterThan node type to the right. The Equal node type to the left of the AndAlso node type has a MemberAccess node type to the left and a Constant node type to the right, and so on:

```text
Lambda! NodeType: Lambda; Expr: r => ((r.Country == "Brazil") AndAlso (r.Wins > 6))
> Parameter! NodeType: Parameter; Expr: r Param Type: Racer
> Body! NodeType: AndAlso; Expr: ((r.Country == "Brazil") AndAlso (r.Wins > 6))
>> Left! NodeType: Equal; Expr: (r.Country == "Brazil") Method: op_Equality
>>> Left! NodeType: MemberAccess; Expr: r.Country Member Name: Country, Type: String
>>>> Member Expr! NodeType: Parameter; Expr: r Param Type: Racer
>>> Right! NodeType: Constant; Expr: "Brazil" Const Value: Brazil
>> Right! NodeType: GreaterThan; Expr: (r.Wins > 6)
>>> Left! NodeType: MemberAccess; Expr: r.Wins Member Name: Wins, Type: Int32
>>>> Member Expr! NodeType: Parameter; Expr: r Param Type: Racer
>>> Right! NodeType: Constant; Expr: 6 Const Value: 6
```

Examples where the `Expression<T>` type is used are with the ADO.NET Entity Framework and the client provider for WCF Data Services. These technologies define methods with `Expression<T>` parameters. This way the LINQ provider accessing the database can create a runtime–optimized query by reading the expressions to get the data from the database.

## LINQ Providers

.NET includes several LINQ providers. A LINQ provider implements the standard query operators for a specific data source. LINQ providers might implement more extension methods than are defined by LINQ, but the standard operators must at least be implemented. LINQ to XML implements additional methods that are particularly useful with XML, such as the methods `Elements`, `Descendants`, and `Ancestors` defined by the class `Extensions` in the `System.Xml.Linq` namespace.

Implementation of the LINQ provider is selected based on the namespace and the type of the first parameter. The namespace of the class that implements the extension methods must be opened; otherwise, the extension class is not in scope. The parameter of the `Where` method defined by LINQ to Objects and the `Where` method defined by LINQ to Entities is different.

The `Where` method of LINQ to Objects is defined with the `Enumerable` class:

```csharp
public static IEnumerable<TSource> Where<TSource>(
    this IEnumerable<TSource> source, Func<TSource, bool> predicate);
```

Inside the `System.Linq` namespace is another class that implements the operator `Where`. This implementation is used by LINQ to Entities. You can find the implementation in the class `Queryable`:

```csharp
public static IQueryable<TSource> Where<TSource>(
    this IQueryable<TSource> source,
    Expression<Func<TSource, bool>> predicate);
```

Both of these classes are implemented in the `System.Core` assembly in the `System.Linq` namespace. How does the compiler select what method to use, and what’s the magic with the `Expression` type? The lambda expression is the same regardless of whether it is passed with a `Func<TSource, bool>` parameter or an `Expression<Func<TSource, bool>>` parameter—only the compiler behaves differently. The selection is done based on the source parameter. The method that

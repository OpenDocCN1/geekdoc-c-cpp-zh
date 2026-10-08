Return (op1 + op2) / op2
End Function

End Module

Lambda expressions provide more concise syntax and type inference so that the operation delegate
can be described in a more straightforward way:

```
Sub Main()
Dim op1 As Double = 12.3
Dim op2 As Double = 23.4
Dim operation As BinaryOperation = Function(x As Double, y As Double) (x + y) / y
Dim result As Double = operation(op1, op2)
End Sub
```

A lambda expression begins with the keyword Function and a parameter list. Parameters in a
lambda expression cannot be declared Optional or ParamArray, and cannot have attributes. Unlike
regular methods, omitting a parameter type for a lambda method does not automatically infer
Object. Instead, when a lambda method is referenced, the omitted parameter types are inferred
from the target type.

# # Query Expressions

Query expressions provide the "language-integrated" experience of LINQ, because they provide
syntax similar to SQL to describe a query. a query expression begins with From or Aggregate
operator and end with any query operator. Other valid clauses for the middle of the expression
include From, Where, Join, Distinct, Take, While, Skip, Aggregate,
Order By, and Group By operators.

Let’s take a look at an example:

```
Dim fruits As String = {"Apple", "Peach", "Orange", "Banana", "Lemon", 
"Pear", "Grapefruit", "Watermelon", "Plum")}

Dim filteredFruits =
From fruit In fruits
Where fruit.StartsWith("P") And fruit.Length < 20
Order By
Select fruit
```

The strength of this notation is that it describes the intention of what you would like to get as a
result, instead of defining how you want to obtain it.

The Basic compiler translates a query expression into method invocations. For example, the
Where clause will translate into a call to a Where method, the Order will translate into a call
to OrderBy, and so on. These methods become extension methods or instance methods
the type being queried. So, in the preceding example, the type representing fruits must have this
characteristic. The method (not the compiler) will determine how to execute the query at run-time.

This kind of extensibility of query expressions makes LINQ a very powerful feature that enables the
shift from an imperative data-processing model to the declarative one.
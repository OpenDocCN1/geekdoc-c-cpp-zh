C# supports two types of lambda expressions, and it is the lambda body that determines what type is being created. If the lambda body consists of a single expression, then an expression lambda is being created. In this case, the body is free-standing—it is not enclosed between braces. If the lambda body consists of a block of statements enclosed by braces, then a statement lambda is being created. A statement lambda can contain multiple statements and include such things as loops, method calls, and if statements. The following sections describe both kinds of lambdas.

# ### Expression Lambdas

In an expression lambda, the expression on the right side of the => acts on the parameter (or parameters) specified by the left side. The result of the expression becomes the result of the lambda operator and is returned.

Here is the general form of an expression lambda that takes only one parameter:

```
param => expr
```

When more than one parameter is required, then the following form is used:

```
(param-list) => expr
```

Therefore, when two or more parameters are needed, they must be enclosed by parentheses. If no parameters are needed, then empty parentheses must be used. Here is a simple expression lambda:

```
count => count + 2
```

Here count is the parameter that is acted on by the expression count + 2. Thus, the result is the value of count increased by two. Here is another example:

```
n => n % 2 == 0
```

In this case, this expression returns true if n is even and false if it is odd.

To use a lambda expression involves two steps. First, declare a delegate type that is compatible with the lambda expression. Second, declare an instance of the delegate, assigning to it the lambda expression. Once this has been done, the lambda expression can be executed by calling the delegate instance. The result of the lambda expression becomes the return value.

The following program shows how to put the two expression lambdas just shown into action. It declares two delegate types. The first, called Incr, takes an int argument and returns an int result. The second, called IsEven, takes an int argument and returns a bool result. It then assigns the lambda expressions to instances of those delegates. Finally, it executes the lambda expressions through the delegate instances.

```
// Use two simple lambda expressions.

using System;

// Declare a delegate that takes an int argument
// and returns an int result.
delegate int Incr(int v);

// Declare a delegate that takes an int argument
// and returns a bool result.
```
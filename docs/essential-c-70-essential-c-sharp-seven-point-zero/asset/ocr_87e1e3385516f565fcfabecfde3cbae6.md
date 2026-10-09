```
```csharp
{
    string _item = item;
    actions.Add(
        () => { Console.WriteLine(_item); } );
}
foreach (Action action in actions)
{
    action();
}
}
```
```

Now there is clearly one fresh variable per loop iteration; each delegate is, in turn, closed over a different variable.

# **Guidelines**

**AVOID** capturing loop variables in anonymous functions.

# Expression Trees

Thus far we’ve seen that lambda expressions are a succinct syntax for declaring an “inline” method that can be converted to a delegate type. Expression lambdas (but not statement lambdas or anonymous methods) can also be converted to **expression trees**. A delegate is an object that enables you to pass around a method like any other object and invoke it at any time. An expression tree is an object that enables you to pass around the compiler’s analysis of the lambda body. But why would you ever need that capability? Obviously, the compiler’s analysis is useful to the compiler when generating the CIL, but why is it useful to the developer to have an object representing that analysis at execution time? Let’s take a look at an example.

# **Using Lambda Expressions as Data**

Consider the lambda expression in the following code:

```
```csharp
persons.Where(
    person => person.Name.ToUpper() == "INIGO MONTOYA");
```
```

Suppose that `persons` is an array of `Persons`, and the formal parameter of the `Where` method that corresponds to the lambda expression argument is of delegate type `Func<Person, bool>`. The compiler emits a method that
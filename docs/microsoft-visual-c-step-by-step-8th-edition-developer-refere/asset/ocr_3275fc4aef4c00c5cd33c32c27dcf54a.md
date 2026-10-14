# Note

C++ programmers should notice that you must provide the overload yourself. The compiler won’t write the overload for you or silently swap the sequence of the two operands to find a matching operator.

# Operators and language interoperability

Not all languages that execute using the common language runtime (CLR) support or understand operator overloading. If you overload an operator, you should provide an alternative mechanism that implements the same functionality to enable the class to be used from languages that do not support operator overloading. For example, suppose that you implement operator+ for the Hour structure, as is illustrated here:

Click here to view code image

```
public static Hour operator +(Hour lhs, int rhs)
{
    ...
}
```

If you need to be able to use your class from a Microsoft Visual Basic application, you should also provide an Add method that achieves the same thing, as demonstrated here:

Click here to view code image

```
public static Hour Add(Hour lhs, int rhs)
{
    ...
}
```

# Understanding compound assignment evaluation

A compound assignment operator (such as +=) is always evaluated in terms of its associated simple operator (such as +). In other words, the statement

```
a += b;
```

is automatically evaluated like this:

```
a = a + b;
```

In general, the expression a @= b (where @ represents any valid operator) is always evaluated as a = a @ b. If you have overloaded the appropriate simple operator, the overloaded version is automatically called when you use its associated compound assignment operator, as is shown in the following example:
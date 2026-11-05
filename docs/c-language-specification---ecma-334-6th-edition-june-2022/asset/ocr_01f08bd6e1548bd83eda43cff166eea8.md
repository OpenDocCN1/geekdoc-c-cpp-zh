```
~~~
return_statement
    : 'return' expression? ';'
    ;
~~~
```

A function member is said to ***compute a value*** if it is a method with a non-void result type (§14.6.11), the get accessor of a property or indexer, or a user-defined operator. Function members that do not compute a value are methods with the effective return type `void`, set accessors of properties and indexers, add and remove accessors of event, instance constructors, static constructors and finalizers.

Within a function member, a `return` statement with no expression can only be used if the function member does not compute a value. Within a function member, a `return` statement with an expression can only be used if the function member computes a value. Where the `return` statement includes an expression, an implicit conversion (§10.2) shall exist from the type of the expression to the effective return type of the containing function member.

`return` statements can also be used in the body of anonymous function expressions (§11.16), and participate in determining which conversions exist for those functions (§10.7.1).

It is a compile-time error for a `return` statement to appear in a `finally` block (§12.11).

A `return` statement is executed as follows:

+   - If the `return` statement specifies an expression, the expression is evaluated and its value is converted to the effective return type of the containing function by an implicit conversion. The result of the conversion becomes the result value produced by the function.
+   - If the `return` statement is enclosed by one or more `try` or `catch` blocks with associated `finally` blocks, control is initially transferred to the `finally` block of the innermost `try` statement. When and if control reaches the end point of a `finally` block, control is transferred to the `finally` block of the next enclosing `try` statement. This process is repeated until the `finally` blocks of all enclosing `try` statements have been executed.
+   - If the containing function is not an `async` function, control is returned to the caller of the containing function along with the result value, if any.
+   - If the containing function is an `async` function, control is returned to the current caller, and the result value, if any, is recorded in the return task as described in (§14.15.2).

Because a `return` statement unconditionally transfers control elsewhere, the end point of a `return` statement is never reachable.

# 12.10.6 The throw statement

The `throw` statement throws an exception.

```
~~~
throw_statement
    : 'throw' expression? ';'
    ;
~~~
```

A `throw` statement with an expression throws an exception produced by evaluating the expression. The expression shall be implicitly convertible to `System.Exception`, and the result of evaluating the expression is converted to `System.Exception` before being thrown. If the result of the conversion is `null`, a `System.NullReferenceException` is thrown instead.

A `throw` statement with no expression can be used only in a `catch` block, in which case, that statement rethrows the exception that is currently being handled by that `catch` block.
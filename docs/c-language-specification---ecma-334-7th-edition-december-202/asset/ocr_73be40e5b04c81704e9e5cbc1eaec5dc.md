constructors, static constructors and finalizers. Function members that are returns-by-ref do not compute a value.

For a return-by-value, an implicit conversion (§10.2) shall exist from the type of expression to the effective return type (§15.6.11) of the containing function member. For a return-by-ref, an identity conversion (§10.2.2) shall exist between the type of expression and the effective return type of the containing function member.

return statements can also be used in the body of anonymous function expressions (§12.19), and participate in determining which conversions exist for those functions (§10.7.1).

It is a compile-time error for a return statement to appear in a finally block (§13.11).

A return statement is executed as follows:

+   - For a return-by-value, expression is evaluated and its value is converted to the effective return type of the containing function by an implicit conversion. The result of the conversion becomes the result value produced by the function. For a return-by-ref, a reference to the variable, reference designated by expression becomes the result produced by the function. That result is a variable. If the enclosing method’s return-by-ref includes readonly, the resulting variable is read-only.
+   - If the return statement is enclosed by one or more try or catch blocks with associated finally blocks, control is initially transferred to the finally block of the innermost try statement. When and if control reaches the end point of a finally block, control is transferred to the finally block of the next enclosing try statement. This process is repeated until the finally blocks of all enclosing try statements have been executed.
+   - If the containing function is not an async function, control is returned to the caller of the containing function along with the result value, if any.
+   - If the containing function is an async function, control is returned to the current caller, and the result value, if any, is recorded in the return task as described in (§15.15.3).

Because a return statement unconditionally transfers control elsewhere, the end point of a return statement is never reachable.

# 13.10.6 The throw statement

The throw statement throws an exception.

```
throw_statement
  : 'throw' expression? ';'
  ;
```

A throw statement with an expression throws an exception produced by evaluating the expression. The expression shall be implicitly convertible to System.Exception, and the result of evaluating the expression is converted to System.Exception before being thrown. If the result of the conversion is null, a System.NullReferenceException is thrown instead.

A throw statement with no expression can be used only in a catch block, in which case, that statement re-throws the exception that is currently being handled by that catch block.

Because a throw statement unconditionally transfers control elsewhere, the end point of a throw statement is never reachable.

When an exception is thrown, control is transferred to the first catch clause in an enclosing try statement that can handle the exception. The process that takes place from the point of the exception being thrown to the point of transferring control to a suitable exception handler is known as exception propagation.
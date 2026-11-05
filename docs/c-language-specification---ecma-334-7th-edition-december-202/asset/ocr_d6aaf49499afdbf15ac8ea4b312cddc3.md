the goto case statement is not enclosed by a switch statement, if the nearest enclosing switch statement does not contain such a case, or if the constant_expression is not implicitly convertible (§10.2) to the governing type of the nearest enclosing switch statement, a compile-time error occurs.

The target of a goto default statement is the statement list in the immediately enclosing switch statement (§13.8.3), which contains a default label. If the goto default statement is not enclosed by a switch statement, or if the nearest enclosing switch statement does not contain a default label, a compile-time error occurs.

A goto statement cannot exit a finally block (§13.11). When a goto statement occurs within a finally block, the target of the goto statement shall be within the same finally block, or otherwise a compile-time error occurs.

A goto statement is executed as follows:

+   - If the goto statement exits one or more try blocks with associated finally blocks, control is initially transferred to the finally block of the innermost try statement. When and if control reaches the end point of a finally block, control is transferred to the finally block of the next enclosing try statement. This process is repeated until the finally blocks of all intervening try statements have been executed.
+   - Control is transferred to the target of the goto statement.

Because a goto statement unconditionally transfers control elsewhere, the end point of a goto statement is never reachable.

# 13.10.5 The return statement

The return statement returns control to the current caller of the function member in which the return statement appears, optionally returning a value or a variable_reference (§9.5).

```
return_statement
  : 'return' ';'
  | 'return' expression ';'
  | 'return' 'ref' variable_reference ';'
  ;
```

A return_statement without expression is called a return-no-value; one containing ref expression is called a return-by-ref, and one containing only expression is called a return-by-value.

It is a compile-time error to use a return-no-value from a method declared as being returns-by-value or returns-by-ref (§15.6.1).

It is a compile-time error to use a return-by-ref from a method declared as being returns-no-value or returns-by-value.

It is a compile-time error to use a return-by-value from a method declared as being returns-no-value or returns-by-ref.

It is a compile-time error to use a return-by-ref if expression is not a variable_reference or is a reference to a variable whose ref-safe-context is not caller-context (§9.7.2).
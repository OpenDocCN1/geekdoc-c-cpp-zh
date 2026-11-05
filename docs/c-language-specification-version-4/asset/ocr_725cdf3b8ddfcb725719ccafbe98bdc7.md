The type and constant-expression of a local constant declaration must follow the same rules as those of a constant member declaration (§10.4). The value of a local constant is obtained in an expression using a simple-name (§7.6.2). The scope of a local constant is the block in which the declaration occurs. It is an error to refer to a local constant in a textual position that precedes its constant-declarator. Within the scope of a local constant, it is a compile-time error to declare another local variable or constant with the same name. A local constant declaration that declares multiple constants is equivalent to multiple declarations of single constants with the same type.

# 8.6 Expression statements

An expression-statement evaluates a given expression. The value computed by the expression, if any, is discarded.

```
expression-statement:
    statement-expression ;
statement-expression:
    invocation-expression
    object-creation-expression
    assignment
    post-increment-expression
    post-decrement-expression
    pre-increment-expression
    pre-decrement-expression
```

Not all expressions are permitted as statements. In particular, expressions such as x + y and x == 1 that merely compute a value (which will be discarded), are not permitted as statements.

Execution of an expression-statement evaluates the contained expression and then transfers control to the end point of the expression-statement. The end point of an expression-statement is reachable if that expression-statement is reachable.

# 8.7 Selection statements

Selection statements select one of a number of possible statements for execution based on the value of some expression.

```
selection-statement:
    if-statement
    switch-statement
```

# 8.7.1 The if statement

The if statement selects a statement for execution based on the value of a boolean expression.

```
if-statement:
    if ( boolean-expression ) embedded-statement
    if ( boolean-expression ) embedded-statement else embedded-statement
```

An else part is associated with the lexically nearest preceding if that is allowed by the syntax. Thus, an if statement of the form if (x) if (y) F(); else G(); is equivalent to
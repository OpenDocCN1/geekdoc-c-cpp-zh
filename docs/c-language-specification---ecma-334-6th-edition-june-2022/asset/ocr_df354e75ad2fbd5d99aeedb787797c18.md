# ## 12.7 Expression statements

An *expression_statement* evaluates a given expression. The value computed by the expression, if any, is discarded.

```
```
expression_statement
    : statement_expression ';'
    ;

statement_expression
    : null_conditional_invocation_expression
    | invocation_expression
    | object_creation_expression
    | assignment
    | post_increment_expression
    | post_decrement_expression
    | pre_increment_expression
    | pre_decrement_expression
    | await_expression
    ;
```
```

Not all expressions are permitted as statements.

> > *Note:* In particular, expressions such as `x + y` and `x == 1`, that merely compute a value (which will be discarded), are not permitted as statements. *end note*

Execution of an *expression_statement* evaluates the contained expression and then transfers control to the end point of the *expression_statement*. The end point of an *expression_statement* is reachable if that *expression_statement* is reachable.

# ## 12.8 Selection statements

# ### 12.8.1 General

Selection statements select one of a number of possible statements for execution based on the value of some expression.

```
```
selection_statement
    : if_statement
    | switch_statement
    ;
```
```

# ### 12.8.2 The if statement

The *if* statement selects a statement for execution based on the value of a Boolean expression.

```
```
if_statement
    : 'if' '(' boolean_expression ')' embedded_statement
    | 'if' '(' boolean_expression ')' embedded_statement 'else' embedded_statement
    ;
```
```

An *else* part is associated with the lexically nearest preceding *if* that is allowed by the syntax.

> > *Example:* Thus, an *if* statement of the form

```
```
if (x) if (y) F(); else G();
```
```

is equivalent to
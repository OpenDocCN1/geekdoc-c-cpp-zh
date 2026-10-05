Label names shall be unique within a function.

Semantics
Any statement may be preceded by a prefix that declares an identifier as a label name.
Labels in themselves do not alter the flow of control, which continues unimpeded across
them.

Forward references: the goto (6.8.6.1), the switch statement (6.8.4.2).

# 6.8.2 Compound statement

Syntax

```
compound-statement:
  { block-item-list_opt }

  block-item-list:
    block-item
    block-item-list block-item

  block-item:
    declaration
    statement
```

Semantics

A compound statement is a block.

# 6.8.3 Expression and null statements

Syntax

```
expression-statement:
  expression_opt ;
```

Semantics

The expression in an expression statement is evaluated as a void expression for its side effects.^{153}$

A null statement (consisting of just a semicolon) performs no operations.

EXAMPLE1 If a function call is evaluated as an expression statement for its side effects only, the discarding of its value may be made explicit by converting the expression to a void expression by means of a cast:

```
int p(int);
/* ... * */
(void)p(0);
```

> 153) Such assignments, and function calls which have side effects.
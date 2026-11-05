Example:

```
```
int x;
if (false)
{
    Console.WriteLine(x);
}
```
```

end example

For all other constant expressions, the definite assignment state of v after the expression is the same as the definite assignment state of v before the expression.

# 9.4.4.22 General rules for simple expressions

The following rule applies to these kinds of expressions: literals (§11.7.2), simple names (§11.7.4), member access expressions (§11.7.6), non-indexed base access expressions (§11.7.13), typeof expressions (§11.7.16), default value expressions (§11.7.19), and nameof expressions (§11.7.20).

+   - The definite assignment state of v at the end of such an expression is the same as the definite assignment state of v at the beginning of the expression.

# 9.4.4.23 General rules for expressions with embedded expressions

The following rules apply to these kinds of expressions: parenthesized expressions (§11.7.5), element access expressions (§11.7.10), base access expressions with indexing (§11.7.13), increment and decrement expressions (§11.7.14, §11.8.6), cast expressions (§11.8.7), unary +, -, ~, * expressions, binary +, -, *, /, %, <<, >>, <, <=, >, >=, ==, !=, is, as, &, |, ^ expressions (§11.9, §11.10, §11.11, §11.12), compound assignment expressions (§11.18.3), checked and unchecked expressions (§11.7.18), array and delegate creation expressions (§11.7.15), and await expressions (§11.8.8).

Each of these expressions has one or more subexpressions that are unconditionally evaluated in a fixed order.

Example: The binary % operator evaluates the left hand side of the operator, then the right hand side. An indexing operation evaluates the indexed expression, and then evaluates each of the index expressions, in order from left to right. end example

For an expression expr, which has subexpressions expr1, expr2, ..., exprx, evaluated in that order:

+   - The definite assignment state of v at the beginning of expr1 is the same as the definite assignment state at the beginning of expr.
+   - The definite assignment state of v at the beginning of expr i (i greater than one) is the same as the definite assignment state at the end of expr i-1.
+   - The definite assignment state of v at the end of expr is the same as the definite assignment state at the end of exprx.

# 9.4.4.24 Invocation expressions and object creation expressions

If the method to be invoked is a partial method that has no implementing partial method declaration, or is a conditional method for which the call is omitted (§15.3.2), then the definite assignment state of v after the invocation is the same as the definite assignment state of v before the invocation. Otherwise the following rules apply:

For an invocation expression expr of the form:

primary_expression ( arg1, arg2, ..., argx )
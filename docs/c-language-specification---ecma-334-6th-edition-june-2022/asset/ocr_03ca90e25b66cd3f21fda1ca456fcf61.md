Lifted (§11.4.8) forms of the unlifted predefined prefix increment and decrement operators defined above are also predefined.

# 11.8.7 Cast expressions

A cast_expression is used to convert explicitly an expression to a given type.

```
cast_expression
  : '(' type ')' unary_expression
  ;
```

A cast_expression of the form (T)E, where T is a type and E is a unary_expression, performs an explicit conversion (§10.3) of the value of E to type T. If no explicit conversion exists from E to T, a binding-time error occurs. Otherwise, the result is the value produced by the explicit conversion. The result is always classified as a value, even if E denotes a variable.

The grammar for a cast_expression leads to certain syntactic ambiguities.

Example: The expression (x)-y could either be interpreted as a cast_expression (a cast of -y to type x) or as an additive_expression combined with a parenthesized_expression (which computes the value x - y). end example

To resolve cast_expression ambiguities, the following rule exists: A sequence of one or more tokens (§6.4) enclosed in parentheses is considered the start of a cast_expression only if at least one of the following are true:

+   - The sequence of tokens is correct grammar for a type, but not for an expression.
+   - The sequence of tokens is correct grammar for a type, and the token immediately following the closing parentheses is the token '~', the token '!', the token '(', an identifier (§6.4.3), a literal (§6.4.5), or any keyword (§6.4.4) except as and is.

The term “correct grammar” above means only that the sequence of tokens shall conform to the particular grammatical production. It specifically does not consider the actual meaning of any constituent identifiers.

Example: If x and y are identifiers, then x.y is correct grammar for a type, even if x.y doesn't actually denote a type. end example

Note: From the disambiguation rule, it follows that, if x and y are identifiers, (x)y, (x)(y), and (x)(-y) are cast_expressions, but (x)-y is not, even if x identifies a type. However, if x is a keyword that identifies a predefined type (such as int), then all four forms are cast_expressions (because such a keyword could not possibly be an expression by itself). end note

# 11.8.8 Await expressions

# 11.8.8.1 General

The await operator is used to suspend evaluation of the enclosing async function until the asynchronous operation represented by the operand has completed.

```
await_expression
  : 'await' unary_expression
  ;
```

An await_expression is only allowed in the body of an async function (§14.15). Within the nearest enclosing async function, an await_expression shall not occur in these places:

+   - Inside a nested (non-async) anonymous function
# ### 12.23 Constant expressions

A constant expression is an expression that shall be fully evaluated at compile-time.

```
constant_expression
    : expression
    ;
```

A constant expression may be either a value type or a reference type. If a constant expression is a value type, it must be one of the following types: `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, `decimal`, `bool`, or any enumeration type. If a constant expression is a reference type, it must be the `string` type, a default value expression (§12.8.20) for some reference type, or the value of the expression must be `null`.

Only the following constructs are permitted in constant expressions:

+   - Literals (including the `null` literal).
+   - References to `const` members of class and struct types.
+   - References to members of enumeration types.
+   - References to local constants.
+   - Parenthesized subexpressions, which are themselves constant expressions.
+   - Cast expressions.
+   - `checked` and `unchecked` expressions.
+   - `nameof` expressions.
+   - The predefined `+`, `-`, `!`, and `~` unary operators.
+   - The predefined `+`, `-`, `*`, `/`, `%`, `<<`, `>>`, `&`, `|`, `^`, `&&`, `||`, `==`, `!=`, `<`, `>`, `<=`, and `>=` binary operators.
+   - The `?:` conditional operator.
+   - `sizeof` expressions, provided the unmanaged-type is one of the types specified in §23.6.9 for which `sizeof` returns a constant value.
+   - Default value expressions, provided the type is one of the types listed above.

The following conversions are permitted in constant expressions:

+   - Identity conversions
+   - Numeric conversions
+   - Enumeration conversions
+   - Constant expression conversions
+   - Implicit and explicit reference conversions, provided the source of the conversions is a constant expression that evaluates to the `null` value.

> *Note: Other conversions including boxing, unboxing, and implicit reference conversions of non-`null` values are not permitted in constant expressions. end note*

*Example:* In the following code

```
class C
{
```
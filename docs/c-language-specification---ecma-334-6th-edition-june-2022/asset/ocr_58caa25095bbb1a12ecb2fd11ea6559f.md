specifically does not affect evaluation of user-defined operators, although user-defined operators can be implemented to exhibit similar effects.

As an example of numeric promotion, consider the predefined implementations of the binary * operator:

```
int operator *(int x, int y);
uint operator *(uint x, uint y);
long operator *(long x, long y);
ulong operator *(ulong x, ulong y);
float operator *(float x, float y);
double operator *(double x, double y);
decimal operator *(decimal x, decimal y);
```

When overload resolution rules (§11.6.4) are applied to this set of operators, the effect is to select the first of the operators for which implicit conversions exist from the operand types.

> Example: For the operation b * s, where b is a byte and s is a short, overload resolution selects operator *(int, int) as the best operator. Thus, the effect is that b and s are converted to int, and the type of the result is int. Likewise, for the operation i * d, where i is an int and d is a double, overload resolution selects operator *(double, double) as the best operator. end example

End of informative text.

# 11.4.7.2 Unary numeric promotions

This subclause is informative.

Unary numeric promotion occurs for the operands of the predefined +, -, and ~ unary operators. Unary numeric promotion simply consists of converting operands of type sbyte, byte, short, ushort, or char to type int. Additionally, for the unary – operator, unary numeric promotion converts operands of type uint to type long

End of informative text.

# 11.4.7.3 Binary numeric promotions

This subclause is informative.

Binary numeric promotion occurs for the operands of the predefined +, -, *, /, %, &, |, ^, ==, !=, >, <, >=, and <= binary operators. Binary numeric promotion implicitly converts both operands to a common type which, in case of the non-relational operators, also becomes the result type of the operation. Binary numeric promotion consists of applying the following rules, in the order they appear here:

+   - If either operand is of type decimal, the other operand is converted to type decimal, or a binding-time error occurs if the other operand is of type float or double.
+   - Otherwise, if either operand is of type double, the other operand is converted to type double.
+   - Otherwise, if either operand is of type float, the other operand is converted to type float.
+   - Otherwise, if either operand is of type ulong, the other operand is converted to type ulong, or a binding-time error occurs if the other operand is of type sbyte, short, int, or long.
+   - Otherwise, if either operand is of type long, the other operand is converted to type long.
+   - Otherwise, if either operand is of type uint and the other operand is of type sbyte, short, or int, both operands are converted to type long.
+   - Otherwise, if either operand is of type uint, the other operand is converted to type uint.
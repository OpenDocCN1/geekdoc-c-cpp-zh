# ### 7.3.6 Numeric Promotions

Numeric promotion consists of automatically performing certain implicit conversions of the operands of the predefined unary and binary numeric operators. Numeric promotion is not a distinct mechanism, but rather an effect of applying overload resolution to the predefined operators. Numeric promotion specifically does not affect evaluation of user-defined operators, although user-defined operators can be implemented to exhibit similar effects.

As an example of numeric promotion, consider the predefined implementations of the binary * operator:

```
```text
int operator *(int x, int y);
uint operator *(uint x, uint y);
long operator *(long x, long y);
ulong operator *(ulong x, ulong y);
float operator *(float x, float y);
double operator *(double x, double y);
decimal operator *(decimal x, decimal y);
```
```

When overload resolution rules (§7.5.3) are applied to this set of operators, the effect is to select the first of the operators for which implicit conversions exist from the operand types. For example, for the operation b * s, where b is a byte and s is a short, overload resolution selects operator *(int, int) as the best operator. Thus the effect is that b and s are converted to int, and the type of the result is int. Likewise, for the operation i * d, where i is an int and d is a double, overload resolution selects operator *(double, double) as the best operator.

# #### 7.3.6.1 *Unary Numeric Promotions*

Unary numeric promotion occurs for the operands of the predefined +, -, and ~ unary operators. Unary numeric promotion simply consists of converting operands of type sbyte, byte, short, ushort, or char to type int. Additionally, for the unary - operator, unary numeric promotion converts operands of type uint to type long.

# #### 7.3.6.2 *Binary Numeric Promotions*

Binary numeric promotion occurs for the operands of the predefined +, -, *, /, %, &, |, ^, ==, !=, >, <, >=, and <= binary operators. Binary numeric promotion implicitly converts both operands to a common type which, in case of the nonrelational operators, also becomes the result type of the operation. Binary numeric promotion consists of applying the following rules, in the order they appear here:

+   - If either operand is of type `decimal`, the other operand is converted to type `decimal`, or a binding-time error occurs if the other operand is of type `float` or `double`.
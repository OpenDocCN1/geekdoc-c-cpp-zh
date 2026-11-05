# 7.7.2 Unary Minus Operator

For an operation of the form -x, unary operator overload resolution (§7.3.3) is applied to select a specific operator implementation. The operand is converted to the parameter type of the selected operator, and the type of the result is the return type of the operator. The predefined negation operators are identified here:

Integer negation:

```
int operator -(int x);
long operator -(long x);
```

The result is computed by subtracting x from zero. If the value of x is the smallest representable value of the operand type (−2³¹ for int or −2⁶³ for long), then the mathematical negation of x is not representable within the operand type. If this occurs within a checked context, a System.OverflowException is thrown; if it occurs within an unchecked context, the result is the value of the operand and the overflow is not reported.

If the operand of the negation operator is of type uint, it is converted to type long. An exception is the rule that permits the int value −2147483648 (−2³¹) to be written as a decimal integer literal (§2.4.4.2).

If the operand of the negation operator is of type ulong, a compile-time error occurs. An exception is the rule that permits the long value −9223372036854775808 (−2⁶³) to be written as a decimal integer literal (§2.4.4.2).

Floating point negation:

```
float operator -(float x);
double operator -(double x);
```

The result is the value of x with its sign inverted. If x is NaN, the result is also NaN.

Decimal negation:

```
decimal operator -(decimal x);
```

The result is computed by subtracting x from zero. Decimal negation is equivalent to using the unary minus operator of type System.Decimal.

# 7.7.3 Logical Negation Operator

For an operation of the form !x, unary operator overload resolution (§7.3.3) is applied to select a specific operator implementation. The operand is converted to the parameter type of the selected operator, and the type of the result is the return type of the operator. Only one predefined logical negation operator exists:

```
bool operator !(bool x);
```
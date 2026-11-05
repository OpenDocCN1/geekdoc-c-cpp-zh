```
D operator +(D x, D y);
```

The binary + operator performs delegate combination when both operands are of some delegate type D. (If the operands have different delegate types, a binding-time error occurs.) If the first operand is null, the result of the operation is the value of the second operand (even if that is also null). Otherwise, if the second operand is null, then the result of the operation is the value of the first operand. Otherwise, the result of the operation is a new delegate instance that, when invoked, invokes the first operand and then invokes the second operand. For examples of delegate combination, see §7.8.5 and §15.4. Since System.Delegate is not a delegate type, operator + is not defined for it.

# 7.8.5 Subtraction operator

For an operation of the form x - y, binary operator overload resolution (§7.3.4) is applied to select a specific operator implementation. The operands are converted to the parameter types of the selected operator, and the type of the result is the return type of the operator.

The predefined subtraction operators are listed below. The operators all subtract y from x.

+   - Integer subtraction:
+   ```
+   int operator -(int x, int y);
+   uint operator -(uint x, uint y);
+   long operator -(long x, long y);
+   ulong operator -(ulong x, ulong y);
+   ```
+   - Floating-point subtraction:
+   ```
+   float operator -(float x, float y);
+   double operator -(double x, double y);
+   ```
+   - Decimal subtraction:
+   ```
+   decimal operator -(decimal x, decimal y);
+   ```

In a checked context, if the difference is outside the range of the result type, a System.OverflowException is thrown. In an unchecked context, overflows are not reported and any significant high-order bits outside the range of the result type are discarded.

The difference is computed according to the rules of IEEE 754 arithmetic. The following table lists the results of all possible combinations of nonzero finite values, zeros, infinities, and NaNs. In the table, x and y are nonzero finite values, and z is the result of x - y. If x and y are equal, z is positive zero. If x - y is too large to represent in the destination type, z is an infinity with the same sign as x - y.

| | y | +0 | -0 | +∞ | -∞ | NaN |
|---|---|---|---|---|---|---|
| x | z | x | x | -∞ | +∞ | NaN |
| +0 | -y | +0 | +0 | -∞ | +∞ | NaN |
| -0 | -y | -0 | +0 | -∞ | +∞ | NaN |
| +∞ | +∞ | +∞ | +∞ | NaN | +∞ | NaN |
| -∞ | -∞ | -∞ | -∞ | -∞ | NaN | NaN |
| NaN | NaN | NaN | NaN | NaN | NaN | NaN |

If the resulting value is too large to represent in the decimal format, a System.OverflowException is thrown. The scale of the result, before any rounding, is the larger of the scales of the two operands.
Decimal subtraction is equivalent to using the subtraction operator of type System.Decimal.
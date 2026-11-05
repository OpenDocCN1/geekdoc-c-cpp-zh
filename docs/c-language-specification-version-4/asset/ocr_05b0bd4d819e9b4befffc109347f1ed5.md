```
```
bool operator !=(int x, int y);
bool operator !=(uint x, uint y);
bool operator !=(long x, long y);
bool operator !=(ulong x, ulong y);
bool operator <(int x, int y);
bool operator <(uint x, uint y);
bool operator <(long x, long y);
bool operator <(ulong x, ulong y);
bool operator >(int x, int y);
bool operator >(uint x, uint y);
bool operator >(long x, long y);
bool operator >(ulong x, ulong y);
bool operator <=(int x, int y);
bool operator <=(uint x, uint y);
bool operator <=(long x, long y);
bool operator <=(ulong x, ulong y);
bool operator >=(int x, int y);
bool operator >=(uint x, uint y);
bool operator >=(long x, long y);
bool operator >=(ulong x, ulong y);
```
```

Each of these operators compares the numeric values of the two integer operands and returns a bool value that indicates whether the particular relation is true or false.

# 7.10.2 Floating-point comparison operators

The predefined floating-point comparison operators are:

```
```
bool operator ==(float x, float y);
bool operator ==(double x, double y);
bool operator !=(float x, float y);
bool operator !=(double x, double y);
bool operator <(float x, float y);
bool operator <(double x, double y);
bool operator >(float x, float y);
bool operator >(double x, double y);
bool operator <=(float x, float y);
bool operator <=(double x, double y);
bool operator >=(float x, float y);
bool operator >=(double x, double y);
```
```

The operators compare the operands according to the rules of the IEEE 754 standard:

+   - If either operand is NaN, the result is false for all operators except !=, for which the result is true. For any two operands, x != y always produces the same result as !(x == y). However, when one or both operands are NaN, the <, >, <=, and >= operators do not produce the same results as the logical negation of the opposite operator. For example, if either of x and y is NaN, then x < y is false, but !(x >= y) is true.
+   - When neither operand is NaN, the operators compare the values of the two floating-point operands with respect to the ordering
+     -∞ < -max < … < -min < -0.0 == +0.0 < +min < … < +max < +∞
+     where min and max are the smallest and largest positive finite values that can be represented in the given floating-point format. Notable effects of this ordering are:
+     - Negative and positive zeros are considered equal.
+     - A negative infinity is considered less than all other values, but equal to another negative infinity.
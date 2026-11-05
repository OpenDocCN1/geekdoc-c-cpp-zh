+   - Otherwise, if either operand is of type double, the other operand is converted to type double.
+   - Otherwise, if either operand is of type float, the other operand is converted to type float.
+   - Otherwise, if either operand is of type ulong, the other operand is converted to type ulong, or a binding-time error occurs if the other operand is of type sbyte, short, int, or long.
+   - Otherwise, if either operand is of type long, the other operand is converted to type long.
+   - Otherwise, if either operand is of type uint and the other operand is of type sbyte, short, or int, both operands are converted to type long.
+   - Otherwise, if either operand is of type uint, the other operand is converted to type uint.
+   - Otherwise, both operands are converted to type int.

Note that the first rule disallows any operations that mix the decimal type with the double and float types. The rule follows from the fact that there are no implicit conversions between the decimal type and the double and float types.

Also note that it is not possible for an operand to be of type ulong when the other operand is of a signed integral type. The reason is that no integral type exists that can represent the full range of ulong as well as the signed integral types.

In both of the above cases, a cast expression can be used to explicitly convert one operand to a type that is compatible with the other operand.

In the example

```
decimal AddPercent(decimal x, double percent)
{
    return x * (1.0 + percent / 100.0);
}
```

a binding-time error occurs because a decimal cannot be multiplied by a double. The error is resolved by explicitly converting the second operand to decimal, as follows:

```
decimal AddPercent(decimal x, double percent)
{
    return x * (decimal)(1.0 + percent / 100.0);
}
```
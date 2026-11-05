# 7.9 Shift Operators

The << and >> operators are used to perform bit shifting operations.

```
shift-expression:
    additive-expression
    shift-expression << additive-expression
    shift-expression right-shift additive-expression
```

If an operand of a shift-expression has the compile-time type dynamic, then the expression is dynamically bound (§7.2.2). In this case, the compile-time type of the expression is dynamic, and the resolution described below will take place at runtime using the runtime type of those operands that have the compile-time type dynamic.

For an operation of the form x << count or x >> count, binary operator overload resolution (§7.3.4) is applied to select a specific operator implementation. The operands are converted to the parameter types of the selected operator, and the type of the result is the return type of the operator.

When declaring an overloaded shift operator, the type of the first operand must always be the class or struct containing the operator declaration, and the type of the second operand must always be int.

The predefined shift operators are listed below.

+   - Shift left:
+   ```
+   int operator <<(int x, int count);
+   uint operator <<(uint x, int count);
+   long operator <<(long x, int count);
+   ulong operator <<(ulong x, int count);
+   ```
+   The << operator shifts x left by a number of bits computed as described below.
+   The high-order bits outside the range of the result type of x are discarded, the remaining bits are shifted left, and the low-order empty bit positions are set to zero.

+   - Shift right:
+   ```
+   int operator >>(int x, int count);
+   uint operator >>(uint x, int count);
+   long operator >>(long x, int count);
+   ulong operator >>(ulong x, int count);
+   ```
+   The >> operator shifts x right by a number of bits computed as described below.
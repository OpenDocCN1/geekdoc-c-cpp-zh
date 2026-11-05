
> **JON SKEET** It's slightly surprising that the .NET System.String type doesn't have an overload for + that would be used in this situation, until you consider the optimizations available to the compiler because it has visibility of more code. An expression such as a+b+c+d doesn't have to result in three intermediate strings being produced: A single call to String.Concat(a, b, c, d) allows the concatenation to be performed more efficiently.

Delegate combination. Every delegate type implicitly provides the following predefined operator, where D is the delegate type:

```
D operator +(D x, D y);
```

The binary + operator performs delegate combination when both operands are of some delegate type D. (If the operands have different delegate types, a binding-time error occurs.) If the first operand is null, the result of the operation is the value of the second operand (even if that is also null). Otherwise, if the second operand is null, then the result of the operation is the value of the first operand. Otherwise, the result of the operation is a new delegate instance that, when invoked, invokes the first operand and then invokes the second operand. For examples of delegate combination, see §7.8.5 and §15.4. Since System.Delegate is not a delegate type, operator + is not defined for it.

## 7.8.5 Subtraction Operator

For an operation of the form x - y, binary operator overload resolution (§7.3.4) is applied to select a specific operator implementation. The operands are converted to the parameter types of the selected operator, and the type of the result is the return type of the operator.

The predefined subtraction operators are listed below. The operators all subtract y from x.

- Integer subtraction:
  ```
  int operator -(int x, int y);
  uint operator -(uint x, uint y);
  long operator -(long x, long y);
  ulong operator -(ulong x, ulong y);
  ```

In a checked context, if the difference is outside the range of the result type, a System.OverflowException is thrown. In an unchecked context, overflows are not reported and any significant high-order bits outside the range of the result type are discarded.

- Floating point subtraction:
  ```
  float operator -(float x, float y);
  double operator -(double x, double y);
  ```

The difference is computed according to the rules of IEEE 754 arithmetic. The following table lists the results of all possible combinations of non-zero finite values, zeros, infinities, and NaNs. In the table, x and y are non-zero finite values; z is the result of x − y. If x and y are equal, z is positive zero. If x − y is too large to represent in the destination type, z is an infinity with the same sign as x − y.

|   | y | +0 | −0 | +∞ | −∞ | NaN |
|---|---|---|---|---|---|---|
| x | z | x | x | −∞ | +∞ | NaN |
| +0 | −y | +0 | +0 | −∞ | +∞ | NaN |
| −0 | −y | −0 | +0 | −∞ | +∞ | NaN |
| +∞ | +∞ | +∞ | +∞ | NaN | +∞ | NaN |
| −∞ | −∞ | −∞ | −∞ | −∞ | NaN | NaN |
| NaN | NaN | NaN | NaN | NaN | NaN | NaN |

- Decimal subtraction:
  ```
  decimal operator −(decimal x, decimal y);
  ```

If the resulting value is too large to represent in the decimal format, a System.OverflowException is thrown. The scale of the result, before any rounding, is the larger of the scales of the two operands.

Decimal subtraction is equivalent to using the subtraction operator of type System.Decimal.

- Enumeration subtraction. Every enumeration type implicitly provides the following predefined operator, where E is the enum type and U is the underlying type of E:
  ```
  U operator −(E x, E y);
  ```
This operator is evaluated exactly as (U)((U)x − (U)y). In other words, the operator computes the difference between the ordinal values of x and y, and the type of the result is the underlying type of the enumeration.

```
E operator −(E x, U y);
```

This operator is evaluated exactly as (E)((U)x − y). In other words, the operator subtracts a value from the underlying type of the enumeration, yielding a value of the enumeration.

## 7. Expressions

- Delegate removal. Every delegate type implicitly provides the following predefined operator, where D is the delegate type:
  ```
  D operator -(D x, D y);
  ```

The binary - operator performs delegate removal when both operands are of some delegate type D. If the operands have different delegate types, a binding-time error occurs. If the first operand is null, the result of the operation is null. Otherwise, if the second operand is null, then the result of the operation is the value of the first operand. Otherwise, both operands represent invocation lists (§15.1) having one or more entries, and the result is a new invocation list consisting of the first operand's list with the second operand's entries removed from it, provided the second operand's list is a proper contiguous sublist of the first's. (To determine sublist equality, corresponding entries are compared as for the delegate equality operator (§7.10.8).) Otherwise, the result is the value of the left operand. Neither of the operands' lists is changed in the process. If the second operand's list matches multiple sublists of contiguous entries in the first operand's list, the rightmost matching sublist of contiguous entries is removed. If removal results in an empty list, the result is null. For example:

```
delegate void D(int x);

class C
{
    public static void M1(int i) { /* ... */ }
    public static void M2(int i) { /* ... */ }
}

class Test
{
    static void Main() {
        D cd1 = new D(C.M1);
        D cd2 = new D(C.M2);
        D cd3 = cd1 + cd2 + cd2 + cd1;  // M1 + M2 + M2 + M1
        cd3 -= cd1;                     // => M1 + M2 + M2

        cd3 = cd1 + cd2 + cd2 + cd1;    // M1 + M2 + M2 + M1
        cd3 -= cd1 + cd2;               // => M2 + M1

        cd3 = cd1 + cd2 + cd2 + cd1;    // M1 + M2 + M2 + M1
        cd3 -= cd2 + cd2;               // => M1 + M1

        cd3 = cd1 + cd2 + cd2 + cd1;    // M1 + M2 + M2 + M1
        cd3 -= cd2 + cd1;               // => M1 + M1

        cd3 = cd1 + cd2 + cd2 + cd1;    // M1 + M2 + M2 + M1
        cd3 -= cd1 + cd1;               // => M1 + M2 + M2 + M1
    }
}
```

## 7.9 Shift Operators

The `<<` and `>>` operators are used to perform bit shifting operations.

```
shift-expression:
    additive-expression
    shift-expression << additive-expression
    shift-expression >> additive-expression
```

If an operand of a `shift-expression` has the compile-time type `dynamic`, then the expression is dynamically bound (§7.2.2). In this case, the compile-time type of the expression is `dynamic`, and the resolution described below will take place at runtime using the runtime type of those operands that have the compile-time type `dynamic`.

For an operation of the form `x << count` or `x >> count`, binary operator overload resolution (§7.3.4) is applied to select a specific operator implementation. The operands are converted to the parameter types of the selected operator, and the type of the result is the return type of the operator.

When declaring an overloaded shift operator, the type of the first operand must always be the class or struct containing the operator declaration, and the type of the second operand must always be `int`.

The predefined shift operators are listed below.

- Shift left:
  ```csharp
  int operator <<(int x, int count);
  uint operator <<(uint x, int count);
  long operator <<(long x, int count);
  ulong operator <<(ulong x, int count);
  ```
  The `<<` operator shifts `x` left by a number of bits computed as described below.
  
  The high-order bits outside the range of the result type of `x` are discarded, the remaining bits are shifted left, and the low-order empty bit positions are set to zero.
- Shift right:
  ```csharp
  int operator >>(int x, int count);
  uint operator >>(uint x, int count);
  long operator >>(long x, int count);
  ulong operator >>(ulong x, int count);
  ```
  The `>>` operator shifts `x` right by a number of bits computed as described below.

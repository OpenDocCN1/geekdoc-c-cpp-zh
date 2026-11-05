
The overflow checking context can also be controlled through the checked and unchecked statements (§13.12).

The following operations are affected by the overflow checking context established by the checked and unchecked operators and statements:

- The predefined ++ and -- operators (§12.7.10 and §12.8.6), when the operand is of an integral or enum type.
- The predefined − unary operator (§12.8.3), when the operand is of an integral type.
- The predefined +, −, *, and / binary operators (§12.9), when both operands are of integral or enum types.
- Explicit numeric conversions (§11.3.2) from one integral or enum type to another integral or enum type, or from float or double to an integral or enum type.

When one of the above operations produces a result that is too large to represent in the destination type, the context in which the operation is performed controls the resulting behavior:

- In a checked context, if the operation is a constant expression (§12.20), a compile-time error occurs. Otherwise, when the operation is performed at run-time, a System.OverflowException is thrown.
- In an unchecked context, the result is truncated by discarding any high-order bits that do not fit in the destination type.

For non-constant expressions (§12.20) (expressions that are evaluated at run-time) that are not enclosed by any checked or unchecked operators or statements, the default overflow checking context is unchecked, unless external factors (such as compiler switches and execution environment configuration) call for checked evaluation.

For constant expressions (§12.20) (expressions that can be fully evaluated at compile-time), the default overflow checking context is always checked. Unless a constant expression is explicitly placed in an unchecked context, overflows that occur during the compile-time evaluation of the expression always cause compile-time errors.

The body of an anonymous function is not affected by checked or unchecked contexts in which the anonymous function occurs.

[Example: In the following code

```
class Test
{
    static readonly int x = 1000000;
    static readonly int y = 1000000;
    static int F() {
        return checked(x * y);    // Throws OverflowException
    }
    static int G() {
        return unchecked(x * y);  // Returns -727379968
    }
    static int H() {
        return x * y;             // Depends on default
    }
}
```

no compile-time errors are reported since neither of the expressions can be evaluated at compile-time. At run-time, the F method throws a System.OverflowException, and the G method returns -727379968 (the lower 32 bits of the out-of-range result). The behavior of the H method depends on the default overflow-checking context for the compilation, but it is either the same as F or the same as G. end example

[Example: In the following code

```
class Test
{
    const int x = 1000000;
    const int y = 1000000;
    static int F() {
        return checked(x * y);    // Compile-time error, overflow
    }
    static int G() {
        return unchecked(x * y);  // Returns -727379968
    }
    static int H() {
        return x * y;             // Compile-time error, overflow
    }
}
```

the overflows that occur when evaluating the constant expressions in F and H cause compile-time errors to be reported because the expressions are evaluated in a checked context. An overflow also occurs when evaluating the constant expression in G, but since the evaluation takes place in an unchecked context, the overflow is not reported. end example

The checked and unchecked operators only affect the overflow checking context for those operations that are textually contained within the "(" and ")" tokens. The operators have no effect on function members that are invoked as a result of evaluating the contained expression. [Example: In the following code

```
class Test
{
    static int Multiply(int x, int y) {
        return x * y;
    }
    static int F() {
        return checked(Multiply(1000000, 1000000));
    }
}
```

the use of checked in F does not affect the evaluation of x * y in Multiply, so x * y is evaluated in the default overflow checking context. end example

The unchecked operator is convenient when writing constants of the signed integral types in hexadecimal notation. [Example:]

```
class Test
{
    public const int AllBits = unchecked((int)0xFFFFFFFF);
    public const int HighBit = unchecked((int)0x80000000);
}
```

Both of the hexadecimal constants above are of type uint. Because the constants are outside the int range, without the unchecked operator, the casts to int would produce compile-time errors. end example

[Note: The checked and unchecked operators and statements allow programmers to control certain aspects of some numeric calculations. However, the behavior of some numeric operators depends on their operands' data types. For example, multiplying two decimals always results in an exception on overflow even within an explicitly unchecked construct. Similarly, multiplying two floats never results in an exception on overflow even within an explicitly checked construct. In addition, other operators are never affected by the mode of checking, whether default or explicit. end note]

### 12.7.15 Default value expressions

A default value expression is used to obtain the default value (§10.3) of a type. Typically a default value expression is used for type parameters, since it might not be known if the type parameter is a value type or a reference type. (No conversion exists from the null literal (§7.4.5.7) to a type parameter unless the type parameter is known to be a reference type (§9.2).)

```
default-value-expression:
  default ( type )
```

If the type in a default-value-expression evaluates at run-time to a reference type, the result is null converted to that type. If the type in a default-value-expression evaluates at run-time to a value type, the result is the value-type's default value (§9.3.3).

A default-value-expression is a constant expression (§12.20) if type is a reference type or a type parameter that is known to be a reference type (§9.2). In addition, a default-value-expression is a constant expression if the type is one of the following value types: sbyte, byte, short, ushort, int, uint, long, ulong, char, float, double, decimal, bool, or any enumeration type.

### 12.7.16 Anonymous method expressions

An anonymous-method-expression is one of two ways of defining an anonymous function. These are further described in §12.16.

## 12.8 Unary operators

### 12.8.1 General

The +, -, !, ~, ++, --, cast, and await operators are called the unary operators.

```
unary-expression:
  primary-expression
  + unary-expression
  - unary-expression
  ! unary-expression
  ~ unary-expression
  pre-increment-expression
  pre-decrement-expression
  cast-expression
  await-expression
```

If the operand of a unary-expression has the compile-time type dynamic, it is dynamically bound (§12.3.3). In this case, the compile-time type of the unary-expression is dynamic, and the resolution described below will take place at run-time using the run-time type of the operand.

### 12.8.2 Unary plus operator

For an operation of the form +x, unary operator overload resolution (§12.4.4) is applied to select a specific operator implementation. The operand is converted to the parameter type of the selected operator, and the type of the result is the return type of the operator. The predefined unary plus operators are:

```
int operator +(int x);
uint operator +(uint x);
long operator +(long x);
ulong operator +(ulong x);
float operator +(float x);
double operator +(double x);
decimal operator +(decimal x);
```

For each of these operators, the result is simply the value of the operand.

Lifted (§12.4.8) forms of the unlifted predefined unary plus operators defined above are also predefined.

### 12.8.3 Unary minus operator

For an operation of the form -x, unary operator overload resolution (§12.4.4) is applied to select a specific operator implementation. The operand is converted to the parameter type of the selected operator, and the type of the result is the return type of the operator. The predefined unary minus operators are:

- Integer negation:

```
int operator -(int x);
long operator -(long x);
```

The result is computed by subtracting x from zero. If the value of x is the smallest representable value of the operand type (−2³¹ for int or −2⁶³ for long), then the mathematical negation of x is not representable within the operand type. If this occurs within a checked context, a System.OverflowException is thrown; if it occurs within an unchecked context, the result is the value of the operand and the overflow is not reported.

If the operand of the negation operator is of type uint, it is converted to type long, and the type of the result is long. An exception is the rule that permits the int value −2147483648 (−2³¹) to be written as a decimal integer literal (§7.4.5.3).

If the operand of the negation operator is of type ulong, a compile-time error occurs. An exception is the rule that permits the long value −9223372036854775808 (−2⁶³) to be written as a decimal integer literal (§7.4.5.3).

- Floating-point negation:

```
float operator -(float x);
double operator -(double x);
```

The result is the value of x with its sign inverted. If x is NaN, the result is also NaN.

- Decimal negation:

```
decimal operator -(decimal x);
```

The result is computed by subtracting x from zero. Decimal negation is equivalent to using the unary minus operator of type System.Decimal.

Lifted (§12.4.8) forms of the unlifted predefined unary minus operators defined above are also predefined.

### 12.8.4 Logical negation operator

### 12.8.5 Bitwise complement operator

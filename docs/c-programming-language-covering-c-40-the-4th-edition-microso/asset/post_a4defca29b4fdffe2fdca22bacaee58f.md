
When x is of type int or long, the low-order bits of x are discarded, the remaining bits are shifted right, and the high-order empty bit positions are set to zero if x is non-negative and set to 1 if x is negative.

When x is of type uint or ulong, the low-order bits of x are discarded, the remaining bits are shifted right, and the high-order empty bit positions are set to zero.

For the predefined operators, the number of bits to shift is computed as follows:

- When the type of x is int or uint, the shift count is given by the low-order five bits of count. In other words, the shift count is computed from `count & 0x1F`.
- When the type of x is long or ulong, the shift count is given by the low-order six bits of count. In other words, the shift count is computed from `count & 0x3F`.

If the resulting shift count is zero, the shift operators simply return the value of x.

> **JON SKEET** Masking the shift count may be efficient, but it can make for some very confusing behavior:
>
> ```csharp
> for (int i = 0; i < 40; i++)
> {
>     Console.WriteLine(int.MaxValue >> i);
> }
> ```
>
> This code prints values that are halved on each iteration—until they cycle back to `int.MaxValue` after reaching 0.

Shift operations never cause overflows and produce the same results in checked and unchecked contexts.

When the left operand of the >> operator is of a signed integral type, the operator performs an arithmetic shift right wherein the value of the most significant bit (the sign bit) of the operand is propagated to the high-order empty bit positions. When the left operand of the >> operator is of an unsigned integral type, the operator performs a logical shift right wherein high-order empty bit positions are always set to zero. To perform the opposite operation of that inferred from the operand type, explicit casts can be used. For example, if x is a variable of type int, the operation unchecked((int)((uint)x >> y)) performs a logical shift right of x.

## 7.10 Relational and Type-Testing Operators

The ==, !=, <, >, <=, >=, is, and as operators are called the relational and type-testing operators.

```
relational-expression:
    shift-expression
    relational-expression < shift-expression
    relational-expression > shift-expression
    relational-expression <= shift-expression
    relational-expression >= shift-expression
    relational-expression is type
    relational-expression as type
```

```
equality-expression:
    relational-expression
    equality-expression == relational-expression
    equality-expression != relational-expression
```

The is operator is described in §7.10.10 and the as operator is described in §7.10.11.

The ==, !=, <, >, <=, and >= operators are comparison operators.

If an operand of a comparison operator has the compile-time type dynamic, then the expression is dynamically bound (§7.2.2). In this case, the compile-time type of the expression is dynamic, and the resolution described below will take place at runtime using the runtime type of those operands that have the compile-time type dynamic.

For an operation of the form x op y, where op is a comparison operator, overload resolution (§7.3.4) is applied to select a specific operator implementation. The operands are converted to the parameter types of the selected operator, and the type of the result is the return type of the operator.

The predefined comparison operators are described in the following sections. All predefined comparison operators return a result of type bool, as described in the following table.

| Operation | Result |
|---|---|
| x == y | true if x is equal to y, false otherwise |
| x != y | true if x is not equal to y, false otherwise |
| x < y | true if x is less than y, false otherwise |
| x > y | true if x is greater than y, false otherwise |
| x <= y | true if x is less than or equal to y, false otherwise |
| x >= y | true if x is greater than or equal to y, false otherwise |

### 7.10.1 Integer Comparison Operators

The predefined integer comparison operators are listed here:

```csharp
bool operator ==(int x, int y);
bool operator ==(uint x, uint y);
bool operator ==(long x, long y);
bool operator ==(ulong x, ulong y);

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

Each of these operators compares the numeric values of the two integer operands and returns a bool value that indicates whether the particular relation is true or false.

### 7.10.2 Floating Point Comparison Operators

The predefined floating point comparison operators are listed here:

```csharp
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

These operators compare the operands according to the rules of the IEEE 754 standard:

- If either operand is NaN, the result is false for all operators except !=, for which the result is true. For any two operands, x != y always produces the same result as !(x == y). However, when one or both operands are NaN, the <, <=, and >= operators do not produce the same results as the logical negation of the opposite operator. For example, if either of x and y is NaN, then x < y is false, but !(x >= y) is true.
- When neither operand is NaN, the operators compare the values of the two floating point operands with respect to the ordering

  ```
  -∞ < -max < ... < -min < -0.0 == +0.0 < +min < ... < +max < +∞
  ```

  where min and max are, respectively, the smallest and largest positive finite values that can be represented in the given floating point format. Notable effects of this ordering are as follows:

  - Negative and positive zeros are considered equal.
  - A negative infinity is considered less than all other values, but equal to another negative infinity.
  - A positive infinity is considered greater than all other values, but equal to another positive infinity.

> PETER SESTOFT It also holds that positive and negative zero are equal by Object.Equals, so their hashcodes as computed by Object.GetHashCode should be equal as well. Unfortunately, this is not the case in all current implementations.

> JOSEPH ALBAHARI Two NaN values, although unequal according to the == operator, are equal according to the Equals method:
>
> ```
> double x = double.NaN;
> Console.WriteLine(x == x);    // False
> Console.WriteLine(x != x);    // True
> Console.WriteLine(x.Equals(x)); // True
> ```
>
> In general, a type's Equals method follows the principle that an object must equal itself. Without this assumption, lists and dictionaries could not operate, because there would be no means of testing element membership. The == and != operators, however, are not obliged to follow this principle.

> PETER SESTOFT Even NaNs that have different payloads (see the annotation on §7.8.1) are equal by Object.Equals.

### 7.10.3 Decimal Comparison Operators

The predefined decimal comparison operators are listed here:

```csharp
bool operator ==(decimal x, decimal y);
bool operator !=(decimal x, decimal y);
bool operator <(decimal x, decimal y);
bool operator >(decimal x, decimal y);
bool operator <=(decimal x, decimal y);
bool operator >=(decimal x, decimal y);
```

Each of these operators compares the numeric values of the two decimal operands and returns a bool value that indicates whether the particular relation is true or false. Each decimal comparison is equivalent to using the corresponding relational or equality operator of type System.Decimal.

### 7.10.4 Boolean Equality Operators

The predefined boolean equality operators are listed here:

```csharp
bool operator ==(bool x, bool y);
bool operator !=(bool x, bool y);
```

The result of == is true if both x and y are true or if both x and y are false. Otherwise, the result is false.

The result of != is false if both x and y are true or if both x and y are false. Otherwise, the result is true. When the operands are of type bool, the != operator produces the same result as the ^ operator.

### 7.10.5 Enumeration Comparison Operators

Every enumeration type implicitly provides the following predefined comparison operators:

```csharp
bool operator ==(E x, E y);
bool operator !=(E x, E y);
bool operator <(E x, E y);
bool operator >(E x, E y);
bool operator <=(E x, E y);
bool operator >=(E x, E y);
```

The result of evaluating x op y, where x and y are expressions of an enumeration type E with an underlying type U, and op is one of the comparison operators, is exactly the same as evaluating ((U)x) op ((U)y). In other words, the enumeration type comparison operators simply compare the underlying integral values of the two operands.

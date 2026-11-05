
> *Note:* Lookup for the right operand of the `is` operator must first test as a type, then as an expression which may span multiple tokens. In the case where the operand is an expression, the pattern expression must have precedence at least as high as `shift_expression`. end note

The `is` operator is described in §12.12.12 and the `as` operator is described in §12.12.13.

The `==`, `!=`, `<`, `>`, `<=` and `>=` operators are comparison operators.

If a `default_literal` (§8.20) is used as an operand of a `<`, `>`, `<=`, or `>=` operator, a compile-time error occurs. If a `default_literal` is used as both operands of a `==` or `!=` operator, a compile-time error occurs. If a `default_literal` is used as the left operand of the `is` or `as` operator, a compile-time error occurs.

If an operand of a comparison operator has the compile-time type `dynamic`, then the expression is dynamically bound (§12.3.3). In this case the compile-time type of the expression is `dynamic`, and the resolution described below will take place at run-time using the run-time type of those operands that have the compile-time type `dynamic`.

For an operation of the form `x «op» y`, where «op» is a comparison operator, overload resolution (§12.4.5) is applied to select a specific operator implementation. The operands are converted to the parameter types of the selected operator, and the type of the result is the return type of the operator. If both operands of an `equality_expression` are the `null` literal, then overload resolution is not performed and the expression evaluates to a constant value of `true` or `false` according to whether the operator is `==` or `!=`.

The predefined comparison operators are described in the following subclauses. All predefined comparison operators return a result of type `bool`, as described in the following table.

| Operation | Result |
| --- | --- |
| x == y | true if x is equal to y, false otherwise |
| x != y | true if x is not equal to y, false otherwise |
| x < y | true if x is less than y, false otherwise |
| x > y | true if x is greater than y, false otherwise |
| x <= y | true if x is less than or equal to y, false otherwise |
| x >= y | true if x is greater than or equal to y, false otherwise |

### 12.12.2 Integer comparison operators

The predefined integer comparison operators are:

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

Each of these operators compares the numeric values of the two integer operands and returns a `bool` value that indicates whether the particular relation is true or false.

Lifted (§12.4.8) forms of the unlifted predefined integer comparison operators defined above are also predefined.

### 12.12.3 Floating-point comparison operators

The predefined floating-point comparison operators are:

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

The operators compare the operands according to the rules of the IEC 60559 standard:

If either operand is NaN, the result is false for all operators except `!=`, for which the result is true. For any two operands, `x != y` always produces the same result as `!(x == y)`. However, when one or both operands are NaN, the `<`, `>`, `<=`, and `>=` operators do not produce the same results as the logical negation of the opposite operator.

Example: If either of `x` and `y` is NaN, then `x < y` is false, but `!(x >= y)` is true. end example

When neither operand is NaN, the operators compare the values of the two floating-point operands with respect to the ordering

```
-∞ < -max < ... < -min < -0.0 == +0.0 < +min < ... < +max < +∞
```

where `min` and `max` are the smallest and largest positive finite values that can be represented in the given floating-point format. Notable effects of this ordering are:

- Negative and positive zeros are considered equal.
- A negative infinity is considered less than all other values, but equal to another negative infinity.
- A positive infinity is considered greater than all other values, but equal to another positive infinity.

Lifted (§12.4.8) forms of the unlifted predefined floating-point comparison operators defined above are also predefined.

### 12.12.4 Decimal comparison operators

The predefined decimal comparison operators are:

```csharp
bool operator ==(decimal x, decimal y);
bool operator !=(decimal x, decimal y);
bool operator <(decimal x, decimal y);
bool operator >(decimal x, decimal y);
bool operator <=(decimal x, decimal y);
bool operator >=(decimal x, decimal y);
```

Each of these operators compares the numeric values of the two decimal operands and returns a `bool` value that indicates whether the particular relation is `true` or `false`. Each decimal comparison is equivalent to using the corresponding relational or equality operator of type `System.Decimal`.

Lifted (§12.4.8) forms of the unlifted predefined decimal comparison operators defined above are also predefined.

### 12.12.5 Boolean equality operators

The predefined Boolean equality operators are:

```csharp
bool operator ==(bool x, bool y);
bool operator !=(bool x, bool y);
```

The result of `==` is `true` if both `x` and `y` are `true` or if both `x` and `y` are `false`. Otherwise, the result is `false`.

The result of `!=` is `false` if both `x` and `y` are `true` or if both `x` and `y` are `false`. Otherwise, the result is `true`. When the operands are of type `bool`, the `!=` operator produces the same result as the `^` operator.

Lifted (§12.4.8) forms of the unlifted predefined Boolean equality operators defined above are also predefined.

### 12.12.6 Enumeration comparison operators

Every enumeration type implicitly provides the following predefined comparison operators:

```csharp
bool operator ==(E x, E y);
bool operator !=(E x, E y);

bool operator <(E x, E y);
bool operator >(E x, E y);
bool operator <=(E x, E y);
bool operator >=(E x, E y);
```

The result of evaluating `x «op» y`, where `x` and `y` are expressions of an enumeration type `E` with an underlying type `U`, and «op» is one of the comparison operators, is exactly the same as evaluating

end note

Example: The following example checks whether an argument of an unconstrained type parameter type is null.

```csharp
class C<T>
{
    void F(T x)
    {
        if (x == null)
        {
            throw new ArgumentNullException();
        }
        ...
    }
}
```

The `x == null` construct is permitted even though `T` could represent a non-nullable value type, and the result is simply defined to be false when `T` is a non-nullable value type.

end example

For an operation of the form `x == y` or `x != y`, if any applicable `operator ==` or `operator !=` exists, the operator overload resolution (§12.4.5) rules will select that operator instead of the predefined reference type equality operator.

> Note: It is always possible to select the predefined reference type equality operator by explicitly casting both of the operands to type `object`. end note

Example: The example

```csharp
class Test
{
    static void Main()
    {
        string s = "Test";
        string t = string.Copy(s);
        Console.WriteLine(s == t);
        Console.WriteLine((object)s == t);
        Console.WriteLine(s == (object)t);
        Console.WriteLine((object)s == (object)t);
    }
}
```

produces the output

```
True
False
False
False
```

The `s` and `t` variables refer to two distinct string instances containing the same characters. The first comparison outputs `True` because the predefined string equality operator (§12.12.8) is selected when both operands are of type `string`. The remaining comparisons all output `False` because the overload of `operator ==` in the `string` type is not applicable when either operand has a binding-time type of `object`.

Note that the above technique is not meaningful for value types. The example

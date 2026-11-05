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

Lifted (§11.4.8) forms of the unlifted predefined unary minus operators defined above are also predefined.

# 11.8.4 Logical negation operator

For an operation of the form !x, unary operator overload resolution (§11.4.4) is applied to select a specific operator implementation. The operand is converted to the parameter type of the selected operator, and the type of the result is the return type of the operator. Only one predefined logical negation operator exists:

```
bool operator !(bool x);
```

This operator computes the logical negation of the operand: If the operand is true, the result is false. If the operand is false, the result is true.

Lifted (§11.4.8) forms of the unlifted predefined logical negation operator defined above are also predefined.

# 11.8.5 Bitwise complement operator

For an operation of the form ~x, unary operator overload resolution (§11.4.4) is applied to select a specific operator implementation. The operand is converted to the parameter type of the selected operator, and the type of the result is the return type of the operator. The predefined bitwise complement operators are:

```
int operator ~(int x);
uint operator ~(uint x);
long operator ~(long x);
ulong operator ~(ulong x);
```

For each of these operators, the result of the operation is the bitwise complement of x.

Every enumeration type E implicitly provides the following bitwise complement operator:

```
E operator ~(E x);
```

The result of evaluating ~x, where x is an expression of an enumeration type E with an underlying type U, is exactly the same as evaluating (E)(~(U)x), except that the conversion to E is always performed as if in an unchecked context (§11.7.18).

Lifted (§11.4.8) forms of the unlifted predefined bitwise complement operators defined above are also predefined.

# 11.8.6 Prefix increment and decrement operators

```
pre_increment_expression
  : '++' unary_expression
  ;
```

## 7.7 Unary operators

The +, -, !, ~, ++, --, and cast operators are called the unary operators.

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
```

If the operand of a unary-expression has the compile-time type dynamic, it is dynamically bound (§7.2.2). In this case the compile-time type of the unary-expression is dynamic, and the resolution described below will take place at run-time using the run-time type of the operand.

### 7.7.1 Unary plus operator

For an operation of the form +x, unary operator overload resolution (§7.3.3) is applied to select a specific operator implementation. The operand is converted to the parameter type of the selected operator, and the type of the result is the return type of the operator. The predefined unary plus operators are:

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

### 7.7.2 Unary minus operator

For an operation of the form -x, unary operator overload resolution (§7.3.3) is applied to select a specific operator implementation. The operand is converted to the parameter type of the selected operator, and the type of the result is the return type of the operator. The predefined negation operators are:

- Integer negation:
- Floating-point negation:

```
int operator -(int x);
long operator -(long x);
```

The result is computed by subtracting x from zero. If the value of x is the smallest representable value of the operand type (-2^31 for int or -2^63 for long), then the mathematical negation of x is not representable within the operand type. If this occurs within a checked context, a System.OverflowException is thrown; if it occurs within an unchecked context, the result is the value of the operand and the overflow is not reported.

```
float operator -(float x);
double operator -(double x);
```

The result is the value of x with its sign inverted. If x is NaN, the result is also NaN.

- Decimal negation:
  `decimal operator -(decimal x);`

The result is computed by subtracting x from zero. Decimal negation is equivalent to using the unary minus operator of type System.Decimal.

### 7.7.3 Logical negation operator

For an operation of the form !x, unary operator overload resolution (§7.3.3) is applied to select a specific operator implementation. The operand is converted to the parameter type of the selected operator, and the type of the result is the return type of the operator. Only one predefined logical negation operator exists:

```
bool operator !(bool x);
```

This operator computes the logical negation of the operand: If the operand is true, the result is false. If the operand is false, the result is true.

### 7.7.4 Bitwise complement operator

For an operation of the form ~x, unary operator overload resolution (§7.3.3) is applied to select a specific operator implementation. The operand is converted to the parameter type of the selected operator, and the type of the result is the return type of the operator. The predefined bitwise complement operators are:

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

The result of evaluating ~x, where x is an expression of an enumeration type E with an underlying type U, is exactly the same as evaluating (E)(~(U)x).

### 7.7.5 Prefix increment and decrement operators

```
pre-increment-expression:
  ++ unary-expression
pre-decrement-expression:
  -- unary-expression
```

The operand of a prefix increment or decrement operation must be an expression classified as a variable, a property access, or an indexer access. The result of the operation is a value of the same type as the operand.

If the operand of a prefix increment or decrement operation is a property or indexer access, the property or indexer must have both a get and a set accessor. If this is not the case, a binding-time error occurs.

Unary operator overload resolution (§7.3.3) is applied to select a specific operator implementation. Predefined ++ and -- operators exist for the following types: sbyte, byte, short, ushort, int, uint, long, ulong, char, float, double, decimal, and any enum type. The predefined ++ operators return the value produced by adding 1 to the operand, and the predefined -- operators return the value produced by subtracting 1 from the operand. In a checked context, if the result of this addition or subtraction is outside the range of the result type and the result type is an integral type or enum type, a System.OverflowException is thrown.

The run-time processing of a prefix increment or decrement operation of the form ++x or --x consists of the following steps:

- If x is classified as a variable:
  - x is evaluated to produce the variable.
  - The selected operator is invoked with the value of x as its argument.
  - The value returned by the operator is stored in the location given by the evaluation of x.
  - The value returned by the operator becomes the result of the operation.
- If x is classified as a property or indexer access:
  - The instance expression (if x is not static) and the argument list (if x is an indexer access) associated with x are evaluated, and the results are used in the subsequent get and set accessor invocations.
  - The get accessor of x is invoked.
  - The selected operator is invoked with the value returned by the get accessor as its argument.
  - The set accessor of x is invoked with the value returned by the operator as its value argument.
  - The value returned by the operator becomes the result of the operation.

The ++ and -- operators also support postfix notation (§7.6.9). Typically, the result of x++ or x-- is the value of x before the operation, whereas the result of ++x or --x is the value of x after the operation. In either case, x itself has the same value after the operation.

An operator ++ or operator -- implementation can be invoked using either postfix or prefix notation. It is not possible to have separate operator implementations for the two notations.

### 7.7.6 Cast expressions

A cast-expression is used to explicitly convert an expression to a given type.

```
cast-expression:
    ( type ) unary-expression
```

A cast-expression of the form (T)E, where T is a type and E is a unary-expression, performs an explicit conversion (§6.2) of the value of E to type T. If no explicit conversion exists from E to T, a binding-time error occurs. Otherwise, the result is the value produced by the explicit conversion. The result is always classified as a value, even if E denotes a variable.

The grammar for a cast-expression leads to certain syntactic ambiguities. For example, the expression (x)-y could either be interpreted as a cast-expression (a cast of -y to type x) or as an additive-expression combined with a parenthesized-expression (which computes the value x - y).

To resolve cast-expression ambiguities, the following rule exists: A sequence of one or more tokens (§2.3.3) enclosed in parentheses is considered the start of a cast-expression only if at least one of the following are true:

- The sequence of tokens is correct grammar for a type, but not for an expression.
- The sequence of tokens is correct grammar for a type, and the token immediately following the closing parentheses is the token "~", the token "!", the token "*", an identifier (§2.4.1), a literal (§2.4.4), or any keyword (§2.4.3) except as and is.

The term "correct grammar" above means only that the sequence of tokens must conform to the particular grammatical production. It specifically does not consider the actual meaning of any constituent identifiers. For example, if x and y are identifiers, then x.y is correct grammar for a type, even if x.y doesn't actually denote a type.

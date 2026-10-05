
When a value of integer type is converted to a real floating type, if the value being converted is unchanged. If the value converted is in the range of values that can be represented but cannot be represented exactly, the result is either the nearest higher or nearest representable value, chosen in an implementation-defined manner. If the value being converted is outside the range of values that can be represented, the behavior is undefined. Results of implicit conversions may be represented in greater range and precision than that required by the new type (see 6.3.1.8 and 6.8.6.4).

### 6.3.1.5 Real floating types

- 1 When value of real floating type is converted to a real floating type, if the value being converted can be represented exactly in the new type, it is unchanged. If the value being converted is in the range of values that can be represented but cannot be represented exactly, the result is either the nearest higher or nearest representable value, in an implementation-defined manner. If the value being converted is outside the range of values that can be represented, the behavior is undefined. Results of implicit conversions may be represented in greater range and precision than that required by the new type (see 6.3.1.8 and 6.8.6.4).

### 6.3.1.6 Complex types

- 1 When a value of complex type is converted to another complex type, both the real and imaginary parts follow the conversion rules for the corresponding real type.

### 6.3.1.7 Real and complex

- 1 When a value of real type is converted to a complex type, the real part of the complex result value is determined by the rules of conversion to the corresponding real type and the imaginary part of the complex result value is a positive zero or an unsigned zero.

- 2 When a value of complex type is converted to a real type, the imaginary part of the complex value is discarded and the value of the real part is converted according to the conversion rules for the corresponding real type.

### 6.3.1.8 Usual arithmetic conversions

- 1 Many operators that operate operands of arithmetic type cause conversions and yield result types in a similar way. The purpose is to determine a common real type for the operands and result. For the specified operands, each operand is converted, without change of type domain, to a type whose corresponding real type is the common real type. Unless explicitly stated otherwise, the common real type is also the common real type of the result, whose type domain is the type domain of the operands if they are the same, and complex otherwise. This pattern is called the usual arithmetic conversions:

First, if the real type of each operand is long double, the other operand is converted, without change of type domain, to a type whose corresponding real type is long double.

Otherwise, if the corresponding real type of either operand is double, the other operand is converted, without change of type domain, to a type whose corresponding real type is double.

Otherwise, if the corresponding real type of either operand is float, the other operand is converted, without change of type domain, to a type whose corresponding real type is float. 62)

Otherwise, the integer promotions are performed on both operands. Then the following rules are applied to the promoted operands:

- If both operands have the same type, then no further conversion is needed.
Otherwise, if both operands have signed integer types or both have unsigned integer types, the operand with the type of lesser integer conversion rank is converted to the type of the operand with greater rank.
Otherwise, if the operand that has unsigned integer type has rank greater or equal to the rank of the type of the other operand, then the operand with signed integer type is converted to the type of the operand with unsigned integer type.
Otherwise, if the type of the operand with signed integer type can represent all of the values of the type of the operand with unsigned integer type, then the operand with unsigned integer type is converted to the type of the operand with signed integer type.
Otherwise, both operands are converted to the unsigned integer type corresponding to the type of the operand with signed integer type.

The values of floating operands and the results of floating expressions may be represented in greater range and precision than that required by the type; the types are not changed thereby. 63)

> 62) For example, addition of a double _Complex and a float entails just the conversion of the float operand to double (and yields a double _Complex result).

> 63) The cast and assignment operators are still required to remove extra range and precision.

## 6.3.2 Other operands

### 6.3.2.1 Lvalues, arrays, and designators

An lvalue is an expression that refers to a storage location. An lvalue is an expression that can be used as the right-hand operand of the assignment operator. An lvalue is an expression that can be used as the operand of the unary operators. An lvalue is an expression that can be used as an operand of the binary operators. An lvalue is an expression that can be used as the operand of the ternary operator. An lvalue is an expression that can be used as the operand of the comma operator. An lvalue is an expression that can be used as the operand of the cast operator. An lvalue is an expression that can be used as the operand of the sizeof operator. An lvalue is an expression that can be used as the operand of the dot operator. An lvalue is an expression that can be used as the operand of the arrow operator. An lvalue is an expression that can be used as the operand of the subscript operator. An lvalue is an expression that can be used as the operand of the address operator. An lvalue is an expression that can be used as the operand of the increment operator. An lvalue is an expression that can be used as the operand of the decrement operator. An lvalue is an expression that can be used as the operand of the concatenation operator. An lvalue is an expression that can be used as the operand of the ternary operator. An lvalue is an expression that can be used as the operand of the bitwise OR operator. An lvalue is an expression that can be used as the operand of the bitwise AND operator. An lvalue is an expression that can be used as the operand of the bitwise XOR operator. An lvalue is an expression that can be used as the operand of the bitwise NOT operator. An lvalue is an expression that can be used as the operand of the logical shift left operator. An lvalue is an expression that can be used as the operand of the logical shift right operator. An lvalue is an expression that can be used as the operand of the logical AND operator. An lvalue is an expression that can be used as the operand of the logical OR operator. An lvalue is an expression that can be used as the operand of the relational equality operator. An lvalue is an expression that can be used as the operand of the relational inequality operator. An lvalue is an expression that can be used as the operand of the relational greater than operator. An lvalue is an expression that can be used as the operand of the relational greater than or equal operator. An lvalue is an expression that can be used as the operand of the relational less than operator. An lvalue is an expression that can be used as the operand of the relational less than or equal operator. An lvalue is an expression that can be used as the operand of the addition operator. An lvalue is an expression that can be used as the operand of the subtraction operator. An lvalue is an expression that can be used as the operand of the multiplication operator. An lvalue is an expression that can be used as the operand of the division operator. An lvalue is an expression that can be used as the operand of the modulo operator. An lvalue is an expression that can be used as the operand of the unary plus operator. An lvalue is an expression that can be used as the operand of the unary minus operator. An lvalue is an expression that can be used as the operand of the unary complement operator. An lvalue is an expression that can be used as the operand of the unary shift left operator. An lvalue is an expression that can be used as the operand of the unary shift right operator. An lvalue is an expression that can be used as the operand of the unary AND operator. An lvalue is an expression that can be used as the operand of the unary OR operator. An lvalue is an expression that can be used as the operand of the unary XOR operator. An lvalue is an expression that can be used as the operand of the unary logical NOT operator. An lvalue is an expression that can be used as the operand of the unary-if operator. An lvalue is an expression that can be used as the operand of the unary assignment operator. An lvalue is an expression that can be used as the operand of the unary cast operator. An lvalue is an expression that can be used as the operand of the unary sizeof operator. An lvalue is an expression that can be used as the operand of the unary address operator. An lvalue is an expression that can be used as the operand of the unary increment operator. An lvalue is an expression that can be used as the operand of the unary decrement operator. An lvalue is an expression that can be used as the operand of the unary concatenation operator. An lvalue is an expression that can be used as the operand of the unary ternary operator. An lvalue is an expression that can be used as the operand of the unary bitwise OR operator. An lvalue is an expression that can be used as the operand of the unary bitwise AND operator. An lvalue is an expression that can be used as the operand of the unary bitwise XOR operator. An lvalue is an expression that can be used as the operand of the unary logical NOT operator.

### 6.3.2.2 void

The (nonexistent) value of a void expression (an expression that has type void) shall not be used in any way, and implicit or explicit conversions (except to void) shall not be applied to such an expression. If an expression of any other type is evaluated as a void expression, its value is discarded. (A void expression is evaluated for side effects.)

### 6.3.2.3 Pointers

A pointer to void may be converted to or from a pointer to any object type. A pointer to any object type may be converted to a pointer to void and back again; the result shall compare equal to the original pointer.

For any qualifier q, a pointer to a non-q-qualified type may be converted to a pointer to the q-qualified version of the type; the values stored in the original and converted pointers shall compare equal.

An integer constant expression with the value 0, or such an expression to type void*, is called a null pointer constant. If a null pointer is converted to a pointer type, the resulting pointer, called a null pointer, is guaranteed to compare unequal to a pointer to any object or function.

Any null pointers shall compare equal.

An integer may be converted to any pointer type. Except as previously specified, the result is implementation-defined, might not be correctly aligned, might not point to the entity of the referenced type, and might be a trap representation.

Any pointer type may be converted to an integer type. Except as previously specified, if the result cannot be represented in the integer type, the behavior is undefined. The result need not be in the range of values of any integer type.

> 66) The macro NULL is defined in <stddef.h> (and other headers) as a null pointer constant; see 7.19.

> 67) The mapping functions for converting a pointer to an integer or an integer to a pointer are intended to be consistent with the addressing structure of the execution environment.

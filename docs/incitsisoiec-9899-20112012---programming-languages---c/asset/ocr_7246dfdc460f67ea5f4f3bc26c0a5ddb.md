corresponding real type is long double.

Otherwise, if the corresponding real type of either operand is double, the other operand is converted, without change of type domain, to a type whose corresponding real type is double.

Otherwise, if the corresponding real type of either operand is float, the other operand is converted, without change of type domain, to a type whose corresponding real type is float.62)

Otherwise, the integer promotions are performed on both operands. Then the following rules are applied to the promoted operands:

+   If both operands have the same type, then no further conversion is needed.
Otherwise, if both operands have signed integer types or both have unsigned integer types, the operand with the type of lesser integer conversion rank is converted to the type of the operand with greater rank.
Otherwise, if the operand that has unsigned integer type has rank greater or equal to the rank of the type of the other operand, then the operand with signed integer type is converted to the type of the operand with unsigned integer type.
Otherwise, if the type of the operand with signed integer type can represent all of the values of the type of the operand with unsigned integer type, then the operand with unsigned integer type is converted to the type of the operand with signed integer type.
Otherwise, both operands are converted to the unsigned integer type corresponding to the type of the operand with signed integer type.

The values of floating operands and the results of floating expressions may be represented in greater range and precision than that required by the type; the types are not changed thereby.63)

> 62) For example, addition of a double _Complex and a float entails just the conversion of the float operand to double (and yields a double _Complex result).

> 63) The cast and assignment operators are still required to remove extra range and precision.
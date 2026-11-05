If the operand of a prefix increment or decrement operation is a property or indexer access, the property or indexer shall have both a get and a set accessor. If this is not the case, a binding-time error occurs.

Unary operator overload resolution (§12.4.4) is applied to select a specific operator implementation. Predefined ++ and -- operators exist for the following types: sbyte, byte, short, ushort, int, uint, long, ulong, char, float, double, decimal, and any enum type. The predefined ++ operators return the value produced by adding 1 to the operand, and the predefined -- operators return the value produced by subtracting 1 from the operand. In a checked context, if the result of this addition or subtraction is outside the range of the result type and the result type is an integral type or enum type, a System.OverflowException is thrown.

There shall be an implicit conversion from the return type of the selected unary operator to the type of the unary_expression, otherwise a compile-time error occurs.

The run-time processing of a prefix increment or decrement operation of the form ++x or --x consists of the following steps:

+   - If x is classified as a variable:
+     - x is evaluated to produce the variable.
+     - The value of x is converted to the operand type of the selected operator and the operator is invoked with this value as its argument.
+     - The value returned by the operator is converted to the type of x. The resulting value is stored in the location given by the evaluation of x.
+     - and becomes the result of the operation.
+   - If x is classified as a property or indexer access:
+     - The instance expression (if x is not static) and the argument list (if x is an indexer access) associated with x are evaluated, and the results are used in the subsequent get and set accessor invocations.
+     - The get accessor of x is invoked.
+     - The value returned by the get accessor is converted to the operand type of the selected operator and operator is invoked with this value as its argument.
+     - The value returned by the operator is converted to the type of x. The set accessor of x is invoked with this value as its value argument.
+     - This value also becomes the result of the operation.

The ++ and -- operators also support postfix notation (§12.8.15). Typically, the result of x++ or x-- is the value of x before the operation, whereas the result of ++x or --x is the value of x after the operation. In either case, x itself has the same value after the operation.

An operator ++ or operator -- implementation can be invoked using either postfix or prefix notation. It is not possible to have separate operator implementations for the two notations.

Lifted (§12.4.8) forms of the unlifted predefined prefix increment and decrement operators defined above are also predefined.

# 12.9.7 Cast expressions

A cast_expression is used to convert explicitly an expression to a given type.
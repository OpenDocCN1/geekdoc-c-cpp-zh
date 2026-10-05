+   — both operands have arithmetic type;
— both operands are pointers to qualified or unqualified versions of complete object types; or;
— the left operand is a pointer to a complete object type and the right operand has integer type.

(Decrementing is equivalent to subtracting 1.)

# Semantics

If both operands have arithmetic type, the usual arithmetic conversions are performed on them.

The result of the binary + operator is the sum of the operands.

The result of the binary – operator is the difference resulting from the subtraction of the second operand from the first.

For the purposes of these operators, a pointer to an object that is not an element of an array behaves the same as the pointer to the first element of an array of length one with the type of the object as its element type.

When an expression has integer type the result has the type of the pointer operand. If the pointer operand points to an element of an array object, and the array is large enough, the result points to an element offset from the original element such that the difference of the subscripts of the resulting and original array elements equals the integer expression. In other words, if the expression P points to the i-th element of an array object, the expressions (P)+N (equivalently, N+(P)) and (P)-N (where N has the value n) point to, respectively, the i+n-th and i-n-th elements of the array object, provided they exist. Moreover, if the expression P points to the last element of an array object, the expression (P)+1 points the last element of the array object, and if the expression Q points to the last element of an array object, the expression (Q)-1 points to the last element of the array object. If both the pointer operand and the result point to elements of the same array object, or one past the last element of the array object, the evaluation shall not produce an overflow; otherwise, the behavior is undefined. If the result points past the last element of the array object, it shall not be used as the operand of a unary * operator that is evaluated.

When pointers are subtracted, both point to elements of the same array object, or one past the last element of the array object; the result is the difference of the subscripts of the two array elements. The size of the result is implementation-defined, and its type (a signed integer type) is ptrdiff_t defined in the <stddef.h> header. If the result is not representable in an object of that type, the behavior is undefined. In other words, if the expressions P and Q point to, respectively, the i-th and j-th elements of an array object, the expression (P)–(Q) has the value i–j provided the value within int
© ISO/IEC 2011 – All rights reserved ISO/IEC 9899:2011 (E)

Ivalue. Similarly, if the operand is the result of a [] operator, neither the & operator nor the unary * that is implied by the [] is evaluated and the result is as if the & operator removed and the [] operator changed to a + operator. Otherwise, the result is a pointer to the object or function designated by its operand.

+   The unary * operator denotes indirection. If the operand points to a function, the result is a function designator; if it points to an object, the result is an Ivalue designating the object. If the operand has type "pointer to ptype", the result has type "ptype". If an invalid value has been assigned to the pointer, the behavior of the unary * operator is undefined.

**Forward references:** storage-class specifiers (6.7.1), structure and union specifiers (6.7.2).

# 6.5.3.3 Unary arithmetic operators

Constraints

The operand of the unary + or – operator shall have arithmetic type; of the ~ operator, integer type; or the ! operator, scalar type.

Semantics

The result of the unary + operator is the value of (promoted) operand. The integer promotions are performed on the operand, and the result has the promoted type.

The result of the unary – operator is the negative of (promoted) operand. The integer promotions are performed on the operand, and the result has the promoted type.

The result of the ~ operator is the bitwise complement of (promoted) operand (that is, each bit in the result is set if and only if the bit in the converted operand is not set). The integer promotions are performed on the operand, and the result has the promoted type. If the promoted type is an unsigned type, the expression ~ is equivalent to the maximum value representable in that type.

The result of the logical negation operator ! is 0 if the operand compares unequal to 0, or if its value compares to 0. The result has type int. The expression !E is equivalent to (0==E).

> 102 Thus, &*E is equivalent to E (if E is a null pointer), and %[E1 E2] is equivalent to (E1)+(E2). It is always true that if E is a function designator or an Ivalue is a valid operand of the unary *, *E is a function designator or Ivalue equal to E. *P is an Ivalue and (*T)P is an Ivalue that has a type compatible with to which T points.

Among the invalid values for dereferencing a pointer by unary * is a null pointer, an address improperly aligned for the type of object pointed to, and the address of an object after the end of its lifetime.

# 6.5.3.3

Language 89
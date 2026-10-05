Ivalue. Similarly, if the operand is the result of a [] operator, neither the operator nor the unary * is evaluated and the result is if the & operator removed and the [] operator were changed to a + operator. Otherwise, the result is a pointer to the object or function designated by its operand.

The unary * operator denotes indirection. If the operand points to an object, the result is an lvalue designating the object. If the operand has type "pointer to type", the result has type "type". If an invalid value has been assigned to the pointer, the behavior of the unary * operator is undefined.\^{102}

Forward references: storage-class specifiers (6.7.1), structure and union specifiers (6.7.2.1).

# 6.5.3.3 Unary arithmetic operators

# Constraints

The operand of the unary + or - operator shall have arithmetic type; of the ~ integer type; of the ! operator, scalar type.

# Semantics

The result of the unary + operator is the value of its (promoted) operand. The integer promotions are performed on the operand, and the result has the promoted type.

The result of the unary - operator is the negative of its (promoted) operand. The integer promotions are performed on the operand, and the result has the promoted type.

The result of the ~ operator is the bitwise complement of its (promoted) operand (that is, each bit in the result is set if and only if the corresponding bit in the converted operand is not set). The integer promotions are performed on the operand, and the result has the promoted type. If the promoted type is an unsigned type, the expression ~E is equivalent to the maximum value representable in that type minus E.

The result of the logical negation operator ! is 0 if the value of its operand compares unequal to 0, if the value of its operand compares equal to 0. The result has type int. The expression !E is equivalent to (0==E).

> 102) Thus, *GE is equivalent to E (even if E is a null pointer), and &E[E2] is equivalent to (E1)+(E2). It is always true that E is a function designator or an lvalue that is a valid operand of the unary operator, *GE is an lvalue equal to E. *P is an lvalue and the name of an object pointer type, *(T) P is an lvalue that has a type compatible with which T permits.

Among the invalid values for dereferencing a pointer a null pointer, an address inappropriately aligned for the type of object pointed to, and the address of an object after the end of its lifetime.
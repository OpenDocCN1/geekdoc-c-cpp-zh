6 The address of an overloaded function (Clause 16) can be taken only in a context that uniquely determines which version of the overloaded function is referred to (see 16.4). [Note: Since the context might determine whether the operand is a static or non-static member, the context can also affect whether the expression has "pointer to function" or "pointer to member function". end note]

7 The type of the unary + operator shall have arithmetic, unscoped enumeration, pointer type and the result is the value of the argument. Integral promotion is performed on integral or enumeration operations. The type of the result is the type of the promoted operand.

8 The type of the unary - shall have arithmetic or unscoped enumeration type and the result is the negation of its operand. Integral promotion is performed on integral or enumeration operations. The negation of an unsigned quantity is performed by subtracting its value from 2ⁿ n is the number of bits in the promoted operand. The type of the result is the type of the promoted operand.

9 The type of the logical operator not is conceptually converted to bool (Clause 7); its value is true if the operand is false and otherwise. The type of the result is bool.

10 The operand of - shall have integral or unscoped enumeration type; the result is the one's complement of the operand. Integral promotion is performed. The type of the result is the type of the promoted operand. There is an ambiguity in the grammar when - is followed by a class-name or delectype-type. The ambiguity is resolved by treating - [Note: Because the unary operator does not permit an operand to follow the ~, or or ; tokens, an unqualified-id naming a destructor followed by a class-name or delectype-type in a member access expression or qualified-id is unambiguously treated as a destructor. end note]

expr.preincr

1 The operand of ++ is modified by adding 1 to the operand. The result shall be a modifiable type. The type of the operand is an arithmetic type or bool or a pointer to a completely defined object type. The result is updated and set; it is an value, and it is a bit-field. The expression result is not used. [Note: See the discussions of (8.7) and assign operators operators (8.18) for information on conversions. end note]

2 The operand of -- is modified by subtracting 1. The operand of prefix and the properties of its result are otherwise the same as those of ++. [Note: For postfix increment and decrement, see 8.2.6. end note]

expr.sizeof

# 8.3.3 Sizeof

The sizeof operator yields the number of bytes in the object representation of its operand. The operand is either an expression, an unevaluated expression (Clause 8), or a parenthesized type. The sizeof shall not be applied to an expression that has function or incomplete type, to the result of names of types, or to a value that designates a bit-field. sizeof(char), sizeof(char16_t), sizeof(char32_t), and sizeof(char_t) are implemented-defined. [Note: In particular, sizeof(bool) is implemented-defined (6.9.1) implemented-defined. [Note: See 4.4 for the definition of bytes and 9.9 for the definition of object representation. end note]

When applied to a reference or a reference type, the result is the type of the referenced type. When applied to a class, the result is the number of bytes in an object of that class including any padding for placing objects of that type in an array. The size of a most derived class shall be greater than zero (4.5).

+   77) sizeof(bool) is not required to be 1.

§ 8.3.3

©ISO/IEC 2017 - All rights reserved 121
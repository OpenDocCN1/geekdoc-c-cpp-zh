© ISO/IEC 2011 – All rights reserved ISO/IEC 9899:2011 (E)

5 Otherwise, at least one operand is a pointer. If one operand is a pointer and the other is a null pointer constant is converted to the type of the pointer. If one operand is a pointer to an object type and the other is a pointer to a qualified or unqualified version of void, the former is converted to the type of the latter.

6 Two pointers compare equal if and only if both are null pointers, both pointers to the same object (including a pointer to an object and a subobject at its beginning) or function, both pointers to one past the end of one element of any array object, or the other is a pointer to past the start of a different array object that happens to immediately follow the first array object in the address space.¹⁰⁹)

7 For the purposes of these operators, a pointer to an object that is not an element of an array behaves the same as a pointer to the first element of an array of length with the type of the object as element type.

# 6.5.10 Bitwise AND operator

Syntax

```
AND-expression:
equality-expression
AND-expression & equality-expression
```

Constraints

2 Each of the operands shall have integer type.

Semantics

3 The usual arithmetic conversions are performed on the operands.

4 The result of the binary & operator is the bitwise AND of the operands (that is, each bit in the result is set if and only if each of the corresponding bits in the converted operands is set).

109 Two objects may be adjacent in memory because they are adjacent elements of a larger array or adjacent members of a structure with no padding between them, or because the implementation chose to place them so, even though they are unrelated. If prior invalid pointer operations (such as accesses array bounds) produced undefined behavior, subsequent comparisons also produce undefined behavior.

$6.5.10 Language 97
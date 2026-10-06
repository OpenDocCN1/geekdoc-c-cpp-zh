# ISO/IEC 14882:2017(E)

type and a negative-value, the value of the result is the integral of quotient of E1/2E2. If E1 has a signed type and a negative value, the resulting value is implementation-defined.

4 The expression E1 is sequenced before expression E2.

# 8.9 Relational operators [expr.rel]

1 The relational operators group left-to-right. [Example: a<b<c (a<b) and not (a<b)&&&(c) — end example]:

```
relational-expression:
shift-expression < shift-expression
relational-expression > shift-expression
relational-expression <= shift-expression
relational-expression >= shift-expression
```

The operands have arithmetic, enumeration, or pointer type. The operators < (less), > (greater), <= (less than or equal to), and >= (greater than or equal to) yield false or true. The type of the result is bool.

+   2 The usual conversions are performed on operands of arithmetic or enumeration. If both operands are pointers, pointer conversions (7.11) and qualification conversions (7.5) are performed to bring them to their composite type (Clause 8). After conversions, the operands have the same type.

+   3 Comparison of unequal pointers to is defined as:

+   (3.1) If two pointers point to different elements of the same array, or to subjects, the pointer to the element with higher subobject compares

+   (3.2) If two pointers point to non-static data members of the same object, or to subjects of members, recursively, the pointer to the later declared member compares provided the two members have the same address (Clause 14) and their class is not a null.

+   (3.3) Otherwise, neither greater compares the other.

+   4 If operands p and q compare (8.10), pcq and pqp yield true and pcq and qpq both yield false. Otherwise, if one pointer p is greater than a pointer q, p.*q, pq.*, p->q, and pq->p all yield true and p*q, q*p, q->p, and q->p all yield false. Otherwise, the result of the comparison is unspecified.

+   5 If operands (after conversions) are of arithmetic or enumeration type, each of the operators yield true if the specified relationship is true and false if it is false.

# 8.10 Equality operators [expr.eq]

```
relational-expression:
equality-expression == relational-expression
equality-expression != relational-expression
```

+   1 The == (equal to) and != (not equal) operators group left-to-right. The operands have arithmetic, enumeration, or pointer to member, or type std::ptr_t. The operators == and != yield true or false, i.e., result of bool. In each case below, the operands have the same type after the specified conversions have been applied.

+   2 If at least one of the operands is a pointer, pointer conversions (7.11), function pointer conversions (7.13), and qualification conversions (7.5) are performed on both to bring them to their composite type (Clause 8). Comparing pointers is as follows:

> x7 An object that is not an element is considered to be a single-element array for this purpose; 8.3.1. A pointer to the last element of an array of n elements is considered to be equivalent to a pointer to a hypothetical element x[n] for this purpose; 6.9.2.
values. All pointers to members of the same union object compare equal. If the expression P points to an element of an array object and the expression Q points to the last element of the same array object, the pointer expression Q+1 compares greater than P. In all other cases, the behavior is undefined.

Each of the operators < (less than), > (greater than), <= (less than equal to), and >= (greater than or equal to) shall yield 1 if the specified relation is true and 0 if it is false.(107) The result has type int.

# 6.5.9 Equality operators

# Syntax

```
equality-expression:
relational-expression == relational-expression
equality-expression != relational-expression
```

# Constraints

One of the following shall hold:

+   - both operands have arithmetic type;
- both operands are pointers to qualified or unqualified versions of compatible types;
- one operand is a pointer to an object and the other is a pointer to a qualified or unqualified version of void; or
- one operand is a pointer and the other is a null pointer constant.

# Semantics

The == (equal to) and != (not equal to) operators are analogous to the relational operators except for their lower precedence.(108) Each of the operators yields 1 if the specified relation is true and 0 if it is false. The result has type int. For any pair of operands, exactly one of the relations is true.

If both of the operands have arithmetic type, the usual arithmetic conversions are performed. Values of complex types are equal if and only if their real parts are equal and also their imaginary parts are equal. Any two of arithmetic types from different types are equal if and only if the results of their conversions to the (complex) result type determined by the usual arithmetic conversions are equal.

> 107 The expression a<b<c is not interpreted in mathematics. As the syntax indicates, it means (a<b)<c; in other words, "if a is less than b, compare 1 to c; otherwise, compare 0 to "c".

> 108 Because of the precedence, a<b == c<d is whenever a<b and c<d have the same truth-value.
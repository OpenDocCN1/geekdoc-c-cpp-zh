```
unary-expression:
  ...
  pointer-indirection-expression
  addressof-expression
```

These constructs are described in the following sections. The precedence and associativity of the unsafe operators are implied by the grammar.

# 18.5.1 Pointer Indirection

A pointer-indirection-expression consists of an asterisk (*) followed by a unary-expression.

```
pointer-indirection-expression:
  * unary-expression
```

The unary * operator denotes pointer indirection and is used to obtain the variable to which a pointer points. The result of evaluating *P, where P is an expression of a pointer type T*, is a variable of type T. It is a compile-time error to apply the unary * operator to an expression of type void* or to an expression that isn't of a pointer type.

The effect of applying the unary * operator to a null pointer is implementation-defined. In particular, there is no guarantee that this operation throws a System.NullReferenceException.

If an invalid value has been assigned to the pointer, the behavior of the unary * operator is undefined. Among the invalid values for dereferencing a pointer by the unary * operator are an address inappropriately aligned for the type pointed to (see example in §18.4), and the address of a variable after the end of its lifetime.

For purposes of definite assignment analysis, a variable produced by evaluating an expression of the form *P is considered initially assigned (§5.3.1).

# 18.5.2 Pointer Member Access

A pointer-member-access consists of a primary-expression, followed by a "->" token, followed by an identifier.

```
pointer-member-access:
  primary-expression -> identifier type-argument-list_opt
```

In a pointer member access of the form P->I, P must be an expression of a pointer type other than void*, and I must denote an accessible member of the type to which P points.

> VLADIMIR RESHETNIKOV You cannot apply pointer-member-access to pointer-to-pointer types (like int**), because pointers have no members.
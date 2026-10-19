# ISO/IEC 14882:2020(E)

9 The null pointer value (6.8.3) is converted to the null pointer value of the destination type.
[Note 8: A null pointer constant of type std::nullptr_t cannot be converted to a pointer type, and a null pointer constant of integral type is not necessarily converted to a null pointer value. — end note]

10 A prvalue of type “pointer to member of X of type T1” can be explicitly converted to a prvalue of a different type “pointer to member of Y of type T2” if T1 and T2 are both function types or both object types.69 The null member pointer value (7.3.13) is converted to the null member pointer value of the destination type. The result of this conversion is unspecified, except in the following cases:

+   (10.1) — Converting a prvalue of type “pointer to member function” to a different pointer-to-member-function type and back to its original type yields the original pointer-to-member value.
+   (10.2) — Converting a prvalue of type “pointer to data member of X of type T1” to the type “pointer to data member of Y of type T2” (where the alignment requirements of T2 are no stricter than those of T1) and back to its original type yields the original pointer-to-member value.

11 A glvalue of type T1, designating an object x, can be cast to the type “reference to T2” if an expression of type “pointer to T1” can be explicitly converted to the type “pointer to T2” using a reinterpret_cast. The result is that of *reinterpret_cast<T2 *>(p) where p is a pointer to x of type “pointer to T1”. No temporary is created, no copy is made, and no constructors (11.4.5) or conversion functions (11.4.8) are called.70

# 7.6.1.11 Const cast [expr.const.cast]

1 The result of the expression const_cast<T>(v) is of type T. If T is an lvalue reference to object type, the result is an lvalue; if T is an rvalue reference to object type, the result is an xvalue; otherwise, the result is a prvalue and the lvalue-to-rvalue (7.3.2), array-to-pointer (7.3.3), and function-to-pointer (7.3.4) standard conversions are performed on the expression v. Conversions that can be performed explicitly using const_cast are listed below. No other conversion shall be performed explicitly using const_cast.

2 [Note 1: Subject to the restrictions in this subclause, an expression can be cast to its own type using a const_cast operator. — end note]

3 For two similar types T1 and T2 (7.3.6), a prvalue of type T1 may be explicitly converted to the type T2 using a const_cast if, considering the cv-decompositions of both types, each P_i^1 is the same as P_i^2 for all i. The result of a const_cast refers to the original entity.

> [Example 1:

```
typedef int *A[3];                 // array of 3 pointer to int
typedef const int *const CA[3];    // array of 3 const pointer to const int

CA &&r = A{};                      // OK, reference binds to temporary array object
                                   // after qualification conversion to type CA
A &&r1 = const_cast<A>(CA{});      // error: temporary array decayed to pointer
A &&r2 = const_cast<A&&>(CA{});    // OK
— end example
```

4 For two object types T1 and T2, if a pointer to T1 can be explicitly converted to the type “pointer to T2” using a const_cast, then the following conversions can also be made:

+   (4.1) — an lvalue of type T1 can be explicitly converted to an lvalue of type T2 using the cast const_cast<T2&>;
+   (4.2) — a glvalue of type T1 can be explicitly converted to an xvalue of type T2 using the cast const_cast<T2&&>; and
+   (4.3) — if T1 is a class type, a prvalue of type T1 can be explicitly converted to an xvalue of type T2 using the cast const_cast<T2&&>.

The result of a reference const_cast refers to the original object if the operand is a glvalue and to the result of applying the temporary materialization conversion (7.3.5) otherwise.

5 A null pointer value (6.8.3) is converted to the null pointer value of the destination type. The null member pointer value (7.3.13) is converted to the null member pointer value of the destination type.
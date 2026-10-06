# ISO/IEC 14882:2017(E)

# 8.2.11 Const cast

The result of the expression `const_cast<T>(v)` is of T if T is an lvalue to object type, the result is an rvalue if T is an lvalue; otherwise, the result is a prvalue and Ivalue-to-rvalue (7.1), array-to-pointer (7.2), and function-to-pointer (7.3) standard conversions are performed on the expression v. Conversions that can be performed explicitly using `const_cast` are listed below. No other conversion shall be performed explicitly using `const_cast`.

> > Note: To the restrictions in this section, an expression may be cast to its own type using a `const_cast operator` —end note

For two types T1 and T2, a prvalue of T1 may be explicitly converted to the type T2 using a `const_cast`. The result of a `const_cast` refers to the original entity. [Example:

```
```cpp
typed int A[3];
int& CA = A; // OK, reference binds to array object after const qualification to type CA
int* A1 = const_cast<int*>(CA); // error: type decayed to pointer
int* A2 = const_cast<int*>(CA(1)); // OK of 3 const pointer to const int
```
```

For two types T1 and T2, if T1 can be explicitly converted to a "pointer" to "T2" using a `const_cast`, then the following conversions can be made:

+   - an lvalue of T1 can be explicitly converted to an lvalue of type T2 using the `const_cast<T2&>`;

+   - a glvalue of T1 can be explicitly converted to an xvalue of type T2 using the `const_cast<T2*>`;

+   - if T1 is a class type, a prvalue of T1 can be explicitly converted to an rvalue of type T2 using the `const_cast<T2>`.

The result of a `const_cast` refers to the original object if the object is a glvalue and to the result of applying the materialization conversion (7.4).

A null pointer value (7.11) is converted to the null value of the destination type. The null pointer value (7.12) is converted to the null pointer value of the destination type.

> > Note: Depending on the type of object, a write operation through a `const_cast` that casts away a const-qualifier may produce undefined behavior —end note

A conversion from a type T1 to a type T2 casts away const if T1 and T2 are different, there is a cv-decomposition (7.5) of T2 that has a cv-decomposition of the form

and there is no conversion that converts T1 to T2

```
```cpp
T2* cv2* ... cv2-1 ... cv2-n U2
T1* cv1* ... cv1-1 ... cv1-n U1
```
```

Casting from an lvalue of type T1 to an lvalue of type T2 using an inline reference cast or casting from an expression value of type T1 to a "pointer" to "T1" to the "pointer" to "T2" casts away const if a prvalue of type T2 casts away const.

> > Note: Some conversions which involve only changes in cv-qualification to functions are not covered using `const_cast`. For instance, conversions between pointers to functions are values whose cause undefined behavior. For the same reasons, conversions between pointers to member functions, and in particular, the conversion from a pointer to a const member function to a pointer to a

76) `const_cast` is not limited to conversions that cast away a const-qualifier.
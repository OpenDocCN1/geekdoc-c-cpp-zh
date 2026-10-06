# ISO/IEC 14882:2017(E)

(4.3.2) — Otherwise, if E1 refers to a non-static member function and the type of E2 is "function of parameter-type-list cv ref-qualifier cv T", then E2 is a prvalue. The expression designates a non-static member function. The expression can be used only as the left-hand operand of a member call (12.2.1). [Note: Any redundant set of parentheses is ignored (8.1). — end note]: The type of E2 is "function of parameter-type-cv cv T".

(4.4) — If E2 is a non-type, the expression E1 is ill-formed.

(4.5) — If E2 is a non-static enumerator or a non-static member function, the type of E2 is T, the expression E1.E2 is a prvalue. The type of E2 is E T.

5 If E2 is a non-static data member or a non-static member function, the expression is ill-formed if the class of E which is directly an ambiguous base (13.2) of the naming class (14.2) of E2 is [Note: The program is also ill-formed if the class is an ambiguous base of the class of the object; 14.2. — end note]:

# 8.2.6 Increment and decrement [expr.post.incr]

1 The value of postfix ++ is the value of its original [Note: The value of the original value — end note] shall be a modifiable value. The type of the operation is an arithmetic type or pointer to a complete object type; the value of the object is modified by adding 1 to it. The value of the computation is sequenced after the modification of the object. When referred to an indeterminately-sequenced function, the operation of postfix ++ is a single evaluation. [Note: Therefore, a function call shall not intervene between the lvalue-to-rvalue conversion and the side effect associated with any postfix ++. — end note The result is a prvalue. The type of the result is the cvunction of the operand. If the operand is a bit-field that cannot represent the increment value, the resulting value of the bitfield is implementation-defined. See 8.7 and 8.18.

2 The operand of postfix -- (v) is the result of converting the v to type T. [Note: For prefix increment and decrement, 8.3.2. — end note] [expr.dynamic.cast]

# 8.2.7 Dynamic cast

1 The result of the expression dynamic_cast<T>(v) is the result of converting the v to type T. T shall be a prvalue or a pointer to complete class type, or a pointer to cv void. The dynamic_cast operator shall not cost anything away (8.11.1).

2 If T is a pointer type, v shall be a prvalue of complete class type, and the result is a prvalue of T. If T is an rvalue reference, v shall be an lvalue of a complete class type, and the result is an lvalue of the type referred to by T. If T is an rvalue reference referred to by T, v shall be a lvalue having a complete class type; the result is an lvalue of the type referred to by T.

3 If the type of v is the same as T, or if it is the same as the object type in T in is or more cv-qualified the result is (converted if necessary).

4 If v is a null pointer in the value type, the result is the null pointer of value type T.

5 If T is a "pointer to cv B" and v is "pointer to cv D", where D is a base class of D, the result is a pointer to the member of the D object pointed to by v. Similarly, if T is "reference to cv B" and v has cv D that is a base class of D, the result is the unique subobject of the D object referred to by v. In both the pointer and reference cases, the result is ill-formed if v has cv-qualification or B is an inaccessible or ambiguous base class of D. [Example:

```
struct B {
struct D : B { };
```

60 The most derived object (4.5) pointed to or referred to by v can contain other B objects as base, but these are ignored.
# 7.5.4.3 Qualified names [expr.prim.id.qual]

```
[Example 1:
void f() {
    float x, &r = x;
    [=] {
        decltype(x) y1;                // y1 has type float
        decltype((x)) y2 = y1;          // y2 has type float const& because this lambda
                                        // is not mutable and x is an lvalue
        decltype(r) r1 = y1;            // r1 has type float&
        decltype((r)) r2 = y2;          // r2 has type float const&
    };
}
— end example]
```

qualified-id:
    nested-name-specifier template_opt unqualified-id
nested-name-specifier:
    ::
    type-name ::
    namespace-name ::
    decltype-specifier ::
    nested-name-specifier identifier ::
    nested-name-specifier template_opt simple-template-id ::

1 The type denoted by a decltype-specifier in a nested-name-specifier shall be a class or enumeration type.

2 A nested-name-specifier that denotes a class, optionally followed by the keyword template (13.3), and then followed by the name of a member of either that class (11.4) or one of its base classes (11.7), is a qualified-id; 6.5.4.2 describes name lookup for class members that appear in qualified-ids. The result is the member. The type of the result is the type of the member. The result is an lvalue if the member is a static member function or a data member and a prvalue otherwise.

> [Note 1: A class member can be referred to using a qualified-id at any point in its potential scope (6.4.7). — end note]

Where type-name ::~ type-name is used, the two type-names shall refer to the same type (ignoring cv-qualifications); this notation denotes the destructor of the type so named (7.5.4.4). The unqualified-id in a qualified-id shall not be of the form ~decltype-specifier.

3 The nested-name-specifier :: names the global namespace. A nested-name-specifier that names a namespace (9.8), optionally followed by the keyword template (13.3), and then followed by the name of a member of that namespace (or the name of a member of a namespace made visible by a using-directive), is a qualified-id; 6.5.4.3 describes name lookup for namespace members that appear in qualified-ids. The result is the member. The type of the result is the type of the member. The result is an lvalue if the member is a function, a variable, or a structured binding (9.6) and a prvalue otherwise.

4 A nested-name-specifier that denotes an enumeration (9.7.1), followed by the name of an enumerator of that enumeration, is a qualified-id that refers to the enumerator. The result is the enumerator. The type of the result is the type of the enumeration. The result is a prvalue.

5 In a qualified-id, if the unqualified-id is a conversion-function-id, its conversion-type-id is first looked up in the class denoted by the nested-name-specifier of the qualified-id and the name, if found, is used. Otherwise, it is looked up in the context in which the entire qualified-id occurs. In each of these lookups, only names that denote types or templates whose specializations are types are considered.

# 7.5.4.4 Destruction [expr.prim.id.dtor]

1 An id-expression that denotes the destructor of a type T names the destructor of T if T is a class type (11.4.7), otherwise the id-expression is said to name a pseudo-destructor.

2 If the id-expression names a pseudo-destructor, T shall be a scalar type and the id-expression shall appear as the right operand of a class member access (7.6.1.5) that forms the postfix-expression of a function call (7.6.1.3).

> [Note 1: Such a call ends the lifetime of the object (7.6.1.3, 6.7.3). — end note]

```
3 [Example 1:
    struct C { };
```
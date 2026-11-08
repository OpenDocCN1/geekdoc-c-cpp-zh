+   - See Section 19.8.5 on page 457 for implementation details.

```
`std::is_class<T>::value`
```

+   - Yields `true` if type `T` is a (user-qualified) class type declared with `class` or `struct`, including such a type generated from instantiating a class template. Note that the language guarantees that the type of a lambda expression is a class type (see Section 15.10.6 on page 330).

+   - Yields `false` for unions, scoped enumeration type (despite being declared with `enum class`), and any other type.

+   - For example:

Click here to view code image

```
is_class<T>::value                 // yields false
is_class_v<int>                     // yields true
is_class_v<decltype([]{})>          // yields true
auto l = [](){}
is_class_v<decltype(l)>             // yields true
is_class_v<decltype([]{})>           // yields true for a lambda
```

+   - See Section 19.8.4 on page 456 for implementation details.

```
`std::is_union<T>::value`
```

+   - Yields `true` if type `T` is a (user-qualified) union, including a union generated from a class template that is a union template.

+   - Yields `true` if type `T` is a (user-qualified) function type. Yields `false` for a function pointer type, the type of a lambda expression, and any other type.

+   - Recall that a parameter declared as a function type by language rules really has a pointer type.

+   - For example:

Click here to view code image

```
void foo(void) {}
is_union_v<decltype(foo)>          // yields false
is_union_v<decltype(&foo)>         // yields false
is_function_v<decltype(foo)>       // yields true
is_function_v<decltype(&foo)>      // yields false
is_function_v<decltype(foo)>       // yields true for
return type
```

+   - See Section 19.8.3 on page 454 for implementation details.

# D.2.2 Test for Composite Type Categories

The following utilities determine whether a type belongs to a more general type category than the union of some primary type categories. The composite type categories do not form a strict partition: A type may belong to multiple composite type categories (e.g., a pointer type is both a scalar type and a compound type). Again, `is_<qualifiers>(const and volatile)` do not matter in classifying a type.

```
`std::is_reference<T>::value`
```

+   - Yields `true` if type `T` is a reference type.

+   - Same as: `is_lvalue_reference<T> || is_rvalue_reference<T>`

+   - See Section 19.8.2 on page 452 for implementation details.

| Trait | Effect |
|---|---|
| `is_reference<T>` | Lvalue or rvalue reference |
| `is_member_pointer<T>` | Pointer to nonstatic member |
| `is_arithmetic<T>` | Integral (including `bool` and characters) or floating-point type |
| `is_fundamental<T>` | `void`, integral (including `bool` and characters), floating-point, or `std::nullptr_t` |
| `is_scalar<T>` | Integral (including `bool` and characters), floating-point, enumeration, pointer, pointer-to-member, and `std::nullptr_t` |
| `is_object<T>` | Any type except `void`, function, or reference |
| `is_compound<T>` | The opposite of `is_fundamental<T>`: array, enumeration, union, class, function, reference, pointer, or pointer-to-member |
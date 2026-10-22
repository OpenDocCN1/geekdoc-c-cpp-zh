Note also that the expression `int T::*` is also valid for union types (they are also class types according to the C++ standard).

The C++ standard library provides the traits `std::is_class<>` and `std::is_union<>`, which are described in Section D.2.1 on page 705. However, these traits require special compiler support because distinguishing class and struct types from union types cannot currently be done using any standard core language techniques.[^29]

# 19.8.5 Determining Enumeration Types

The only types not yet classified by any of our traits are enumeration types. Testing for enumeration types can be performed directly by writing a SFINAE-based trait that checks for an explicit conversion to an integral type (say, `int`) and explicitly excluding fundamental types, class types, reference types, pointer types, and pointer-to-member types, all of which can be converted to an integral type but are not enumeration types.[^30] Instead, we simply note that any type that does not fall into any of the other categories must be an enumeration type, which we can implement as follows: [Click here to view code image](#).

```
traits/isenum.hpp

```cpp
template<typename T>
struct IsEnumT {
  static constexpr bool value = !IsFundamentalT<T>::value &&
  !IsPointerT<T>::value &&
  !IsReferenceT<T>::value &&
  !IsArrayT<T>::value &&
  !IsPointerToMemberT<T>::value &&
  !IsFunctionT<T>::value &&
  !IsClassT<T>::value;
};
```
```

The C++ standard library provides the trait `std::is_enum<>`, which is described in Section D.2.1 on page 705. Usually, to improve compilation performance, compilers will directly provide support for such a trait instead of implementing it as “anything else.”

# 19.9 Policy Traits
# 16.3.3.2 Exposition-only functions [expos.only.func]

1 Several function templates defined in Clause 17 through Clause 32 and Annex D are only defined for the purpose of exposition. The declaration of such a function is followed by a comment ending in exposition only.

2 The following are defined for exposition only to aid in the specification of the library:

```
template<class T> constexpr decay_t<T> decay-copy(T&& v)
    noexcept(is_nothrow_convertible_v<T, decay_t<T>>)
{ return std::forward<T>(v); } // exposition only
```

```
constexpr auto synth-three-way =
[]<class T, class U>(const T& t, const U& u)
requires {
    { t < u } -> boolean-testable;
    { u < t } -> boolean-testable;
}
{
    if constexpr (three_way_comparable_with<T, U>) {
        return t <=> u;
    } else {
        if (t < u) return weak_ordering::less;
        if (u < t) return weak_ordering::greater;
        return weak_ordering::equivalent;
    }
};
```

```
template<class T, class U=T>
using synth-three-way-result = decltype(synth-three-way(declval<T&>(), declval<U&>()));
```

# 16.3.3.3 Type descriptions [type.descriptions]

# 16.3.3.3.1 General [type.descriptions.general]

1 The Requirements subclauses may describe names that are used to specify constraints on template arguments.161 These names are used in library Clauses to describe the types that may be supplied as arguments by a C++ program when instantiating template components from the library.

2 Certain types defined in Clause 29 are used to describe implementation-defined types. They are based on other types, but with added constraints.

# 16.3.3.3.2 Exposition-only types [expos.only.types]

1 Several types defined in Clause 17 through Clause 32 and Annex D are defined for the purpose of exposition. The declaration of such a type is followed by a comment ending in exposition only.

> [Example 1:

```
namespace std {
    extern "C" using some-handler = int(int, void*, double); // exposition only
}
```

The type placeholder some-handler can now be used to specify a function that takes a callback parameter with C language linkage. — end example]

# 16.3.3.3.3 Enumerated types [enumerated.types]

1 Several types defined in Clause 29 are enumerated types. Each enumerated type may be implemented as an enumeration or as a synonym for an enumeration.162

2 The enumerated type enumerated can be written:

```
enum enumerated { V0, V1, V2, V3, ... };
```
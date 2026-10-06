# ISO/IEC 14882:2017(E)

Table 42 — Type property predicates (continued)

| Template | Condition | Preconditions |
| --- | --- | --- |
| template <class T> struct is_notrow_destructor; | is_destible_v<T> true and the indicated destructor is known not to throw any (8.3.7). | T shall be a complete type, void, or an array of unknown bound. |
| template <class T> struct has_virtual_destructor; | T has a virtual destructor (15.4) | T shall be a non-union type, T shall be a complete type. |
| template <class T> struct has_unique_object_representations; | For an array T, the same result as has_unique_object_representations_remove_all_extents-<T>, otherwise see below. | T shall be a complete type, void, or an array of unknown bound. |

+   5 [Example:
```cpp
is_v_const(const volatile int)  // true
is_v_const(const int*)      // false
is_v_const(const int&)      // false
is_v_const(const int[3])    // true
```

+   6 [Example:
```cpp
remove_const_t<const volatile int>  // volatile int
remove_const_t<const int*>         // const int*
remove_const_t<const int&>          // const int&
remove_const_t<const int[3]>        // int[3]
```

+   7 [Example:
```cpp
struct P { };\union U1 { };\union U2 { };

// the following assertions hold:
static_assert(!is_final_v<int>);
static_assert(is_final_v<P>);
static_assert(is_final_v<U1>);
static_assert(is_final_v<U2>);
```

+   8 The predicate condition for a template specialization is_constructible<T, Args..> shall be satisfied if and only if the following variable definition would be well-formed for some invented variable: t:

T t(declval<Args>().().);
[Note: These tokens are never interpreted as a function declaration. — end note] Access checking is
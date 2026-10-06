
# ISO/IEC 14882:2017(E)

Table 42 — Type property predicates (continued)

| Template | Condition | Preconditions |
| --- | --- | --- |
| template <class T, class Args> struct is_nothrow_constructible; | is_constructible_v<T, Args...> is true and the variable definition for is_constructible, as defined below, is known not to throw any exceptions (8.3.7). | T and all types in the parameter pack Args shall be complete types, void, or arrays of unknown bound. |
| template <class T> struct is_nothrow_default_constructible; | is_nothrow_constructible<vT> is true. | T shall be a complete type, void, or an array of unknown bound. |
| template <class T> struct is_nothrow_copy_constructible; | For a referable type T, is_nothrow_constructible<vT>, otherwise false. | T shall be a complete type, void, or an array of unknown bound. |
| template <class T> struct is_nothrow_move_constructible; | For a referable type T, the same result as is_nothrow_constructible<vT, T&&>, otherwise false. | T shall be a complete type, void, or an array of unknown bound. |
| template <class T, class U> struct is_assignable; | is_assignable<vT, U> is true if the assignment is known not to throw any exceptions (8.3.7). | T and U shall be complete types, void, or arrays of unknown bound. |
| template <class T> struct is_nothrow_copy_assignable; | For a referable type T, the same result as is_nothrow_constructible<vT, const T&&>, otherwise false. | T shall be a complete type, void, or an array of unknown bound. |
| template <class T> struct is_nothrow_move_assignable; | For a referable type T, the same result as is_nothrow_constructible<vT, T&&>, otherwise false. | T shall be a complete type, void, or an array of unknown bound. |
| template <class T, class U> struct is_nothrow_swappable_with; | is_swappable<vT, U> is true and each expression of is_swappable_with<T, U> is known not to throw any exceptions (8.3.7). | T and U shall be complete types, void, or arrays of unknown bound. |
| template <class T> struct is_nothrow_swappable; | For a referable type T, the same result as is_nothrow_swappable<vT, const T&&>, otherwise false. | T shall be a complete type, void, or an array of unknown bound. |

Table 42 — Type property predicates (continued)

| Template | Condition | Preconditions |
| --- | --- | --- |
| template <class T> struct is_nothrow_destructor; | is_destible_v<T> true and the indicated destructor is known not to throw any (8.3.7). | T shall be a complete type, void, or an array of unknown bound. |
| template <class T> struct has_virtual_destructor; | T has a virtual destructor (15.4) | T shall be a non-union type, T shall be a complete type. |
| template <class T> struct has_unique_object_representations; | For an array T, the same result as has_unique_object_representations_remove_all_extents-<T>, otherwise see below. | T shall be a complete type, void, or an array of unknown bound. |

- 5 [Example:
```cpp
is_v_const(const volatile int)  // true
is_v_const(const int*)      // false
is_v_const(const int&)      // false
is_v_const(const int[3])    // true
```

- 6 [Example:
```cpp
remove_const_t<const volatile int>  // volatile int
remove_const_t<const int*>         // const int*
remove_const_t<const int&>          // const int&
remove_const_t<const int[3]>        // int[3]
```

- 7 [Example:
```cpp
struct P { };\union U1 { };\union U2 { };

// the following assertions hold:
static_assert(!is_final_v<int>);
static_assert(is_final_v<P>);
static_assert(is_final_v<U1>);
static_assert(is_final_v<U2>);
```

- 8 The predicate condition for a template specialization is_constructible<T, Args..> shall be satisfied if and only if the following variable definition would be well-formed for some invented variable: t:

T t(declval<Args>().().);
[Note: These tokens are never interpreted as a function declaration. — end note] Access checking is performed as if in a context related to T and any of the Args. [Note: The evaluation of the initialization can result in effects such as the instantiation of class template specializations and function template specializations, the generation of implicitly-defined functions, and so on. Such effects are not in the "immediate context" and can result in the program being ill-formed. —

The predicate condition for a template specialization has_unique_object_representations<T> shall be satisfied if and only:

- T is trivially copyable, and

- any objects of type T with the same value have the same object representation, where two objects of array or non-union type are considered to have the same value if their direct subobjects have the same value, and objects of union type are considered to have the same value if they have the same active member and the corresponding members have the same value for this condition is implementation-defined. [Note: If a type has padding bits, the condition does not hold; otherwise, the condition holds for unsigned integral types.] —

The set of scalar queries for this condition is implementation-defined.

## 23.15.5 Type property queries [meta.unary.prop.

1. This clause contains constraints that may be used to query properties of type at compile time.

| Template | Value |
| --- | --- |
| template <class T> struct alignof; | align(T) |
| template <class T> struct size; | If T is an array type, an integer representing the number of elements |
| template <class T, unsigned I = 0; struct rank; | If T is an array type, or if I is less than or equal to the dimension of T, then 0 |

2. The predicate condition for a template specialization is_constructible<T, Args..> shall be satisfied if and only if the following variable definition would be well-formed for some invented variable: 

3 [Example:
```cpp
// the following assertions hold:
assert(size_v<int> == 0);
assert(size_v<int[2]> == 2);
assert(size_v<int[4]> == 4);
```

4 [Example:
```cpp
// the following assertions hold:
assert(rank_v<int> == 0);
assert(rank_v<int[2]> == 1);
assert(rank_v<int[4]> == 2);
```

6. Relationships between types
1. This subclause contains templates that may be used to query relationships between types at compile time.
2 Each of these templates shall be a true_type if the corresponding condition is true, otherwise false_type.

| Template | Condition | Comments |
| --- | --- | --- |
| template <class T, class U> struct is_same; | T and U make the same name with the cv-qualifications | |
| template <class Base, class Derived> struct is_base_of; | Base is a base of Derived (Clause 13) without regard to cv-qualifiers or Derived are not union and make the same name without regard to cv | Derived shall be a complete type. [Note: Base classes that are private, protected, or ambiguous, cannot be void types.] |
| template <class From, class To> see below | From and To shall be complete types, arrays of unknown bound, or be void types. |
| template <class Fn, ... ArgTypes> struct is_invocable_; | The expression INVOKE(declval<Fn>(), declval<ArgTypes>(...)) is well when treated as an unvaluated operand | Fn and all types in the parameter pack ArgsTypes shall be complete types, cv void, or arrays of unknown bound. |
| template <class R, class Fn, ... ArgTypes> struct is_invocable_r; | The expression INVOKE(declval<Fn>(), declval<ArgTypes>(...)) is well when treated as an unvaluated operand | R and all types in the parameter pack ArgsTypes shall be complete types, cv void, or arrays of unknown bound. |
| template <class Fn, ... ArgTypes> struct is_not_invocable_; | is_invocable_v Fn, ArgTypes>.. is true and INVOKE(declval<Fn>(), declval<ArgTypes>(...)) is known not to throw any exceptions | Fn and all types in the parameter pack ArgsTypes shall be complete types, cv void, or arrays of unknown bound. |
| template <class R, class Fn, ... ArgTypes> struct is_not_invocable_r; | is_invocable_r R, Fn, ArgTypes>.. is true and the expression INVOKE(declval<Fn>(), declval<ArgTypes>(...)) is known not to throw any exceptions | R and all types in the parameter pack ArgsTypes shall be complete types, cv void, or arrays of unknown bound. |

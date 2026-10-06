
# ISO/IEC 14882:2017(E)

Table 41 — Composite type category predicates (continued)

| Template | Condition | Comments |
| --- | --- | --- |
| template <class T> struct_fundamental; | T is a fundamental type (6.9.1) | |
| template <class T> struct_object; | T is an object type (6.9) | |
| template <class T> struct_scalar; | T is a scalar type (6.9) | |
| template <class T> struct_compound; | T is a compound type (6.9.2) | |
| template <class T> struct_member_pointer; | T is a pointer to non-static data member or non-static function | [meta.unary.prop ] |

## 23.15.4 Type properties

- 1 These templates provide access to some of the library without defining any full or partial specializations of any of these templates.

- 2 It is unspecified whether declared in this subclause, instantiating template with a template-argument that is a class template specialization may result in the implicit instantiation of the template if only the semantics of X require that the argument be a complete type.

- 3 For the purpose of defining the templates in this subclause, a function expression declcl<T>() for any type T is considered a trivial (6.9.5) function that is not an-use (6.9.2) of declcl in the context of the corresponding definition notwithstanding the restrictions of 23.2.7.

Table 42 — Type properties predicates

| Template | Condition | Preconditions |
| --- | --- | --- |
| template <class T> struct_const; | T is const-qualified (6.9.3) | |
| template <class T> struct_volatile; | T is volatile-qualified (6.9.3) | remove_all_extents_<T> shall be a complete type or cv void |
| template <class T> struct_trivial; | T is a trivial type (6.9) | remove_all_extents_<T> shall be a complete type or cv void |
| template <class T> struct_trivially_copyable; | T is a trivially copyable type (6.9) | remove_all_extents_<T> shall be a complete type or cv void |
| template <class T> struct_is_layout; | T is a standard-layout type (6.9) | remove_all_extents_<T> shall be a complete type or cv void |
| template <class T> struct_pod; | T is a POD type (6.9) | remove_all_extents_<T> shall be a complete type or cv void |

Table 42 — Type property predicates (continued)

| Template | Condition | Preconditions |
|---|---|---|---|
| `<class T> struct is_empty` | T is a class type, but not a union type, with non-static data members other than bit-fields of length 0, no member functions, no virtual base classes, and base B for `is_empty_vB` is false. | If T is a non-union class type, T shall be a complete type. |
| `<class T> struct is_polymorphic` | T is a polymorphic class (class 13.3) | If T is a non-union class type, T shall be a complete type. |
| `<class T> struct is_abstract` | T is an abstract class (class 13.4) | If T is a non-union class type, T shall be a complete type. |
| `<class T> struct is_final` | T is a class type marked with the `class-virt-specifier` final (Clause 12). [Note: A union is a class type that can be marked with final. — end note] | If T is a class type, T shall be a complete type. |
| `<class T> struct is_aggregate` | T is an aggregate type (11.6.1) | `remove_all_extents_<T>` shall be a complete type or void. |
| `<class T> struct is_signed` | If `is_arithmetic_v<T>` is true, the result same as `T(-1) < T(0)`; false | |
| `<class T> struct is_unsigned` | If `is_arithmetic_v<T>` is true, the result same as `T(0) < T(-1)`; false | |
| `<class T, class... Args> struct is_constructible` | For a function T or for const type T, `is_constructible_v<T, Args...>` is true; otherwise see [below] | T and all types in the parameter pack Args shall be complete types, `void`, or an array of unknown bound. |
| `<class T> struct is_default_constructible` | If `is_constructible_v<T>` is true. | T shall be a complete type, `void`, or an array of unknown bound. |
| `<class T> struct is_copy_constructible` | For a reference type T in (20.3.18), the result same as `is_constructible_v<const T&>`; otherwise false. | T shall be a complete type, `void`, or an array of unknown bound. |

Table 42 — Type property predicates (continued)

| Template | Condition | Preconditions |
| --- | --- | --- |
| template <class T> struct is_move_constructible; | For a referable type T, the same result as `is_constructible_v<T,>&>`, otherwise false. | T shall be a complete type, void, or an array of unknown bound. |
| template <class T, class U> struct is_assignable; | The decltype() = decltype(v) is well-treated as an unvaluated operand (Clause 5). Access checking is performed as if in a context unrelated to T and U. Only the validity of the immediate context of the assignment expression is considered. [Note: The completion of the expression can result in side effects such as the instantiation of template specializations and function template specializations, the generation of implicitly-defined functions, and so on. Such side effects are not in the "immediate context" and can result in the program being ill-formed.—note] | T and U shall be complete types, void, or arrays of unknown bound. |
| template <class T> struct is_copy_assignable; | For a referable type T, the same result as `is_assignable_v<T>&`, otherwise false. | T shall be a complete type, void, or an array of unknown bound. |
| template <class T> struct is_move_assignable; | For a referable type T, the same result as `is_assignable_v<T>&`, otherwise false. | | shall be a complete type, void, or an array of unknown bound. |
| template <class T, class U> struct is_swappable_with; | The expressions swap(declval<T>(), declval<U>()) and swap(declval<U>()) are each well-formed treated as an unevaluated operand (Clause 8) in overload-context (23.2.7). Only the validity of the immediate context of the assignment expression is considered. [Note: The completion of the expression can result in side effects such as the instantiation of template specializations and function template specializations, the generation of implicitly-defined functions, and so on. Such side effects are not in the "immediate context" and can result in the program being ill-formed.—note] | T and U shall be complete types, void, or arrays of unknown bound. |
| template <class T> struct is_swappable; | For a referable type T, the same result as `is_swappable_with<T>`, otherwise false. | T shall be a complete type, void, or an array of unknown bound. |
| template <class T> struct is_destructible; | Either T is a reference type, or T is a complete object for which declval<T>().operator() is well-formed as an unevaluated operand (Clause 8), where remove_all_extents_<T>. | |

Table 42 — Type property predicates (continued)

| Template | Condition | Preconditions |
|---|---|---|
| template <class T, class... Args> struct is_trivially_constructible; | is_constructible_v<T, Args...> is true, as defined by is_constructible, is known to call no operation that is not trivial (6.9,15). | T and all types in the parameter pack Args shall be complete types, void, or arrays of unknown bound. |
| template <class T> struct is_trivially_default_constructible; | is_constructible_v<T> is true. | T shall be a complete type, void, or an array of unknown bound. |
| template <class T> struct is_trivially_move_constructible; | For a referable type T, the same result as `is_constructible_v<T,>&>`, otherwise false. | T shall be a complete type, void, or an array of unknown bound. |
| template <class T> struct is_trivially_copy_constructible; | For a reference type T in (20.3.18), the result same as `is_constructible_v<const T&>`; otherwise false. | T shall be a complete type, void, or an array of unknown bound. | own| template <class T, class U> struct is_trivially_assignable; | The decltype() = decltype(v) is well-treated as an unvaluated operand (Clause 5). | T and U shall be complete types, void, or arrays of unknown bound. | |
| template <class T> struct is_trivially_copy_assignable; | For a referable type T, the same result as `is_assignable_v<T>&`, otherwise false. | T shall be a complete type, void, or an array of unknown bound. |
| template <class T> struct is_trivially_move_assignable; | For a referable type T, the same result as `is_assignable_v<T>&`, otherwise false. | T shall be a complete type, void, or an array of unknown bound. |

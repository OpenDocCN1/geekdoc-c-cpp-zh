
7 [Example 3:
// Given:
struct P final { };
union U1 { };
union U2 final { };

// the following assertions hold:
static_assert(!is_final_v<int>);
static_assert(is_final_v<P>);
static_assert(!is_final_v<U1>);
static_assert(is_final_v<U2>);
— end example]

8 The predicate condition for a template specialization is_constructible<T, Args... > shall be satisfied if and only if the following variable definition would be well-formed for some invented variable t:

T t(declval<Args>()...);

> [Note 4: These tokens are never interpreted as a function declaration. — end note]

Access checking is performed as if in a context unrelated to T and any of the Args. Only the validity of the immediate context of the variable initialization is considered.

> [Note 5: The evaluation of the initialization can result in side effects such as the instantiation of class template specializations and function template specializations, the generation of implicitly-defined functions, and so on. Such side effects are not in the “immediate context” and can result in the program being ill-formed. — end note]

9 The predicate condition for a template specialization has_unique_object_representations<T> shall be satisfied if and only if:

+   (9.1) — T is trivially copyable, and
+   (9.2) — any two objects of type T with the same value have the same object representation, where two objects of array or non-union class type are considered to have the same value if their respective sequences of direct subobjects have the same values, and two objects of union type are considered to have the same value if they have the same active member and the corresponding members have the same value.

The set of scalar types for which this condition holds is implementation-defined.

> [Note 6: If a type has padding bits, the condition does not hold; otherwise, the condition holds true for integral types. — end note]

## 20.15.6 Type property queries [meta.unary.prop.query]

1 This subclause contains templates that may be used to query properties of types at compile time.

Table 50: Type property queries [tab:meta.unary.prop.query]

| Template | Value |
|---|---|
| template<class T> struct alignment_of; | alignof(T). Mandates: alignof(T) is a valid expression (7.6.2.6) |
| template<class T> struct rank; | If T names an array type, an integer value representing the number of dimensions of T; otherwise, 0. |
| template<class T, unsigned I = 0> struct extent; | If T is not an array type, or if it has rank less than or equal to I, or if I is 0 and T has type “array of unknown bound of U”, then 0; otherwise, the bound (9.3.4.5) of the Iᵗʰ dimension of T, where indexing of I is zero-based |

2 Each of these templates shall be a Cpp17UnaryTypeTrait (20.15.2) with a base characteristic of integral_constant<size_t, Value>.

3 [Example 1:
// the following assertions hold:
assert(rank_v<int> == 0);
assert(rank_v<int[2]> == 1);

```
assert(rank_v<int[] [4]> == 2);
— end example
```

4 [Example 2:

```
// the following assertions hold:
assert(extent_v<int> == 0);
assert(extent_v<int[2]> == 2);
assert(extent_v<int[2][4]> == 2);
assert(extent_v<int[][4]> == 0);
assert((extent_v<int, 1>) == 0);
assert((extent_v<int[2], 1>) == 0);
assert((extent_v<int[2][4], 1>) == 4);
assert((extent_v<int[][4], 1>) == 4);
— end example
```

## 20.15.7 Relationships between types [meta.rel]

1 This subclause contains templates that may be used to query relationships between types at compile time.

2 Each of these templates shall be a Cpp17BinaryTypeTrait (20.15.2) with a base characteristic of true_type if the corresponding condition is true, otherwise false_type.

Table 51: Type relationship predicates [tab:meta.rel]

| Template | Condition | Comments |
|---|---|---|
| template<class T, class U> struct is_same; | T and U name the same type with the same cv-qualifications | |
| template<class Base, class Derived> struct is_base_of; | Base is a base class of Derived (11.7) without regard to cv-qualifiers or Base and Derived are not unions and name the same class type without regard to cv-qualifiers | If Base and Derived are non-union class types and are not possibly cv-qualified versions of the same type, Derived shall be a complete type. [Note 1: Base classes that are private, protected, or ambiguous are, nonetheless, base classes. — end note] |
| template<class From, class To> struct is_convertible; | see below | From and To shall be complete types, cv void, or arrays of unknown bound. |
| template<class From, class To> struct is_nothrow_convertible; | is_convertible_v<From, To> is true and the conversion, as defined by is_convertible, is known not to throw any exceptions (7.6.2.7) | From and To shall be complete types, cv void, or arrays of unknown bound. |
| template<class T, class U> struct is_layout_compatible; | T and U are layout-compatible (6.8) | T and U shall be complete types, cv void, or arrays of unknown bound. |
| template<class Base, class Derived> struct is_pointer_interconvertible_base_of; | Derived is unambiguously derived from Base without regard to cv-qualifiers, and each object of type Derived is pointer-interconvertible (6.8.3) with its Base subobject, or Base and Derived are not unions and name the same class type without regard to cv-qualifiers. | If Base and Derived are non-union class types and are not (possibly cv-qualified versions of) the same type, Derived shall be a complete type. |

### Table 51: Type relationship predicates (continued)

| Template | Condition | Comments |
|---|---|---|
| template<class Fn, class... ArgTypes> struct is_invocable; | The expression `INVOKE(declval<Fn>(), declval<ArgTypes>()...)` is well-formed when treated as an unevaluated operand | Fn and all types in the template parameter pack ArgTypes shall be complete types, cv void, or arrays of unknown bound. |
| template<class R, class Fn, class... ArgTypes> struct is_invocable_r; | The expression `INVOKE<R>(declval<Fn>(), declval<ArgTypes>()...)` is well-formed when treated as an unevaluated operand | Fn, R, and all types in the template parameter pack ArgTypes shall be complete types, cv void, or arrays of unknown bound. |
| template<class Fn, class... ArgTypes> struct is_nothrow_invocable; | is_invocable_v<Fn, ArgTypes...> is true and the expression `INVOKE(declval<Fn>(), declval<ArgTypes>()...)` is known not to throw any exceptions (7.6.2.7) | Fn and all types in the template parameter pack ArgTypes shall be complete types, cv void, or arrays of unknown bound. |
| template<class R, class Fn, class... ArgTypes> struct is_nothrow_invocable_r; | is_invocable_r_v<R, Fn, ArgTypes...> is true and the expression `INVOKE<R>(declval<Fn>(), declval<ArgTypes>()...)` is known not to throw any exceptions (7.6.2.7) | Fn, R, and all types in the template parameter pack ArgTypes shall be complete types, cv void, or arrays of unknown bound. |

For the purpose of defining the templates in this subclause, a function call expression `declval<T>()` for any type T is considered to be a trivial (6.8, 11.4.4) function call that is not an odr-use (6.3) of declval in the context of the corresponding definition notwithstanding the restrictions of 20.2.6.

[Example 1:

struct B {};
struct B1 : B {};
struct B2 : B {};
struct D : private B1, private B2 {};

is_base_of_v<B, D>                // true
is_base_of_v<const B, D>           // true
is_base_of_v<B, const D>           // true
is_base_of_v<B, const B>           // true
is_base_of_v<D, B>                // false
is_base_of_v<B&, D&>              // false
is_base_of_v<B[3], D[3]>           // false
is_base_of_v<int, int>             // false

— end example]

The predicate condition for a template specialization `is_convertible<From, To>` shall be satisfied if and only if the return expression in the following code would be well-formed, including any implicit conversions to the return type of the function:

```
To test() {
    return declval<From>();
}
```

> [Note 2: This requirement gives well-defined results for reference types, void types, array types, and function types. — end note]

Access checking is performed in a context unrelated to To and From. Only the validity of the immediate context of the expression of the return statement (8.7.4) (including initialization of the returned object or reference) is considered.

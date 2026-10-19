# Table 57: Other transformations (continued)

| Template | Comments |
|---|---|
| `template<class Fn, class... ArgTypes> struct invoke_result;` | If the expression `INVOKE(declval<Fn>(), declval<ArgTypes>()...)` is well-formed when treated as an unevaluated operand ([7.2]), the member typedef type names the type `decltype(INVOKE(declval<Fn>(), declval<ArgTypes>()...))`; otherwise, there shall be no member type. Access checking is performed as if in a context unrelated to `Fn` and `ArgTypes`. Only the validity of the immediate context of the expression is considered. _[Note 2: The compilation of the expression can result in side effects such as the instantiation of class template specializations and function template specializations, the generation of implicitly-defined functions, and so on. Such side effects are not in the “immediate context” and can result in the program being ill-formed. — end note]_ _Preconditions:_ `Fn` and all types in the template parameter pack `ArgTypes` are complete types, cv void, or arrays of unknown bound. | 
| `template<class T> struct unwrap_reference;` | If `T` is a specialization `reference_wrapper<X>` for some type `X`, the member typedef type of `unwrap_reference<T>` is `X&`, otherwise it is `T`. |
| `template<class T> unwrap_ref_decay;` | The member typedef type of `unwrap_ref_decay<T>` denotes the type `unwrap_reference_t<decay_t<T>>`. |

> ¹ [Note 3: A typical implementation would define `aligned_storage` as:
> 
> ```cpp
> template<size_t Len, size_t Alignment>
> struct aligned_storage {
>   typedef struct {
>     alignas(Alignment) unsigned char __data[Len];
>   } type;
> };
> ```
> 
> — end note]

² In addition to being available via inclusion of the `<type_traits>` header, the templates `unwrap_reference`, `unwrap_ref_decay`, `unwrap_reference_t`, and `unwrap_ref_decay_t` are available when the header `<functional>` (20.14.2) is included.

+   ³ Let:
+   
+   (3.1) — `CREF(A)` be `add_lvalue_reference_t<const remove_reference_t<A>>`,
+   
+   (3.2) — `XREF(A)` denote a unary alias template T such that `T<U>` denotes the same type as U with the addition of A’s cv and reference qualifiers, for a non-reference cv-unqualified type U,
+   
+   (3.3) — `COPYCV(FROM, TO)` be an alias for type `TO` with the addition of `FROM`’s top-level cv-qualifiers, _[Example 1: `COPYCV(const int, volatile short)` is an alias for `const volatile short`. — end example]_
+   
+   (3.4) — `COND-RES(X, Y)` be `decltype(false ? declval<X(&)>()() : declval<Y(&)>()())`.
+   
+   Given types A and B, let X be `remove_reference_t<A>`, let Y be `remove_reference_t<B>`, and let `COMMON-REF(A, B)` be:
+   
+   (3.5) — If A and B are both lvalue reference types, `COMMON-REF(A, B)` is `COND-RES(COPYCV(X, Y) &, COPYCV(Y, X) &)` if that type exists and is a reference type.
+   
+   (3.6) — Otherwise, let C be `remove_reference_t<COMMON-REF(X&&, Y&&)> &&`. If A and B are both rvalue reference types, C is well-formed, and `is_convertible_v<A, C> && is_convertible_v<B, C>` is true, then `COMMON-REF(A, B)` is C.
+   
+   (3.7) — Otherwise, let D be `COMMON-REF(const X&, Y&)`. If A is an rvalue reference and B is an lvalue reference and D is well-formed and `is_convertible_v<A, D>` is true, then `COMMON-REF(A, B)` is D.
+   
+   (3.8) — Otherwise, if A is an lvalue reference and B is an rvalue reference, then `COMMON-REF(A, B)` is `COMMON-REF(B, A)`.
+   
+   (3.9) — Otherwise, `COMMON-REF(A, B)` is ill-formed.
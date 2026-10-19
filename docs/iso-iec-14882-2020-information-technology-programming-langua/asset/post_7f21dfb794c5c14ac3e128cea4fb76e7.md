
## 20.13.5 Operators [scoped.adaptor.operators]

```cpp
scoped_allocator_adaptor select_on_container_copy_construction() const;
```

Returns: A new scoped_allocator_adaptor object where each allocator A in the adaptor is initialized from the result of calling allocator_traits<A>::select_on_container_copy_construction() on the corresponding allocator in *this.

```cpp
template<class OuterA1, class OuterA2, class... InnerAllocs>
bool operator==(const scoped_allocator_adaptor<OuterA1, InnerAllocs...>& a,
    const scoped_allocator_adaptor<OuterA2, InnerAllocs...>& b) noexcept;
```

Returns: If sizeof...(InnerAllocs) is zero,

a.outer_allocator() == b.outer_allocator()

otherwise

a.outer_allocator() == b.outer_allocator() && a.inner_allocator() == b.inner_allocator()

## 20.14 Function objects [function.objects]

### 20.14.1 General [function.objects.general]

1 A function object type is an object type (6.8) that can be the type of the postfix-expression in a function call (7.6.1.3, 12.4.2.2).<sup>225</sup> A function object is an object of a function object type. In the places where one would expect to pass a pointer to a function to an algorithmic template (Clause 25), the interface is specified to accept a function object. This not only makes algorithmic templates work with pointers to functions, but also enables them to work with arbitrary function objects.

225) Such a type is a function pointer or a class type which has a member operator() or a class type which has a conversion to a pointer to function.

### 20.14.2 Header \<functional\> synopsis [functional.syn]

```cpp
namespace std {
  // 20.14.5, invoke
  template<class F, class... Args>
  constexpr invoke_result_t<F, Args...> invoke(F&& f, Args&&... args)
    noexcept(is_nothrow_invocable_v<F, Args...>);

  // 20.14.6, reference_wrapper
  template<class T> class reference_wrapper;

  template<class T> constexpr reference_wrapper<T> ref(T&) noexcept;
  template<class T> constexpr reference_wrapper<const T> cref(const T&) noexcept;
  template<class T> void ref(const T&&) = delete;
  template<class T> void cref(const T&&) = delete;

  template<class T> constexpr reference_wrapper<T> ref(reference_wrapper<T>) noexcept;
  template<class T> constexpr reference_wrapper<const T> cref(reference_wrapper<T>) noexcept;

  // 20.14.7, arithmetic operations
  template<class T = void> struct plus;
  template<class T = void> struct minus;
  template<class T = void> struct multiplies;
  template<class T = void> struct divides;
  template<class T = void> struct modulus;
  template<class T = void> struct negate;
  template<> struct plus<void>;
  template<> struct minus<void>;
  template<> struct multiplies<void>;
  template<> struct divides<void>;
  template<> struct modulus<void>;
  template<> struct negate<void>;

  // 20.14.8, comparisons
  template<class T = void> struct equal_to;
  template<class T = void> struct not_equal_to;
  template<class T = void> struct greater;
  template<class T = void> struct less;
  template<class T = void> struct greater_equal;
  template<class T = void> struct less_equal;
  template<> struct equal_to<void>;
  template<> struct not_equal_to<void>;
  template<> struct greater<void>;
  template<> struct less<void>;
  template<> struct greater_equal<void>;
  template<> struct less_equal<void>;

  // 20.14.8.8, class compare_three_way
  struct compare_three_way;

  // 20.14.10, logical operations
  template<class T = void> struct logical_and;
  template<class T = void> struct logical_or;
  template<class T = void> struct logical_not;
  template<> struct logical_and<void>;
  template<> struct logical_or<void>;
  template<> struct logical_not<void>;

  // 20.14.11, bitwise operations
  template<class T = void> struct bit_and;
  template<class T = void> struct bit_or;
  template<class T = void> struct bit_xor;
  template<class T = void> struct bit_not;
  template<> struct bit_and<void>;
  template<> struct bit_or<void>;
  template<> struct bit_xor<void>;
  template<> struct bit_not<void>;

  // 20.14.12, identity
  struct identity;

  // 20.14.13, function template not_fn
  template<class F> constexpr unspecified not_fn(F&& f);

  // 20.14.14, function template bind_front
  template<class F, class... Args> constexpr unspecified bind_front(F&&, Args&&...);

  // 20.14.15, bind
  template<class T> struct is_bind_expression;
  template<class T>
    inline constexpr bool is_bind_expression_v = is_bind_expression<T>::value;
  template<class T> struct is_placeholder;
  template<class T>
    inline constexpr int is_placeholder_v = is_placeholder<T>::value;

  template<class F, class... BoundArgs>
    constexpr unspecified bind(F&&, BoundArgs&&...);
  template<class R, class F, class... BoundArgs>
    constexpr unspecified bind(F&&, BoundArgs&&...);

  namespace placeholders {
    // M is the implementation-defined number of placeholders
    see below _1;
    see below _2;
    .
    .
    .
    see below _M;
  }

  // 20.14.16, member function adaptors
  template<class R, class T>
    constexpr unspecified mem_fn(R T::*) noexcept;

  // 20.14.17, polymorphic function wrappers
  class bad_function_call;

  template<class> class function;      // not defined
  template<class R, class... ArgTypes> class function<R(ArgTypes...)>;

  template<class R, class... ArgTypes>
    void swap(function<R(ArgTypes...)>&, function<R(ArgTypes...)>&) noexcept;

  template<class R, class... ArgTypes>
    bool operator==(const function<R(ArgTypes...)>&, nullptr_t) noexcept;

  // 20.14.18, searchers
  template<class ForwardIterator, class BinaryPredicate = equal_to<>>
    class default_searcher;

  template<class RandomAccessIterator,
        class Hash = hash<typename iterator_traits<RandomAccessIterator>::value_type>,
        class BinaryPredicate = equal_to<>>
    class boyer_moore_searcher;

  template<class RandomAccessIterator,
        class Hash = hash<typename iterator_traits<RandomAccessIterator>::value_type>,
        class BinaryPredicate = equal_to<>>
    class boyer_moore_horspool_searcher;

  // 20.14.19, class template hash
  template<class T>
    struct hash;

  namespace ranges {
    // 20.14.9, concept-constrained comparisons
    struct equal_to;
    struct not_equal_to;
    struct greater;
    struct less;
    struct greater_equal;
    struct less_equal;
  }
}
```

1 [Example 1: If a C++ program wants to have a by-element addition of two vectors a and b containing double and put the result into a, it can do:

transform(a.begin(), a.end(), b.begin(), a.begin(), plus<double>());

— end example]

2 [Example 2: To negate every element of a:

transform(a.begin(), a.end(), a.begin(), negate<double>());

— end example]

### 20.14.3 Definitions [func.def]

1 The following definitions apply to this Clause:

2 A call signature is the name of a return type followed by a parenthesized comma-separated list of zero or more argument types.

3 A callable type is a function object type (20.14) or a pointer to member.

4 A *callable object* is an object of a callable type.

5 A *call wrapper type* is a type that holds a callable object and supports a call operation that forwards to that object.

6 A *call wrapper* is an object of a call wrapper type.

7 A *target object* is the callable object held by a call wrapper.

8 A call wrapper type may additionally hold a sequence of objects and references that may be passed as arguments to the target object. These entities are collectively referred to as *bound argument entities*.

9 The target object and bound argument entities of the call wrapper are collectively referred to as *state entities*.

### 20.14.4 Requirements [func.require]

1 Define *INVOKE*(f, t₁, t₂, …, tₙ) as follows:

- (1.1) — (t₁.*f)(t₂, …, tₙ) when f is a pointer to a member function of a class T and is_base_of_v<T, remove_reference_t<decltype(t₁)>> is true;
- (1.2) — (t₁.get().*f)(t₂, …, tₙ) when f is a pointer to a member function of a class T and remove_cvref_t<decltype(t₁)> is a specialization of reference_wrapper;
- (1.3) — ((*t₁).*f)(t₂, …, tₙ) when f is a pointer to a member function of a class T and t₁ does not satisfy the previous two items;
- (1.4) — t₁.*f when N == 1 and f is a pointer to data member of a class T and is_base_of_v<T, remove_reference_t<decltype(t₁)>> is true;
- (1.5) — t₁.get().*f when N == 1 and f is a pointer to data member of a class T and remove_cvref_t<decltype(t₁)> is a specialization of reference_wrapper;
- (1.6) — (*t₁).*f when N == 1 and f is a pointer to data member of a class T and t₁ does not satisfy the previous two items;
- (1.7) — f(t₁, t₂, …, tₙ) in all other cases.

2 Define *INVOKE<R>*(f, t₁, t₂, …, tₙ) as static_cast<void>(INVOKE(f, t₁, t₂, …, tₙ)) if R is cv void, otherwise INVOKE(f, t₁, t₂, …, tₙ) implicitly converted to R.

3 Every call wrapper (20.14.3) meets the *Cpp17MoveConstructible* and *Cpp17Destructible* requirements. An *argument forwarding call wrapper* is a call wrapper that can be called with an arbitrary argument list and delivers the arguments to the wrapped callable object as references. This forwarding step delivers rvalue arguments as rvalue references and lvalue arguments as lvalue references.

> [Note 1: In a typical implementation, argument forwarding call wrappers have an overloaded function call operator of the form
> template<class... UnBoundArgs>
>   constexpr R operator()(UnBoundArgs&&... unbound_args) cv-qual;
> — end note]

```cpp
template<class... UnBoundArgs>
  constexpr R operator()(UnBoundArgs&&... unbound_args) cv-qual;
```

4 A *perfect forwarding call wrapper* is an argument forwarding call wrapper that forwards its state entities to the underlying call expression. This forwarding step delivers a state entity of type T as cv T& when the call is performed on an lvalue of the call wrapper type and as cv T&& otherwise, where cv represents the cv-qualifiers of the call wrapper and where cv shall be neither volatile nor const volatile.

5 A *call pattern* defines the semantics of invoking a perfect forwarding call wrapper. A postfix call performed on a perfect forwarding call wrapper is expression-equivalent (3.20) to an expression e determined from its call pattern cp by replacing all occurrences of the arguments of the call wrapper and its state entities with references as described in the corresponding forwarding steps.

6 A *simple call wrapper* is a perfect forwarding call wrapper that meets the *Cpp17CopyConstructible* and *Cpp17CopyAssignable* requirements and whose copy constructor, move constructor, and assignment operators are constexpr functions that do not throw exceptions.

7 The copy/move constructor of an argument forwarding call wrapper has the same apparent semantics as if memberwise copy/move of its state entities were performed (11.4.5.3).

> [Note 2: This implies that each of the copy/move constructors has the same exception-specification as the corresponding implicit definition and is declared as constexpr if the corresponding implicit definition would be considered to be constexpr. — end note]

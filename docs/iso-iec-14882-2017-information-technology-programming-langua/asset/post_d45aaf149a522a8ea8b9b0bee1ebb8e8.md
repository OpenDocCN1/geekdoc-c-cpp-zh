
# ISO/IEC 14882:2017(E)

v<T1, Arg1..., inner_allocator_type&> is true, xprime is:
tuple<std::move(x), tuple<inner_allocator_type&>(inner_allocator())>

Otherwise, the program is ill-formed.
constructs a tuple object y by the following rules:

- If uses_allocator_v<T2>, inner_allocator_type& is false and is_constructible<T2, Arg2..> is true, then yprime is y.

- Otherwise, if uses_allocator_v<T2>, inner_allocator_type& is true and is_constructible<T2, allocator_arg_t, inner_allocator_type&, Arg2..> is true, then yprime is:
tuple<allocator_arg, inner_allocator_type&>(allocator_arg, inner_allocator()), std::move(y)>

- Otherwise, if uses_allocator_v<T2>, inner_allocator_type& is true and is_constructible<T2, Arg2.., ..., inner_allocator_type&>(ntuple<std::move(y), tuple<inner_allocator_type&>()>())

Otherwise, the program is ill-formed.
then calls:
OUTERNMOST_TRAITS(*this)::construct(
OUTERNMOST*(this), p, piecewise_construct, std::move(xprime), std::move(yprime))

```cpp
template <class T1, class T2>
void construct(pair<T1, T2*>* p);
```

Equivalent to:
construct(p, piecewise_construct, tuple<>(), tuple<U>());

```cpp
template <class T1, class T2, class U, class V>
void construct(pair<T1, T2*>* p, const U& x, V& y);
```

Equivalent to:
construct(p, piecewise_construct,
forward_as_tuple(std::forward<U>(x)),
forward_as_tuple(std::forward<V>(y)));

Equivalent to:
construct(p, piecewise_construct,
forward_as_tuple(x.first),
forward_as_tuple(x.second));

```cpp
template <class T1, class T2, class U, class V>
void construct(pair<T1, T2*>* p, pair<U, V>& x);
```

Equivalent to:
construct(p, piecewise_construct,
forward_as_tuple(std::forward<U>(x.first)),
forward_as_tuple(std::forward<V>(x.second)));

```cpp
template <class T>
void destroy(T* p);
```

# ISO/IEC 14882:2017(E)

16 Effects: Calls OUTERMOST_ALLOC_TRAITS(*this)~:destroy(OUTERMOST(*this), p).

17 scoped_allocator_adaptor select_on_container_type_construction() const;
Returns: A new scoped_allocator_adaptor where each allocator A in the adaptor is initialized from the calling of allocator_traits<A>::select_on_container_type_construction() of the corresponding allocator to *this.

## 23.13.5 Scoped allocator operators [scoped.adaptor.operators]

```cpp
template <class Outer1, class Outer2, class InnerLocs>
bool operator()=(const scoped_allocator_adaptor<Outer1, InnerLocs..>&& a,
               const scoped_allocator_adaptor<Outer2, InnerLocs..>&& b) noexcept {
// 1 Returns: if (InnerLocs) is zero,
//    a.allocator() == b.allocator();
//    otherwise
//    a.allocator() == b.allocator() && a.inner_allocator() == b.inner_allocator()
}
template <class Outer1, class Outer2, class InnerLocs>
bool operator()=(const scoped_allocator_adaptor<Outer1, InnerLocs..>&& a,
               const scoped_allocator_adaptor<Outer2, InnerLocs..>&& b) noexcept;
```

## 23.14 Function objects [function.objects]

1 A function object is an object type (6.9) that can be the type of the postfix-expression in a function call (8.2.2, 16.3.1).
2 A function is an object of object type. In the places where one would expect to pass a pointer to a function to an algorithmic template (Clause 28), the interface is specified to accept a function object. This not only makes algorithmic templates work with pointers to functions, but also enables them to work with arbitrary function objects.

## 23.14.1 Header <functional> synopsis [function.syn]

```cpp
namespace {
// 23.14.4. invoke
template <class F, class... Args>
invoke_result<F, Args...> invoke(F&& f, Args&&... args)
  noexcept(is_not_invocable_v<F, Args...>);
// 23.14.5. reference_wrapper
template <class T> reference_wrapper<T>
  reference_wrapper(const T&) noexcept;
template <class T> T& ref(const T&) const noexcept;
template <class T> void ref(const T&&) = delete;
template <class T> T& ref(const reference_wrapper<T>&) const;
template <class T> void ref(const reference_wrapper<T>&) = delete;
// 23.14.6. arithmetic operations
template <class T = void> struct plus {
// 2 Such a type is a function pointer or a class which has a member operator() or a conversion to function.
template <class T = void> struct minus;
template <class T = void> struct multiplies;
template <class T = void> struct divides;
template <class T = void> struct modulus;
};
// 23.14.7. comparisons
template <class T = void> struct equal_to;
template <class T = void> struct not_equal_to;
template <class T = void> struct greater;
template <class T = void> struct less;
template <class T = void> struct greater_equal;
template <class T = void> struct less_equal;
};

// 23.14.8. logical operations
template <class T = void> struct logical_and;
template <class T = void> struct logical_or;
template <class T = void> struct logical_not;
template <class T = void> struct logical_and_not<void>;
template <class T = void> struct logical_or_not<void>;
template <class T = void> struct logical_not_not<void>;

// 23.14.9. bitwise operations
template <class T = void> struct bit_and;
template <class T = void> struct bit_or;
template <class T = void> struct bit_xor;
template <class T = void> struct bit_not;
template <class T = void> struct bit_and_not<void>;
template <class T = void> struct bit_xor_not<void>;
template <class T = void> struct bit_not_not<void>;

// 23.14.10. function template not_fn
template <class F> auto not_fn(F&);

// 23.14.11. bind
template<class T> struct is_bind_expression;
template<class T> struct is_placeholder;

template<class F, class... BoundArgs>
auto bind(F&, BoundArgs&...);
template<class R, class F, class... BoundArgs>
R bind(F&, BoundArgs&...);

```cpp
namespace placeholders {
    // M is the implementation-defined number of placeholders
    // see below _1;
    // see below _2;
    ...
    // see below _M;
}
```

```cpp
// 23.14.12, member function adaptors
template<class R, class D> auto mem_fn(R T::*) noexcept;

template<class T> struct bad_function_call;

template<class T> class function; // not defined
template<class R, class... ArgTypes> class function<R(ArgTypes...)>;

template<class R, class... ArgTypes>
void swap(function<R(ArgTypes...)>&) noexcept;

template<class R, class... ArgTypes>
auto operator*(const function<R(ArgTypes...)>&, void*) noexcept;
template<class R, class... ArgTypes>
auto operator*(void*, const function<R(ArgTypes...)>&) noexcept;
```

```cpp
// 23.14.11, searchers
template<class ForwardIterator, class BinaryPredicate = equal_to<>>
class default_searcher;

template<class RandomAccessIterator>
class Hash = hashtype<typename iterator_traits<RandomAccessIterator>::value_type,
             class BinaryPredicate = equal_to<>>
class boyer_more_horspool_searcher;
```

```cpp
// 23.14.10, hash function primary template
template<class T>
struct hash;
```

```cpp
// 23.14.11, function object binders
template<class T>
inline constexpr bool is_bind_expression_v = is_bind_expression<T>;
template<class T>
inline constexpr bool is_placeholder_v = is_placeholder<T>;
```

# ISO/IEC 14882:2017(E)

1 Example: If a C++ program wants to have a addition of two vectors a containing double and put the result into a, it can do:
transform(a.begin(), a.end(), a.begin(), plus<double>());

2 Example: To negate every element of:
transform(a.begin(), a.end(), negate<double>());

# ISO/IEC 14882:2017(E)

## 23.14.2 Definitions [func.def]

1 The following definitions apply to this:
2 A call signature is the name of return type followed by a parenthesized comma-separated list of argument types.
3 A callable type is a function object (23.14) or a pointer to member.
4 A callable object is an object of callable type.
5 A wrapper type is a type that holds a callable object and supports a call operation that forwards to that object.
6 A wrapper object is an object of wrapper type.

## 23.14.3 Requirements [func.require]

1 Define INVOKEF(f, t1, ..., tN) as follows:
(1.1) (t1).*f(t2, ..., tN) if f is a pointer to a member of a class T and base_of_v<T, decay_t<type(t1)>> is true;
(1.2) (t1).get(t2, ..., tN) if f is a pointer to a member of a class T and decay_t<type(t1)> is a specialization of reference_wrapper;
(1.3) (*t1).*f(t2, ..., tN) if f is a pointer to a member of a class T and t1 does not satisfy the following two:
(1.4) (*t1).*f if N == 1 and f is a pointer to data member of class T and base_of_v<T, decay_t<type(t1)>> is true;
(1.5) (t1).get() if N == 1 and f is a pointer to data member of class T and t1 does not satisfy the following two:
(1.6) f(t1, t2, ..., tN), in all other cases.

2 Define INVOKER(f, t1, ..., tN) as static_cast<void>(INVOKEF(f, t1, ..., tN)) if R is void; otherwise INVOKEF(f, t1, ..., tN) implicitly converted to R.

3 Every callable (23.14) must be Constructible. A forwarding callable is a wrapper class that can be called with an arbitrary argument list and defines the arguments to the callable object as references. This forwarding call shall ensure that rvalue arguments are delivered as rvalue references and lvalue arguments are delivered as lvalue references. A simple wrapper is a forwarding wrapper that is Copyible and Assignable and whose copy constructor, move constructor, and assignment operator do not throw exceptions. Note: In a typical implementation forwarding wrappers have an overloaded function call operator of the

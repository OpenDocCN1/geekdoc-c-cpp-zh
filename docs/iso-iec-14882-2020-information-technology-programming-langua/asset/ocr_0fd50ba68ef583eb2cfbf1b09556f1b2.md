```
see below _M;
}
```

```
// 20.14.16, member function adaptors
template<class R, class T>
    constexpr unspecified mem_fn(R T::*) noexcept;
```

```
// 20.14.17, polymorphic function wrappers
class bad_function_call;

template<class> class function;      // not defined
template<class R, class... ArgTypes> class function<R(ArgTypes...)>;

template<class R, class... ArgTypes>
    void swap(function<R(ArgTypes...)>&, function<R(ArgTypes...)>&) noexcept;

template<class R, class... ArgTypes>
    bool operator==(const function<R(ArgTypes...)>&, nullptr_t) noexcept;
```

```
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
```

```
// 20.14.19, class template hash
template<class T>
    struct hash;
```

```
namespace ranges {
    // 20.14.9, concept-constrained comparisons
    struct equal_to;
    struct not_equal_to;
    struct greater;
    struct less;
    struct greater_equal;
    struct less_equal;
}
```

1 [Example 1: If a C++ program wants to have a by-element addition of two vectors a and b containing double and put the result into a, it can do:
transform(a.begin(), a.end(), b.begin(), a.begin(), plus<double>());
— end example]

2 [Example 2: To negate every element of a:
transform(a.begin(), a.end(), a.begin(), negate<double>());
— end example]

# 20.14.3 Definitions [func.def]

1 The following definitions apply to this Clause:

2 A call signature is the name of a return type followed by a parenthesized comma-separated list of zero or more argument types.

3 A callable type is a function object type (20.14) or a pointer to member.
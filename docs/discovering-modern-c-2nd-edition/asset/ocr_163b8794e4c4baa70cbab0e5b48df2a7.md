In our concept we split the syntactic and semantic concepts. The former can be expressed directly in the language as seen in the first two requirements. Apparently, we request that the result of the operation is convertible into the `Value` type and that there exists an `identity` function for our operation whose result is also convertible into the `Value` type.

The semantic properties must be explicitly declared by the user in terms of a type trait where we use the function-based approach from Section 6.6.2 (which applies to derived classes opposed to techniques based on template specialization). As long as an operation for a given type isn't yet declared to be a commutative monoid it is assumed not to be:

> Click here to view code image

```
std::false_type cm_map_impl(...);
template <typename Op, typename Value>
constexpr bool commutative_monoid_map=
    decltype(cm_map_impl(std::declval<Op>(),
    std::declval<Value>()))::value;
```

You probably think now that it is a shame to realize advanced concepts with the nasty varargs ellipsis. We share your feelings. But it's only our low-priority fall-back function. To declare the addition to be a monoid, we introduce an `add` functor:

> Click here to view code image

```
struct add
{
    template <typename T>
    T operator()(T x, T y) const noexcept { return x + y; }
};
```

and provide it an according `identity` function:

```
template <typename Value>
Value identity(add, Value)
{
    return Value();
}
```

And since the addition of any reasonable `Value` type is commutative and associative, we declare them all additions to be commutative monoids by default:
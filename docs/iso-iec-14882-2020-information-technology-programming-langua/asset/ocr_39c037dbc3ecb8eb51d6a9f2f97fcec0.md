3 Let i be a dereferenceable value of type In. In and Out model indirectly_movable_storable<In, Out> only if after the initialization of the object obj in
iter_value_t<In> obj(ranges::iter_move(i));
obj is equal to the value previously denoted by *i. If iter_rvalue_reference_t<In> is an rvalue reference type, the resulting state of the value denoted by *i is valid but unspecified (16.4.6.16).

# 23.3.7.3 Concept indirectly_copyable [alg.req.ind.copy]

1 The indirectly_copyable concept specifies the relationship between a indirectly_readable type and a indirectly_writable type between which values may be copied.

```
template<class In, class Out>
concept indirectly_copyable =
    indirectly_readable<In> &&
    indirectly_writable<Out, iter_reference_t<In>>;
```

2 The indirectly_copyable_storable concept augments indirectly_copyable with additional requirements enabling the transfer to be performed through an intermediate object of the indirectly_readable type’s value type. It also requires the capability to make copies of values.

```
template<class In, class Out>
concept indirectly_copyable_storable =
    indirectly_copyable<In, Out> &&
    indirectly_writable<Out, iter_value_t<In>&> &&
    indirectly_writable<Out, const iter_value_t<In>&> &&
    indirectly_writable<Out, iter_value_t<In>&&> &&
    indirectly_writable<Out, const iter_value_t<In>&&> &&
    copyable<iter_value_t<In>> &&
    constructible_from<iter_value_t<In>, iter_reference_t<In>> &&
    assignable_from<iter_value_t<In>&, iter_reference_t<In>>;
```

3 Let i be a dereferenceable value of type In. In and Out model indirectly_copyable_storable<In, Out> only if after the initialization of the object obj in
iter_value_t<In> obj(*i);
obj is equal to the value previously denoted by *i. If iter_reference_t<In> is an rvalue reference type, the resulting state of the value denoted by *i is valid but unspecified (16.4.6.16).

# 23.3.7.4 Concept indirectly_swappable [alg.req.ind.swap]

1 The indirectly_swappable concept specifies a swappable relationship between the values referenced by two indirectly_readable types.

```
template<class I1, class I2 = I1>
concept indirectly_swappable =
    indirectly_readable<I1> && indirectly_readable<I2> &&
    requires(const I1 i1, const I2 i2) {
        ranges::iter_swap(i1, i1);
        ranges::iter_swap(i2, i2);
        ranges::iter_swap(i1, i2);
        ranges::iter_swap(i2, i1);
    };
```

# 23.3.7.5 Concept indirectly_comparable [alg.req.ind.cmp]

1 The indirectly_comparable concept specifies the common requirements of algorithms that compare values from two different sequences.

```
template<class I1, class I2, class R, class P1 = identity,
    class P2 = identity>
concept indirectly_comparable =
    indirect_binary_predicate<R, projected<I1, P1>, projected<I2, P2>>;
```

# 23.3.7.6 Concept permutable [alg.req.permutable]

1 The permutable concept specifies the common requirements of algorithms that reorder elements in place by moving or swapping them.
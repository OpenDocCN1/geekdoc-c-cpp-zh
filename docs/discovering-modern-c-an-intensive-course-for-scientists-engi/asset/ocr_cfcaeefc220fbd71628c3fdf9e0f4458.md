```
{
    using std::abs;
    typedef typename Vector::value_type value_type;
    multi_tmp<BSize, value_type> multi_sum(0);
    unsigned s = size(v), sb = s / BSize * BSize;
    for (unsigned i = 0; i < sb; i += BSize)
        one_norm_ftor<0, BSize>()(multi_sum, v, i);
    value_type sum = multi_sum.sum();
    for (unsigned i = sb; i < s; ++i)
        sum += abs(v[i]);
    return sum;
}
```

There is still one piece missing: we must reduce the partial sums in `multi_sum` at the end. Unfortunately, we cannot write a loop over the members of `multi_sum`. So, we need a recursive function that dives into `multi_sum` which is easiest to implement as a member function with the corresponding specialization:

```
template <unsigned BSize, typename Value>
struct multi_tmp
{
    Value sum() const { return value + sub.sum(); }
};
```

Note that we started the summation with the empty `multi_tmp`, not the innermost value member. Otherwise we would need an extra specialization for `multi_tmp<1, Value>`. Likewise, we could implement a general reduction as in `accumulate`, but this would require the presence of an initial element:

```
template <unsigned BSize, typename Value>
struct multi_tmp
{
    template <typename Op>
    Value reduce(Op op, const Value& init) const
    { return op(value, sub.reduce(op, init)); }
};
```

```
template <typename Value>
struct multi_tmp<0, Value>
{
    template <typename Op>
    Value reduce(Op op, const Value& init) const { return init; }
};
```
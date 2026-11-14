```
template <unsigned BSize, typename Vector>
typename Vector::value_type
inline one_norm(const Vector& v)
{
    using std::abs;
    using value_type = typename Vector::value_type;
    multi_tmp<BSize, value_type> multi_sum{0};

    unsigned s = size(v), sb= s / BSize * BSize;
    for (unsigned i = 0; i < sb; i+= BSize)
        one_norm_ftor<0, BSize>::eval(multi_sum, v, i);

    value_type sum = multi_sum.sum();
    for (unsigned i = sb; i < s; ++i)
        sum+= abs(v[i]);

    return sum;
}
```
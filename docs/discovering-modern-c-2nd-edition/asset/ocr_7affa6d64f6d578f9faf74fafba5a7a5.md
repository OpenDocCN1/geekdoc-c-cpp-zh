```
template <unsigned Offset, unsigned Max>
struct one_norm_ftor
{
    template <typename S, typename V>
    static void eval(S& sum, const V& v, unsigned i)
    {
        using std::abs;
        if constexpr (Offset < Max) {
            sum.value+= abs(v[i+Offset]);
            one_norm_ftor<Offset+1, Max>::eval(sum.sub, v, i);
        }
    }
}
};
```
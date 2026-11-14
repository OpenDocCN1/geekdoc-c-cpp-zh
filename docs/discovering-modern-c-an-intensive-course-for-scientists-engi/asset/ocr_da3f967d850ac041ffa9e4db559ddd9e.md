# 5.4 Meta-Tuning: Write Your Own Compiler Optimization

How many temporaries are actually used in the iteration block depends on the template parameter BSize. Unfortunately, we cannot change the number of arguments in a function call depending on a template parameter, i.e., passing fewer arguments for smaller values of BSize. Thus, we have to pass all variables to the iteration block functor:

```
```cpp
for (unsigned i= 0; i < sb; i += BSize)
    one_norm_ftor<0, BSize<>()(s0, s1, s2, s3, s4, s5, s6, s7, v, i);
```
```

The first calculation in each block accumulates on s0, the second on s1, and so on. Unfortunately, we cannot select the temporary argument-dependently (unless we specialize for every value).

Alternatively, each computation is performed on its first function argument and subsequent functors are called without the first argument:

```
```cpp
one_norm_ftor<1, BSize<>()(s1, s2, s3, s4, s5, s6, s7, v, i);
one_norm_ftor<2, BSize<>()(s2, s3, s4, s5, s6, s7, v, i);
one_norm_ftor<3, BSize<>()(s3, s4, s5, s6, s7, v, i);
```
```

This is not realizable with templates either.

The solution is to rotate the references:

```
```cpp
one_norm_ftor<1, BSize<>()(s1, s2, s3, s4, s5, s6, s7, s0, v, i);
one_norm_ftor<2, BSize<>()(s2, s3, s4, s5, s6, s7, s0, s1, v, i);
one_norm_ftor<3, BSize<>()(s3, s4, s5, s6, s7, s0, s1, s2, v, i);
```
```

This rotation is achieved by the following functor implementation:

```
```cpp
template <unsigned Offset, unsigned Max>
struct one_norm_ftor
{
    template <typename S, typename V>
    void operator()(S& s0, S& s1, S& s2, S& s3, S& s4, S& s5, S& s6,
                    S& s7, const V& v, unsigned i)
    {
        using std::abs;
        s0+= abs(v[i+Offset]);
        one_norm_ftor<Offset+1, Max>()(s1, s2, s3, s4, s5, s6, s7,
                                    s0, v, i);
    }
};

template <unsigned Max>
struct one_norm_ftor<Max, Max>
{
    template <typename S, typename V>
    void operator()(S& s0, S& s1, S& s2, S& s3, S& s4, S& s5, S& s6,
                    S& s7, const V& v, unsigned i) {}
};
```
```

The corresponding one_norm function based on this functor is straightforward:

```
```cpp
template <unsigned BSize, typename Vector>
typename Vector::value_type
```
```
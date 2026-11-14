

```cpp
for (unsigned i = 0; i < s; i += 4) {
    u[i] = 3.0f * v[i] + w[i];
    u[i + 1] = 3.0f * v[i + 1] + w[i + 1];
    u[i + 2] = 3.0f * v[i + 2] + w[i + 2];
    u[i + 3] = 3.0f * v[i + 3] + w[i + 3];
}
```

```cpp
unsigned sb = s / 4 * 4;
for (unsigned i = 0; i < sb; i += 4) {
    u[i] = 3.0f * v[i] + w[i];
    u[i + 1] = 3.0f * v[i + 1] + w[i + 1];
    u[i + 2] = 3.0f * v[i + 2] + w[i + 2];
    u[i + 3] = 3.0f * v[i + 3] + w[i + 3];
}
for (unsigned i = sb; i < s; ++i)
    u[i] = 3.0f * v[i] + w[i];
```

- 原生循环计算时间为 0.801699 μs。
- 展开循环计算时间为 0.600912 μs。

- 原生循环计算时间为 0.610174 µs。
- 展开循环计算时间为 0.586364 µs。

- 原生循环计算时间为 0.474725 µs。
- 展开循环计算时间为 0.471488 µs。

```cpp
template <unsigned BSize, typename U, typename V, typename W>
void my_axpy(U& u, const V& v, const W& w)
{
    assert(u.size() == v.size() && v.size() == w.size());
    unsigned s = u.size(), sb = s / BSize * BSize;

    for (unsigned i = 0; i < sb; i += BSize)
        my_axpy_ftor<0, BSize>::eval(u, v, w, i);

    for (unsigned i = sb; i < s; ++i)
        u[i] = 3.0f * v[i] + w[i];
}
```

```cpp
template <unsigned Offset, unsigned Max>
struct my_axpy_ftor
{
    template <typename U, typename V, typename W>
    static void eval(U& u, const V& v, const W& w, unsigned i)
    {
        if constexpr (Offset < Max) {
            u[i + Offset] = 3.0f * v[i + Offset] + w[i + Offset];
            my_axpy_ftor<Offset + 1, Max>::eval(u, v, w, i);
        }
    }
};
```

- unrolled<2> 循环计算时间为 0.667546 µs。
- unrolled<4> 循环计算时间为 0.601179 µs。
- unrolled<6> 循环计算时间为 0.565536 µs。
- unrolled<8> 循环计算时间为 0.570061 µs。

```cpp
template <typename T>
class vector
{
    template <typename Src>
    vector& operator=(const Src& that)
    {
        check_size(size(that));
        unsigned s = my_size, sb = s / 4 * 4;

        for (unsigned i = 0; i < sb; i += 4)
            assign<0, 4>::eval(*this, that, i);

        for (unsigned i = sb; i < s; ++i)
            data[i] = that[i];
        return *this;
    }
};
```

```cpp
template <unsigned Offset, unsigned Max>
struct assign
{
    template <typename U, typename V>
    static void eval(U& u, const V& v, unsigned i)
    {
        if constexpr (Offset < Max) {
            u[i + Offset] = v[i + Offset];
            assign<Offset + 1, Max>::eval(u, v, i);
        }
    }
};
```

```cpp
template <unsigned BSize, typename Src>
vector& operator=(const Src& that)
{
    check_size(size(that));
    unsigned s = my_size, sb = s / BSize * BSize;

    for (unsigned i = 0; i < sb; i += BSize)
        assign<0, BSize>::eval(*this, that, i);

    for (unsigned i = sb; i < s; ++i)
        data[i] = that[i];

    return *this;
}
```

```cpp
u.template operator=<4>(v + v + w);
```

```cpp
template <unsigned BSize, typename Vector>
auto unroll(Vector& v)
{
    return unroll_vector<BSize, Vector>(v);
}
```

```cpp
template <unsigned BSize, typename V>
class unroll_vector
{
public:
    unroll_vector(V& ref) : ref(ref) {}

    template <typename Src>
    V& operator=(const Src& that)
    {
        assert(size(ref) == size(that));
        unsigned s = size(ref), sb = s / BSize * BSize;

        for (unsigned i = 0; i < sb; i += BSize)
            assign<0, BSize>::eval(ref, that, i);

        for (unsigned i = sb; i < s; i++)
            ref[i] = that[i];

        return ref;
    }

private:
    V& ref;
};
```

- unroll<1>(u) = v + v + w 的计算时间为 1.72 μs。
- unroll<2>(u) = v + v + w 的计算时间为 1.52 μs。
- unroll<4>(u) = v + v + w 的计算时间为 1.36 μs。
- unroll<6>(u) = v + v + w 的计算时间为 1.37 μs。
- unroll<8>(u) = v + v + w 的计算时间为 1.4 μs。

```cpp
template <unsigned BSize, typename Vector>
typename Vector::value_type
inline one_norm(const Vector& v)
{
    using std::abs;
    typename Vector::value_type sum{0};
    unsigned s = size(v), sb = s / BSize * BSize;

    for (unsigned i = 0; i < sb; i += BSize)
        one_norm_ftor<0, BSize>::eval(sum, v, i);
    for (unsigned i = sb; i < s; ++i)
        sum += abs(v[i]);

    return sum;
}
```

```cpp
template <unsigned Offset, unsigned Max>
struct one_norm_ftor
{
    template <typename S, typename V>
    static void eval(S& sum, const V& v, unsigned i)
    {
        using std::abs;
        if constexpr (Offset < Max) {
            sum += abs(v[i + Offset]);
            one_norm_ftor<Offset + 1, Max>::eval(sum, v, i);
        }
    }
};
```

- one_norm<1>(v) 的计算时间为 0.788445 μs。
- one_norm<2>(v) 的计算时间为 0.43087 µs。
- one_norm<4>(v) 的计算时间为 0.436625 µs。
- one_norm<6>(v) 的计算时间为 0.43035 µs。
- one_norm<8>(v) 的计算时间为 0.461095 µs。

```cpp
template <unsigned BSize, typename Vector>
typename Vector::value_type
inline one_norm(const Vector& v)
{
    using std::abs;
    typename Vector::value_type sum[BSize] = {};

    unsigned s = size(v), sb = s / BSize * BSize;
    for (unsigned i = 0; i < sb; i += BSize)
        one_norm_ftor<0, BSize>::eval(sum, v, i);

    for (unsigned i = 1; i < BSize; ++i)
        sum[0] += sum[i];
    for (unsigned i = sb; i < s; ++i)
        sum[0] += abs(v[i]);

    return sum[0];
}
```

```cpp
template <unsigned Offset, unsigned Max>
struct one_norm_ftor
{
    template <typename S, typename V>
    static void eval(S* sum, const V& v, unsigned i)
    {
        using std::abs;
        if constexpr (Offset < Max) {
            sum[Offset] += abs(v[i + Offset]);
            one_norm_ftor<Offset + 1, Max>::eval(sum, v, i);
        }
    }
};
```

- one_norm<1>(v) 的计算时间为 0.797224 μs。
- one_norm<2>(v) 的计算时间为 0.45923 µs。
- one_norm<4>(v) 的计算时间为 0.538913 µs。
- one_norm<6>(v) 的计算时间为 0.467529 µs。
- one_norm<8>(v) 的计算时间为 0.506729 µs。

```cpp
template <unsigned BSize, typename Value>
struct multi_tmp
{
    using sub_type = multi_tmp<BSize - 1, Value>;

    multi_tmp(const Value& v) : value(v), sub(v) {}

    Value value;
    sub_type sub;
};

template <typename Value>
struct multi_tmp<0, Value>
{
    multi_tmp(const Value& v) {}
};
```

```cpp
template <unsigned Offset, unsigned Max>
struct one_norm_ftor
{
    template <typename S, typename V>
    static void eval(S& sum, const V& v, unsigned i)
    {
        using std::abs;
        if constexpr (Offset < Max) {
            sum.value += abs(v[i + Offset]);
            one_norm_ftor<Offset + 1, Max>::eval(sum.sub, v, i);
        }
    }
};
```

```cpp
template <unsigned BSize, typename Vector>
typename Vector::value_type
inline one_norm(const Vector& v)
{
    using std::abs;
    using value_type = typename Vector::value_type;
    multi_tmp<BSize, value_type> multi_sum{0};

    unsigned s = size(v), sb = s / BSize * BSize;
    for (unsigned i = 0; i < sb; i += BSize)
        one_norm_ftor<0, BSize>::eval(multi_sum, v, i);

    value_type sum = multi_sum.sum();
    for (unsigned i = sb; i < s; ++i)
        sum += abs(v[i]);

    return sum;
}
```

```cpp
template <unsigned BSize, typename Value>
struct multi_tmp
{
    Value sum() const { return value + sub.sum(); }
};
```

```cpp
template <typename Value>
struct multi_tmp<0, Value>
{
    Value sum() const { return 0; }
};
```

```cpp
template <unsigned BSize, typename Value>
struct multi_tmp
{
    template <typename Op>
    Value reduce(Op op, const Value& init) const
    { return op(value, sub.reduce(op, init)); }
};
```

```cpp
template <typename Value>
struct multi_tmp<0, Value>
{
    template <typename Op>
    Value reduce(Op, const Value& init) const { return init; }
};
```

- one_norm<1>(v) 的计算时间为 0.786668 μs。
- one_norm<2>(v) 的计算时间为 0.442476 µs。
- one_norm<4>(v) 的计算时间为 0.441455 µs。
- one_norm<6>(v) 的计算时间为 0.410978 µs。
- one_norm<8>(v) 的计算时间为 0.426368 µs。

```cpp
inline one_norm(const Vector& v)
{
    typename Vector::value_type s0{0}, s1{0}, s2{0}, ...
}
```


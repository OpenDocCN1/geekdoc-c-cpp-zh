

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
            assign<0, 4>()(*this, that, i);

        for (unsigned i = sb; i < s; ++i)
            data[i] = that[i];
        return *this;
    }
};
```

The assign functor is realized analogously to my_axpy_ftor:

```cpp
template <unsigned Offset, unsigned Max>
struct assign
{
    template <typename U, typename V>
    void operator()(U& u, const V& v, unsigned i)
    {
        u[i + Offset] = v[i + Offset];
        assign<Offset + 1, Max>()(u, v, i);
    }
};
```

```cpp
template <unsigned Max>
struct assign<Max, Max>
{
    template <typename U, typename V>
    void operator()(U& u, const V& v, unsigned i) {}
};
```

Computing the expression above yields

```
Compute time is 1.37 µs.
```

With this rather simple modification we now accelerated all vector expression templates. In comparison to the previous implementation, however, we lost the flexibility to customize the loop unrolling. The functor assign has two arguments, thus allowing for customization. The problem is the assignment operator. In principle we can define an explicit template argument here:

```cpp
template <unsigned BSize, typename Src>
vector& operator=(const Src& that)
{
    check_size(size(that));
    unsigned s = my_size, sb = s / BSize * BSize;
    for (unsigned i = 0; i < sb; i += BSize)
        assign<0, BSize>()(*this, that, i);
    for (unsigned i = sb; i < s; ++i)
        data[i] = that[i];
    return *this;
}
```

The drawback is that we cannot use the symbol = as a natural infix operator any longer. Instead we must write:

```
u.operator<=(v + v + w);
```

This has indeed a certain geeky charm, and one could also argue that people did, and still do, much more painful things for performance. Nonetheless, it does not meet our ideals of intuitiveness and readability.

Alternative notations are

```
unroll<4>(u = v + v + w);
```

or

```
unroll<4>(u) = v + v + w;
```

Both versions are implementable but while we find the latter more readable. The former expresses more correctly what we are doing, while the latter is easier to implement and the structure of the computed expression retains better visibility. Therefore we show the realization of the second form.

The function unroll is simple to implement: it just returns an object of type unroll_vector (see below) with a reference to the vector and type information for the unroll size:

```cpp
template <unsigned BSize, typename Vector>
unroll_vector<BSize, Vector> inline unroll(Vector& v)
{
    return unroll_vector<BSize, Vector>(v);
}
```

The class unroll_vector is not complicated either. It only needs to take a reference of the target vector and to provide an assignment operator:

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
            assign<0, BSize>()(ref, that, i);

        for (unsigned i = sb; i < s; ++i)
            ref[i] = that[i];
        return ref;
    }

private:
    V& ref;
};
```

Evaluating the considered vector expressions for some block sizes yields

- Compute time unroll<1>(v) = v + v + w is 1.72 µs.
- Compute time unroll<2>(v) = v + v + w is 1.52 µs.
- Compute time unroll<4>(v) = v + v + w is 1.36 µs.
- Compute time unroll<6>(v) = v + v + w is 1.37 µs.
- Compute time unroll<8>(v) = v + v + w is 1.4 µs.

These few benchmarks are consistent with the previous results; ie., unroll<1> is equal to the canonical implementation and unroll<4> is as fast as the hard-wired unrolling.

## 5.4.6 Tuning Reduction Operations

The techniques in this section are applicable in similar fashion to a variety of vector and matrix norms. They can also be used for dot products and tensor reductions.

### 5.4.6.1 Reducing on a Single Variable

```
=> c++03/reduction_unroll_example.cpp
```

In the preceding vector operations, the i-th entry of each vector was handled independently of any other entry. For reduction operations, they are related by one or more temporary variables. And these temporary variables can become a serious bottleneck.

First, we test whether a reduction operation, say, the discrete L1 norm (also known as the Manhattan norm), can be accelerated by the techniques from Section 5.4.4. We implement the one_norm function in terms of a functor for the iteration block:

```cpp
template <unsigned BSize, typename Vector>
typename Vector::value_type
inline one_norm(const Vector& v)
{
    using std::abs;

    typename Vector::value_type sum(0);
    unsigned s = size(v), sb = s / BSize * BSize;

    for (unsigned i = 0; i < sb; i += BSize)
        one_norm_ftor<0, BSize>()(sum, v, i);
    for (unsigned i = sb; i < s; ++i)
        sum += abs(v[i]);
    return sum;
}
```

The functor is also implemented in the same manner as before:

```cpp
template <unsigned Offset, unsigned Max>
struct one_norm_ftor
{
    template <typename S, typename V>
    void operator()(S& sum, const V& v, unsigned i)
    {
        using std::abs;
        sum += abs(v[i + Offset]);
        one_norm_ftor<Offset + 1, Max>()(sum, v, i);
    }
};

template <unsigned Max>
struct one_norm_ftor<Max, Max>
{
    template <typename S, typename V>
    void operator()(S& sum, const V& v, unsigned i) {}
};
```

For reductions, we can see a tuning benefit with more recent compilers like gcc 4.8:

- Compute time one_norm<1>(v) is 0.788445 µs.
- Compute time one_norm<2>(v) is 0.438087 µs.
- Compute time one_norm<4>(v) is 0.436625 µs.
- Compute time one_norm<6>(v) is 0.430335 µs.
- Compute time one_norm<8>(v) is 0.461095 µs.

This corresponds to a speedup of 1.8. Let us try some alternative implementations.

### 5.4.6.2 Reducing on an Array

```
=> c++0x/reduction_unroll_array_example.cpp
```

When we look at the previous computation, we see that a different entry of v is used in each iteration. But every computation accesses the same temporary variable sum, and this limits the concurrency. To provide more concurrency, we can use multiple temporaries7 in an array, for instance. The modified function then reads:

```cpp
template <unsigned BSize, typename Vector>
typename Vector::value_type
```

7. Strictly speaking, this is not true for every possible scalar type we can think of. The addition of the sum type must be a commutative monoid because we change the evaluation order. This holds of course for all intrinsic numeric types and certainly for almost all user-defined arithmetic types. However, we are free to define an addition that is not commutative or non-monoidal. In this case, our transformation would be wrong. To deal with such exceptions, we need semantic concepts which will hopefully become part of C++ at some point. (Especially since the author has already spent a lot of time with them.)

```cpp
inline one_norm(const Vector& v)
{
    using std::abs;
    typename Vector::value_type sum[BSize];
    for (unsigned i = 0; i < BSize; ++i)
        sum[i] = 0;

    unsigned s = size(v), sb = s / BSize * BSize;
    for (unsigned i = 0; i < sb; i += BSize)
        one_norm_ftor<0, BSize>()(sum, v, i);

    for (unsigned i = 1; i < BSize; ++i)
        sum[0] += sum[i];
    for (unsigned i = sb; i < s; ++i)
        sum[0] += abs(v[i]);

    return sum[0];
}
```

Now, each instance of one_norm_ftor operates on another entry of the sum array:

```cpp
template <unsigned Offset, unsigned Max>
struct one_norm_ftor
{
    template <typename S, typename V>
    void operator()(S* sum, const V& v, unsigned i)
    {
        using std::abs;
        sum[Offset] = abs(v[i + Offset]);
        one_norm_ftor<Offset + 1, Max>()(sum, v, i);
    }
};
```

```cpp
template <unsigned Max>
struct one_norm_ftor<Max, Max>
{
    template <typename S, typename V>
    void operator()(S* sum, const V& v, unsigned i) {}
};
```

Running this implementation on the test machine yielded

- Compute time one_norm<1>(v) is 0.797224 µs.
- Compute time one_norm<2>(v) is 0.45923 µs.
- Compute time one_norm<4>(v) is 0.538913 µs.
- Compute time one_norm<6>(v) is 0.467529 µs.
- Compute time one_norm<8>(v) is 0.586729 µs.

This is even a bit slower than the version with one variable. Maybe an array is more expensive to pass as an argument even in an inline function. Let us try something else.


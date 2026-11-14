
As mentioned before, deduced template types, like the vector types in our case, must be defined at the end of the parameter list and the explicitly given arguments, in our case the block size, must be passed to the first template parameters. The implementation of the block statement in the first loop can be implemented similarly to the static functor in Section 5.4.1. We deviate a bit from this implementation by using two template parameters where the first one is increased until it is equal to the second. We observed that this approach yielded faster binaries on g++ than using only one argument and counting it down to zero. In addition, the two-argument version is more consistent with the multi-dimensional implementation in Section 5.4.7. As for fixed-size unrolling, we need a recursive template definition. Within each eval, a single operation is performed:

```
template <unsigned Offset, unsigned Max>
struct my_axpy_ftor
{
 template <typename U, typename V, typename W>
 static void eval(U& u, const V& v, const W& w, unsigned i)
 {
 if constexpr (Offset < Max) {
 u[i+Offset]= 3.0f * v[i+Offset] + w[i+Offset];
 my_axpy_ftor<Offset+1, Max>::eval(u, v, w, i);
 }
 }
};
```

The only difference from fixed-size unrolling is that the indices are relative to the index i. eval() is first called with Offset equal to 0, then with 1, 2, and so on. Since each call is inlined, the (static) functor call behaves like one monolithic block of operations without loop control and function call. Thus, the call of my_axpy_ftor<0, 4>::eval(u, v, w, i) performs the same operations as one iteration of the first loop in Listing 5-5. Performing the considered vector operation with different unrolling parameters resulted in:

```
Compute time unrolled<2> loop is 0.667546 µs.
Compute time unrolled<4> loop is 0.601179 µs.
Compute time unrolled<6> loop is 0.565536 µs.
Compute time unrolled<8> loop is 0.570061 µs.
```

Now we can call this operation for any block size we like. On the other hand, it is an unacceptable programming effort to provide such functors for each vector expression. Therefore, we will now combine this technique with expression templates.

## 5.4.5 Tuning an Expression Template

```
=> c++17/vector_unroll_example2.cpp
```

In Section 5.3.3, we implemented expression templates for vector sums (without unrolling). In the same manner we could implement a scalar-vector product, but we leave this as Exercise 5.7.5 for the motivated reader and consider expressions with addition only, e.g.:

```
u = v + v + w
```

Our baseline performance is:

```
Compute time is 1.72 µs.
```

To incorporate meta-tuning into expression templates, we only need to modify the actual assignment because this is where all loop-based vector operations are performed. The other operations (addition, subtraction, scaling, ...) solely return small objects containing references. We can split the loop in operator= as before into the unrolled part at the beginning and the completion at the end:

```
template <typename T>
class vector
{
	template <typename Src>
	vector& operator=(const Src& that)
	{
		check_size(size(that));
		unsigned s = my_size, sb = s / 4 * 4;

		for (unsigned i=0; i < sb; i+= 4)
			assign<0, 4>::eval(*this, that, i);

		for (unsigned i=sb; i < s; ++i)
			data[i] = that[i];
	}

	return *this;
};
};
```

The `assign` functor is realized analogously to `my_axpy_ftor`:

```
template <unsigned Offset, unsigned Max>
struct assign
{
    template <typename U, typename V>
    static void eval(U& u, const V& v, unsigned i)
    {
        if constexpr (Offset < Max) {
            u[i+Offset] = v[i+Offset];
            assign<Offset+1, Max>::eval(u, v, i);
        }
    }
};
```

Computing the expression above yielded:

```
Compute time is 1.37 µs.
```

With this rather simple modification we now accelerated all vector expression templates. In comparison to the previous implementation, however, we lost the flexibility to customize the loop unrolling. The functor `assign` has two arguments, thus allowing for customization. The problem is the assignment operator. In principle we can define an explicit template argument here:

```
template <unsigned BSize, typename Src>
vector& operator=(const Src& that)
{
    check_size(size(that));
    unsigned s= my_size, sb= s / BSize * BSize;

    for (unsigned i= 0; i < sb; i+= BSize)
        assign<0, BSize>::eval(*this, that, i);

    for (unsigned i= sb; i < s; ++i)
        data[i]= that[i];

    return *this;
}
```

But the drawback of this is that we cannot use the symbol = as a natural infix operator any longer. Instead we must write:

```
u.template operator=<4>(v + v + w);
```

This has indeed a certain geeky charm, and one could also argue that people did, and still do, much more painful things for performance. Nonetheless, it does not meet our ideals of intuitiveness and readability. Alternative notations are:

```
unroll<4>(u = v + v + w);
```

and:

```
unroll<4>(u) = v + v + w;
```

Both versions can be implemented. The former expresses better what we do. The second is easier to implement and more readable as the structure of the calculated expression is clearer without the surrounding parentheses. Therefore, we will implement the latter (as in MTL4). The function unroll is simple to implement: it just returns an object of type unroll_vector with a reference to the vector and type information for the unroll size:

```
template <unsigned BSize, typename Vector>
auto unroll(Vector& v)
{
    return unroll_vector<BSize, Vector>(v);
}
```

The class unroll_vector is not complicated either. It only needs to take a reference of the target vector and to provide an assignment operator:

```
template <unsigned BSize, typename V>
class unroll_vector
{
    public:
    unroll_vector(V& ref) : ref(ref) {}

    template <typename Src>
    V& operator=(const Src& that)
    {
        assert(size(ref) == size(that));
        unsigned s = size(ref), sb= s / BSize * BSize;

        for (unsigned i=0; i < sb; i+= BSize)
            assign<0, BSize>::eval(ref, that, i);

        for (unsigned i=sb; i < s; i++)
            ref[i]= that[i];
        return ref;
    }
private:
    V& ref;
};
```

Evaluating the considered vector expressions for some block sizes resulted in:

```
Compute time unroll<1>(u) = v + v + w is 1.72 µs.
Compute time unroll<2>(u) = v + v + w is 1.52 µs.
Compute time unroll<4>(u) = v + v + w is 1.36 µs.
Compute time unroll<6>(u) = v + v + w is 1.37 µs.
Compute time unroll<8>(u) = v + v + w is 1.4 µs.
```

These few benchmarks are consistent with the previous results; i.e., unroll<1> is equal to the canonical implementation and unroll<4> is as fast as the hard-wired unrolling.

## 5.4.6 Tuning Reduction Operations

The techniques in this section are applicable in similar fashion to a variety of vector and matrix norms. They can also be used for dot products and tensor reductions.

### 5.4.6.1 Reducing on a Single Variable

```
=> c++17/reduction_unroll_example.cpp
```

In the preceding vector operations, the i-th entry of each vector was handled independently of any other entry. For reduction operations, all operations are related to one or a few temporary variables. And these temporary variables can become a serious bottleneck.

First, we test whether a reduction operation, say, the discrete L1 norm, can be accelerated by the techniques from Section 5.4.4. We implement the one_norm function by calling a functor in the block iteration:

```
template <unsigned BSize, typename Vector>
typename Vector::value_type inline one_norm(const Vector& v)
{
    using std::abs;
    typename Vector::value_type sum(0);
    unsigned s = size(v), sb= s / BSize * BSize;
    for (unsigned i= 0; i < sb; i+= BSize)
        one_norm_ftor<0, BSize>::eval(sum, v, i);
    for (unsigned i= sb; i < s; ++i)
        sum+= abs(v[i]);
    return sum;
}
```

The functor is also implemented in the same manner as before:

```
template <unsigned Offset, unsigned Max>
struct one_norm_ftor
{
    template <typename S, typename V>
    static void eval(S& sum, const V& v, unsigned i)
    {
        using std::abs;
        if constexpr (Offset < Max) {
            sum+= abs(v[i+Offset]);
            one_norm_ftor<Offset+1, Max>::eval(sum, v, i);
        }
    }
};
```

For reductions, we can see a tuning benefit with g++ 4.8:

```
Compute time one_norm<1>(v) is 0.788445 µs.
Compute time one_norm<2>(v) is 0.43087 µs.
Compute time one_norm<4>(v) is 0.436625 µs.
```

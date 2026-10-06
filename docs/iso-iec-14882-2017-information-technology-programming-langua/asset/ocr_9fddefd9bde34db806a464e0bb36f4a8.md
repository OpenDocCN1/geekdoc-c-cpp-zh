# ISO/IEC 14882:2017(E)

# 29.6.8.2 Uniform distributions [rand.dist.uni]

# 29.6.8.2.1 Class template uniform_int_distribution [rand.dist.uni.int]

A uniform_int_distribution random number distribution produces random integers, $a \le t \le b$, distributed according to the constant discrete probability function

> $p(i|a, b) = 1/(b - a + 1)$

```
template<class IntType = int>
class uniform_int_distribution {
public:
    // types
    using result_type = IntType;
    using param_type = unspecified;

    // constructors and reset functions
    explicit uniform_int_distribution(IntType a = 0, IntType b = numeric_limits<IntType>::max());
    explicit uniform_int_distribution(const param_type& param);
    void reset();

    // generating functions
    template<class URG>
    result_type operator()(URG& g);
    template<class URG>
    result_type operator()(URG& g, const param_type& param);

    // property functions
    result_type a() const;
    result_type b() const;
    param_type param() const;
    void param(const param_type& param);
    result_type min() const;
    result_type max() const;
};
lex uniform_int_distribution(IntType a = 0, IntType b = numeric_limits<IntType>::max());
```

+   - a <= b.

+   - Effects: Constructs a uniform_int_distribution object; and a and b correspond to the respective parameters of the distribution.

result_type a() const;

+   - Returns: The value of the parameter with which the object was constructed.

result_type b() const;

+   - Returns: The value of the b parameter with which the object was constructed.

# 29.6.8.2.2 Class template uniform_real_distribution [rand.dist.real]

A uniform_real_distribution random number distribution produces random numbers, $a \le x \le b$, distributed according to the constant probability density function

> $p(x|a, b) = 1/(b - a)$

[Note: This implies that $p(x|a, b)$ is undefined when $a == b$.]
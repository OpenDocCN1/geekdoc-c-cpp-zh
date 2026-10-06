
# ISO/IEC 14882:2017(E)

```cpp
template<class RealType = double>
class uniform_real_distribution {
public:
    // types
    using result_type = RealType;
    using parm_type = unspecified;

    // constructors and reset functions
    explicit uniform_real_distribution(RealType a = 0.0, RealType b = 1.0);
    explicit uniform_real_distribution(const parm_type& b);
    void reset();

    // generating functions
    template<class URBG>
    result_type operator()(URBG& g);
    template<class URBG>
    result_type operator()(URBG& g, const parm_type& b);

    // property functions
    result_type a() const;
    result_type b() const;
    parm_type param() const;
    void set_param(const parm_type& b);
    result_type min() const;
    result_type max() const;
};
```

uniform_real_distribution(RealType a = 0.0, RealType b = 1.0);

> Requires: a ≤ b and a >= numeric_limits<RealType>::max().

> Effects: Constructs a uniform_real_distribution object; a and b correspond to the parameters of the distribution.

result_type a() const;

> Returns: The value of the a parameter with which the object was constructed.

result_type b() const;

> Returns: The value of the b parameter with which the object was constructed.

# 29.6.8.3 Bernoulli distributions

## 29.6.8.3.1 Class Bernoulli_distribution

A bernoulli_distribution random number distribution produces values b distributed according to the discrete probability function

```
P(b|p) = { p if b = true; 1 - p if b = false }
```

```cpp
class bernoulli_distribution {
public:
    // types
    using result_type = bool;
    using parm_type = unspecified;

    // constructors and reset functions
    explicit bernoulli_distribution(double p = 0.5);
    explicit bernoulli_distribution(const param_type& param);
    void reset();

    // generating functions
    template<class URBG>
    result_type operator()(URBG& g);
    template<class URBG>
    result_type operator()(URBG& g, const param_type& param);

    // property functions
    double p() const;
    param_type param() const;
    void param(const param_type& param);
    result_type min() const;
    result_type max() const;
};
```

explicit bernoulli_distribution(double p = 0.5);

- Requires: 0 ≤ p ≤ 1.
- Effects: Constructs a bernoulli_distribution object; p corresponds to the parameter of the distribution.

double p() const;

- Returns: The value of the p parameter with which the object was constructed.

## 29.6.8.3 Class binomial_distribution [rand.dist.bern.bin]

A Binomial distribution random number produces integer values i ≥ 0 distributed according to the discrete probability function

> $P(i, t, p) = \binom{t}{i} p^i (1-p)^{t-i}$

```cpp
template<class IntType = int>
class binomial_distribution {
public:
    // types
    using result_type = IntType;
    using param_type = unspecified;

    // constructors and reset functions
    explicit binomial_distribution(IntType t = 1, double p = 0.5);
    explicit binomial_distribution(const param_type& param);
    void reset();

    // generating functions
    template<class URBG>
    result_type operator()(URBG& g);
    template<class URBG>
    result_type operator()(URBG& g, const param_type& param);

    // property functions
    IntType t() const;
    double p() const;
    param_type param() const;
    void param(const param_type& parm);
    result_type min() const;
    result_type max() const;
};
```

explicit binomial_distribution(IntType t = 1, double p = 0.5);

- Requires: 0 ≤ p ≤ 1 and 0 ≤ t.
- Effects: Constructs a binomial_distribution object; t and p correspond to the respective parameters of the distribution.

IntType t() const;

- Returns: The value of the t parameter with which the object was constructed.

double p() const;

## 29.6.8.3.3 Class template geometric_distribution [rand.dist.geo]

- A geometric_distribution random number generator produces integer i ≥ 0 distributed according to the discrete probability function

> P(i) = p(1-p)i.

```cpp
template<class IntType>
class geometric_distribution {
public:
    // types
    using result_type = IntType;
    using param_type = unspecified;

    // constructors and reset functions
    explicit geometric_distribution(double p = 0.5);
    explicit geometric_distribution(const param_type& parm);
    void reset();

    // generating functions
    template<class URBG>
    result_type operator()(URBG& g);
    template<class URBG>
    result_type operator()(URBG& g, const param_type& parm);

    // property functions
    double p() const;
    param_type param() const;
    void param(const param_type& parm);
    result_type min() const;
    result_type max() const;
};
```

explicit geometric_distribution(double p = 0.5);

- Requires: 0 < p < 1.
- Effects: Constructs a geometric_distribution object; p corresponds to the parameter of the distribution.

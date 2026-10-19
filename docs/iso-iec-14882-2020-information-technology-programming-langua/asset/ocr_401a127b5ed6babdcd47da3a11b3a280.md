# ISO/IEC 14882:2020(E)

The distribution parameter μ is also known as this distribution's mean.

```
template<class IntType = int>
class poisson_distribution
{
public:
    // types
    using result_type = IntType;
    using param_type  = unspecified;

    // constructors and reset functions
    poisson_distribution() : poisson_distribution(1.0) {}
    explicit poisson_distribution(double mean);
    explicit poisson_distribution(const param_type& parm);
    void reset();

    // generating functions
    template<class URBG>
        result_type operator()(URBG& g);
    template<class URBG>
        result_type operator()(URBG& g, const param_type& parm);

    // property functions
    double mean() const;
    param_type param() const;
    void param(const param_type& parm);
    result_type min() const;
    result_type max() const;
};
```

```
explicit poisson_distribution(double mean);
```

2 Preconditions: 0 < mean.

3 Remarks: mean corresponds to the parameter of the distribution.

```
double mean() const;
```

4 Returns: The value of the mean parameter with which the object was constructed.

# 26.6.9.4.2 Class template exponential_distribution [rand.dist.pois.exp]

1 An exponential_distribution random number distribution produces random numbers x > 0 distributed according to the probability density function

p(x | λ) = λ e^{-λ x}.

```
template<class RealType = double>
class exponential_distribution {
public:
    // types
    using result_type = RealType;
    using param_type  = unspecified;

    // constructors and reset functions
    exponential_distribution() : exponential_distribution(1.0) {}
    explicit exponential_distribution(RealType lambda);
    explicit exponential_distribution(const param_type& parm);
    void reset();

    // generating functions
    template<class URBG>
        result_type operator()(URBG& g);
    template<class URBG>
        result_type operator()(URBG& g, const param_type& parm);
```
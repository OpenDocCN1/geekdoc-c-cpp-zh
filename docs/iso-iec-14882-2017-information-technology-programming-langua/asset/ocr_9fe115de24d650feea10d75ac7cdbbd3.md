# ISO/IEC 14882:2017(E)

using result_type = RealType;
using param_type = unspecified;

// constructors and reset functions
explicit exponential_distribution(RealType lambda = 1.0);
explicit exponential_distribution(const param_type& parm);
void reset();

// generating functions
template<class URBG>
result_type operator()(URBG& g);
template<class URBG>
result_type operator()(URBG& g, const param_type& parm);

// property functions
RealType lambda() const;
param_type param() const;
void param(const param_type& parm);
result_type min() const;
result_type max() const;
};

exponential_distribution(RealType lambda = 1.0);

+   Requires: 0 < lambda.
Effects: Constructs an exponential_distribution object; lambda corresponds to the parameter of the distribution.

RealType lambda() const;

Returns: The value of the lambda parameter with which the object was constructed.

# 29.6.8.4.3 Class gamma_distribution [rand.dist.pois.gamma]

A gamma_distribution random number produces random numbers x > 0 distributed according to the probability function

```
$p(x|\alpha,\beta) = \frac{e^{-x/\beta}}{\Gamma(\alpha)} x^{\alpha-1}$
```

```
templateclass RealType = double
class gamma_distribution {
public:
    // types
    using result_type = RealType;
    using param_type = unspecified;

    // constructors and reset functions
    explicit gamma_distribution(RealType alpha = 1.0, RealType beta = 1.0);
    explicit gamma_distribution(const param_type& parm);
    void reset();

    // generating functions
template<class URBG>
    result_type operator()(URBG& g);
template<class URBG>
    result_type operator()(URBG& g, const param_type& parm);
```

§ 29.6.8.4.3 ©ISO/IEC 2017 - All reserved 1089
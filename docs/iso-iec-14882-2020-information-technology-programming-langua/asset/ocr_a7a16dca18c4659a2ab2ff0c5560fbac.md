# ISO/IEC 14882:2020(E)

# 26.6.9.6.2 Class template piecewise_constant_distribution [rand.dist.samp.pconst]

1 A piecewise_constant_distribution random number distribution produces random numbers x, b0 ≤ x < b_n, uniformly distributed over each subinterval [b_i, b_{i+1}) according to the probability density function

p(x | b0, …, b_n, ρ0, …, ρ_{n−1}) = ρ_i , for b_i ≤ x < b_{i+1}.

2 The n + 1 distribution parameters b_i, also known as this distribution’s interval boundaries, shall satisfy the relation b_i < b_{i+1} for i = 0, …, n − 1. Unless specified otherwise, the remaining n distribution parameters are calculated as:

ρ_k = w_k / [S · (b_{k+1} − b_k)] for k = 0, …, n − 1 ,

in which the values w_k, commonly known as the weights, shall be non-negative, non-NaN, and non-infinity. Moreover, the following relation shall hold: 0 < S = w0 + ⋯ + w_{n−1}.

```
template<class RealType = double>
class piecewise_constant_distribution {
public:
// types
using result_type = RealType;
using param_type = unspecified;

// constructor and reset functions
piecewise_constant_distribution();
template<class InputIteratorB, class InputIteratorW>
piecewise_constant_distribution(InputIteratorB firstB, InputIteratorB lastB, InputIteratorW firstW);
template<class UnaryOperation>
piecewise_constant_distribution(initializer_list<RealType> b1, UnaryOperation fw);
template<class UnaryOperation>
piecewise_constant_distribution(size_t nw, RealType xmin, RealType xmax, UnaryOperation fw);
explicit piecewise_constant_distribution(const param_type& parm);
void reset();

// generating functions
template<class URBG>
result_type operator()(URBG& g);
template<class URBG>
result_type operator()(URBG& g, const param_type& parm);

// property functions
vector<result_type> intervals() const;
vector<result_type> densities() const;
param_type param() const;
void param(const param_type& parm);
result_type min() const;
result_type max() const;
};

piecewise_constant_distribution();
```

3 Effects: Constructs a piecewise_constant_distribution object with n = 1, ρ0 = 1, b0 = 0, and b1 = 1.

```
template<class InputIteratorB, class InputIteratorW>
piecewise_constant_distribution(InputIteratorB firstB, InputIteratorB lastB, InputIteratorW firstW);
```

4 Mandates: Both of

+   (4.1) — is_convertible_v<iterator_traits<InputIteratorB>::value_type, double>
+   (4.2) — is_convertible_v<iterator_traits<InputIteratorW>::value_type, double>
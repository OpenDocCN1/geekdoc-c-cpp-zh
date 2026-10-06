
# ISO/IEC 14882:2017(E)

```
InputIteratorW first;
template<class UnaryOperation>
piecewise_constant_distribution(initializer_list<RealType> bl, UnaryOperation fw);
template<class UnaryOperation>
piecewise_constant_distribution(size_t nw, RealType xmin, RealType xmax,
UnaryOperation fw);
explicit piecewise_constant_distribution(const param_type& param);
void reset();

// generating functions
template<class URBG>
result_type operator()(URBG& g);
template<class URBG>
result_type operator()(URBG& g, const param_type& param);

// property functions
vector<result_type> intervals() const;
vector<param_type> densities() const;
param_type param() const;
void param(const param_type& param);
result_type min() const;
result_type max() const;
```

```
piecewise_constant_distribution();
```

- 3 Effects: Constructs a piecewise_constant_distribution object with n = 1, ρ0 = 1, b0 = 0, and b1 = 1.

```
template<class IteratorB, class IteratorW>
piecewise_constant_distribution(IteratorB firstB, IteratorB firstB, IteratorB lastB,
IteratorW firstW);
```

- 4 Requires: IteratorB and IteratorW shall satisfy the requirements of an input iterator (Table T9). Moreover, traits<IteratorB>::value_type and traits<IteratorW>::value_type shall define a type that is convertible to double. If firstB == lastB or ++firstB == lastB, then shall form a sequence b of length n + 1, the length of the sequence starting from firstW shall be at least n, and any w_k for k ≥ n shall be given by the distribution.

- 5 Effects: Constructs a piecewise_constant_distribution object with parameters as specified above.

```
template<class UnaryOperation>
piecewise_constant_distribution(initializer_list<RealType> bl, UnaryOperation fw);
```

- 6 Requires: Each instance of type UnaryOperation shall be a function (23.14) whose return value shall be convertible to double. Moreover, double shall be convertible to the type of UnaryOperation’s parameter.

- 7 Effects: Constructs a piecewise_constant_distribution object with parameters or calculated from the following values: if bl.size() < 2, then n = 1, b0 = 0, and b1 = 1. Otherwise, let bl.begin(), bl.end() form a sequence b0, b1, ..., bn, and w_k = fw((b_{k+1}+b_k)/2) for k = 0, ..., n-1.

- 8 Complexity: The number of invocations of fw shall not exceed n.

```
template<class UnaryOperation>
piecewise_constant_distribution(size_t nw, RealType xmin, RealType xmax, UnaryOperation fw);
```

- 9 Requires: Each instance of type UnaryOperation shall be a function (23.14) whose return type shall be convertible to double. Moreover, double should be convertible to the UnaryOperation's sole parameter. If nw = 0, n = 1, otherwise n = nw. The relation 0 < δ = (xmax - xmin)/n shall hold.

Effects: A piecewise_constant_distribution object with parameters taken calculated from the following values: b_k = xmin-k*δ for k = 0, ..., n, and w_k = fw(b_k+δ/2) for k = 0, ..., n-1.

Complexity: The number of invocations of fw shall not exceed n.

```
template<result_type> invokes() const;
```

Returns: A vector<result_type> whose size member n + 1 and whose operator[] member b_k when invoked for k = 0, ..., n.

```
vector<result_type> densities() const;
```

Returns: A vector<result_type> whose size member n and whose operator[] member w_k when invoked for k = 0, ..., n.

## 29.6.8.3 Class piecewise_linear_distribution

A piecewise_linear_distribution random number produces random numbers x, b_0 ≤ x ≤ bn, over each subinterval [b_i, b_{i+1}) to the probability density function

```
p(x|b_0, ..., b_n, ρ_0, ..., ρ_n) = ρ_i * (x - b_i)/(b_{i+1} - b_i) + ρ_{i+1} * (b_{i+1} - x)/(b_{i+1} - b_i), for b_i ≤ x < b_{i+1}.
```

The 2 parameters b_i and ρ_i also known as, shall satisfy the interval boundaries b_0 < b_1 < ... < b_n for i = 0, ..., n-1. Unless specified, the remaining n+1 distribution parameters are calculated as ρ_k = w_k/S for k = 0, ..., n, in which values w_k, commonly known as the weights at boundaries, are non-negative, not NaN and not infinity. Moreover, the following relation shall hold:

```
0 < S = ∑_{k=0}^{n-1} (w_k + w_{k+1})*(b_{k+1} - b_k)/2.
```

```
template<class RealType = double>
public:
  // types
  using result_type = RealType;
  using param_type = unspecified;

  // constructor and reset functions
  template<class IteratorB>
  piecewise_linear_distribution(IteratorB firstB, IteratorB lastB, IteratorB firstB, IteratorB first);

  template<class UnaryOperation>
  piecewise_linear_distribution(initializer_list<RealType> bl, UnaryOperation fw);

  template<class UnaryOperation>
  piecewise_linear_distribution(size_t n, RealType xmin, RealType xmax, UnaryOperation fw);
  explicit piecewise_linear_distribution(const param_type& param);

  void reset() {
  

  // generating functions
  template<class URB>
  result_type operator()(URB& g);

  template<class URBG>
  result_type operator()(URBG& g, const param_type& param);

  // property functions
vector<result_type> intervals() const;
vector<result_type> densities() const;
param_type param() const;
void param(const param_type& param) const;
result_type min() const;
result_type max() const;
};

piecewise_linear_distribution();

Effects: Constructs a piecewise_linear_distribution object with n = 1, ρ₀ = 1, b₀ = 0, and b₁ = 1.

```
template<class IteratorB, class IteratorW>
piecewise_linear_distribution(IteratorB firstB, IteratorB lastB, IteratorWW = IteratorW())
```

Requires: IteratorB and IteratorW each satisfy the requirements of an input iterator (Table 9). Moreover, traits<IteratorB>::value_type and traits<IteratorW>::value_type must be convertible to double. If firstB == lastB, then shall form a sequence of length n+1, and the length of the sequence starting from firstW shall be at least n+1, and any w_k for k ≥ n+1 shall be ignored by the distribution.

Effects: Constructs a piecewise_linear_distribution with parameters as specified above.

```
template<class UnaryOperation>
piecewise_linear_distribution(initial_value, list<RealType>, UnaryOperation fw);
```

Requires: Each instance of type UnaryOperation shall be a function (23.14) whose return value shall be convertible to double. Moreover, double shall be convertible to the type of UnaryOperation’s parameter.

Effects: Constructs a piecewise_linear_distribution object with parameters or calculated from the following values: if bl.size() < 2, then n = 1, b0 = 0, and b1 = 1. Otherwise, let bl.begin(), bl.end() form a sequence b0, b1, ..., bn, and w_k = fw((b_{k+1}+b_k)/2) for k = 0, ..., n-1.

Complexity: The number of invocations of fw shall not exceed n+1.

```
template<class UnaryOperation>
piecewise_linear_distribution(size_t nw, RealType xmin, RealType xmax, UnaryOperation fw);
```

Requires: Each instance of type UnaryOperation shall be a function (23.14) whose return type shall be convertible to double. Moreover, double should be convertible to the UnaryOperation's sole parameter. If nw = 0, n = 1, otherwise n = nw. The relation 0 < δ = (xmax - xmin)/n shall hold.

Effects: A piecewise_linear_distribution object with parameters taken calculated from the following values: b_k = xmin-k*δ for k = 0, ..., n, and w_k = fw(b_k+δ/2) for k = 0, ..., n-1.

Complexity: The number of invocations of fw shall not exceed n+1.

```
template<result_type> invokes() const;
```

Returns: A vector<result_type> whose size member n + 1 and whose operator[] member b_k when invoked for k = 0, ..., n.

```
vector<result_type> densities() const;
```

Returns: A vector<result_type> whose size member n and whose operator[] member w_k when invoked for k = 0, ..., n.

## 29.6.9 Low-quality random number generation

Note: The header <stdlib> (21.2.2) defines the functions described in this subclause.

```
int rand();
void srand(unsigned int seed);
```

Effects: The rand and srand functions have the semantics specified in the C library.

Remarks: The implementation may specify that particular library functions may call rand. It is implementation-defined whether the rand function may data race (29.5.5.9). Note: The other random number generation facilities in this document (29.6) are often preferable to rand, because rand's underlying algorithm is unpredictable and of questionable quality and performance.

SEE ALSO: ISO C 7.2.2

## 29.7 Numeric arrays

### 29.7.1 Header <initializer_list>

```cpp
#include <initializer_list>

namespace std {
template<class T> class valarray; // An array of type T
class slice;
template<class T> class slice_array; // a BLAS-like slice out of an array
class gslice; // a generalized slice
template<class T> class gslice_array; // a generalized slice out of an array
template<class T> class mask_array; // a masked array
template<class T> class indirect_array; // an indirect array

template<class T> void swap(valarray<T>, valarray<T>) noexcept;

template<class T> valarray<T> operator+(const valarray<T>&, const valarray<T>&);
template<class T> valarray<T> operator+(const valarray<T>&, const T&);
template<class T> valarray<T> operator+(const T&, const valarray<T>);

template<class T> valarray<T> operator-(const valarray<T>&, const valarray<T>&);
template<class T> valarray<T> operator-(const valarray<T>&, const T&);
template<class T> valarray<T> operator-(const T&, const valarray<T>);

template<class T> valarray<T> operator*(const valarray<T>&, const valarray<T>&);
template<class T> valarray<T> operator*(const valarray<T>&, const T&);
template<class T> valarray<T> operator*(const T&, const valarray<T>);

template<class T> valarray<T> operator+=(const valarray<T>&, const valarray<T>&);
template<class T> valarray<T> operator+=(const valarray<T>&, const T&);
template<class T> valarray<T> operator+=(const T&, const valarray<T>);

template<class T> valarray<T> operator-=(const valarray<T>&, const valarray<T>&);
template<class T> valarray<T> operator-=(const valarray<T>&, const T&);
template<class T> valarray<T> operator-=(const T&, const valarray<T>);

template<class T> valarray<T> operator*=(const valarray<T>&, const valarray<T>&);
template<class T> valarray<T> operator*=(const valarray<T>&, const T&);
template<class T> valarray<T> operator*=(const T&, const valarray<T>);

template<class T> valarray<T> operator-();
```

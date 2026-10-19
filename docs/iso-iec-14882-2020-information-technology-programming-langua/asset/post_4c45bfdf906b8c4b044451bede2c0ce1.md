
```
template<class UnaryOperation>
    piecewise_linear_distribution(initializer_list<RealType> bl, UnaryOperation fw);
template<class UnaryOperation>
    piecewise_linear_distribution(size_t nw, RealType xmin, RealType xmax, UnaryOperation fw);
explicit piecewise_linear_distribution(const param_type& parm);
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
```

```
piecewise_linear_distribution();
```

Effects: Constructs a piecewise_linear_distribution object with n = 1, ρ₀ = ρ₁ = 1, b₀ = 0, and b₁ = 1.

```
template<class InputIteratorB, class InputIteratorW>
piecewise_linear_distribution(InputIteratorB firstB, InputIteratorB lastB,
                                InputIteratorW firstW);
```

Mandates: is_invocable_r_v<double, UnaryOperation&, double> is true.

Preconditions: InputIteratorB and InputIteratorW each meet the Cpp17InputIterator requirements (23.3.5.3). If firstB == lastB or ++firstB == lastB, let n = 1, ρ₀ = ρ₁ = 1, b₀ = 0, and b₁ = 1. Otherwise, [firstB,lastB) forms a sequence b of length n + 1, the length of the sequence w starting from firstW is at least n + 1, and any w_k for k ≥ n + 1 are ignored by the distribution.

Effects: Constructs a piecewise_linear_distribution object with parameters as specified above.

```
template<class UnaryOperation>
piecewise_linear_distribution(initializer_list<RealType> bl, UnaryOperation fw);
```

Mandates: is_invocable_r_v<double, UnaryOperation&, double> is true.

Effects: Constructs a piecewise_linear_distribution object with parameters taken or calculated from the following values: If bl.size() < 2, let n = 1, ρ₀ = ρ₁ = 1, b₀ = 0, and b₁ = 1. Otherwise, let [bl.begin(),bl.end()) form a sequence b₀,...,bₙ, and let w_k = fw(b_k) for k = 0,...,n.

Complexity: The number of invocations of fw does not exceed n + 1.

```
template<class UnaryOperation>
piecewise_linear_distribution(size_t nw, RealType xmin, RealType xmax, UnaryOperation fw);
```

Mandates: is_invocable_r_v<double, UnaryOperation&, double> is true.

Preconditions: If nw = 0, let n = 1, otherwise let n = nw. The relation 0 < δ = (xmax − xmin)/n holds.

Effects: Constructs a piecewise_linear_distribution object with parameters taken or calculated from the following values: Let b_k = xmin + k · δ for k = 0,...,n, and w_k = fw(b_k) for k = 0,...,n.

Complexity: The number of invocations of fw does not exceed n + 1.

```
vector<result_type> intervals() const;
```

Returns: A vector<result_type> whose size member returns n + 1 and whose operator[] member returns b_k when invoked with argument k for k = 0,...,n.

## ISO/IEC 14882:2020(E)

```
valarray<bool> operator!() const;
```

Mandates: The indicated operator can be applied to operands of type T and returns a value of type T (bool for operator!) or which may be unambiguously implicitly converted to type T (bool for operator!).

Returns: A valarray whose length is size(). Each element of the returned array is initialized with the result of applying the indicated operator to the corresponding element of the array.

### 26.7.2.7 Compound assignment [valarray.cassign]

```
valarray& operator*= (const valarray& v);
valarray& operator/= (const valarray& v);
valarray& operator%= (const valarray& v);
valarray& operator+= (const valarray& v);
valarray& operator-= (const valarray& v);
valarray& operator^= (const valarray& v);
valarray& operator&= (const valarray& v);
valarray& operator|= (const valarray& v);
valarray& operator<<=(const valarray& v);
valarray& operator>>=(const valarray& v);
```

Mandates: The indicated operator can be applied to two operands of type T.

Preconditions: size() == v.size() is true.

The value of an element in the left-hand side of a valarray compound assignment operator does not depend on the value of another element in that left hand side.

Effects: Each of these operators performs the indicated operation on each of the elements of *this and the corresponding element of v.

Returns: *this.

Remarks: The appearance of an array on the left-hand side of a compound assignment does not invalidate references or pointers.

```
valarray& operator*= (const T& v);
valarray& operator/= (const T& v);
valarray& operator%= (const T& v);
valarray& operator+= (const T& v);
valarray& operator-= (const T& v);
valarray& operator^= (const T& v);
valarray& operator&= (const T& v);
valarray& operator|= (const T& v);
valarray& operator<<=(const T& v);
valarray& operator>>=(const T& v);
```

Mandates: The indicated operator can be applied to two operands of type T.

Effects: Each of these operators applies the indicated operation to each element of *this and v.

Returns: *this

Remarks: The appearance of an array on the left-hand side of a compound assignment does not invalidate references or pointers to the elements of the array.

### 26.7.2.8 Member functions [valarray.members]

```
void swap(valarray& v) noexcept;
```

Effects: *this obtains the value of v. v obtains the value of *this.

Complexity: Constant.

```
size_t size() const;
```

Returns: The number of elements in the array.

Complexity: Constant time.

Returns: A valarray whose length is equal to the length of the argument arrays. Each element of the returned array is initialized with the result of applying the indicated operator to the corresponding elements of the argument arrays.

```
template<class T> valarray<T> operator* (const valarray<T>&,
                                  const typename valarray<T>::value_type&);
template<class T> valarray<T> operator* (const typename valarray<T>::value_type&,
                                  const valarray<T>&);
template<class T> valarray<T> operator/ (const valarray<T>&,
                                  const typename valarray<T>::value_type&);
template<class T> valarray<T> operator/ (const typename valarray<T>::value_type&,
                                  const valarray<T>&);
template<class T> valarray<T> operator% (const valarray<T>&,
                                  const typename valarray<T>::value_type&);
template<class T> valarray<T> operator% (const typename valarray<T>::value_type&,
                                  const valarray<T>&);
template<class T> valarray<T> operator+ (const valarray<T>&,
                                  const typename valarray<T>::value_type&);
template<class T> valarray<T> operator+ (const typename valarray<T>::value_type&,
                                  const valarray<T>&);
template<class T> valarray<T> operator- (const valarray<T>&,
                                  const typename valarray<T>::value_type&);
template<class T> valarray<T> operator- (const typename valarray<T>::value_type&,
                                  const valarray<T>&);
template<class T> valarray<T> operator^ (const valarray<T>&,
                                  const typename valarray<T>::value_type&);
template<class T> valarray<T> operator^ (const typename valarray<T>::value_type&,
                                  const valarray<T>&);
template<class T> valarray<T> operator& (const valarray<T>&,
                                  const typename valarray<T>::value_type&);
template<class T> valarray<T> operator& (const typename valarray<T>::value_type&,
                                  const valarray<T>&);
template<class T> valarray<T> operator| (const valarray<T>&,
                                  const typename valarray<T>::value_type&);
template<class T> valarray<T> operator| (const typename valarray<T>::value_type&,
                                  const valarray<T>&);
template<class T> valarray<T> operator<< (const valarray<T>&,
                                  const typename valarray<T>::value_type&);
template<class T> valarray<T> operator<< (const typename valarray<T>::value_type&,
                                  const valarray<T>&);
template<class T> valarray<T> operator>> (const valarray<T>&,
                                  const typename valarray<T>::value_type&);
template<class T> valarray<T> operator>> (const typename valarray<T>::value_type&,
                                  const valarray<T>&);
```

Mandates: The indicated operator can be applied to operands of type T and returns a value of type T or which can be unambiguously implicitly converted to T.

Returns: A valarray whose length is equal to the length of the array argument. Each element of the returned array is initialized with the result of applying the indicated operator to the corresponding element of the array argument and the non-array argument.

### 26.7.3.2  Logical operators

[valarray.comparison]

```
template<class T> valarray<bool> operator==(const valarray<T>&, const valarray<T>&);
template<class T> valarray<bool> operator!=(const valarray<T>&, const valarray<T>&);
template<class T> valarray<bool> operator< (const valarray<T>&, const valarray<T>&);
template<class T> valarray<bool> operator> (const valarray<T>&, const valarray<T>&);
template<class T> valarray<bool> operator<=(const valarray<T>&, const valarray<T>&);
template<class T> valarray<bool> operator>=(const valarray<T>&, const valarray<T>&);
template<class T> valarray<bool> operator&&(const valarray<T>&, const valarray<T>&);
template<class T> valarray<bool> operator||(const valarray<T>&, const valarray<T>&);
```

Mandates: The indicated operator can be applied to operands of type T and returns a value of type bool or which can be unambiguously implicitly converted to bool.

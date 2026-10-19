
```cpp
explicit random_device(const string& token);
```

*Remarks:* The semantics of the token parameter and the token value used by the default constructor are implementation-defined.[^250]

*Throws:* A value of an implementation-defined type derived from exception if the random_device cannot be initialized.

```cpp
double entropy() const noexcept;
```

*Returns:* If the implementation employs a random number engine, returns 0.0. Otherwise, returns an entropy estimate[^251] for the random numbers returned by operator(), in the range min() to log2(max() + 1).

```cpp
result_type operator()();
```

*Returns:* A nondeterministic random value, uniformly distributed between min() and max() (inclusive). It is implementation-defined how these values are generated.

*Throws:* A value of an implementation-defined type derived from exception if a random number cannot be obtained.

## 26.6.8 Utilities [rand.util]

### 26.6.8.1 Class seed_seq [rand.util.seedseq]

```cpp
class seed_seq {
public:
  // types
  using result_type = uint_least32_t;

  // constructors
  seed_seq();
  template<class T>
    seed_seq(initializer_list<T> il);
  template<class InputIterator>
    seed_seq(InputIterator begin, InputIterator end);

  // generating functions
  template<class RandomAccessIterator>
    void generate(RandomAccessIterator begin, RandomAccessIterator end);

  // property functions
  size_t size() const noexcept;
  template<class OutputIterator>
    void param(OutputIterator dest) const;

  // no copy functions
  seed_seq(const seed_seq&) = delete;
  void operator=(const seed_seq&) = delete;

private:
  vector<result_type> v;      // exposition only
};
```

```cpp
seed_seq();
```

*Postconditions:* v.empty() is true.

*Throws:* Nothing.

```cpp
template<class T>
  seed_seq(initializer_list<T> il);
```

*Mandates:* T is an integer type.

*Effects:* Same as seed_seq(il.begin(), il.end()).

```cpp
template<class InputIterator>
    seed_seq(InputIterator begin, InputIterator end);
```

*Mandates:* iterator_traits<InputIterator>::value_type is an integer type.

*Preconditions:* InputIterator meets the Cpp17InputIterator requirements (23.3.5.3).

*Effects:* Initializes v by the following algorithm:

```cpp
for (InputIterator s = begin; s != end; ++s)
    v.push_back((*s) mod 2^32);
```

```cpp
template<class RandomAccessIterator>
void generate(RandomAccessIterator begin, RandomAccessIterator end);
```

*Mandates:* iterator_traits<RandomAccessIterator>::value_type is an unsigned integer type capable of accommodating 32-bit quantities.

*Preconditions:* RandomAccessIterator meets the Cpp17RandomAccessIterator requirements (23.3.5.7) and the requirements of a mutable iterator.

*Effects:* Does nothing if begin == end. Otherwise, with s = v.size() and n = end − begin, fills the supplied range [begin, end) according to the following algorithm in which each operation is to be carried out modulo 2^32, each indexing operator applied to begin is to be taken modulo n, and T(x) is defined as x xor (x >> 27):

- By way of initialization, set each element of the range to the value 0x8b8b8b8b. Additionally, for use in subsequent steps, let p = (n − t)/2 and let q = p + t, where

  t = (n ≥ 623) ? 11 : (n ≥ 68) ? 7 : (n ≥ 39) ? 5 : (n ≥ 7) ? 3 : (n − 1)/2;

- With m as the larger of s + 1 and n, transform the elements of the range: iteratively for k = 0,…,m − 1, calculate values

  r1 = 1664525 · T(begin[k] xor begin[k + p] xor begin[k − 1])

  r2 = r1 + { s, k = 0; k mod n + v[k − 1], 0 < k ≤ s; k mod n, s < k }

  and, in order, increment begin[k + p] by r1, increment begin[k + q] by r2, and set begin[k] to r2.

- Transform the elements of the range again, beginning where the previous step ended: iteratively for k = m,…,m + n − 1, calculate values

  r3 = 1566083941 · T(begin[k] + begin[k + p] + begin[k − 1])

  r4 = r3 − (k mod n)

  and, in order, update begin[k + p] by xoring it with r3, update begin[k + q] by xoring it with r4, and set begin[k] to r4.

*Throws:* What and when RandomAccessIterator operations of begin and end throw.

```cpp
size_t size() const noexcept;
```

*Returns:* The number of 32-bit units that would be returned by a call to param().

*Complexity:* Constant time.

```cpp
template<class OutputIterator>
void param(OutputIterator dest) const;
```

*Mandates:* Values of type result_type are writable (23.3.1) to dest.

*Preconditions:* OutputIterator meets the Cpp17OutputIterator requirements (23.3.5.4).

*Effects:* Copies the sequence of prepared 32-bit units to the given destination, as if by executing the following statement:

```cpp
copy(v.begin(), v.end(), dest);
```

*Throws:* What and when OutputIterator operations of dest throw.

### 26.6.8.2 Function template generate_canonical [rand.util.canonical]

```cpp
template<class RealType, size_t bits, class URBG>
RealType generate_canonical(URBG& g);
```

*Complexity:* Exactly k = max(1, ⌈b / log2 R⌉) invocations of g, where b[^252] is the lesser of numeric_limits<RealType>::digits and bits, and R is the value of g.max() − g.min() + 1.

*Effects:* Invokes g() k times to obtain values g₀, …, gₖ₋₁, respectively. Calculates a quantity

```
S = Σᵢ₌₀ᵏ⁻¹ (gᵢ − g.min()) · Rⁱ
```

using arithmetic of type RealType.

*Returns:* S / Rᵏ.

[Note 1: 0 ≤ S / Rᵏ < 1. — end note]

*Throws:* What and when g throws.

[Note 2: If the values gᵢ produced by g are uniformly distributed, the instantiation's results are distributed as uniformly as possible. Obtaining a value in this way can be a useful step in the process of transforming a value generated by a uniform random bit generator into a value that can be delivered by a random number distribution. — end note]

## 26.6.9 Random number distribution class templates [rand.dist]

### 26.6.9.1 In general [rand.dist.general]

Each type instantiated from a class template specified in this subclause 26.6.9 meets the requirements of a random number distribution (26.6.3.6) type.

Descriptions are provided in this subclause 26.6.9 only for distribution operations that are not described in 26.6.3.6 or for operations where there is additional semantic information. In particular, declarations for copy constructors, for copy assignment operators, for streaming operators, and for equality and inequality operators are not shown in the synopses.

The algorithms for producing each of the specified distributions are implementation-defined.

The value of each probability density function p(z) and of each discrete probability function P(zᵢ) specified in this subclause is 0 everywhere outside its stated domain.

### 26.6.9.2 Uniform distributions [rand.dist.uni]

#### 26.6.9.2.1 Class template uniform_int_distribution [rand.dist.uni.int]

A uniform_int_distribution random number distribution produces random integers i, a ≤ i ≤ b, distributed according to the constant discrete probability function

P(i | a, b) = 1 / (b − a + 1).

```cpp
template<class IntType = int>
class uniform_int_distribution {
public:
    // types
    using result_type = IntType;
    using param_type = unspecified;

    // constructors and reset functions
    uniform_int_distribution() : uniform_int_distribution(0) {}
    explicit uniform_int_distribution(IntType a, IntType b = numeric_limits<IntType>::max());
    explicit uniform_int_distribution(const param_type& parm);
    void reset();

    // generating functions
    template<class URBG>
    result_type operator()(URBG& g);
    template<class URBG>
    result_type operator()(URBG& g, const param_type& parm);

    // property functions
    result_type a() const;
    result_type b() const;
    param_type param() const;
    void param(const param_type& parm);
    result_type min() const;
    result_type max() const;
};
```

```cpp
explicit uniform_int_distribution(IntType a, IntType b = numeric_limits<IntType>::max());
```

*Preconditions:* a ≤ b.

*Remarks:* a and b correspond to the respective parameters of the distribution.

```cpp
result_type a() const;
```

*Returns:* The value of the a parameter with which the object was constructed.

```cpp
result_type b() const;
```

*Returns:* The value of the b parameter with which the object was constructed.

#### 26.6.9.2.2 Class template uniform_real_distribution [rand.dist.uni.real]

A uniform_real_distribution random number distribution produces random numbers x, a ≤ x < b, distributed according to the constant probability density function

p(x | a, b) = 1/(b − a).

> [Note 1: This implies that p(x | a, b) is undefined when a == b. — end note]

```cpp
template<class RealType = double>
class uniform_real_distribution {
public:
    // types
    using result_type = RealType;
    using param_type = unspecified;

    // constructors and reset functions
    uniform_real_distribution() : uniform_real_distribution(0.0) {}
    explicit uniform_real_distribution(RealType a, RealType b = 1.0);
    explicit uniform_real_distribution(const param_type& parm);
    void reset();

    // generating functions
    template<class URBG>
    result_type operator()(URBG& g);
    template<class URBG>
    result_type operator()(URBG& g, const param_type& parm);

    // property functions
    result_type a() const;
    result_type b() const;
    param_type param() const;
    void param(const param_type& parm);
    result_type min() const;
    result_type max() const;
};
```

```cpp
explicit uniform_real_distribution(RealType a, RealType b = 1.0);
```

*Preconditions:* a ≤ b and b − a ≤ numeric_limits<RealType>::max().

*Remarks:* a and b correspond to the respective parameters of the distribution.

```cpp
result_type a() const;
```

*Returns:* The value of the a parameter with which the object was constructed.

[^250]: The parameter is intended to allow an implementation to differentiate between different sources of randomness.

[^251]: If a device has n states whose respective probabilities are P₀, …, Pₙ₋₁, the device entropy S is defined as S = −Σᵢ₌₀ⁿ⁻¹ Pᵢ · log Pᵢ.

[^252]: b is introduced to avoid any attempt to produce more bits of randomness than can be held in RealType.


// constructors and seeding functions
subtract_with_carry_engine() : subtract_with_carry_engine(default_seed) {}
explicit subtract_with_carry_engine(result_type value);
template<class Sseq> explicit subtract_with_carry_engine(Sseq& q);
void seed(result_type value = default_seed);
template<class Sseq> void seed(Sseq& q);

// generating functions
result_type operator()();
void discard(unsigned long long z);

The following relations shall hold: 0u < s, s < r, 0 < w, and w <= numeric_limits<UIntType>::digits.

The textual representation consists of the values of X_{i-r}, ..., X_{i-1}, in that order, followed by c.

```
explicit subtract_with_carry_engine(result_type value);
```

Effects: Sets the values of X_{-r},...,X_{-1}, in that order, as specified below. If X_{-1} is then 0, sets c to 1; otherwise sets c to 0.

To set the values X_k, first construct e, a linear_congruential_engine object, as if by the following definition:

```
linear_congruential_engine<result_type,
40014u,0u,2147483563u> e(value == 0u ? default_seed : value);
```

Then, to set each X_k, obtain new values z_0,...,z_{n-1} from n = ⌈w/32⌉ successive invocations of e taken modulo 2^32. Set X_k to (∑_{j=0}^{n-1} z_j · 2^{32j}) mod m.

Complexity: Exactly n · r invocations of e.

```
template<class Sseq> explicit subtract_with_carry_engine(Sseq& q);
```

Effects: With k = ⌈w/32⌉ and a an array (or equivalent) of length r·k, invokes q.generate(a + 0, a + r·k) and then, iteratively for i = −r,...,−1, sets X_i to (∑_{j=0}^{k-1} a_{k(i+r)+j}·2^{32j}) mod m. If X_{-1} is then 0, sets c to 1; otherwise sets c to 0.

## 26.6.5 Random number engine adaptor class templates [rand.adapt]

### 26.6.5.1 In general [rand.adapt.general]

Each type instantiated from a class template specified in this subclause 26.6.5 meets the requirements of a random number engine adaptor (26.6.3.5) type.

Except where specified otherwise, the complexity of each function specified in this subclause 26.6.5 is constant.

Except where specified otherwise, no function described in this subclause 26.6.5 throws an exception.

Every function described in this subclause 26.6.5 that has a function parameter q of type Sseq& for a template type parameter named Sseq that is different from type seed_seq throws what and when the invocation of q.generate throws.

Descriptions are provided in this subclause 26.6.5 only for adaptor operations that are not described in subclause 26.6.3.5 or for operations where there is additional semantic information. In particular, declarations for copy constructors, for copy assignment operators, for streaming operators, and for equality and inequality operators are not shown in the synopses.

Each template specified in this subclause 26.6.5 requires one or more relationships, involving the value(s) of its non-type template parameter(s), to hold. A program instantiating any of these templates is ill-formed if any such required relationship fails to hold.

### 26.6.5.2 Class template discard_block_engine [rand.adapt.disc]

A discard_block_engine random number engine adaptor produces random numbers selected from those produced by some base engine e. The state x_i of a discard_block_engine engine adaptor object x consists of the state e_i of its base engine e and an additional integer n. The size of the state is the size of e's state plus 1.

4 The generation algorithm uses the values produced while advancing the state as described above to yield a quantity S obtained as if by the following algorithm:

```
S = 0;
for (k = 0; k != n0; k += 1) {
  do u = e() - e.min(); while (u >= y0);
  S = 2^w0 . S + u mod 2^w0;
}
for (k = n0; k != n; k += 1) {
  do u = e() - e.min(); while (u >= y1);
  S = 2^w0+1 . S + u mod 2^w0+1;
}
```

```
template<class Engine, size_t w, class UIntType>
class independent_bits_engine {
public:
  // types
  using result_type = UIntType;

  // engine characteristics
  static constexpr result_type min() { return 0; }
  static constexpr result_type max() { return 2^w - 1; }

  // constructors and seeding functions
  independent_bits_engine();
  explicit independent_bits_engine(const Engine& e);
  explicit independent_bits_engine(Engine&& e);
  explicit independent_bits_engine(result_type s);
  template<class Sseq> explicit independent_bits_engine(Sseq& q);
  void seed();
  void seed(result_type s);
  template<class Sseq> void seed(Sseq& q);

  // generating functions
  result_type operator()();
  void discard(unsigned long long z);

  // property functions
  const Engine& base() const noexcept { return e; };

private:
  Engine e;    // exposition only
};
```

5 The following relations shall hold: 0 < w and w <= numeric_limits<result_type>::digits.

6 The textual representation consists of the textual representation of e.

### 26.6.5.4 Class template shuffle_order_engine [rand.adapt.shuf]

1 A shuffle_order_engine random number engine adaptor produces the same random numbers that are produced by some base engine e, but delivers them in a different sequence. The state x of a shuffle_order_engine engine adaptor object x consists of the state e of its base engine e, an additional value Y of the type delivered by e, and an additional sequence V of k values also of the type delivered by e. The size of the state is the size of e’s state plus k + 1.

2 The transition algorithm permutes the values produced by e. The state transition is performed as follows:
- (2.1) — Calculate an integer j = ⌊ k·(Y−e_min)/(e_max−e_min+1) ⌋.
- (2.2) — Set Y to V_j and then set V_j to e().

3 The generation algorithm yields the last value of Y produced while advancing e’s state as described above.

```
template<class Engine, size_t k>
class shuffle_order_engine {
public:
  // types
  using result_type = typename Engine::result_type;

  // engine characteristics
  static constexpr size_t table_size = k;
  static constexpr result_type min() { return Engine::min(); }
  static constexpr result_type max() { return Engine::max(); }

  // constructors and seeding functions
  shuffle_order_engine();
  explicit shuffle_order_engine(const Engine& e);
  explicit shuffle_order_engine(Engine&& e);
  explicit shuffle_order_engine(result_type s);
  template<class Sseq> explicit shuffle_order_engine(Sseq& q);
  void seed();
  void seed(result_type s);
  template<class Sseq> void seed(Sseq& q);

  // generating functions
  result_type operator()();
  void discard(unsigned long long z);

  // property functions
  const Engine& base() const noexcept { return e; };

private:
    Engine e;        // exposition only
    result_type V[k];    // exposition only
    result_type Y;      // exposition only
};
```

4 The following relation shall hold: 0 < k.

5 The textual representation consists of the textual representation of e, followed by the k values of V, followed by the value of Y.

6 In addition to its behavior pursuant to subclause 26.6.3.5, each constructor that is not a copy constructor initializes V[0], …, V[k-1] and Y, in that order, with values returned by successive invocations of e().

## 26.6.6 Engines and engine adaptors with predefined parameters [rand.predef]

```
using minstd_rand0 =
    linear_congruential_engine<uint_fast32_t, 16'807, 0, 2'147'483'647>;
```

1 Required behavior: The 10000th consecutive invocation of a default-constructed object of type minstd_rand0 produces the value 1043618065.

```
using minstd_rand =
    linear_congruential_engine<uint_fast32_t, 48'271, 0, 2'147'483'647>;
```

2 Required behavior: The 10000th consecutive invocation of a default-constructed object of type minstd_rand produces the value 399268537.

```
using mt19937 =
    mersenne_twister_engine<uint_fast32_t, 32, 624, 397, 31,
        0x9908'b0df, 11, 0xffff'ffff, 7, 0x9d2c'5680, 15, 0xefc6'0000, 18, 1'812'433'253>;
```

3 Required behavior: The 10000th consecutive invocation of a default-constructed object of type mt19937 produces the value 4123659995.

```
using mt19937_64 =
    mersenne_twister_engine<uint_fast64_t, 64, 312, 156, 31,
        0xb502'6f5a'a966'19e9, 29, 0x5555'5555'5555'5555, 17,
        0x7d1d'7fff'eda6'0000, 37, 0xffff'ffee'0000'0000, 43, 6'364'136'223'846'793'005>;
```

4 Required behavior: The 10000th consecutive invocation of a default-constructed object of type mt19937_64 produces the value 9981545732273789042.

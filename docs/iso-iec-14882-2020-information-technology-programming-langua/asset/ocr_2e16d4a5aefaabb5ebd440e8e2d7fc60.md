```
// constructors and seeding functions
subtract_with_carry_engine() : subtract_with_carry_engine(default_seed) {}
explicit subtract_with_carry_engine(result_type value);
template<class Sseq> explicit subtract_with_carry_engine(Sseq& q);
void seed(result_type value = default_seed);
template<class Sseq> void seed(Sseq& q);
```

```
// generating functions
result_type operator()();
void discard(unsigned long long z);
```

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

# 26.6.5 Random number engine adaptor class templates [rand.adapt]

# 26.6.5.1 In general [rand.adapt.general]

Each type instantiated from a class template specified in this subclause 26.6.5 meets the requirements of a random number engine adaptor (26.6.3.5) type.

Except where specified otherwise, the complexity of each function specified in this subclause 26.6.5 is constant.

Except where specified otherwise, no function described in this subclause 26.6.5 throws an exception.

Every function described in this subclause 26.6.5 that has a function parameter q of type Sseq& for a template type parameter named Sseq that is different from type seed_seq throws what and when the invocation of q.generate throws.

Descriptions are provided in this subclause 26.6.5 only for adaptor operations that are not described in subclause 26.6.3.5 or for operations where there is additional semantic information. In particular, declarations for copy constructors, for copy assignment operators, for streaming operators, and for equality and inequality operators are not shown in the synopses.

Each template specified in this subclause 26.6.5 requires one or more relationships, involving the value(s) of its non-type template parameter(s), to hold. A program instantiating any of these templates is ill-formed if any such required relationship fails to hold.

# 26.6.5.2 Class template discard_block_engine [rand.adapt.disc]

A discard_block_engine random number engine adaptor produces random numbers selected from those produced by some base engine e. The state x_i of a discard_block_engine engine adaptor object x consists of the state e_i of its base engine e and an additional integer n. The size of the state is the size of e's state plus 1.
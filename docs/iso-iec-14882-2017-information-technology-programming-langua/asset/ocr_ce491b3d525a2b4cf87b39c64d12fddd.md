# ISO/IEC 14882:2017(E)

```
template<class UIntType, size_t w, size_t s, size_t r>
class subtract_with_carry_engine {
public:
    //types
    using result_type = UIntType;

    //engine characteristics
    static constexpr size_t word_size = w;
    static constexpr size_t short_lag = s;
    static constexpr size_t long_lag = r;
    static constexpr result_type min() { return 0; }
    static constexpr result_type max() { return m - 1; }
    static constexpr result_type default_seed = 19780503u;
```

```
//constructors and seeding functions
explicit subtract_with_carry_engine(result_type value = default_seed);
template<class Seq> explicit subtract_with_carry_engine(Seq& q);
void seed(result_type value = default_seed);
template<class Seq> void seed(Seq& q);
```

```
// generating functions
result_type operator()
void discard(unsigned long z);
```

5 The following relations shall hold: Ou < s < r, w and w <= numeric_limits<UIntType>::digits.

6 The textual representations of the values of X_{-j}, ..., X_{n-1}, in that order, be constructed as follows:

```
explicit subtract_with_carry_engine(result_type value = default_seed);
```

7 Effects: Constructs a subtract_with_carry_engine object. The values of X_{-j}, ..., X_{n-1}, in that order, are specified as follows: If X_j is not one, set it to 0; otherwise set it to 1.

To set each X_k, obtain new values from a linear_congruential_engine object, as is defined by this section

```
linear_congruential_engine_type;
4001u,2147483643u*value = Ou ? default_seed : value;
```

Then, to set each X_k, obtain new values z_0, ..., z_{n-1} from n = [w/32] invocations of e taken modulo 2^w.

```
Set X_k by (sum_{j=0}^{k-1} z_j * 2^j) mod m.
```

8 Complexity: Exactly n iterations of e.

```
template<class Seq> explicit subtract_with_carry_engine(Seq& q);
```

9 Effects: Constructs a subtract_with_carry_engine object. With k = [w/32] and an array (or) of length r-k, it invokes q(generate(a+ r-k)) and then, iteratively for i = -r, ..., -1, sets X_i to (sum_{j=k}^{i} z_j * 2^j) mod m. If X_i is 1, set it to 0; otherwise set it to 1.

# 29.6.4 Random number engine adaptor classes

[rand.adapt]

# 29.6.4.1 In general

1 Each type instantiated from a class template specified in this section 29.6.4 satisfies the requirements of a random number engine adaptor (29.6.1.5) type.

2 Except where specified otherwise, the complexity of each function specified in this section 29.6.4 is constant.

3 Except where specified otherwise, no function described in this section 29.6.4 throws an exception.

§ 29.6.4.1  ©ISO/IEC 2017 - All rights reserved  1074
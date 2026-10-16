```
37, 0xfff7eee000000000,
43, 6364136223846793005>;
using ranlux24_base = subtract_with_carry_engine<uint_fast32_t, 24, 10, 24>; using ranlux48_base = subtract_with_carry_engine<uint_fast64_t, 48, 5, 12>; using ranlux24 = discard_block_engine<ranlux24_base , 223, 23>; using ranlux48 = discard_block_engine<ranlux48_base , 389, 11>; using knuth_b = shuffle_order_engine<minstd_rand0,256>;
```

# 40.7.2 Random Device

If an implementation is able to offer a truly random number generator, that source of random numbers is presented as a uniform random number generator called random_device:

random_device (§iso.26.5.6)

random_device rd {s}; The string s identifies a source of random numbers; implementation-defined; explicit

d=rd.entropy() d is a double; d==0.0 for a pseudo-random number generator Think of s as the name of a random number source, such as a Geiger counter, a Web service, or a file/device containing the record of a truly random source. The entropy() is defined as

i=n-1
S(P0,..., Pn-1)=− Σ Pi log Pi
i=0

for a device with n states whose respective probabilities are P0,..., Pn−1. The entropy is an estimate of the randomness, the degree of unpredictability, of the generated numbers. In contrast to thermodynamics, high entropy is good for random numbers because that means that it is hard to guess subsequent numbers. The formula reflects the result of repeatedly throwing a perfect n-sided dice.

The random_device is intended to be useful for cryptographic applications, but it would be against all rules of that kind of application to trust an implementation of random_device without first studying it closely.

# 40.7.3 Distributions

A random number distribution is a function object that, when called with a random number generator argument, produces a sequence of values of its result_type:

Random Number Distribution D (§iso.26.5.1.6) (continues)

```
D::result_type
D::param_type
D d {};
D d {p};
```

The type of an element of D
The type of the set of arguments needed to construct a D Default constructor
Construct from param_type p

Random Number Distribution D (continued) (§iso.26.5.1.6) d.reset() Reset to default
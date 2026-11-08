```
{
    using wide_t = unsigned long long;
    independent_bits_engine<
        default_random_engine,
        sizeof(wide_t)*8, wide_t>
    e {};
    measure("indep<default>", e);
}
```

Listing 28.18  Speeds of the random number generators.

The results always vary on different systems, of course. Consider the following excerpt:

```
default:           12 ns/loop      126342116 ns
device:            41 ns/loop      417456044 ns
minstd_rand0:      12 ns/loop      122354003 ns
indep<ranlux>:   1086 ns/loop      10865420582 ns
```

As you can see, the device here (!) is not that slow, and if you use indep<ranlux>, you should have a reason for it.

# 28.3.4  Distributions

Random numbers can be generated with various characteristics or distributions—from a simple six-sided die to floating-point values.

With a six-sided die, each of the numbers 1 to 6 should appear roughly equally often. But other random experiments behave differently. If you throw 10 coins (together) and count how often heads appears, then the possible outcomes 0 to 10 are binomially distributed. If you repeat this experiment several times in a row, you will see 0 heads less often than 5 heads. For such experiments, you do not need to generate the numbers 0 or 1 for heads or tails 10 times from the computer, but you can directly generate a number between 0 and 10 with the appropriate probability using binomial_distribution.

You have already seen in Listing 28.17 what a uniform distribution looks like for a single die. Let's choose a binomial distribution in Listing 28.19 to simulate tossing 10 coins.

```
// https://godbolt.org/z/r5vW5PYa
#include <random>
#include <vector>
#include <iostream>
using namespace std;
int main() {
    static const size_t size = 10;
```
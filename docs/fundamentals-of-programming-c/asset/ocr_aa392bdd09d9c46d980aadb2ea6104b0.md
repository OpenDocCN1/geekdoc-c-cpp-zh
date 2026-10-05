# 16.6 Convenient High-quality Pseudorandom Numbers

In Section 13 we used classes from the standard C++ library to generate high-quality pseudorandom numbers. Listing 13.10 (highqualityrandom.cpp) used three kinds of objects—random_device, mt19937, and uniform_int_distribution to produce good pseudorandom sequences.

The C++ class construct allows us to combine multiple sources of randomness into one convenient package. Listing 16.12 (uniformrandom.h) contains the UniformRandomGenerator class.

```
Listing 16.12: uniformrandom.h
#ifndef UNIFORM_RANDOM_DEFINED
#define UNIFORM_RANDOM_DEFINED_

#include <random>

using std::uniform_int_distribution;
using std::random_device;
using std::mt19937;

class UniformRandomGenerator {
    // A uniform distribution object
    uniform_int_distribution<int> dist;
    // A Mersenne Twister random number generator with the seed
    // obtained from a random_device object
    mt19937 mt;
public:
    // The smallest pseudorandom number this generator can produce
    const int MIN;

    // The largest pseudorandom number this generator can produce
    const int MAX;

    // Create a pseudorandom number generator that produces values in
    // the range low...high
    UniformRandomGenerator(int low, int high) : dist(low, high),
        mt(random_device()()), MIN(low), MAX(high) {}

    // Return a pseudorandom number in the range MIN...MAX
    int operator()() {
        return dist(mt);
    }
};
#endif
```

The UniformRandomGenerator class provides a simplified interface to programmers who need access to high-quality pseudorandom numbers. Every UniformRandomGenerator object contains its uniform_int_distribution object and mt19937. The constructor accepts the minimum and maximum values in the range of pseudorandom numbers desired. The constructor uses this range to construct the appropriate uniform_int_distribution object for this range. The constructor also initializes the mt19937 object field. The UniformRandomGenerator constructor passes to the constructor of the mt19937 class a temporary random_device object. Since
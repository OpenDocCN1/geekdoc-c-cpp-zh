```
3.52615
}
```

# Listing 28.20 A "double" random number.

# Different Roll Every Time

If you already provide the range to the constructor of uniform_int_distribution<int> where the random numbers should be generated, do you always need to create a new distribution if the boundaries change each time?

No, fortunately not. Each distribution has a param_type with the same constructor arguments as the distribution. You can pass such a param_type instance to the generating call of operator() and change the conditions for generation from call to call.

```
// https://godbolt.org/z/xz64qK3e5
#include <random>
#include <iostream>
int main() {
    std::default_random_engine e();
    using Dstr = std::uniform_int_distribution<int>; // generate
    Dstr card(e);
distribution
    for(int n=32; n>=1; --n) {
        std::cout << "" << (e, Dstr::param_type{1,n}) << "\n"; // parameters
    }
    only here
    std::cout << '\n';
    // output for example:
    // 1 25 13 14 15 6 2 17 22 9 11 17 1 1 10 11 6 1 6 8 9 7 4 1
}
```

# Listing 28.21 Change generation parameters for each random number individually.
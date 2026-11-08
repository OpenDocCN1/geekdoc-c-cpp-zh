# ## Mutable Lambdas

In Chapter 13, Section 13.10.10, I promised to explain mutable for lambdas, and I will do so here.

With `mutable`, you allow changes to capture variables that were copied into the lambda. To do this, place the word `mutable` after the lambda.

```
```cpp
//https://godbolt.org/z/zMWo69974
#include <iostream>
int main() {
    int count = 0;
    auto plus1 = [count](int x) mutable {  // count as a copy
        std::cout << ++count; return x+1;
    };
    for(int i=0; i<5; ++i) {
        plus1(i);
    }
    std::cout << "\n";
    // Output: 12345
}
```
```

**Listing 23.22 "mutable" makes value captures in lambdas mutable.**

Even `mutable` should be used with caution. Maybe you want a reference capture on `count`. If so, you can change that without `mutable` as well.

```
```cpp
// https://godbolt.org/z/8GxPMEcSo
#include <iostream>
int main() {
    int count = 0;
    auto plus1 = [&count](int x) { // count as reference
        ++count; return x+1;
    };
    for(int i=0; i<5; ++i) { plus1(i); }
    std::cout << "plus1 was called " << count << " times\n";
    // Output: plus1 was called 5 times
}
```
```

**Listing 23.23 If possible, better without mutable.**

However, if the lambda is passed as a return value or as a parameter, then a reference can be dangerous because the referenced variable might no longer exist. `mutable` can help here in exceptional cases.
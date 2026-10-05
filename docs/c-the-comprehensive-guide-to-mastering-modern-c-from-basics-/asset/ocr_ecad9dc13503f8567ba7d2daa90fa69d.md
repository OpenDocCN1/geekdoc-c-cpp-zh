# 6.5 Algorithms

In addition to the capabilities of the containers, there are **algorithms**. Most of them can be found in the <algorithm> header. There is a long list of auxiliary functions that help you to solve specific problems using general methods.

All these algorithms consistently work on iterators, which is why they work on (almost) all containers. It is important to know that the power of the containers is not exhausted by their methods.

In the following example, a vector is filled with an algorithm, and then elements meeting a specific criterion are counted.

```
// https://godbolt.org/z/4G67rso8T
#include <vector>
#include <algorithm>             // count_if
#include <numeric>                // iota
#include <iostream>
bool even(int n) { return n==0; }  // test for even
int main() {
    std::vector<int> data(100);          // 100 x zero
    std::iota(data.begin(), data.end(), 0); // 0, 1, 2, ... 99
    // counts even numbers
    std::cout << std::count_if(data.begin(), data.end(), even);
}
```

**Listing 6.13** Counting with an algorithm.
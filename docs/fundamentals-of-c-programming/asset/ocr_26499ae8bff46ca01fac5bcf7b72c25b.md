```
i += 5;
else
    i++;
return result;
}
std::cout << nums << '\n';
// Finally, populate the vector with pseudorandom
// integers in the range 0, 1, ..., 100
std::generate(std::begin(nums), std::end(nums), gen);
std::cout << nums << '\n';
}
```

One run of Listing 20.40 (testgenerate.cpp) produces the following output:

```
{2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2}
{10, 15, 16, 17, 18, 19, 20, 25, 26, 27, 28, 29, 30, 35, 36, 37, 38, 39}
{24, 3, 57, 51, 94, 36, 83, 30, 99, 67, 10, 11, 82, 88, 85, 100, 12, 11}
```

The first two lines of the output will always be the same, but the last line will vary from one run to the next.

std::accumulate. The std::accumulate function applies a binary operation to a range of elements of a container. (A binary operation is an operator or function that expects two arguments.) The binary operation combines elements within the range, two by two, to produce a single value. One example of its use is adding up the elements in a numeric list. Listing 20.41 (testaccumulate.cpp) shows the std::accumulate function in action.

```
Listing 20.41: testaccumulate.cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <numeric>
#include <random>

// Uniform pseudorandom number generator from an earlier chapter
#include "uniformrandom.h"
#include "vectorsprint.h"

int main() {
    std::vector<int> nums(6);

    UniformRandomGenerator gen(1, 5);

    // Populate the vector with pseudorandom
    // integers in the range 0, 1, ..., 5
    std::generate(std::begin(nums), std::end(nums), gen);
    std::cout << nums << '\n';

    // Add up the elements
    std::cout << std::accumulate(std::begin(nums), std::end(nums), 0,
                                 [](int a, int b) { return a + b; })
              << '\n';
}
```
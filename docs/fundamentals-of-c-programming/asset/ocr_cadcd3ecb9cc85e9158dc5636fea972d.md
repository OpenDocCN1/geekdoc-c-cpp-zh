The Fibonacci numbers grow very quickly, so the functions in Listing 21.21 (fibonacci.h) return unsigned long long values. For convenience it introduces the type alias Integer for unsigned long long to simplify the code. Under Visual C++, for example, this type supports values in the range 0 ... 18,446,744,073,709,551,615, inclusive. Listing 21.22 (fibonacci.cpp) provides the implementations for the two functions.

```
Listing 21.22: fibonacci.cpp
#include <unordered_map>
#include "fibonacci.h"

// Returns the nth Fibonacci number
Integer fibonacci(unsigned n) {
    if (n < 0)
        return 0;
    else if (n == 1)
        return 1;
    else
        return fibonacci(n - 2) + fibonacci(n - 1);
}

// Returns the nth Fibonacci number. Caches a
// recursively computed result to be used when needed
// in the future. Provides a huge performance improvement
// over the recursive version.
Integer fibonacci2(unsigned n) {
    // ans is a map for caching the results of the fibonacci2 function.
    // Declared static so it persists between function calls.
    // Precomputes the results for 0 and 1.
    static std::unordered_map<unsigned, Integer> ans {{0, 0}, {1, 1}};
    if (n > 1 && ans[n] == 0)
        ans[n] = fibonacci2(n - 2) + fibonacci2(n - 1);
    return ans[n];
}
```

When compiled and linked with the code in Listing 21.22 (fibonacci.cpp), Listing 21.23 (testfib.cpp) verifies that the fibonacci2 function produces the same results as the fibonacci function when given the same arguments. It tests unsigned values up to 50. You will observe that as the arguments become larger, the program takes longer to print the results.

```
Listing 21.23: testfib.cpp
#include <iostream>
#include "fibonacci.h"

// Compares the behaviors of the fibonacci and fibonacci2 functions.
int main() {
    // Print the first 50 Fibonacci numbers
    for (unsigned i = 0; i < 50; ++i) {
        std::cout << "i = " << i << " fibonacci(i) << " "
                  << fibonacci2(i) << "\n";
    }
}
```

The following shows the first 20 lines of the output of Listing 21.23 (testfib.cpp):
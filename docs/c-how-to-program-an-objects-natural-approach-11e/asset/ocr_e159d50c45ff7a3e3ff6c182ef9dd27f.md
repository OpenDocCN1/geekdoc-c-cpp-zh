```
```cpp
// fig05_15.cpp
// Recursive function fibonacci.
#include <format>
#include <iostream>
using namespace std;

long fibonacci(long number); // function prototype

int main() {
   // calculate the fibonacci values of 0 through 10
   for (int counter{0}; counter <= 10; ++counter) {
      cout << format("fibonacci({}) = {}\\n",
         counter, fibonacci(counter));
   }

   // display higher fibonacci values
   cout << format("fibonacci(20) = {}\\n", fibonacci(20))
      << format("fibonacci(30) = {}\\n", fibonacci(30))
      << format("fibonacci(35) = {}\\n", fibonacci(35));
}

// recursive function fibonacci
long fibonacci(long number) {
   if ((0 == number) || (1 == number)) { // base cases
      return number;
   }
   else { // recursion step
      return fibonacci(number - 1) + fibonacci(number - 2);
   }
}
```
```

```
```text
fibonacci(0) = 0
fibonacci(1) = 1
fibonacci(2) = 1
fibonacci(3) = 2
fibonacci(4) = 3
fibonacci(5) = 5
fibonacci(6) = 8
fibonacci(7) = 13
fibonacci(8) = 21
fibonacci(9) = 34
fibonacci(10) = 55

fibonacci(20) = 6765
fibonacci(30) = 832040
fibonacci(35) = 9227465
```
```

**Fig. 5.15**  |  Recursive function fibonacci.

Function fibonacci (lines 23–30) recursively calculates the nth Fibonacci number. Each initial call to function fibonacci from main is not a recursive call. However, all subsequent calls to fibonacci performed from function fibonacci’s block are recursive because, at that point, the calls are initiated by the function itself. Each call to fibonacci immediately tests for the base cases—number equal to 0 or number equal to 1. If number
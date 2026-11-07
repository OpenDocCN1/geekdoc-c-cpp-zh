```
```c
// fig05_10.c
// Recursive fibonacci function.
#include <stdio.h>

unsigned long long int fibonacci(int n); // function prototype

int main(void) {
    // calculate and display fibonacci(number) for 0-10
    for (int number = 0; number <= 10; number++) {
        printf("Fibonacci(%d) = %llu\n", number, fibonacci(number));
    }

    printf("Fibonacci(20) = %llu\n", fibonacci(20));
    printf("Fibonacci(30) = %llu\n", fibonacci(30));
    printf("Fibonacci(40) = %llu\n", fibonacci(40));
}

// Recursive definition of function fibonacci
unsigned long long int fibonacci(int n) {
    if (0 == n || 1 == n) { // base case
        return n;
    }
    else { // recursive step
        return fibonacci(n - 1) + fibonacci(n - 2);
    }
}
```
```

```
```text
Fibonacci(0) = 0
Fibonacci(1) = 1
Fibonacci(2) = 1
Fibonacci(3) = 2
Fibonacci(4) = 3
Fibonacci(5) = 5
Fibonacci(6) = 8
Fibonacci(7) = 13
Fibonacci(8) = 21
Fibonacci(9) = 34
Fibonacci(10) = 55
Fibonacci(20) = 6765
Fibonacci(30) = 832040
Fibonacci(40) = 102334155
```
```

*Fig. 5.10* | Recursive fibonacci function.

The fibonacci calls from main are *not* recursive (lines 10 and 13–15), but all subsequent calls to fibonacci are recursive (line 24). Each time fibonacci is invoked, it immediately tests for the *base case*—n is equal to 0 or 1. If this is true, n is returned. Interestingly, if n is greater than 1, the recursion step generates *two* recursive calls, each a slightly simpler problem than the original call to fibonacci. The following diagram shows how function fibonacci would evaluate fibonacci(3):
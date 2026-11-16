```
* Computes n!
* Returns the factorial of n.
*/
int factorial(int n) {
    if (n == 0)
        return 1;
    else
        return n * factorial(n - 1);
}

int main() {
    // Try out the factorial function
    std::cout << "0! = " << factorial(0) << '\n';
    std::cout << "1! = " << factorial(1) << '\n';
    std::cout << "6! = " << factorial(6) << '\n';
    std::cout << "10! = " << factorial(10) << '\n';
}
```

Observe that the factorial function in Listing 10.6 (factorialtest.cpp) uses no loop to compute its result. The factorial function simply calls itself. The call factorial(6) is computed as follows:

```
factorial(6) = 6 * factorial(5)
    = 6 * 5 * factorial(4)
    = 6 * 5 * 4 * factorial(3)
    = 6 * 5 * 4 * 3 * factorial(2)
    = 6 * 5 * 4 * 3 * 2 * factorial(1)
    = 6 * 5 * 4 * 3 * 2 * 1 * factorial(0)
    = 6 * 5 * 4 * 3 * 2 * 1 * 1
    = 6 * 5 * 4 * 3 * 2 * 1
    = 6 * 5 * 4 * 3 * 2
    = 6 * 5 * 4 * 6
    = 6 * 5 * 24
    = 6 * 120
    = 720
```

Note that the factorial function can be slightly optimized by changing the if's condition from (n == 0) to (n < 2). This change results in a function execution trace that eliminates two function calls at the end:

```
factorial(6) = 6 * factorial(5)
    = 6 * 5 * factorial(4)
    = 6 * 5 * 4 * factorial(3)
    = 6 * 5 * 4 * 3 * factorial(2)
    = 6 * 5 * 4 * 3 * 2 * 1
    = 6 * 5 * 4 * 3 * 2
    = 6 * 5 * 4 * 6
    = 6 * 5 * 24
    = 6 * 120
    = 720
```

Figure 10.1 shows the call sequence for factorial(6) invoked from within a main function.

A correct simple recursive function definition is based on four key concepts:
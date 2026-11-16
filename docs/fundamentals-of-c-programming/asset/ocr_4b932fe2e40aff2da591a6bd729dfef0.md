the local variables declared within any function it calls. In fact, the local variables for a function exist only when the function is active (that is, executing). When the function returns to its caller all of its local variables disappear from memory. During subsequent invocations, the function's local variables reappear when the function becomes active and disappear again when it finishes.

# ## 9.4 Function Examples

This section contains a number of examples of how we can use functions to organize a program's code.

# ### 9.4.1 Better Organized Prime Generator

Listing 9.10 (primefunc.cpp) is a simple enhancement of Listing 8.5 (moreefficientprimes.cpp). It uses the square root optimization and adds a separate is_prime function.

```
Listing 9.10: primefunc.cpp

#include <iostream>
#include <cmath>

/*
 * is_prime(n)
 *  Determines the primality of a given value
 *  n an integer to test for primality
 *  Returns true if n is prime; otherwise, returns false
 */
bool is_prime(int n) {
    bool result = true;   // Provisionally, n is prime
    double root_n = sqrt(r);
    // Try all possible factors from 2 to the square
    // root of
    for (int trial_factor = 2;
         result && trial_factor <= root; trial_factor++)
        result = (n % trial_factor != 0);
    return result;
}

/*
 * main
 *  Tests for primality each integer from 2
 *  up to a value provided by the user.
 *  If an integer is prime, it prints it;
 *  otherwise, the number is not printed.
 */
int main() {
    int max_value;
    std::cout << "Display primes up to what value? ";
    std::cin >> max_value;
    for (int value = 2; value <= max_value; value++)
        if (is_prime(value)) // See if value is prime
            std::cout << value << " "; // Display the prime number
    std::cout << "\n"; // Move cursor down to next line
}
```
```
* is_prime(n)
* Determines the primality of a given value
*
* n An integer to test for primality
* Returns true if n is prime; otherwise, returns false
*/
bool is_prime(int n) {
    bool result = true; // Provisionally, n is prime
    double r = n, root = sqrt(r);
    // Try all possible factors from 2 to the square
    // root of n
    for (int trial_factor = 2; result && trial_factor <= root; trial_factor++)
        result = (n % trial_factor != 0);
    return result;
}
```

The code in Listing 10.11 (prime.cpp) is placed in prime.cpp, a different file from prime.h. It provides an implementation of the is_prime function. Notice the #include preprocessor directive in Listing 10.11 (prime.cpp) that references the file prime.h. While not required, this serves as a good check to see if the implementation code in this file is faithful to the prototype specified in prime.h. This prime.cpp file is compiled separately, and the compiler will report an error if the implementation of is_prime disagrees with the information in the header file.

Note that the file prime.cpp does not contain a main function; main will appear in another file. Also observe that we do not need to #include the iostream header, since the std::cout and std::cin objects are not used anywhere in this file. The cmath header is #included since is_prime uses the sqrt function.

The final piece of the program is the calling code. Suppose Listing 10.12 (primetester.cpp) is added to the project in a file named primetester.cpp.

# Listing 10.12: primetester.cpp

```
#include <iostream>
#include "prime.h"

/*
 * main
 * Tests for primality each integer from 2
 * up to a value provided by the user.
 * If an integer is prime, it prints it;
 * otherwise, the number is not printed.
 */
int main() {
    int max_value;
    std::cout << "Display primes up to what value? ";
    std::cin >> max_value;
    for (int value = 2; value <= max_value; value++)
        if (is_prime(value)) // See if value is prime
            std::cout << value << " "; // Display the prime number
    std::cout << '\n'; // Move cursor down to next line
}
```

Note that the file primetester.cpp uses a function named is_prime, but its definition is missing. The definition for is_prime is found, of course, in prime.cpp.
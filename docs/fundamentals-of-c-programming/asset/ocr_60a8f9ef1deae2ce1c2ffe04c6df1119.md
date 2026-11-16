```
#include <iostream>

int main() {
    int max_value;
    std::cout << "Display primes up to what value? ";
    std::cin >> max_value;
    for (int value = 2; value <= max_value; value++) {
        // See if value is prime
        bool is_prime = true; // Provisionally, value is prime
        // Try all possible factors from 2 to value - 1
        for (int trial_factor = 2;
             is_prime && trial_factor < value;
             trial_factor++) {
            is_prime = (value % trial_factor != 0);
        }
        if (is_prime)
            std::cout << value << " "; // Display the prime number
    }
    std::cout << '\n'; // Move cursor down to next line
}
```

As shown in Listing 7.7 (forprintprimes.cpp), the conditional expression in the `for` loop is not limited to a simple test of the loop control variable; it can be any legal Boolean expression. Programmers can use the logical `&&`, `||`, and `!` operators to create complex Boolean expressions, if necessary. The modification part of the `for` loop is not limited to simple arithmetic and can be quite elaborate. For example:

```
for (double d = 1000; d >= 1; std::cin >> d) {
    /* Body goes here */
}
```

Here d is reassigned from the input stream. If necessary, multiple variables can be initialized in the initialization part:

```
for (int i = 0, j = 100; i < j; i++) {
    /* Body goes here */
}
```

While the `for` statement supports such complex headers, simpler is usually better. Ordinarily the `for` loop should manage just one control variable, and the initialization, condition, and modification parts should be straightforward. If a particular programming situation warrants an overly complicated `for` construction, consider using another kind of loop.

Any or all of the parts of the `for` statement (initialization, condition, modification, and body) may be omitted:

+   * Initialization. If the initialization is missing, as in

```
for (; i < 10; i++)
    /* Body goes here */
```

then no initialization is performed by the `for` loop, and it must be done elsewhere.
# Chapter 8

# Using Functions

Suppose you must write a C++ program that computes the square root of a number supplied by the user. Listing 8.1 (computesquareroot.cpp) provides a simple implementation.

```
Listing 8.1 computesquareroot.cpp

// File squareroot.cpp

#include <iostream>

int main() {
    double input;
    // Get value from the user
    std::cout << "Enter number: ";
    std::cin >> input;
    double diff;
    // Compute a provisional square root
    double root = 1.0;

    do { // Loop until the provisional root
        // is close enough to the actual root
        root = (root + input/root) / 2.0;
        std::cout << "root is " << root << "\n";
        // How bad is the approximation?
        diff = root * root - input;
    } while (diff > 0.0001 || diff < -0.0001);

    // Report approximate square root
    std::cout << "Square root of " << input << " = " << root << "\n";
}
```

The program is based on a simple algorithm, Newton's Method, that uses successive approximations to zero in on an answer that is within 0.0001 of the true answer.

One sample run is

```
Enter number: 2
```
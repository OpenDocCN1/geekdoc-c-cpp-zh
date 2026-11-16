# 14.5 Defining a New Numeric Type

C++'s class feature allows us to define our own complete types. We will define a new numeric type that models mathematical rational numbers. In mathematics, a rational number is defined as the ratio of two integers, where the second integer must be nonzero. Commonly called a fraction, a rational number's two integer components are called numerator and denominator. Rational numbers possess certain properties; for example, two fractions can have different numerators and denominators but still be considered equal (1/2 = 2/4). Listing 14.5 (simplerational.cpp) shows how we can define and use rational numbers.

```
Listing 14.5: simplerational.cpp
#include <iostream>
#include <cstdlib>

// Models a mathematical rational number
class SimpleRational {
 int numerator;
 int denominator;
public:
 // Initializes the components of a Rational object
 SimpleRational(int n, int d): numerator(n), denominator(d) {
 if (d == 0) {
 // Display error message
 std::cout << "Zero denominator error\n";
 exit(1); // Exit the program
 }
 }

 // The default constructor makes a zero rational number
 // 0/1
 SimpleRational(): numerator(0), denominator(1) {}

 // Allows a client to reassign the numerator
 void set_numerator(int n) {
 numerator = n;
 }

 // Allows a client to reassign the denominator.
 // Disallows an illegal fraction (zero denominator).
 void set_denominator(int d) {
 if (d != 0)
 denominator = d;
 else {
 // Display error message
 std::cout << "Zero denominator error\n";
 exit(1); // Exit the program
 }
 }

 // Allows a client to see the numerator's value.
 int get_numerator() {
 return numerator;
 }
}
```
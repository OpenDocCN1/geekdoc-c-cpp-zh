```
if (d == 0) {
    // Display error message
    std::cout << "Zero denominator error\n";
    exit(1); // Exit the program
}
}
```

```
// The default constructor makes a zero rational number
// 0/1
OpaqueRational() : OpaqueRational(0, 1) {}
};
```

Note that clients can make an OpaqueRational object, but after its creation clients can neither see nor change the internals of the object. Gone are the set_numerator, set_denominator, get_numerator, and get_denominator methods of the SimpleRational class.

We would like to be able to print an OpaqueRational object as easily as the following:

```
OpaqueRational frac(1, 2); // Make the fraction 1/2
std::cout << frac << '\n';
```

We would like the std::cout statement to print the text

![](bbox=[0.115, 0.455, 0.8, 0.475])

This would require an operator<< function overloaded to accept a OpaqueRational object, and this operator<< function would need to be able to access the private instance variables of the OpaqueRational object.

A class can grant access to an outside function or another class via the friend reserved word. In Listing 15.13 (printonlyrational.cpp) we specify a friend function that allows clients to display in human-readable form an opaque rational number object via operator<< with an output stream object.

# Listing 15.13: printonlyrational.cpp

```
#include <iostream>
#include <cstdlib>
// Models a mathematical rational number
class PrintOnlyRational {
  int numerator;
  int denominator;
public:
  // Initializes the components of an PrintOnlyRational object
  PrintOnlyRational(int n, int d): numerator(n), denominator(d) {
    if (d == 0) {
      // Display error message
      std::cout << "Zero denominator error\n";
      exit(1); // Exit the program
    }
  }
  // The default constructor makes a zero rational number
  // 0/1
  PrintOnlyRational(): PrintOnlyRational(0, 1) {}
```
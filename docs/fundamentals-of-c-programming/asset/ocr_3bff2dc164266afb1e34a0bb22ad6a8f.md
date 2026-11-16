The output of Listing 4.15 (impreciseddifference.cpp) is:

```
0.5
0.5799999999999272
```

The program uses an additional #include directive:

```
#include <iomanip>
```

This preprocessor directive allows us to use the std::setprecision output stream manipulator that directs the std::cout output stream object to print more decimal places in floating-point values. During the program's execution, the first subtraction yields the correct answer. We now know that some floating-point numbers (like 0.5) have exact internal representations while others are only approximations. The exact answer for the second subtraction should be 0.58, and if we round the reported result to 12 decimal places, the answer matches. Floating-point arithmetic often produces results that are close approximations of the true answer.

Listing 4.16 (precise8th.cpp) computes zero in a roundabout way:

1 - 1/8 - 1/8 - 1/8 - 1/8 - 1/8 - 1/8 - 1/8 - 1/8 = 0

```
#include <iostream>

int main() {
    double one = 1.0,
           one_eighth = 1.0/8.0,
           zero = one - one_eighth - one_eighth - one_eighth - one_eighth
                - one_eighth - one_eighth - one_eighth;

    std::cout << "one = " << one << ", one_eighth = " << one_eighth
              << ", zero = " << zero << '\n';
}
```

Listing 4.16 (precise8th.cpp) prints

```
one = 1, one_eighth = 0.125, zero = 0
```

The number 1/8 has an exact decimal representation, 0.125. It also has an exact binary representation, 0.001₂.

Consider, however, 1/5 While 1/5 = 0.2 has a finite representation in base 10, it has no finite representation in base 2:

1/5 = 0.2 = 0.0011001100110011...₂

In the binary representation the 0011 bit sequence repeats without end. This means 1/5 does not have an exact floating-point representation. Listing 4.17 (imprecise5th.cpp) illustrates with arithmetic involving 1/5.
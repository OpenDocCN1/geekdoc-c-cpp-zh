# Common Programming Error 6.6

A compilation error occurs if an enum constant’s value is outside the range that can be represented by the enum’s underlying type.

# 6.9 C++11 Random Numbers

According to CERT, function rand does not have “good statistical properties” and can be predictable, which makes programs that use rand less secure (CERT guideline MSC30-CPP). As we mentioned in Section 6.7, C++11 provides a new, more secure library of random-number capabilities that can produce nondeterministic random numbers for simulations and security scenarios where predictability is undesirable. These new capabilities are located in the C++ Standard Library’s <random> header.

Random-number generation is a mathematically sophisticated topic for which mathematicians have developed many random-number generation algorithms with different statistical properties. For flexibility based on how random numbers are used in programs, C++11 provides many classes that represent various random-number generation *engines* and *distributions*. An engine implements a random-number generation algorithm that produces pseudorandom numbers. A distribution controls the range of values produced by an engine, the types of those values (e.g., int, double, etc.) and the statistical properties of the values. In this section, we’ll use the default random-number generation engine—`default_random_engine`—and a `uniform_int_distribution`, which *evenly* distributes pseudorandom integers over a specified range of values. The default range is from 0 to the maximum value of an int on your platform.

# Rolling a Six-Sided Die

Figure 6.12 uses the `default_random_engine` and the `uniform_int_distribution` to roll a six-sided die. Line 14 creates a `default_random_engine` object named engine. Its constructor argument seeds the random-number generation engine with the current time. If you don’t pass a value to the constructor, the default seed will be used and the program will produce the same sequence of numbers each time it executes. Line 15 creates randomInt—a `uniform_int_distribution` object that produces unsigned int values (as specified by <unsigned int>) in the range 1 to 6 (as specified by the constructor arguments). The expression `randomInt(engine)` (line 21) returns one unsigned int value in the range 1 to 6.

```
```cpp
// Fig. 6.12: fig06_12.cpp
// Using a C++11 random-number generation engine and distribution
// to roll a six-sided die.
#include <iostream>
#include <iomanip>
#include <random> // contains C++11 random number generation features
#include <ctime>
using namespace std;

int main()
{
```
```

**Fig. 6.12** | Using a C++11 random-number generation engine and distribution to roll a six-sided die. (Part 1 of 2.)
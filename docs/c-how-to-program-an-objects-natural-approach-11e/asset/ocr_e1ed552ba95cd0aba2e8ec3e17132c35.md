The C++ Core Guidelines provide many constructor recommendations. We’ll see more in the next two chapters. If a class has a class invariant²¹—that is, it requires its data members to have specific values or ranges of values (as in class `Time`)—the class should define a constructor that validates its arguments and, if any are invalid, throws an exception to prevent the object from being created.²²,²³,²⁴

# Testing the Updated Class `Time`

Function `main` in Fig. 9.12 initializes five `Time` objects:

+   - one with all three arguments defaulted in the implicit constructor call (line 16),
+   - one with one argument specified (line 17),
+   - one with two arguments specified (line 18),
+   - one with three arguments specified (line 19), and
+   - one with three invalid arguments specified (line 29).

The program displays each object in 24-hour and 12-hour time formats. The program displays an error message for `Time` object `t5` (line 29) because its constructor arguments are out of range. The variable `t5` never represents a fully constructed object in this program because the exception is thrown during construction.

```
```cpp
// fig09_12.cpp
// Constructor with default arguments.
#include <format>
#include <iostream>
#include <stdexcept>
#include <string>
#include "Time.h" // include definition of class Time from Time.h

// displays a Time in 24-hour and 12-hour formats
void displays(std::string_view message, const Time& time) {
    std::cout << std::format("\n24-hour time: {}\n12-hour time: {}\n",
        message, time.to24HourString(), time.to12HourString());
}

int main() {
    const Time t1{}; // all arguments defaulted
    const Time t2{2}; // hour specified; minute & second defaulted
    const Time t3{21, 34}; // hour & minute specified; second defaulted
    const Time t4{12, 25, 42}; // hour, minute & second specified
}
```
```

**Fig. 9.12** | Constructor with default arguments. (Part 1 of 2.)

21. “Class invariant.” Wikipedia, Wikimedia Foundation. Accessed April 14, 2023. https://en.wiki\npedia.org/wiki/Class_invariant.

22. C++ Core Guidelines, “C.40: Define a Constructor if a Class Has an Invariant.” Accessed April 14, 2023. https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rc-ctor.

23. C++ Core Guidelines, “C.41: A Constructor Should Create a Fully Initialized Object.” Accessed April 14, 2023. https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rc-complete.

24. C++ Core Guidelines, “C.42: If a Constructor Cannot Create a Fully Initialized Object, Throw an Exception.” Accessed April 14, 2023. https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rc-throw.
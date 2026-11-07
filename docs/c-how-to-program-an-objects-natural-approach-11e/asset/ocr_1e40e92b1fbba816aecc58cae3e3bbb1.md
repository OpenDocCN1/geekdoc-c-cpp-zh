functions. An example would be a `std::array`’s or a `std::vector`’s empty function. A program might test empty before attempting to read an item from the container object.[^19]

# Utility functions

A utility function (also called a helper function) is a private member function that supports the operation of a class’s other member functions and is not intended for use by the class’s clients. Typically, a utility function contains code that would otherwise be duplicated in several other member functions. Many codebases have naming conventions for private member functions, such as preceding their names with an underscore (`_`).

# Checkpoint

+   1. *(Fill-in)* A(n) ________ is an access function that tests whether a condition is true or false.  
+      **Answer:** predicate function.
+   2. *(Fill-in)* A(n) ________ typically contains code that would otherwise be duplicated in several other member functions.  
+      **Answer:** utility function.

# 9.11 Time Class Case Study: Constructors with Default Arguments

The program of Figs. 9.10–9.12 enhances class Time to demonstrate a constructor with default arguments.

# 9.11.1 Class Time

Like other functions, constructors can specify default arguments. Line 11 of Fig. 9.10 declares a Time constructor with the default argument value 0 for each parameter. A constructor with default arguments for all its parameters is also a default constructor—that is, it can be invoked with no arguments. There can be only one default constructor per class.[^20] Any change to a function’s default argument values requires the client code to be recompiled (to ensure that the program still functions correctly).

```
```cpp
// Fig. 9.10: Time.h
// Time class containing a constructor with default arguments.
// Member functions defined in Time.cpp.
#pragma once // prevent multiple inclusions of header
#include <string>
```
```

**Fig. 9.10** | Time class containing a constructor with default arguments. (Part 1 of 2.)

+   19. Many programmers prefer to begin the names of predicate functions with the word “is.” For example, useful predicate functions for our Time class might be `isAM` and `isPM`. Such functions also should be preceded with the attribute `[[nodiscard]]` so the compiler confirms that the return value is used in the caller, rather than ignored.
+   20. You’ll see that C++20 concepts (Chapter 15) enable you to overload any function or member function for use with types that match specific requirements.
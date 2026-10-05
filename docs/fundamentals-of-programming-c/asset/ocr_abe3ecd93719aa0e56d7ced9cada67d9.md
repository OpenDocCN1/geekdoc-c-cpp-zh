# Chapter 10

# Managing Functions and Data

This chapter covers some additional aspects of functions in C++. Recursion, a key concept in computer science is introduced.

# 10.1 Global Variables

All variables to this point have been local to functions or local to blocks within the bodies of conditional or iterative statements. Local variables have some desirable properties:

+   * A local variable occupies memory only when the variable is in scope. When the program execution leaves the scope of a local variable, it frees up the memory for that variable. This freed memory is available for use by the local variables in other functions during their invocations.

+   * We can use the same variable name in different functions without any conflict. The compiler derives all of its information from a local variable used within a function from the declaration of variable in that function. The compiler will not look for the declaration of a local variable of another function. Thus, there is no local variable in one function can interfere with a local variable declared in another function.

A local variable transparency, so its value is lost between function invocations. Sometimes it is desirable to have a variable that lives as long as the program is running; that is, until the main function completes. In contrast to a local variable, a global variable is declared outside all functions and is not local to any particular function. In fact, any function that appears in the text of the source code after the point of the global variable's declaration may legally access and/or modify that variable.

Listing 10.1: globalcalculator.cpp is a modification of Listing 9.10 (calculator.cpp) that uses a global variable named result that is shared by all functions in the program.

```
Listing 10.1: globalcalculator.cpp
#include <iostream>
#include <cmath>
using namespace std;
```
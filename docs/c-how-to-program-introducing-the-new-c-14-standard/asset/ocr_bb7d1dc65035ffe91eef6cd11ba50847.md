# 6.2 Program Components in C++

C++ programs are typically written by combining “prepackaged” functions and classes available in the C++ Standard Library with new functions and classes you write. The C++ Standard Library provides a rich collection of functions for common mathematical calculations, string manipulations, character manipulations, input/output, error checking and many other useful operations.

Functions allow you to modularize a program by separating its tasks into self-contained units. You’ve used a combination of library functions and your own functions in almost every program you’ve written.

There are several motivations for modularizing a program with functions:

+   - Software reuse. For example, in earlier programs, we did not have to define how to read a line of text from the keyboard—C++ provides this capability via the `getline` function of the `<string>` header.
+   - Avoiding code repetition.
+   - Dividing a program into meaningful functions makes the program easier to test, debug and maintain.
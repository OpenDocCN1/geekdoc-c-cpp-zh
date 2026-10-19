# Building Your Own Assertion Mechanism

Cross-Reference Building your own assertion routine is a good example of programming “into” a language rather than just programming “in” a language. For more details on this distinction, see Section 34.4, “Program into Your Language, Not in It.”

Many languages have built-in support for assertions, including C++, Java, and Microsoft Visual Basic. If your language doesn’t directly support assertion routines, they are easy to write. The standard C++ assert macro doesn’t provide for text messages. Here’s an example of an improved ASSERT implemented as a C++ macro:

```
C++ Example of an Assertion Macro
#define ASSERT( condition, message ) {
    if ( !(condition) ) {
        LogError( "Assertion failed: ",
            #condition, message );
        exit( EXIT_FAILURE );
    }
}
```

# Guidelines for Using Assertions

Here are some guidelines for using assertions:

*Use error-handling code for conditions you expect to occur; use assertions for conditions that should never occur*  Assertions check for conditions that should never occur. Error-handling code checks for off-nominal circumstances that might not occur very often, but that have been anticipated by the programmer who wrote the code and that need to be handled by the production code. Error handling typically checks for bad input data; assertions check for bugs in the code.

If error-handling code is used to address an anomalous condition, the error handling will enable the program to respond to the error gracefully. If an assertion is fired for an anomalous condition, the corrective action is not merely to handle an error gracefully—the corrective action is to change the program’s source code, recompile, and release a new version of the software.

A good way to think of assertions is as executable documentation—you can’t rely on them to make the code work, but they can document assumptions more actively than program-language comments can.

*Avoid putting executable code into assertions*  Putting code into an assertion raises the possibility that the compiler will eliminate the code when you turn off the assertions. Suppose you have an assertion like this:
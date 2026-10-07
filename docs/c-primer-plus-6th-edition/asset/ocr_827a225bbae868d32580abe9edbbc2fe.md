Still, the problem remains macros don't pass by value. Even with this new definition,
SQUARE(c++) increments c twice, the inline square () function in Listing 8.1 evaluates
c, passes that value to be squared, and then increments c once.

The intent here not to show you how to use C macros. Rather, it is to suggest that if younhave using C macros to perform function-like services, you should consider converting
them to C++ inline functions.

# # Reference Variables

C++ adds a new compound type to the language—the reference variable. A reference is a
name that acts as an alias, or another name, for a previously defined variable. For
example, if you make tween reference to the clemens variable, you can use tween and
clemens interchangeably to represent variable. What of use of such an alias? It is to
help people who are embarrassed by this choice of variable names? Maybe, the main
use for a reference variable is a formal argument to a function. If you use a reference as
argument, the function works with the original data instead of a copy. References
provide a convenient alternative to pointers for processing large structures with a func-
tion, and they are essential for designing classes. Before you see how to use references with
functions, however, lets examine the basics of defining and using a reference. Keep in
mind the purpose of the following discussion is to illustrate how references work, not
how they are typically used.

# # Creating a Reference Variable

You might recall that C and C++ use the & symbol to indicate the address of a variable.
C++ assigns an additional meaning to the & symbol and presses it into service for declar-
ing references. For example, to make rodents an alternative name for the variable rats,
you could do the following:

```
int rats;
int & rodents = rats;    // makes rodents an alias for rats
```

In this context, & is not the operator identifier. Instead, it serves as part of the type identifi-
ier. Just as char * in a declaration means pointer-to-char, int & means reference-to-
int. The declaration allows you to use rats and rodents interchangeably; both
fer the same value and same memory location. Listing 8.2 illustrates the truth of
this claim.

Listing 8.2 firstref.cpp

```
// firstref.cpp -- defining and using a reference
#include <iostream>
int main() {
    using namespace std;
    int rats = 101;
    int & rodents = rats;    // rodents is a reference
```
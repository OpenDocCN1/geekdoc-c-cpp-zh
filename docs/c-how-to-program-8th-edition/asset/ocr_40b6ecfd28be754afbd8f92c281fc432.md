You’ve now seen how valuable the stack data structure is in implementing a key mechanism that supports program execution. Data structures have many important applications in computer science. We discussed stacks, queues, lists, trees and other data structures in Chapter 20, Custom Templated Data Structures, and Chapter 22, Standard Template Library (STL).

# 6.12 Functions with Empty Parameter Lists

In C++, an empty parameter list is specified by writing either `void` or nothing at all in parentheses. The prototype

`void print();`

specifies that function print does not take arguments and does not return a value.

Figure 6.17 shows both ways to declare and use functions with empty parameter lists.

```
```cpp
// Fig. 6.17: fig06_17.cpp
// Functions that take no arguments.
#include <iostream>
using namespace std;

void function1();            // function that takes no arguments
void function2( void );      // function that takes no arguments

int main()
{
   function1(); // call function1 with no arguments
   function2(); // call function2 with no arguments
} // end main

// function1 uses an empty parameter list to specify that
// the function receives no arguments
void function1()
{
   cout << "function1 takes no arguments" << endl;
} // end function1

// function2 uses a void parameter list to specify that
// the function receives no arguments
void function2( void )
{
   cout << "function2 also takes no arguments" << endl;
} // end function2
```
```

```
```text
function1 takes no arguments
function2 also takes no arguments
```
```

**Fig. 6.17** | Functions that take no arguments.

# 6.13 Inline Functions

Implementing a program as a set of functions is good from a software engineering standpoint, but function calls involve execution-time overhead. C++ provides **inline functions**.
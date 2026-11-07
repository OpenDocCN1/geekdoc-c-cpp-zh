In this section, we discuss these areas of memory and how we can use them. Understanding the characteristics and knowing how to use each area enables us to write better programs.

# 9.4.1 Code Memory

**Code memory** holds the program code. When the program is running, the running environment of C++ executes each statement, one after another, or branches to another statement. No objects are stored in this area of memory. Code memory is released when the program is terminated.

> > **Code memory stores the program code;**
> > **it is released when the program terminates.**

# 9.4.2 Static Memory

**Static memory** is used to hold **global objects** (those that are not part of any function, including `main`) and **static objects** created anywhere in the program (in the global area or inside functions). These objects are automatically destroyed and their memory is released when the program is terminated.

> > **Static memory stores the global and static objects;**
> > **it is released when the program terminates.**

# EXAMPLE 9.23

Program 9.13 shows a very simple program. The memory locations for three data variables, *first*, *second*, and *third*, are created in static memory. The first is a global variable; the second and the third are static variables.

# **Program 9.13**  Using static memory

```
```cpp
/******************************************************
* The program shows how global and static objects are visible
* at any point in the program. They last through the life of the
* program.
******************************************************/
#include <iostream>
using namespace std;

int first = 20;             // Global variable in static memory
static int second = 30;     // Static variable created in static memory

int main()
{
    static int third = 50;  // Static variable in static memory

    cout << "Value of global variable: " << first << endl;
```
```

*(continued)*
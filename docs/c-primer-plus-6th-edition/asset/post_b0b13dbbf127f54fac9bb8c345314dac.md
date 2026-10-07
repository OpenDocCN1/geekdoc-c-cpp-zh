
# Chapter 9 Memory Models and Namespaces

files (extern is used with no initialization.).A variable defined outside any function but qualified with the keyword static has file scope but is not made available to other files (internal linkage). A variable defined inside a block qualified with the keyword static is local to block (local scope, no linkage) retains its value for the duration of the program.

By default, C++ functions have external linkage, so they can be shared across files. Functions qualified with the keyword static have internal linkage and are confined to the defining file.

Dynamic memory allocation and deallocation, using new and delete, use the free store, or heap, for data. The memory comes in when new is called and is free when delete is called. The program uses pointers to keep track of these memory locations.

Namespaces let you define regions in which you can declare identifiers. The intent is to reduce name conflicts, particularly in large programs that use code from several vendors. You can make available identifiers in a namespace by using the scope-resolution operator, by using a declaration, or by using a directive.

# Chapter Review

- 1. What storage scheme would you use for the following situations?
  a. homer is a formal argument (parameter) to a function.
  b. The secret variable is to be shared by two files.
  c. The topsecret variable is to be shared by the functions in one file but hidden from other files.
  d. beencalled keeps track of how many times the function containing has been called.

- 2. Describe the differences between a using declaration and a using directive.

- 3. Rewrite the following so that it doesn't use using declarations or using directives:

```cpp
#include <iostream>
using namespace std;
int main()
{
    double x;
    cout << "Enter value: ";
    while (!cin >> x)
    {
        cout << "Bad input. Please enter a number: ";
        cin.clear();
        while (cin.get() != '\n')
            continue;
    }
}
```

```cpp
}
cout << "Value = " << x << endl;
return 0;
}
```

- 4. Rewrite the following so that it uses using declarations instead of the using directive:

```cpp
#include <iostream>
using namespace std;
int main()
{
    double x;
    cout << "Enter value: ";
    while (! cin >> x) {
        cout << "Bad input. Please enter a number: ";
        cin.clear();
        while (cin.get() != '\n')
            continue;
    }
    cout << "Value = " << x << endl;
    return 0;
}
```

- 5. Suppose you want the average(3,6) function to return an int average of the two arguments when it is called in one file, and you want to return a double average of the two int arguments when it is called in a second file in the same program. How could you set this up?

- 6. What will the following two-file program display?

```cpp
// file.cpp
#include <iostream>
using namespace std;
void other();
void another();
int x = 10;
int y;

int main()
{
    cout << x << endl;
    {
        int x = 4;
        cout << x << endl;
        cout << y << endl;
    }
}
other();
another();
return 0;
}
```

```cpp
void other() {
    int y = 1;
    cout << "Other: " << x << ", " << y << endl;
}
```

```cpp
// file 2.cpp
#include <iostream>
using namespace std;
extern int x;
namespace {
    int y = -4;
}
```

```cpp
void another() {
    cout << "another(): " << x << ", " << y << endl;
}
```

- 7. What will the following program display?

```cpp
#include <iostream>
using namespace std;
void other()
namespace n1 {
    int x = 1;
}

namespace n2 {
    int x = 2;
}

int main() {
    using namespace n1;
    cout << x << endl;
}

int x = 4;
cout << x << ", " << n1::x << " " << n2::x << endl;
}
using n2::x;
cout << x << endl;
other();
return 0;
}
```

```cpp
void other()
{
using namespace n2;
cout << x << endl;
{
int x = 4;
cout << x << ", " << n1::x << " " << n2::x << endl;
}
using n2::x;
cout << x << endl;
}
```

# Programming Exercises

- 1. Here is a header file:
// golf.h -- for pe9-1.cpp

```cpp
const int Len = 40;
struct golf
{
char fullname[Len];
int handicap;
};
```

> // non-interactive version:
// function sets golf structure to provided name, handicap
// using values passed as arguments to the function
void setgolf(golf &g, const char * name, int hc);

> // interactive version:
// function solicits name and handicap from user
// and sets the members of g to the values

- 2. Redo Listing 9.9, replacing the character array with a string. The program no longer have to check the input string fits, and it can check the input string.

- 3. Begin with the following structure:

```cpp
struct chaff
{
    char dross[20];
    int slag;
};
```
Write a program that uses placement new to place an array of such structures in a buffer. Then assign values to the structure members (remembering to use strcpy() for the char array) and use a loop to display the contents. Option 1 is to use a static array, like in 9.10, for the buffer. Option 2 is to use new to allocate the buffer.

- 4. Write a three-file program based on the following namespace:

```cpp
namespace SALES
{
    const int QUARTERS = 4;
    struct Sales
    {
        double sales[QUARTERS];
        double average;
        double max;
        double min;
    }; // copies the lesser of 4 or n items from the array
// to the sales member of s and computes and stores the
// average, maximum, and minimum values of the entered items;
// remaining elements of s, if any, set to 0
void setSales(Sales &s, const double ar[], int n);
// gathers sales for 4 quarters interactively, stores them
// in the sales member of s and computes and stores the
// average, maximum, and minimum values
void setSales(Sales &s);
// display all information in structure s
void showSales(const Sales &s);
}
```

The first file should be a header file that contains the namespace. The second file should be a source code file that extends the namespace to provide definitions for the prototyped functions. The third file should declare two Sales objects. It should use the interactive version of setSales() to provide values for one structure and the non-interactive version of setSales() to provide values for the second structure. It should display the contents of both structures by using showSales().

# Objects and Classes

In this chapter you'll learn about the:

- Procedural and object-oriented programming
- The concept of classes
- How to define and implement a class
- Public and private class access
- Class data members
- Class methods (also called class function members)
- Creating and using class objects
- Class constructors and destructors
- const member functions
- The this pointer
- Creating arrays of objects
- Class scope
- Abstract data types

Object-oriented programming (OOP) is a particular conceptual approach to designing programs, and C++ has enhanced C features that ease the way to applying that approach.The following are the most important OOP features:

- Abstraction
- Encapsulation and data hiding
- Polymorphism
- Inheritance
- Reusability of code

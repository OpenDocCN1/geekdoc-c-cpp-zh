C++, a general-purpose programming language, was created by Dr. Bjame Strous-strup from AT&T Bell labs in 1980. C++ was developed to support the object-oriented program designs based on the C language. C++ has two main features: one is that it is fully compatible with C; the other is that it supports object-oriented methods.

Data is the processing object in programs, which can be classified by its characistics. Data types in C++ can be divided into basic types and user-defined types. Basic types are predefined in the C++ compiling system, including the bool type, char (character) type, int (integer) type, float type (real numbers), and double type (double precision floating point type, or double precision). Apart from the bool type, these basic types can be classified into two categories: integer type and float type. Here char type is an integer type essentially: it is an integer whose length is 1, and used to store the ASCII code of characters. C++ language does not only have predefined basic types, but also allows user-defined types. User-defined types include enumeration type, structure type, union type, array type, and union type in this chapter. Class type is the core of C++ object-oriented program design, and it is the main content of the following chapters. The other user-defined data types will also be introduced in the following chapters. We introduced the basic methods of data input/output in this chapter.

Program design includes data structure and algorithm design. An algorithm is made up of a sequence of control structures. Sequential, case, and loop structures are the basic control structures in program design and they are the basis of constructing complex algorithms.

# Exercises

2.1 What are the main characteristics and advantages of C++?

2.2 Which of the following identifiers are legal?

Program,-page, _lock, test2, 3in1, @mail, A_B_C_D

2.3 What is the effect of each statement in Example 2.1?

```
#include <iostream>
using namespace std;
int main()
{
  cout<<"Hello!\n";
  cout<<"Welcome to c++!\n"
}
```
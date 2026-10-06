
## 2.5 User-Defined Data Type

| | c_data | s_data | l_data |
|---|---|---|---|
| uarea | | | |
| | | |

Fig. 2.10: Storage structure of a variable of union type uarea.

For example, the following is a declaration of a union type:

```cpp
union
{ char c_data;
 short s_data;
 long l_data;
}
```

Figure 2.10 is the storage structure of a variable of union type uarea.
A union may have no name when it is declared, and at this time it is called an anonymous union. Anonymous unions do not have names; they only declare a collection of members that have the same memory address. We can access these members by their member names directly.

For example, declare an unnamed union:

```cpp
union
{ int i;
 float f;
}
```

We can use it in a program like this:

```cpp
i=10;
f=2.2;
```

An unnamed union is usually used as a nested member in a structure body, see Example 2.14.

Example 2.14: A structure that can describe fighters, bombers, or transport planes.

```cpp
// 2_14.cpp
#include <iostream>
using namespace std;
struct aircraft
{
 int wingspan; //wingspread
 int passengers; //passenger
```

```cpp
union //Unnamed union used as a nested member in the structure body
{
    float fuel_load;      //fuel carried by fighters
    float bomb_load;      //bombs carried by bombers
    int pallets;           //pallets of transport planes
} fighter, bomber, transport;
```

```cpp
int main()
{
    fighter.wingspan = 40;
    fighter.passengers = 1;
    fighter.fuel_load = 12000.0;
```

```cpp
bomber.wingspan = 90;
bomber.passengers = 12;
bomber.bomb_load = 14000.0;
```

```cpp
transport.wingspan = 106;
transport.passengers = 4;
transport.pallets = 42;
```

```cpp
transport.fuel_load = 18000.0;
fighter.pallets = 4;

cout << "The fighter carries " << " pallets.\n";
cout << "The bomber bomb load is " << bomber.bomb_load << "\n";
}
```

Result:

| The fighter carries 4 pallets. |
| The bomber bomb load is 14000 |

## 2.6 Summary

C++ is evolved from Dennis Ritchie from Bell Labs created the C language on the B language in 1972. It has many advantages: concision and flexibility, plenty of operators and data structures, structured control statements, high execution efficiency of procedures, and having both the advantages of a high-level language and an assembly language.

C++, a general-purpose programming language, was created by Dr. Bjarne Stroustrup from AT&T Bell labs in 1980. C++ was developed to support the object-oriented program designs based on the C language. C++ has two main features: one is that it is fully compatible with C; the other is that it supports object-oriented methods.

Data is the processing object in programs, which can be classified by its characteristics. Data types in C++ can be divided into basic types and user-defined types. Basic types are predefined in the C++ compiling system, including the bool type, char (character) type, int (integer) type, float type (real numbers), and double type (double precision floating point type, or double precision). Apart from the bool type, these basic types can be classified into two categories: integer type and float type. Here char type is an integer type essentially: it is an integer whose length is 1, and used to store the ASCII code of characters. C++ language does not only have predefined basic types, but also allows user-defined types. User-defined types include enumeration type, structure type, union type, array type, and union type in this chapter. Class type is the core of C++ object-oriented program design, and it is the main content of the following chapters. The other user-defined data types will also be introduced in the following chapters. We introduced the basic methods of data input/output in this chapter.

Program design includes data structure and algorithm design. An algorithm is made up of a sequence of control structures. Sequential, case, and loop structures are the basic control structures in program design and they are the basis of constructing complex algorithms.

## Exercises

2.1 What are the main characteristics and advantages of C++?

2.2 Which of the following identifiers are legal?

Program,-page, _lock, test2, 3in1, @mail, A_B_C_D

2.3 What is the effect of each statement in Example 2.1?

```cpp
#include <iostream>
using namespace std;
int main()
{
  cout<<"Hello!\n";
  cout<<"Welcome to c++!\n";
}
```

2.4 What is the advantage of using the keyword const instead of using a #define statement?

2.5 Please write a statement in C++ that declares a constant PI with the value of 3.1415; and then declare a float variable a, and assign the value of PI to a.

2.6 What is the value of BLUE in the following enumeration?

```cpp
enum COLOR { WHITE, BLACK = 100, GREEN, BLUE };
```

2.7 What is the use of comments? What form does C++ have?

2.8 What is an expression? What is its value?

2.9 What are the values of the following?

- a) 201/4
- b) 201%4
- c) 201.0

2.10 What is the value of a, b, and c after executing the following?

```cpp
int a, b, c;
a++;
b = ++a;
```

2.11 Can we initialize variables in a for statement? How to achieve this?

2.12 What is the value of n after executing the following?

```cpp
int n;
for (n = 0; n < 100; n++);
```

2.13 What is the difference between i++ and ++i?

2.14 What is the range of a variable in if statement?

2.15 What is scope? What is global variable?

2.16 Given two variables x and y, write a if statement to show the smaller value.

2.17 Correct the errors in the following program. What is the result?

```cpp
#include <iostream>
using namespace std;
int main() {
int i, j;
i = 10;
j = 20;
cout << i + j;
return 0;
}
```

2.18 Write a program to prompt users to enter a number and then show the number on the screen.

2.19 What data types does C++ have?

2.20 Write a program to output the ASCII code of characters between 32 and 127.

2.21 Run the following program. Is it the same as you think?

```cpp
#include <iostream>
using namespace std;
int main() {
unsigned int x;
unsigned int y = 100;
unsigned int z = 50;
x = y - z;
cout << "Difference is: " << x << endl;
}
```

2.22 Run the following program, observe the difference between i++ and ++i.

```cpp
#include <iostream>
using namespace std;
int main() {
{
    int myAge = 39;
    int yourAge = 39;
    cout << "I am: " << myAge << "\n";
    cout << "You are: " << yourAge << "\n";
    myAge++; // postfix increment
    ++yourAge; // prefix increment
    cout << "One year passes...\n";
    cout << "I am: " << myAge << "\n";
    cout << "You are: " << yourAge << "\n";
    cout << "Another year passes:" << myAge << "\n";
    cout << "You are: " << ++yourAge << "\n";
    cout << "Let's print it again.\n";
    cout << "I am: " << myAge << "\n";
    cout << "You are: " << yourAge << "\n";
}
}
```

2.23 What is a constant? What is a variable?

2.24 Which storage types do variables have?

2.25 Write down the values of the following expressions:

- a) 2 < 3 && 6 < 9
- b) ! (4 < 7)
- c) !(3 > 5) || (6 < 2)

2.26 If a = 1, b = 2, c = 3, then what are the results of the following expressions?

- a) a|b-c
- b) a^b&-c
- c) a&b&c
- d) a|b&c

2.27 If a = 1, what are the results of the following expressions?

- a) !a|a
- b) -a|a
- c) c^a
- d) a>>2

2.28 Write a program to achieve this function: ask the user "Is it raining now?" and prompt the user to enter Y or N. If the user enters Y, display "It is raining now.*; if N is entered, display "It is not raining now."; otherwise, continue asking "Is it raining now?"

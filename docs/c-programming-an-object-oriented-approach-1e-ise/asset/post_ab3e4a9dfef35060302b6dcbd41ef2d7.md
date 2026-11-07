
## Program 9.2 Using a swap function with pass-by-reference (Continued)

```cpp
int temp = rX;
rX = rY;
rY = temp;
}
```

Run:
Values of x and y before swapping.
x: 10 y: 20
Values of x and y after swapping.
x: 20 y: 10

## Return-by-Reference

In the second case, **return-by-reference**, a called function has an object that must be returned to the calling function.

**Characteristics of Return-by-Value** In return-by-value, the called function returns an object of the desired type using the following prototype.

```cpp
type function (...);
```

Return-by-value is simple and can be used anywhere. We can return the value of a parameter or a local variable. The only drawback is the cost of copying. If the object to be returned is a fundamental type, we should not worry; if it is an object of a class type, we know that the copy constructor will be called and the cost may be high.

**Characteristics of Return-by-Reference** In **return-by-reference**, the type of the object to be returned is a reference to another object, as shown in the following prototype.

```cpp
type& function (...);
```

This method eliminates the cost of copying, but it has a drawback: We cannot return an object by reference if it is a value parameter or a local variable (except static). The reason, as we will discuss later in the chapter, is that when a function is terminated all local variables and value parameters are destroyed. When an object is destroyed, we cannot have an alias name to it, but we can return a reference to a reference parameter.

## EXAMPLE 9.9

Assume we want to write a function to find the larger between two integers. We could use either the combination of pass-by-value and return-by-value or the combination of pass-by-reference and return-by-reference. The following shows the two programs side by side for comparison.

```cpp
#include <iostream>                    #include <iostream>
using namespace std;                   using namespace std;

// Return-by-value                                      // Return-by-reference
int larger (int x, int y)                              int& larger (int& x, int& y)
{                                                     {
    if (x > y)                                            if (x > y)
    {                                                     {
        return x;                                            return x;
    }                                                     }
    return y;                                              return y;
}                                                     }
int main ()                                            int main ()
{                                                     {
    int x = 10;                                             int x = 10;
    int y = 20;                                             int y = 20;
    int z = larger (x, y);                                  int z = larger (x, y);
    cout << z;                                              cout << z;
    return 0;                                               return 0;
}                                                     }

Run:                                                  Run:
20                                                    20
```

We see examples of both practices in cases like this because the cost of copying is small in pass-by-value and return-by-value.

## EXAMPLE 9.10

In this example we find the larger between two objects of class types. In Chapter 7 we created a fraction class. We do not repeat the interface and the implementation file here (separate compilation). We just create an application file that uses pass-by-reference and return-by-reference to find the larger of two fractions. Program 9.3 shows the application file.

## Program 9.3 Finding the larger of two fractions

```cpp
/***************************************************************
 * The program creates two pairs of fractions and then calls a  *
 * function named larger to find the larger in each pair        *
 ***************************************************************/
#include "fraction.h"

Fraction& larger (Fraction&, Fraction&);  // Prototype

int main ( )
{
    // Creating first pair of fractions and finding the larger
    Fraction fract1 (3, 13);
    Fraction fract2 (5, 17);
    cout << "Larger of the first pair of fractions: ";
    larger (fract1, fract2).print ();
    // Creating second pair of fractions and finding the larger
    17    Fraction fract3 (4, 9);
    18    Fraction fract4 (1, 6);
    19    cout << "Larger of the second pair of fractions: ";
    20    larger (fract3, fract4).print ();
    21    return 0;
    22 }
    23 /********************************************************
    24  * The function gets two fractions by reference, compares them *
    25  * and returns the larger.                                  *
    26  ********************************************************/
    27 Fraction& larger (Fraction& fract1, Fraction& fract2)
    28 {
    29    if (fract1.getNumer() * fract2.getDenom() >
    30          fract2.getNumer() * fract1.getDenom())
    31    {
    32        return fract1;
    33    }
    34    return fract2;
    35 }
```

Run:
Larger of first pair of fractions: 5/17
Larger of second pair of fractions: 4/9

The interesting point is that in each call, the returned item is an *lvalue*, one of the objects that was sent to the function. This is why we can apply the *print* function defined in the class to the object (lines 17 and 22).

## 9.2 POINTERS

A **pointer type** is a compound type representing the address of a memory location. A pointer variable is a variable whose contents are of pointer type. In this section, we discuss addresses, pointer types, pointer variables, and some related issues.

### 9.2.1 Addresses

When we talk about addresses, we must consider two separate concepts: addresses in memory and the address of a variable.

### Addresses in Memory

As we discussed briefly in Chapter 1, computer memory is a sequence of bytes. In other words, the smallest accessible unit is a *byte*. When we say that a computer has a memory (random access memory, or RAM) of 1 kilobyte, we mean that memory is made of 2<sup>10</sup> or 1024 bytes. Today’s computers have memories in the range of megabytes (2<sup>20</sup>), gigabytes (2<sup>30</sup>), or even terabytes (2<sup>40</sup>).

Each byte of memory has an address. The addresses are shown in hexadecimal format. For example, in a computer with 1 kilobyte of memory, the bytes are numbered from 0x000 to 0x3ff (0 to 1023 in decimal) as shown in Figure 9.7.

![](img/d68f6199646ca63591a6d8419e0ed4ba_410_0.png)

### Address of a Variable

In our programs, we define variables of different types: Boolean, character, integer, floating point, and class. Each variable occupies one or more bytes of memory. A variable of type *bool* or *char* normally occupies one byte of memory. A variable of type *int* may occupy four or more bytes of memory. A variable of type *double* may also occupy four or more bytes of memory (the *sizeof* operator can be used to determine the number of bytes). The address of a variable is the address of the first byte it occupies. This is an important point we must remember when we are working with addresses or pointers, as we will see. To get the address of a variable, we use the **address operator (&)** in front of the variable.

> The address of a variable is the address of the first byte occupied by that variable.

## EXAMPLE 9.1

In this example we write a simple program that prints the addresses of three variables: *bool*, *int*, and *double* (Program 9.4).

### Program 9.4 Printing size, value, and addresses

```cpp
/**************************************************************
 * The program to define three variables and to print their    *
 * values and their addresses in the memory                    *
 **************************************************************/
#include <iostream>
using namespace std;

int main ( )
{
    // Declaration of three data variables
    bool flag = true;
    int score = 92;
    double average = 82.56;
    // Printing size, value, and address of the flag variable
    cout << "A variable of type bool" << endl;
    cout << "Size: " << sizeof (flag) << " " ;
    cout << "Value: " << flag << " " ;
    cout << "Address: " << &flag << endl << endl;
```

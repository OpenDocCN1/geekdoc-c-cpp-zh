
## Chapter 12
Programming Projects

4. (Program) a. Write a program that has a declaration in main() to store the string
Vacation is near in an array named message. Include a function call that accepts
message in an argument named str and displays the contents of message by
using the pointer *(str + i).

b. Modify the display function in Exercise 4a to alter the address in message.
Also, use the expression *str rather than (*str + i) to retrieve the correct
element.

5. (Program) Write a program that declares three-dimensional arrays named price,
quantity, and amount. Each array should be declared in main() and be capable of
hiding double-precision numbers. The numbers to be stored in price are 10.62,
14.89, 13.21, 16.55, 18.62, 19.47, 6.58, 18.32, 12.15, and 3.98. The numbers to be stored in
quantity are 4, 8, 6, 7, 9, 15, 3, 5, 2.9, and 4.8. Have your program pass these
three arrays to a function called extend(), which calculates the elements in the
amount array as the product of the equivalent elements in price and quantity
for example, amount[1] = price[1] * quantity[1].

After extend() has put values in the amount array, the values in the array
within main(). Write the extend() function by using pointers.

6. (Desk Check) a. Determine the output of the following program:

```cpp
#include <iostream>
using namespace std;

void arr(int [][][]); // equivalent to void arr(int (*)[][]);

int main()
{
    const int ROWS = 2;
    const int COLS = 3;
    int nums [ROWS][COLS] = {{33,16,29}, {54,67,99}};

    arr(nums);
    return 0;
}

void arr(int (*val)[3])
{
    cout << endl << *(val);
    cout << endl << *(val + 1);
    cout << endl << *(val + 1) + 2;
    cout << endl << *(val) + 1;
    return;
}
```

b. Given the declaration for val in the arr() function, is the notation val[1][2]
valid in the function?

## Chapter 13 Structures

- 13.1 Single Structures
- 13.2 Arrays of Structures
- 13.3 Structures as Function Arguments
- 13.4 Linked Lists
- 13.5 Dynamic Data Structure Allocation
- 13.6 Unions
- 13.7 Common Programming Errors
- 13.8 Chapter Summary

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_726_0.png)

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

### 13.1 Single Structures

In a1's,, a a structure can be thought of as a class that has all, instance variables and a methods.., applications, a a is a, to, is the the.
, a a...




 a a





,,,,, the,, the, the data items are the,..., a1... voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

```.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

### 13.1 Single Structures

In C++, a structure is defined using the `struct` keyword. It allows you to group variables of different types together under a single name. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage. 

A structure is a historical holdover from C. From a programmer's perspective, a structure can be thought of as a class that has all public instance variables and member methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C and C++, a structure provides a way to store values of different data types, such as an integer part number, a character part type, and a double-precision supply voltage.

To define a structure, use the following syntax:

```cpp
struct Part {
    int partNumber; own    char partType;
    double supplyVoltage;
};
```

Once a structure is defined, you can create variables of that type:

```cpp
Part p1;
p1.partNumber = 101;
p1.partType = 'A';
p1.supplyVoltage = 12.5;
```

You can also initialize the structure at the time of declaration:

```cpp
Part p2 = {102, 'B', 5.5};
```

Accessing members of a structure is done using the dot operator (`.`):

```cpp
cout << p1.partNumber << endl;
```

Structures are useful for organizing related data. For example, if you need to manage information for multiple parts, you can use an array of structures:

```cpp
Part inventory[10];
inventory[0].partNumber = 201;
```

Structures can also be passed to functions and returned from functions:

```cpp
void displayPart(const Part& p) {
    cout << p.partNumber << " " << p.partType << " " << p.supplyVoltage << endl;
}

int main() {
    Part p = {301, 'C', 3.3};
    displayPart(p);
    return 0;
}
```

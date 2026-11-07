
## Releasing Dynamic Memory with delete

To destroy a dynamically allocated object and free the space for the object, use the `delete` operator as follows:

```cpp
delete timePtr;
```

This statement first *calls the destructor for the object to which timePtr points, then deallocates the memory associated with the object, returning the memory to the free store.*

> **Common Programming Error 10.2**
> *Not releasing dynamically allocated memory when it is no longer needed can cause the system to run out of memory prematurely. This is sometimes called a “memory leak.”*

![](img/b42ba5cd262b1358d16610173f975e4d_487_0.png)

> **Error-Prevention Tip 10.1**
> *Do not delete memory that was not allocated by new. Doing so results in undefined behavior.*

![](img/b42ba5cd262b1358d16610173f975e4d_487_1.png)

> **Error-Prevention Tip 10.2**
> *After you delete a block of dynamically allocated memory, be sure not to delete the same block again. One way to guard against this is to immediately set the pointer to nullptr. Deleting a nullptr has no effect.*

![](img/b42ba5cd262b1358d16610173f975e4d_487_2.png)

## Initializing Dynamic Memory

You can provide an initializer for a newly created fundamental-type variable, as in

```cpp
double *ptr = new double(3.14159);
```

which initializes a newly created double to 3.14159 and assigns the resulting pointer to ptr. The same syntax can be used to specify a comma-separated list of arguments to the constructor of an object. For example,

```cpp
Time *timePtr = new Time(12, 45, 0);
```

initializes a new Time object to 12:45 PM and assigns the resulting pointer to timePtr.

## Dynamically Allocating Built-In Arrays with new []

You can also use the new operator to allocate built-in arrays dynamically. For example, a 10-element integer array can be allocated and assigned to gradesArray as follows:

```cpp
int *gradesArray = new int[10]();
```

which declares int *gradesArray and assigns to it a pointer to the first element of a dynamically allocated 10-element array of ints. The parentheses following new int[10] evaluate the array’s elements—fundamental numeric types are set to 0, bools are set to false, pointers are set to nullptr and class objects are initialized by their default constructors. The size of an array created at compile time must be specified using an integral constant expression; however, a dynamically allocated array’s size can be specified using any non-negative integral expression that can be evaluated at execution time.

## C++11: Using a List Initializer with a Dynamically Allocated Built-In Array

![](img/b42ba5cd262b1358d16610173f975e4d_487_3.png)

Prior to C++11, when allocating a built-in array of objects dynamically, you *could not* pass arguments to each object’s constructor—each object was initialized by its *default constructor*.

- When a built-in array is passed to a general-purpose function designed to handle arrays of any size, the array’s **size** must be passed as an additional argument.
- One built-in array cannot be *assigned* to another with the assignment operator(s).

Class development is an interesting, creative and intellectually challenging activity—always with the goal of *crafting valuable classes*. With C++, you can implement more robust array capabilities via classes and operator overloading as has been done with class templates `array` and `vector` in the C++ Standard Library. In this section, we’ll develop our own custom array class that’s preferable to built-in arrays. When we refer to “arrays” in this case study, we mean built-in arrays.

In this example, we create a powerful `Array` class that performs range checking to ensure that subscripts remain within the bounds of the `Array`. The class allows one `Array` object to be assigned to another with the assignment operator. `Array` objects know their size, so the size does not need to be passed separately to functions that receive `Array` parameters. Entire `Arrays` can be input or output with the stream extraction and stream insertion operators, respectively. You can compare `Arrays` with the equality operators `==` and `!=`.

## 10.10.1 Using the Array Class

The program of Figs. 10.9–10.11 demonstrates class `Array` and its overloaded operators. First we walk through `main` (Fig. 10.9) and the program’s output, then we consider the class definition (Fig. 10.10) and each of its member-function definitions (Fig. 10.11).

```cpp
// Fig. 10.9: fig10_09.cpp
// Array class test program.
#include <iostream>
#include <stdexcept>
#include "Array.h"
using namespace std;

int main()
{
    Array<int> integers1( 7 ); // seven-element Array
    Array<int> integers2; // 10-element Array by default

    // print integers1 size and contents
    cout << "Size of Array integers1 is "
         << integers1.getSize()
         << "\nArray after initialization:\n" << integers1;

    // print integers2 size and contents
    cout << "\nSize of Array integers2 is "
         << integers2.getSize()
         << "\nArray after initialization:\n" << integers2;

    // input and print integers1 and integers2
    cout << "\nEnter 17 integers:" << endl;
    cin >> integers1 >> integers2;
```

**Fig. 10.9** | Array class test program. (Part 1 of 3.)

```text
Size of Array integers1 is 7
Array after initialization:
             0          0          0          0
             0          0          0


Size of Array integers2 is 10
Array after initialization:
             0          0          0          0
             0          0          0          0
             0          0          0

Enter 17 integers:
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17

After input, the Arrays contain:
integers1:
             1          2          3          4
             5          6          7
integers2:
             8          9          10         11
             12         13         14         15
             16         17

Evaluating: integers1 != integers2
integers1 and integers2 are not equal

Size of Array integers3 is 7
Array after initialization:
             1          2          3          4
             5          6          7

Assigning integers2 to integers1:
integers1:
             8          9          10         11
             12         13         14         15
             16         17

integers2:
             8          9          10         11
             12         13         14         15
             16         17

Evaluating: integers1 == integers2
integers1 and integers2 are equal

integers1[5] is 13

Assigning 1000 to integers1[5]
integers1:
             8          9          10         11
             12         1000       14         15
             16         17

Attempt to assign 1000 to integers1[15]
An exception occurred: Subscript out of range
```

**Fig. 10.9** | Array class test program. (Part 3 of 3.)

### Creating Arrays, Outputting Their Size and Displaying Their Contents

The program begins by instantiating two objects of class Array—integers1 (Fig. 10.9, line 10) with seven elements, and integers2 (line 11) with the default Array size—10 elements (specified by the Array default constructor’s prototype in Fig. 10.10, line 14). Lines 14–16 in Fig. 10.9 use member function getSize to determine the size of integers1 then output integers1’s contents, using the Array overloaded stream insertion operator. The sample output confirms that the Array elements were set correctly to zeros by the constructor. Next, lines 19–21 output the size of Array integers2 then output integers2’s contents, using the Array overloaded stream insertion operator.

### Using the Overloaded Stream Extraction Operator to Fill an Array

Line 24 prompts the user to input 17 integers. Line 25 uses the Array overloaded stream extraction operator to read the first seven values into integers1 and the remaining 10 values into integers2. Lines 27–29 output the two arrays with the overloaded Array stream insertion operator to confirm that the input was performed correctly.

### Using the Overloaded Inequality Operator

Line 34 tests the overloaded inequality operator by evaluating the condition

```cpp
integers1 != integers2
```

The program output shows that the Arrays are not equal.

### Initializing a New Array with a Copy of an Existing Array’s Contents

Line 39 instantiates a third Array called integers3 and initializes it with a copy of Array integers1. This invokes class Array’s copy constructor to copy the elements of integers1 into integers3. We discuss the details of the copy constructor shortly. The copy constructor can also be invoked by writing line 39 as follows:

```cpp
Array<int> integers3 = integers1;
```

The equal sign in the preceding statement is not the assignment operator. When an equal sign appears in the declaration of an object, it invokes a constructor for that object. This form can be used to pass only a single argument to a constructor—specifically, the value on the right side of the = symbol.

Lines 41–43 output the size of integers3 then output integers3’s contents, using the Array overloaded stream insertion operator to confirm that integers3’s elements were set correctly by the copy constructor.

### Using the Overloaded Assignment Operator

Line 47 tests the overloaded assignment operator (=) by assigning integers2 to integers1. Lines 49–50 display both Array objects’ contents to confirm that the assignment was successful. Array integers1 originally held 7 integers, but was resized to hold a copy of the 10 elements in integers2. As we’ll see, the overloaded assignment operator performs this resizing operation in a manner that’s transparent to the client code.

### Using the Overloaded Equality Operator

Line 55 uses the overloaded equality operator (==) to confirm that objects integers1 and integers2 are indeed identical after the assignment in line 47.

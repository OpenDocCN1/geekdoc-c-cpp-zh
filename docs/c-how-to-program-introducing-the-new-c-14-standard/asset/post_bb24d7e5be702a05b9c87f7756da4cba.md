
## Releasing Dynamically Allocated Built-In Arrays with `delete[]`

To deallocate the memory to which `gradesArray` points, use the statement

```cpp
delete[] gradesArray;
```

If the pointer points to a built-in array of objects, the statement first calls the destructor for every object in the array, then deallocates the memory. If the preceding statement did *not* include the square brackets (`[]`) and `gradesArray` pointed to a built-in array of objects, the result is *undefined*—some compilers call the destructor only for the first object in the array. Using `delete` or `delete[]` on a `nullptr` has no effect.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1371_0.png)

## Common Programming Error 10.2

Using `delete` instead of `delete[]` for built-in arrays of objects can lead to runtime logic errors. To ensure that every object in the array receives a destructor call, always delete memory allocated as an array with operator `delete[]`. Similarly, always delete memory allocated as an individual element with operator `delete`—the result of deleting a single object with operator `delete[]` is undefined.

## C++11: Managing Dynamically Allocated Memory with `unique_ptr`

C++11’s `unique_ptr` is a “smart pointer” for managing dynamically allocated memory. When a `unique_ptr` goes out of scope, its destructor automatically returns the managed memory to the free store. In **Chapter 17**, we introduce `unique_ptr` and show how to use it to manage dynamically allocated objects or a dynamically allocated built-in arrays.

## 10.10 Case Study: `Array` Class

We discussed built-in arrays in **Chapter 8**. Pointer-based arrays have many problems, including:

- A program can easily “walk off” either end of a built-in array, because *C++ does not check whether subscripts fall outside the range of the array* (though you can still do this explicitly).
- Built-in arrays of size *n* must number their elements 0, …, *n* − 1; alternate subscript ranges are *not allowed*.
- An entire built-in array cannot be input or output at once; each element must be read or written individually (unless the array is a null-terminated C string).
- Two built-in arrays cannot be meaningfully compared with equality or relational operators (because the array names are simply pointers to where the arrays begin in memory and two arrays will always be at different memory locations).
- When a built-in array is passed to a general-purpose function designed to handle arrays of any size, the array’s *size* must be passed as an additional argument.
- One built-in array cannot be assigned to another with the assignment operator(s).

Class development is an interesting, creative and intellectually challenging activity—always with the goal of crafting valuable classes. With C++, you can implement more robust array capabilities via classes and operator overloading as has been done with class templates `array` and `vector` in the C++ Standard Library. In this section, we’ll develop our own custom array class that’s preferable to built-in arrays. When we refer to “arrays” in this case study, we mean built-in arrays.

In this example, we create a powerful `Array` class that performs range checking to ensure that subscripts remain within the bounds of the `Array`. The class allows one `Array` object to be assigned to another with the assignment operator. `Array` objects know their size, so the size does not need to be passed separately to functions that receive `Array` parameters. Entire `Array`s can be input or output with the stream extraction and stream insertion operators, respectively. You can compare `Array`s with the equality operators `==` and `!=`.

As a new C++ programmer, you’re likely to encounter C++ legacy code that uses older C++ features and techniques. Though current C++ compilers fully support using smart pointers to simplify dynamic memory management, we explicitly manage class `Array`’s dynamic memory using built-in pointers and operators `new` and `delete` to help you understand, maintain and modify the code you’ll see in industry.

### 10.10.1 Using the `Array` Class

The program of **Figs. 10.9–10.11** demonstrates class `Array` and its overloaded operators. First we walk through `main` (**Fig. 10.9**) and the program’s output, then we consider the class definition (**Fig. 10.10**) and each of its member-function definitions (**Fig. 10.11**).

```cpp
// Fig. 10.9: fig10_09.cpp
// Array class test program.
#include <iostream>
#include <stdexcept>
#include "Array.h"
using namespace std;

int main() {
   Array integers1{7}; // seven-element Array
   Array integers2; // 10-element Array by default

   // print integers1 size and contents
   cout << "Size of Array integers1 is " << integers1.getSize()
      << "\nArray after initialization: " << integers1;

   // print integers2 size and contents
   cout << "\nSize of Array integers2 is " << integers2.getSize()
      << "\nArray after initialization: " << integers2;

   // input and print integers1 and integers2
   cout << "\nEnter 17 integers: " << endl;
   cin >> integers1 >> integers2;

   cout << "\nAfter input, the Arrays contain:\n"
      << "integers1: " << integers1
      << "integers2: " << integers2;

   // use overloaded inequality (!=) operator
   cout << "\nEvaluating: integers1 != integers2" << endl;

   if (integers1 != integers2) {
      cout << "integers1 and integers2 are not equal" << endl;
   }

   // create Array integers3 using integers1 as an
   // initializer; print size and contents
   Array integers3{integers1}; // invokes copy constructor

   cout << "\nSize of Array integers3 is " << integers3.getSize()
      << "\nArray after initialization: " << integers3;

   // use overloaded assignment (=) operator
   cout << "\nAssigning integers2 to integers1: " << endl;
   integers1 = integers2; // note target Array is smaller

   cout << "integers1: " << integers1 << "integers2: " << integers2;

   // use overloaded equality (==) operator
   cout << "\nEvaluating: integers1 == integers2" << endl;

   if (integers1 == integers2) {
      cout << "integers1 and integers2 are equal" << endl;
   }

   // use overloaded subscript operator to create rvalue
   cout << "\nintegers1[5] is " << integers1[5];

   // use overloaded subscript operator to create lvalue
   cout << "\nAssigning 1000 to integers1[5]" << endl;
   integers1[5] = 1000;
   cout << "integers1: " << integers1;

   // attempt to use out-of-range subscript
   try {
      cout << "\nAttempt to assign 1000 to integers1[15]" << endl;
      integers1[15] = 1000; // ERROR: subscript out of range
   }
   catch (out_of_range& ex) {
      cout << "An exception occurred: " << ex.what() << endl;
   }
}
```

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1378_0.png)

Fig. 10.9 **Array** class test program.

### Creating *Arrays*, Outputting Their Size and Displaying Their Contents

The program begins by instantiating two objects of class `Array`—`integers1` (Fig. 10.9, line 9) with seven elements, and `integers2` (line 10) with the default `Array` size—10 elements (specified by the `Array` default constructor’s prototype in **Fig. 10.10**, line 13). Lines 13–14 in **Fig. 10.9** use member function `getSize` to determine the size of `integers1`, then output `integers1`’s contents, using the `Array` overloaded stream insertion operator. The sample output confirms that the `Array` elements were set correctly to zeros by the constructor. Next, lines 17–18 output the size of `Array` `integers2`, then output `integers2`’s contents, using the `Array` overloaded stream insertion operator.

### Using the Overloaded Stream Extraction Operator to Fill an `Array`

Line 21 prompts the user to input 17 integers. Line 22 uses the `Array` overloaded stream extraction operator to read the first seven values into `integers1` and the remaining 10 values into `integers2`. Lines 24–26 output the two arrays with the overloaded `Array` stream insertion operator to confirm that the input was performed correctly.

### Using the Overloaded Inequality Operator

Line 31 tests the overloaded inequality operator by evaluating the condition

```cpp
integers1 != integers2
```


A unary operator such as ! may be overloaded as a global function with one parameter in two different ways—either with a parameter that is an object (this requires a copy of the object, so the side effects of the function are not applied to the original object), or with a parameter that is a reference to an object (no copy of the original object is made, so all side effects of this function are applied to the original object). If s is a String class object (or a reference to a String class object), then !s is treated as if the call operator!(s) had been written, invoking the global operator! function that is declared as follows:

```cpp
bool operator!( const String & );
```

## 11.7 Overloading Binary Operators

A binary operator can be overloaded as a non-static member function with one parameter or as a global function with two parameters (one of those parameters must be either a class object or a reference to a class object).

Later in this chapter, we’ll overload < to compare two String objects. When overloading binary operator < as a non-static member function of a String class with one argument, if y and z are String-class objects, then y < z is treated as if y.operator<(z) had been written, invoking the operator< member function declared below

```cpp
class String
{
public:
    bool operator<( const String & ) const;

}; // end class String
```

As a global function, binary operator < must take two arguments—one of which must be an object (or a reference to an object) of the class. If y and z are String-class objects or references to String-class objects, then y < z is treated as if the call operator<(y, z) had been written in the program, invoking global-function operator< declared as follows:

```cpp
bool operator<( const String &, const String & );
```

## 11.8 Dynamic Memory Management

A standard C++ array data structure is fixed in size once it’s created. The size is specified with a constant at compile time. Sometimes it’s useful to determine the size of an array dynamically at execution time and then create the array. C++ enables you to control the allocation and deallocation of memory in a program for objects and for arrays of any built-in or user-defined type. This is known as dynamic memory management and is performed with the operators new and delete.

You can use the new operator to dynamically allocate (i.e., reserve) the exact amount of memory required to hold an object or array at execution time. The object or array is created in the free store (also called the heap)—a region of memory assigned to each program for storing dynamically allocated objects. Once memory is allocated in the free store, you can access it via the pointer that operator new returns. When you no longer need the memory, you can return it to the free store by using the delete operator to deallocate (i.e., release) the memory, which can then be reused by future new operations.

(e.g., chars are initialized to the null character, `'\0'`). Although an array name is a pointer to the array’s first element, the following is not allowed for dynamically allocated memory:

```cpp
int gradesArray[] = new int[ 10 ];
```

### Releasing Dynamically Allocated Arrays with `delete []`

To deallocate the memory to which gradesArray points, use the statement

```cpp
delete [] gradesArray;
```

If the pointer points to an array of objects, the statement first calls the destructor for every object in the array, then deallocates the memory. If the preceding statement did not include the square brackets ([]) and gradesArray pointed to an array of objects, the result is undefined. Some compilers call the destructor only for the first object in the array. Using delete on a null pointer (i.e., a pointer with the value 0) has no effect.

> **Common Programming Error 11.6**
> 
> *Using `delete` instead of `delete []` for arrays of objects can lead to runtime logic errors. To ensure that every object in the array receives a destructor call, always delete memory allocated as an array with operator `delete []`. Similarly, always delete memory allocated as an individual element with operator `delete`—the result of deleting a single object with operator `delete []` is undefined.*

## 11.9 Case Study: Array Class

We discussed arrays in Chapter 7. An array is not much more than a pointer to some space in memory. Pointer-based arrays have many problems, including:

- A program can easily “walk off” either end of an array, because C++ does not check whether subscripts fall outside the range of an array (though you can still do this explicitly).
- Arrays of size *n* must number their elements 0, …, *n* – 1; alternate subscript ranges are not allowed.
- An entire array cannot be input or output at once; each array element must be read or written individually (unless the array is a null-terminated C string).
- Two arrays cannot be meaningfully compared with equality or relational operators (because the array names are simply pointers to where the arrays begin in memory and two arrays will always be at different memory locations).
- When an array is passed to a general-purpose function designed to handle arrays of any size, the array’s size must be passed as an additional argument.
- One array cannot be assigned to another with the assignment operator(s) (because array names are const pointers and a *constant* pointer cannot be used on the left side of an assignment operator).

C++ provides the means to implement more robust array capabilities via classes and operator overloading. You can develop an array class that is preferable to “raw” arrays. In this example, we create a powerful `Array` class that performs range checking to ensure that subscripts remain within the bounds of the `Array`. The class allows one array object to be assigned to another with the assignment operator. Array objects know their size, so the size does not need to be passed separately to functions that receive Array parameters. Entire Arrays can be input or output with the stream extraction and stream insertion operators, respectively. You can compare Arrays with the equality operators == and !=. Recall that C++ Standard Library class template vector (introduced in Chapter 7) provides many of these capabilities as well. Chapter 22 explains class template vector in detail.

This example will sharpen your appreciation of data abstraction. Class development is an interesting, creative and intellectually challenging activity—always with the goal of “crafting valuable classes.” The program of Figs. 11.6–11.8 demonstrates class Array and its overloaded operators. First we walk through main (Fig. 11.8), then we consider the class definition (Fig. 11.6) and each of its member-function definitions (Fig. 11.7).

```cpp
// Fig. 11.6: Array.h
// Array class definition with overloaded operators.
#ifndef ARRAY_H
#define ARRAY_H

#include <iostream>
using namespace std;

class Array
{
   friend ostream &operator<<( ostream &, const Array & );
   friend istream &operator>>( istream &, Array & );
public:
   Array( int = 10 ); // default constructor
   Array( const Array & ); // copy constructor
   ~Array(); // destructor
   int getSize() const; // return size

   const Array &operator=( const Array & ); // assignment operator
   bool operator==( const Array & ) const; // equality operator

   // inequality operator; returns opposite of == operator
   bool operator!=( const Array &right ) const
   {
      return !( *this == right ); // invokes Array::operator==
   } // end function operator!=

   // subscript operator for non-const objects returns modifiable lvalue
   int &operator[]( int );

   // subscript operator for const objects returns rvalue
   int operator[]( int ) const;
private:
   int size; // pointer-based array size
   int *ptr; // pointer to first element of pointer-based array
}; // end class Array

#endif
```

Fig. 11.6  |  Array class definition with overloaded operators.

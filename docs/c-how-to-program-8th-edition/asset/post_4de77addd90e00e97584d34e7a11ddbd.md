
### *Initializing a New Array with a Copy of an Existing Array’s Contents*

Line 38 instantiates a third Array called integers3 and initializes it with a copy of Array integers1. This invokes class Array’s copy constructor to copy the elements of integers1 into integers3. We discuss the details of the copy constructor shortly. The copy constructor can also be invoked by writing line 38 as follows:

```
Array integers3 = integers1;
```

The equal sign in the preceding statement is *not* the assignment operator. When an equal sign appears in the declaration of an object, it invokes a constructor for that object. This form can be used to specify a single argument to a constructor—specifically, the value on the right side of the = symbol.

Lines 40–42 output the size of integers3 then output integers3’s contents, using the Array overloaded stream insertion operator to confirm that integers3’s elements were set correctly by the copy constructor.

### *Using the Overloaded Assignment Operator*

Line 46 tests the overloaded assignment operator (=) by assigning integers2 to integers1. Lines 48–49 display both Array objects’ contents to confirm that the assignment was successful. integers1 originally held 7 integers, but was resized to hold a copy of the 10 elements in integers2. As we’ll see, the overloaded assignment operator performs this resizing operation in a manner that’s transparent to the client code.

### *Using the Overloaded Equality Operator*

Line 54 uses the overloaded equality operator (==) to confirm that objects integers1 and integers2 are indeed identical after the assignment in line 46.

### *Using the Overloaded Subscript Operator*

Line 58 uses the overloaded subscript operator to refer to integers1[5]—an in-range element of integers1. This subscript name is used as an *rvalue* to print the value stored in integers1[5]. Line 62 uses integers1[5] as a modifiable *lvalue* on the left side of an assignment statement to assign a new value, 1000, to element 5 of integers1. We’ll see that operator[] returns a reference to use as the modifiable *lvalue* after the operator confirms that 5 is a valid subscript for integers1.

Line 69 attempts to assign the value 1000 to integers1[15]—an *out-of-range* element. In this example, operator[] determines that the subscript is out of range and throws an out_of_range exception.

Interestingly, the *array subscript operator []* is not restricted for use only with arrays; it also can be used, for example, to select elements from other kinds of *container* classes, such as linked lists, strings and dictionaries. Also, when overloaded operator[] functions are defined, *subscripts no longer have to be integers*—characters, strings or even objects of user-defined classes also could be used. In Chapter 22, we discuss the STL map class that allows string subscripts.

## 11.10.2 Array Class Definition

Now that we’ve seen how this program operates, let’s walk through the class header (Fig. 11.10). As we refer to each member function in the header, we discuss that function’s implementation in Fig. 11.11. In Fig. 11.10, lines 34–35 represent the private data members of class Array. Each Array object consists of a size member indicating the number of elements in the Array and an int pointer—that points to the dynamically allocated pointer-based array of integers managed by the Array object.

Fig. 11.10 | Array class definition with overloaded operators.

```cpp
// Fig. 11.10: Array.h
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
   Array( int = 10 );                 // default constructor
   Array( const Array & );             // copy constructor
   ~Array();                           // destructor
   int getSize() const;                // return size

   const Array operator=( const Array & ); // assignment operator
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

Fig. 11.11 | Array class member- and friend-function definitions. (Part 1 of 4.)

```cpp
// Fig 11.11: Array.cpp
// Array class member- and friend-function definitions.
#include <iostream>
#include <iomanip>
#include <cstdlib> // exit function prototype
#include "Array.h" // Array class definition

using namespace std;

// default constructor for class Array (default size 10)
Array::Array( int arraySize )
{
   // validate arraySize
   if ( arraySize > 0 )
      size = arraySize;
   else
      throw invalid_argument( "Array size must be greater than 0" );

   ptr = new int[ size ]; // create space for pointer-based array

   for ( int i = 0; i < size; ++i )
      ptr[ i ] = 0; // set each pointer-based array element
} // end Array default constructor

// copy constructor for class Array;
// must receive a reference to prevent infinite recursion
Array::Array( const Array &arrayToCopy )
   : size( arrayToCopy.size )
{
   ptr = new int[ size ]; // create space for pointer-based array

   for ( int i = 0; i < size; ++i )
      ptr[ i ] = arrayToCopy.ptr[ i ]; // copy into object
} // end Array copy constructor

// destructor for class Array
Array::~Array()
{
   delete [] ptr; // release pointer-based array space
} // end destructor

// return number of elements of Array
int Array::getSize() const
{
   return size; // number of elements in Array
} // end function getSize

// overloaded assignment operator;
// const return avoids: ( a1 = a2 ) = a3
const Array& Array::operator=( const Array &right )
{
   if ( &right != this ) // avoid self-assignment
   {
      // for Arrays of different sizes, deallocate original
      // left-side array, then allocate new left-side array
      if ( size != right.size )
      {
         delete [] ptr; // release space
         size = right.size; // resize this object
```

Fig. 11.11 | Array class member- and friend-function definitions. (Part 2 of 4.)

Class Array’s default constructor to set the size of the Array to 10 elements. The default constructor (defined in Fig. 11.1, lines 10–22) validates and assigns the argument to data member size, uses new to obtain the memory for the internal pointer-based representation of this array and assigns the pointer returned by new to data member ptr. Then the constructor uses a for statement to set all the elements of the array to zero. It’s possible to have an Array class that does not initialize its members if, for example, these members are to be read at some later time; but this is considered to be a poor programming practice. Arrays, and objects in general, should be properly initialized as they’re created.

### Array Copy Constructor

Line 15 of Fig. 11.10 declares a copy constructor (defined in Fig. 11.11, lines 26–33) that initializes an Array by making a copy of an existing Array object. Such copying must be done carefully to avoid the pitfall of leaving both Array objects pointing to the same dynamically allocated memory. This is exactly the problem that would occur with default memberwise copying, if the compiler is allowed to define a default copy constructor for this class. Copy constructors are invoked whenever a copy of an object is needed, such as in

- passing an object by value to a function
- returning an object by value from a function
- initializing an object with a copy of another object of the same class.

The copy constructor is called in a declaration when an object of class Array is instantiated and initialized with another object of class Array, as in the declaration in line 38 of Fig. 11.9.

The copy constructor for Array uses a member initializer (Fig. 11.11, line 27) to copy the size of the initializer Array into data member size using new (line 29) to obtain the memory for the internal pointer-based representation of this Array and assigns the pointer returned by new to data member ptr.¹ Then the copy constructor uses a for statement to copy all the elements of the initializer Array into the new Array object. An object of a class can look at the private data of any other object of that class (using a handle that indicates which object to access).

> **Software Engineering Observation 11.2**
> 
> The argument to a copy constructor should be a const reference to allow a const object to be copied.

![](img/bfd978e7e9b192bab46ec2a89e481263_513_0.png)

> **Common Programming Error 11.3**
> 
> A copy constructor must receive its argument by reference, not by value. Otherwise, the copy constructor call results in infinite recursion (a fatal logic error) because receiving an object by value requires the copy constructor to make a copy of the argument object. Recall that any time a copy of an object is required, the class’s copy constructor is called. If the copy constructor received its argument by value, the copy constructor would call itself recursively to make a copy of its argument.

![](img/bfd978e7e9b192bab46ec2a89e481263_513_1.png)

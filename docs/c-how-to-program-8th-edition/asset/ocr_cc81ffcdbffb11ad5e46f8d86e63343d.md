Members of class Array. Each Array object consists of a size member indicating the number of elements in the Array and an int pointer—that points to the dynamically allocated pointer-based array of integers managed by the Array object.

```
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
```

# Fig. 11.10 | Array class definition with overloaded operators.

```
```cpp
// Fig 11.11: Array.cpp
// Array class member- and friend-function definitions.
#include <iostream>
#include <iomanip>
#include <cstdlib> // exit function prototype
#include "Array.h" // Array class definition
```
```

# Fig. 11.11 | Array class member- and friend-function definitions. (Part 1 of 4.)
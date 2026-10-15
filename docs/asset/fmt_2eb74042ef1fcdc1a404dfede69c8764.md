
### Member function definitions of class Integer

```cpp
Integer::Integer( int i )
    : value( i )
{
    cout << "Constructor for Integer " << value << endl;
} // end Integer constructor
```

```cpp
// Integer destructor
Integer::~Integer()
{
    cout << "Destructor for Integer " << value << endl;
} // end Integer destructor
```

```cpp
// set Integer value
void Integer::setInteger( int i )
{
    value = i;
} // end function setInteger
```

```cpp
// return Integer value
int Integer::getInteger() const
{
    return value;
} // end function getInteger
```

Fig. 16.9 | Member function definitions of class Integer.

Line 18 of Fig. 16.10 creates `auto_ptr` object `ptrToInteger` and initializes it with a pointer to a dynamically allocated `Integer` object that contains the value 7. Line 21 uses the `auto_ptr` overloaded `->` operator to invoke function `setInteger` on the `Integer` object that `ptrToInteger` manages. Line 24 uses the `auto_ptr` overloaded `*` operator to dereference `ptrToInteger`, then uses the dot (`.`) operator to invoke function `getInteger` on the `Integer` object. Like a regular pointer, an `auto_ptr`’s `->` and `*` overloaded operators can be used to access the object to which the `auto_ptr` points.

Because `ptrToInteger` is a local automatic variable in `main`, `ptrToInteger` is destroyed when `main` terminates. The `auto_ptr` destructor forces a `delete` of the `Integer` object pointed to by `ptrToInteger`, which in turn calls the `Integer` class destructor. The memory that `Integer` occupies is released, regardless of how control leaves the block (e.g., by a `return` statement or by an exception). Most importantly, using this technique can prevent memory leaks. For example, suppose a function returns a pointer aimed at some object. Unfortunately, the function caller that receives this pointer might not `delete` the object, thus resulting in a memory leak. However, if the function returns an `auto_ptr` to

```cpp
// Fig. 16.10: Fig16_10.cpp
// Demonstrating auto_ptr.
#include <iostream>
using std::cout;
using std::endl;

#include <memory>
using std::auto_ptr; // auto_ptr class definition

#include "Integer.h"

// use auto_ptr to manipulate Integer object
int main()
{
    cout << "Creating an auto_ptr object that points to an Integer\n";

    // "aim" auto_ptr at Integer object
    auto_ptr< Integer > ptrToInteger( new Integer( 7 ) );

    cout << "\nUsing the auto_ptr to manipulate the Integer\n";
    ptrToInteger->setInteger( 99 ); // use auto_ptr to set Integer value

    // use auto_ptr to get Integer value
    cout << "Integer after setInteger: " << ( *ptrToInteger ).getInteger()
    return 0;
} // end main
```

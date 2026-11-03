```
public:
    Integer( int i = 0 ); // Integer default constructor
    ~Integer(); // Integer destructor
    void setInteger( int i ); // set Integer value
    int getInteger() const; // return Integer value
private:
    int value;
}; // end class Integer
```

Fig. 22.7 | Integer class definition. (Part 2 of 2.)

```
// Fig. 22.8: Integer.cpp
// Integer member function definitions.
#include <iostream>
#include "Integer.h"
using namespace std;

// Integer default constructor
Integer::Integer( int i )
: value( i )
{
    cout << "Constructor for Integer " << value << endl;
} // end Integer constructor

// Integer destructor
Integer::~Integer()
{
    cout << "Destructor for Integer " << value << endl;
} // end Integer destructor

// set Integer value
void Integer::setInteger( int i )
{
    value = i;
} // end function setInteger

// return Integer value
int Integer::getInteger() const
{
    return value;
} // end function getInteger
```

Fig. 22.8 | Member function definitions of class Integer.

Line 15 of Fig. 22.9 creates unique_ptr object ptrToInteger and initializes it with a pointer to a dynamically allocated Integer object that contains the value 7. Line 18 uses the unique_ptr overloaded -> operator to invoke function setInteger on the Integer object that ptrToInteger manages. Line 21 uses the unique_ptr overloaded * operator to dereference ptrToInteger, then uses the dot (.) operator to invoke function getInteger on the Integer object. Like a regular pointer, a unique_ptr’s -> and * overloaded operators can be used to access the object to which the unique_ptr points.
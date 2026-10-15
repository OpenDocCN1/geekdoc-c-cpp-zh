just as a regular pointer variable is. Figure 16.10 demonstrates an auto_ptr object that points to a dynamically allocated object of class Integer (Figs. 16.8–16.9).

```
// Fig. 16.8: Integer.h
// Integer class definition.
class Integer
{
public:
    Integer( int i = 0 ); // Integer default constructor
    ~Integer(); // Integer destructor
    void setInteger( int i ); // functions to set Integer
    int getInteger() const; // function to return Integer
private:
    int value;
}; // end class Integer
```

Fig. 16.8 | Integer class definition.

```
// Fig. 16.9: Integer.cpp
// Integer member function definitions.
#include <iostream>
using std::cout;
using std::endl;

#include "Integer.h"

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

Fig. 16.9 | Member function definitions of class Integer.
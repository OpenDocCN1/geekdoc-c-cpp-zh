```
```cpp
// Fig. 10.26: Interface.cpp
// Implementation of class Interface--client receives this file only
// as precompiled object code, keeping the implementation hidden.
#include "Interface.h" // Interface class definition
#include "Implementation.h" // Implementation class definition

// constructor
Interface::Interface( int v )
    : ptr ( new Implementation( v ) ) // initialize ptr to point to
                                      // a new Implementation object
{   // empty body
} // end Interface constructor

// call Implementation's setValue function
void Interface::setValue( int v )
{
    ptr->setValue( v );
} // end function setValue

// call Implementation's getValue function
int Interface::getValue() const
{
    return ptr->getValue();
} // end function getValue

// destructor
Interface::~Interface()
{
    delete ptr;
} // end ~Interface destructor
```
```

**Fig. 10.26** | Interface class member-function definitions.

# Software Engineering Observation 10.14

> A proxy class insulates client code from implementation changes.

```
```cpp
// Fig. 10.27: fig10_27.cpp
// Hiding a class’s private data with a proxy class.
#include <iostream>
using std::cout;
using std::endl;

#include "Interface.h" // Interface class definition

int main()
{
    Interface i( 5 ); // create Interface object

    cout << "Interface contains: " << i.getValue()
         << " before setValue" << endl;
```
```

**Fig. 10.27** | Implementing a proxy class. (Part 1 of 2.)
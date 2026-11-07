# **Program 12.36**  File ta.h (Continued)

```
```cpp
#ifndef TA_H
#define TA_H
#include "person.h"
#include "stdtype.h"
#include "prftype.h"

class TA: public Person, public StdType, public PrfType
{
public:
    TA (string name, double gpa, double salary);
    void printGPA ();
    void printSalary();
    void print ();
};
#endif
```
```

Program 12.37 shows the implementation file for the Person class. Program 12.38 shows the implementation file for the Student class. Note that it inherits the gpa data member as a protected data member from the StdType class. This data member is accessible in the Student class but cannot be initialized in this class. We must assign a value to it in the constructor.

# **Program 12.37**  File person.cpp

```
```cpp
/***************************************************************
 * The implementation file for Person concrete class            *
 ***************************************************************/
#include "person.h"

// Constructor
Person :: Person (string nm)
: name(nm)
{
}
// Print member function
void Person :: print ( )
{
    cout << "Name: " << name << endl;
}
```
```

# **Program 12.38**  File student.cpp

```
```cpp
/***************************************************************
 * The implementation file for Student concrete class           *
 ***************************************************************/
```
```
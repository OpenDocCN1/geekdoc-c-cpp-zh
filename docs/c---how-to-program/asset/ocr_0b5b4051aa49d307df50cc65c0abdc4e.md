# 17.9 Default Memberwise Assignment

The assignment operator (=) can be used to assign an object of the same class. By default, such assignment is performed by memberwise assignment (also called copy assignment)—each data member of the object on the right of the assignment operator is assigned individually to the same data member in the object on the left of the assignment operator. Figures 17.13–17.14 define a Date class. Line 18 of Fig. 17.15 uses default memberwise assignment to assign the data members of Date object date1 to the corresponding data members of Date object date2. In this case, the month member of date1 is assigned to the month member of date2, the day member of date1 is assigned to the day member of date2 and the year member of date1 is assigned to the year member of date2. [Caution: Memberwise assignment can cause serious problems when used with a class whose data members contain pointers to dynamically allocated memory; we discuss these problems in Chapter 18 and show how to deal with them.]

```
// Fig. 17.13: Date.h
// Date class declaration. Member functions are defined in Date.cpp.

// prevent multiple inclusions of header
#ifndef DATE_H
#define DATE_H

// class Date definition
class Date
{
public:
    explicit Date( int = 1, int = 1, int = 2000 ); // default constructor
    void print();
private:
    unsigned int month;
    unsigned int day;
    unsigned int year;
}; // end class Date

#endif
```

Fig. 17.13 | Date class declaration.

```
// Fig. 17.14: Date.cpp
// Date class member-function definitions.
#include <iostream>
#include "Date.h" // include definition of class Date from Date.h
using namespace std;

// Date constructor (should do range checking)
Date::Date( int m, int d, int y )
    : month( m ), day( d ), year( y )
{
} // end constructor Date
```

Fig. 17.14 | Date class member-function definitions. (Part I of 2.)
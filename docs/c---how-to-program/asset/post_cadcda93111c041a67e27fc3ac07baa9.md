
```cpp
// Fig. 17.11: Time.cpp
// Time class member-function definitions.
#include <stdexcept>
#include "Time.h" // include definition of class Time
using namespace std;

// constructor function to initialize private data; calls member function
// setTime to set variables; default values are 0 (see class definition)
Time::Time( int hr, int min, int sec )
{
    setTime( hr, min, sec );
} // end Time constructor

// set values of hour, minute and second
void Time::setTime( int h, int m, int s )
{
    // validate hour, minute and second
    if ( ( h >= 0 && h < 24 ) && ( m >= 0 && m < 60 ) &&
         ( s >= 0 && s < 60 ) )
    {
        hour = h;
        minute = m;
        second = s;
    } // end if
    else
        throw invalid_argument(
            "hour, minute and/or second was out of range" );
} // end function setTime

// return hour value
unsigned int Time::getHour()
{
    return hour;
} // end function getHour

// poor practice: returning a reference to a private data member.
unsigned int &Time::badSetHour( int hh )
{
    if ( hh >= 0 && hh < 24 )
        hour = hh;
    else
        throw invalid_argument( "hour must be 0-23" );

    return hour; // dangerous reference return
} // end function badSetHour
```

Fig. 17.11 | Time class member-function definitions.

Figure 17.12 declares Time object t (line 10) and reference hourRef (line 13), which is initialized with the reference returned by the call t.badSetHour(20). Line 15 displays the value of the alias hourRef. This shows how hourRef breaks the encapsulation of the class—statements in main should not have access to the private data of the class. Next, line 16 uses the alias to set the value of hour to 30 (an invalid value) and line 17 displays the value returned by function getHour to show that assigning a value to hourRef actually modifies the private data in the Time object t. Finally, line 21 uses the badSetHour function call itself as an *lvalue* and assigns 74 (another invalid value) to the reference returned by the function. Line 26 again displays the value returned by function getHour to show that assigning a value to the result of the function call in line 21 modifies the private data in the Time object t.

![](img/d0d3b7423c2d9e5650be79209ea1885d_681_0.png)

### Software Engineering Observation 17.7

> Returning a reference or a pointer to a private data member breaks the encapsulation of the class and makes the client code dependent on the representation of the class’s data. There are cases where doing this is appropriate—we’ll show an example of this when we build our customer class in Section 18.10.

```cpp
// Fig. 17.12: fig17_12.cpp
// Demonstrating a public member function that
// returns a reference to a private data member.
#include <iostream>
#include "Time.h" // include definition of class Time
using namespace std;

int main()
{
   Time t; // create Time object

   // initialize hourRef with the reference returned by badSetHour
   int &hourRef = t.badSetHour( 20 ); // 20 is a valid hour

   cout << "Valid hour before modification: " << hourRef;
   hourRef = 30; // use hourRef to set value in Time object t
   cout << "\nInvalid hour after modification: " << t.getHour();

   // Dangerous: Function call that returns
   // a reference can be used as an lvalue!
   t.badSetHour( 12 ) = 74; // assign another invalid value to hour

   cout << "\n\n**********************************************\n"
        << "POOR PROGRAMMING PRACTICE!!!!!!!!!!\n"
        << "t.badSetHour( 12 ) as an lvalue, invalid hour: "
        << t.getHour()
        << "\n**********************************************" << endl;
} // end main
```

Valid hour before modification: 20
Invalid hour after modification: 30

**************************************************
POOR PROGRAMMING PRACTICE!!!!!!!!!!
t.badSetHour( 12 ) as an lvalue, invalid hour: 74
**************************************************

**Fig. 17.12** — public member function that returns a reference to a private data member.

## 17.9 Default Memberwise Assignment

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

~~~cpp
12
13 // print Date in the format mm/dd/yyyy
14 void Date::print()
15 {
16     cout << month << '/' << day << '/' << year;
17 } // end function print
~~~

**Fig. 17.14** | Date class member-function definitions. (Part 2 of 2.)

~~~cpp
1 // Fig. 17.15: fig17_15.cpp
2 // Demonstrating that class objects can be assigned
3 // to each other using default memberwise assignment.
4 #include <iostream>
5 #include "Date.h" // include definition of class Date from Date.h
6 using namespace std;
7
8 int main()
9 {
10    Date date1( 7, 4, 2004 );
11    Date date2; // date2 defaults to 1/1/2000
12
13    cout << "date1 = ";
14    date1.print();
15    cout << "\ndate2 = ";
16    date2.print();
17
18    date2 = date1; // default memberwise assignment
19
20    cout << "\n\nAfter default memberwise assignment, date2 = ";
21    date2.print();
22    cout << endl;
23 } // end main
~~~

~~~
date1 = 7/4/2004
date2 = 1/1/2000

After default memberwise assignment, date2 = 7/4/2004
~~~

**Fig. 17.15** | Class objects can be assigned to each other using default memberwise assignment.

Objects may be passed as function arguments and may be returned from functions. Such passing and returning is performed using pass-by-value by default—a copy of the object is passed or returned. In such cases, C++ creates a new object and uses a copy constructor to copy the original object's values into the new object. For each class, the compiler provides a default copy constructor that copies each member of the original object into the corresponding member of the new object. Like memberwise assignment, copy constructors can cause serious problems when used with a class whose data members contain pointers to dynamically allocated memory. Chapter 18 discusses how to define customized copy constructors that properly copy objects containing pointers to dynamically allocated memory.

Line 20 in Fig. 17.16 generates a compilation error even though member function `printStandard` of class `Time` *does not* modify the object on which it’s invoked. The fact that a member function does not modify an object is *not* sufficient—the function must explicitly be declared `const`.

## 17.11 Composition: Objects as Members of Classes

An AlarmClock object needs to know when it’s supposed to sound its alarm, so why not include a Time object as a member of the AlarmClock class? Such a capability is called composition and is sometimes referred to as a *has-a relationship*—a class can have objects of other classes as members.

> **Software Engineering Observation 17.9**
> 
> *A common form of software reusability is composition, in which a class has objects of other types as members.*

![](img/d0d3b7423c2d9e5650be79209ea1885d_686_0.png)

Previously, we saw how to pass arguments to the constructor of an object we created in `main`. Now we show how a class constructor can pass arguments to member-object constructors via member initializers.

> **Software Engineering Observation 17.10**
> 
> *Data members are constructed in the order in which they’re declared in the class definition (not in the order they’re listed in the constructor’s member initializer list) and before their enclosing class objects (sometimes called host objects) are constructed.*

![](img/d0d3b7423c2d9e5650be79209ea1885d_686_1.png)

The next program uses classes Date (Figs. 17.17–17.18) and Employee (Figs. 17.19–17.20) to demonstrate composition. Class Employee’s definition (Fig. 17.19) contains private data members firstName, lastName, birthDate and hireDate. Members birthDate and hireDate are const objects of class Date, which contains private data members month, day and year. The Employee constructor’s header (Fig. 17.20, lines 10–11) specifies that the constructor has four parameters (first, last, dateOfBirth and dateOfHire). The first two parameters are passed via member initializers to the string class constructor for the firstName and lastName data members. The last two are passed via member initializers to the Date class constructor for the birthDate and hireDate data members.

```cpp
// Fig. 17.17: Date.h
// Date class definition; Member functions defined in Date.cpp
#ifndef DATE_H
#define DATE_H

class Date
{
public:
   static const unsigned int monthsPerYear = 12; // months in a year
   explicit Date( int = 1, int = 1, int = 1900 ); // default constructor
   void print() const; // print date in month/day/year format
   ~Date(); // provided to confirm destructor order
};
```

**Fig. 17.17** | Date class definition. (Part 1 of 2.)

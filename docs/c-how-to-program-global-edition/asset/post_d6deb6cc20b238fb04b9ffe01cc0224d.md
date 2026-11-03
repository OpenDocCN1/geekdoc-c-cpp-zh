
```cpp
// Fig. 17.3: fig17_03.cpp
// Program to test class Time.
// NOTE: This file must be compiled with Time.cpp.
#include <iostream>
#include <stdexcept>  // for invalid_argument exception class
#include "Time.h"     // include definition of class Time from Time.h
using namespace std;

int main()
{
    Time t;  // instantiate object t of class Time

    // output Time object t's initial values
    cout << "The initial universal time is ";
    t.printUniversal();  // 00:00:00
    cout << "\nThe initial standard time is ";
    t.printStandard();   // 12:00:00 AM

    t.setTime( 13, 27, 6 );  // change time

    // output Time object t's new values
    cout << "\n\nUniversal time after setTime is ";
    t.printUniversal();  // 13:27:06
    cout << "\nStandard time after setTime is ";
    t.printStandard();   // 1:27:06 PM

    // attempt to set the time with invalid values
    try
    {
        t.setTime( 99, 99, 99 );  // all values out of range
    } // end try
    catch ( invalid_argument &e )
    {
        cout << "Exception: " << e.what() << endl;
    } // end catch

    // output t's values after specifying invalid values
    cout << "\n\nAfter attempting invalid settings:"
         << "\nUniversal time: ";
    t.printUniversal();  // 13:27:06
    cout << "\nStandard time: ";
    t.printStandard();   // 1:27:06 PM
    cout << endl;
} // end main
```

The initial universal time is 00:00:00
The initial standard time is 12:00:00 AM

Universal time after setTime is 13:27:06
Standard time after setTime is 1:27:06 PM

Exception: hour, minute and/or second was out of range

## Class Scope and Block Scope

Variables declared in a member function have block scope and are known only to that function. If a member function defines a variable with the same name as a variable with class scope, the class-scope variable is hidden in the function by the block-scope variable. Such a hidden variable can be accessed by preceding the variable name with the class name followed by the scope resolution operator (::). Hidden global variables can be accessed with the scope resolution operator, as in ::globalVariableName.

## Dot (.) and Arrow (->) Member Selection Operators

The dot member selection operator (.) is preceded by an object's name or with a reference to an object to access the object's members. The arrow member selection operator (->) is preceded by a pointer to an object to access the object's members.

## Accessing public Class Members Through Objects, References and Pointers

Consider an Account class that has a public setBalance member function. Given the following declarations:

```
Account account; // an Account object
// accountRef refers to an Account object
Account &accountRef = account;
// accountPtr points to an Account object
Account *accountPtr = &account;
```

You can invoke member function setBalance using the dot (.) and arrow (->) member selection operators as follows:

```
// call setBalance via the Account object
account.setBalance( 123.45 );

// call setBalance via a reference to the Account object
accountRef.setBalance( 123.45 );

// call setBalance via a pointer to the Account object
accountPtr->setBalance( 123.45 );
```

## 17.4 Access Functions and Utility Functions

### Access Functions

Access functions can read or display data. Another common use for access functions is to test the truth or falsity of conditions—such functions are often called predicate functions. An example of a predicate function would be an isEmpty function for any container class—a class capable of holding many objects, like a vector. A program might test isEmpty before attempting to read another item from the container object. An isFull predicate function might test a container-class object to determine whether it has no additional room. Useful predicate functions for our Time class might be isAM and isPM.

### Utility Functions

A utility function (also called a helper function) is a private member function that supports the operation of a class's other member functions. Utility functions are declared private because they're not intended for use by the class's clients. A common use of a utility function would be to place in a function some common code that would otherwise be duplicated in several other member functions.

## 17.5 Time Class Case Study: Constructors with Default Arguments

The program of Figs. 17.4–17.6 enhances class Time to demonstrate how arguments are implicitly passed to a constructor. The constructor defined in Fig. 17.2 initialized hour, minute and second to 0 (i.e., midnight in universal time). Like other functions, constructors can specify default arguments. Line 13 of Fig. 17.4 declares the Time constructor to include default arguments, specifying a default value of zero for each argument passed to the constructor. The constructor is declared explicit because it can be called with one argument. We discuss explicit constructors in Section 18.13.

~~~cpp
1  // Fig. 17.4: Time.h
2  // Time class containing a constructor with default arguments.
3  // Member functions defined in Time.cpp.
4
5  // prevent multiple inclusions of header
6  #ifndef TIME_H
7  #define TIME_H
8
9  // Time class definition
10 class Time
11 {
12 public:
13    explicit Time( int = 0, int = 0, int = 0 ); // default constructor
14
15    // set functions
16    void setTime( int, int, int ); // set hour, minute, second
17    void setHour( int ); // set hour (after validation)
18    void setMinute( int ); // set minute (after validation)
19    void setSecond( int ); // set second (after validation)
20
21    // get functions
22    unsigned int getHour() const; // return hour
23    unsigned int getMinute() const; // return minute
24    unsigned int getSecond() const; // return second
25
26    void printUniversal() const; // output time in universal-time format
27    void printStandard() const; // output time in standard-time format
28 private:
29    unsigned int hour; // 0 - 23 (24-hour clock format)
30    unsigned int minute; // 0 - 59
31    unsigned int second; // 0 - 59
32 }; // end class Time
33
34 #endif
~~~

Fig. 17.4 | Time Class containing a constructor with default arguments.

In Fig. 17.5, lines 10–13 define the new version of the Time constructor that receives values for parameters hour, minute and second that will be used to initialize private data members hour, minute and second, respectively. The default arguments to the constructor ensure that, even if no values are provided in a constructor call, the constructor still initializes the data members. A constructor that defaults all its arguments is also a default constructor—that is, a constructor that can be invoked with no arguments. There can be at most one default constructor per class. The version of class Time in this example provides set and get functions for each data member. The Time constructor now calls setTime, which calls the setHour, setMinute and setSecond functions to validate and assign values to the data members.

### Software Engineering Observation 17.5

![](img/bf54db922e6fa8319cba11069e785521_664_0.png)

> Any change to the default argument values of a function requires the client code to be recompiled (to ensure that the program still functions correctly).

```
// Fig. 17.5: Time.cpp
// Member-function definitions for class Time.
#include <iostream>
#include <iomanip>
#include <stdexcept>
#include "Time.h" // include definition of class Time from Time.h
using namespace std;

// Time constructor initializes each data member
Time::Time( int hour, int minute, int second )
{
    setTime( hour, minute, second ); // validate and set time
} // end Time constructor

// set new Time value using universal time
void Time::setTime( int h, int m, int s )
{
    setHour( h ); // set private field hour
    setMinute( m ); // set private field minute
    setSecond( s ); // set private field second
} // end function setTime

// set hour value
void Time::setHour( int h )
{
    if ( h >= 0 && h < 24 )
        hour = h;
    else
        throw invalid_argument( "hour must be 0-23" );
} // end function setHour

// set minute value
void Time::setMinute( int m )
{
    if ( m >= 0 && m < 60 )
        minute = m;
    else
        throw invalid_argument( "minute must be 0-59" );
} // end function setMinute
```


## 9.5 Time Class Case Study: Constructors with Default Arguments

The program of Figs. 9.4–9.6 enhances class Time to demonstrate how arguments are implicitly passed to a constructor. The constructor defined in Fig. 9.2 initialized hour, minute and second to 0 (i.e., midnight in universal time). Like other functions, constructors can specify *default arguments*. Line 13 of Fig. 9.4 declares the Time constructor to include default arguments, specifying a default value of zero for each argument passed to the constructor. The constructor is declared `explicit` because it can be called with one argument. We discuss explicit constructors in detail in Section 10.13.

```cpp
// Fig. 9.4: Time.h
// Time class containing a constructor with default arguments.
// Member functions defined in Time.cpp.

// prevent multiple inclusions of header
#ifndef TIME_H
#define TIME_H

// Time class definition
class Time
{
public:
   explicit Time( int = 0, int = 0, int = 0 ); // default constructor

   // set functions
   void setTime( int, int, int ); // set hour, minute, second
   void setHour( int ); // set hour (after validation)
   void setMinute( int ); // set minute (after validation)
   void setSecond( int ); // set second (after validation)

   // get functions
   unsigned int getHour() const; // return hour
   unsigned int getMinute() const; // return minute
   unsigned int getSecond() const; // return second

   void printUniversal() const; // output time in universal-time format
   void printStandard() const; // output time in standard-time format
private:
   unsigned int hour; // 0 - 23 (24-hour clock format)
   unsigned int minute; // 0 - 59
   unsigned int second; // 0 - 59
}; // end class Time

#endif
```

**Fig. 9.4** | Time class containing a constructor with default arguments.

In Fig. 9.5, lines 10–13 define the new version of the Time constructor that receives values for parameters hour, minute and second that will be used to initialize private data members hour, minute and second, respectively. The default arguments to the constructor ensure that, even if no values are provided in a constructor call, the constructor still initializes the data members. A constructor that defaults all its arguments is also a default constructor—that is, a constructor that can be invoked with no arguments. There can be at most one default constructor per class. The version of class Time in this example provides set and get functions for each data member. The Time constructor now calls setTime, which calls the setHour, setMinute and setSecond functions to validate and assign values to the data members.

> **Software Engineering Observation 9.5**
>
> *Any change to the default argument values of a function requires the client code to be recompiled (to ensure that the program still functions correctly).*

```cpp
// Fig. 9.5: Time.cpp
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

**Fig. 9.5** | Member-function definitions for class Time. (Part 1 of 2.)

```text
Constructed with:

t1: all arguments defaulted
  00:00:00
  12:00:00 AM

t2: hour specified; minute and second defaulted
  02:00:00
  2:00:00 AM

t3: hour and minute specified; second defaulted
  21:34:00
  9:34:00 PM

t4: hour, minute and second specified
  12:25:42
  12:25:42 PM

Exception while initializing t5: hour must be 0-23
```

**Fig. 9.6** | Constructor with default arguments. (Part 2 of 2.)

### Notes Regarding Class Time’s Set and Get Functions and Constructor

Time’s set and get functions are called throughout the class’s body. In particular, function setTime (lines 16–21 of Fig. 9.5) calls functions setHour, setMinute and setSecond, and functions printUniversal and printStandard call functions getHour, getMinute and getSecond in lines 71–72 and lines 78–80. In each case, these functions could have accessed the class’s private data directly. However, consider changing the representation of the time from three int values (requiring 12 bytes of memory on systems with four-byte ints) to a single int value representing the total number of seconds that have elapsed since midnight (requiring only four bytes of memory). If we made such a change, only the bodies of the functions that access the private data directly would need to change—in particular, the individual set and get functions for the hour, minute and second. There would be no need to modify the bodies of functions setTime, printUniversal or printStandard, because they do not access the data directly. Designing the class in this manner reduces the likelihood of programming errors when altering the class’s implementation.

Similarly, the Time constructor could be written to include a copy of the appropriate statements from function setTime. Doing so may be slightly more efficient, because the extra call to setTime is eliminated. However, duplicating statements in multiple functions or constructors makes changing the class’s internal data representation more difficult. Having the Time constructor call setTime and having setTime call setHour, setMinute and setSecond enables us to limit the changes to code that validates the hour, minute or second to the corresponding set function. This reduces the likelihood of errors when altering the class’s implementation.

![](img/b42ba5cd262b1358d16610173f975e4d_426_0.png)

> **Software Engineering Observation 9.6**
>
> If a member function of a class already provides all or part of the functionality required by a constructor (or other member function) of the class, call that member function from the constructor (or other member function). This simplifies the maintenance of the code and reduces the likelihood of an error if the implementation of the code is modified. As a general rule: Avoid repeating code.

```cpp
Time::Time( int hour )
    : Time( hour, 0, 0 ) // delegate to Time( int, int, int )
{
} // end constructor with one argument
Time::Time( int hour, int minute )
    : Time( hour, minute, 0 ) // delegate to Time( int, int, int )
{
} // end constructor with two arguments
```

## 9.6 Destructors

A **destructor** is another type of special member function. The name of the destructor for a class is the **tilde character (~)** followed by the class name. This naming convention has intuitive appeal, because as we’ll see in a later chapter, the tilde operator is the bitwise complement operator, and, in a sense, the destructor is the complement of the constructor. A destructor may not specify parameters or a return type.

A class’s destructor is called *implicitly* when an object is destroyed. This occurs, for example, as an object is destroyed when program execution leaves the scope in which that object was instantiated. *The destructor itself does not actually release the object’s memory*—it performs **termination housekeeping** before the object’s memory is reclaimed, so the memory may be reused to hold new objects.

Even though destructors have not been defined for the classes presented so far, *every class has one destructor*. If you do not *explicitly* define a destructor, the compiler defines an “empty” destructor. [*Note: We’ll see that such an implicitly created destructor does, in fact, perform important operations on class-type objects that are created through composition* (Section 9.11) *and inheritance* (Chapter 11).] In Chapter 10, we’ll build destructors appropriate for classes whose objects contain dynamically allocated memory (e.g., for arrays and strings) or use other system resources (e.g., files on disk, which we study in Chapter 14). We discuss how to dynamically allocate and deallocate memory in Chapter 10.

## 9.7 When Constructors and Destructors Are Called

Constructors and destructors are called *implicitly* by the compiler. The order in which these function calls occur depends on the order in which execution enters and leaves the scopes where the objects are instantiated. Generally, destructor calls are made in the *reverse order* of the corresponding constructor calls, but as we’ll see in Figs. 9.7–9.9, the storage classes of objects can alter the order in which destructors are called.

### Constructors and Destructors for Objects in Global Scope

Constructors are called for objects defined in global scope (also called global namespace scope) *before* any other function (including main) in that program begins execution (although the order of execution of global object constructors between files is *not guaranteed*). The corresponding destructors are called when main terminates. Function **exit** forces a program to terminate immediately and does *not* execute the destructors of local objects. The exit function often is used to terminate a program when a fatal unrecoverable error occurs. Function **abort** performs similarly to function exit but forces the program to terminate *immediately*, without allowing the destructors of any objects to be called. Function

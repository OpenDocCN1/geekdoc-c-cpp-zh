
```cpp
private:
    unsigned int month; // 1-12 (January-December)
    unsigned int day; // 1-31 based on month
    unsigned int year; // any year

    // utility function to check if day is proper for month and year
    unsigned int checkDay( int ) const;
}; // end class Date

#endif
```

**Fig. 17.17** | Date class definition. (Part 2 of 2.)

```cpp
// Fig. 17.18: Date.cpp
// Date class member-function definitions.
#include <array>
#include <iostream>
#include <stdexcept>
#include "Date.h" // include Date class definition
using namespace std;

// constructor confirms proper value for month; calls
// utility function checkDay to confirm proper value for day
Date::Date( int mn, int dy, int yr )
{
    if ( mn > 0 && mn <= monthsPerYear ) // validate the month
        month = mn;
    else
        throw invalid_argument( "month must be 1-12" );

    year = yr; // could validate yr
    day = checkDay( dy ); // validate the day

    // output Date object to show when its constructor is called
    cout << "Date object constructor for date ";
    print();
    cout << endl;
} // end Date constructor

// print Date object in form month/day/year
void Date::print() const
{
    cout << month << '/' << day << '/' << year;
} // end function print

// output Date object to show when its destructor is called
Date::~Date()
{
    cout << "Date object destructor for date ";
    print();
    cout << endl;
} // end ~Date destructor
```

**Fig. 17.18** | Date class member-function definitions. (Part 1 of 2.)

```cpp
40
41  // utility function to confirm proper day value based on
42  // month and year; handles leap years, too
43  unsigned int Date::checkDay( int testDay ) const
44  {
45      static const array< int, monthsPerYear + 1 > daysPerMonth =
46          { 0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31 };
47
48      // determine whether testDay is valid for specified month
49      if ( testDay > 0 && testDay <= daysPerMonth[ month ] )
50          return testDay;
51
52      // February 29 check for leap year
53      if ( ( month == 2 && testDay == 29 && ( year % 400 == 0 ||
54          ( year % 4 == 0 && year % 100 != 0 ) ) ) )
55          return testDay;
56
57      throw invalid_argument( "Invalid day for current month and year" );
58  } // end function checkDay
```

**Fig. 17.18** | Date class member-function definitions. (Part 2 of 2.)

```cpp
1   // Fig. 17.19: Employee.h
2   // Employee class definition showing composition.
3   // Member functions defined in Employee.cpp.
4   #ifndef EMPLOYEE_H
5   #define EMPLOYEE_H
6
7   #include <string>
8   #include "Date.h" // include Date class definition
9
10  class Employee
11  {
12  public:
13      Employee( const std::string &, const std::string &,
14          const Date &, const Date & );
15      void print() const;
16      ~Employee(); // provided to confirm destruction order
17  private:
18      std::string firstName; // composition: member object
19      std::string lastName; // composition: member object
20      const Date birthDate; // composition: member object
21      const Date hireDate; // composition: member object
22  }; // end class Employee
23
24  #endif
```

**Fig. 17.19** | Employee class definition showing composition.

```cpp
// Fig. 17.20: Employee.cpp
// Employee class member-function definitions.
#include <iostream>
#include "Employee.h" // Employee class definition
#include "Date.h" // Date class definition
using namespace std;

// constructor uses member initializer list to pass initializer
// values to constructors of member objects
Employee::Employee( const string &first, const string &last,
    const Date &dateOfBirth, const Date &dateOfHire )
    : firstName( first ), // initialize firstName
      lastName( last ), // initialize lastName
      birthDate( dateOfBirth ), // initialize birthDate
      hireDate( dateOfHire ) // initialize hireDate
{
    // output Employee object to show when constructor is called
    cout << "Employee object constructor: "
         << firstName << ' ' << lastName << endl;
} // end Employee constructor

// print Employee object
void Employee::print() const
{
    cout << lastName << ", " << firstName << "  Hired: ";
    hireDate.print();
    cout << "  Birthday: ";
    birthDate.print();
    cout << endl;
} // end function print

// output Employee object to show when its destructor is called
Employee::~Employee()
{
    cout << "Employee object destructor: "
         << lastName << ", " << firstName << endl;
} // end ~Employee destructor
```

**Fig. 17.20** | Employee class member-function definitions.

### Employee Constructor's Member Initializer List

The colon (:) following the constructor's header (Fig. 17.20, line 12) begins the member initializer list. The member initializers specify the Employee constructor parameters being passed to the constructors of the string and Date data members. Parameters first, last, dateOfBirth and dateOfHire are passed to the constructors for objects firstName (line 12), lastName (line 13), birthDate (line 14) and hireDate (line 15), respectively. Again, member initializers are separated by commas. The order of the member initializers does not matter. They're executed in the order that the member objects are declared in class Employee.

### Good Programming Practice 17.3

For clarity, list member initializers in the order that the class's data members are declared.

### Date Class's Default Copy Constructor

As you study class Date (Fig. 17.17), notice that the class does *not* provide a constructor that receives a parameter of type Date. So, why can the Employee object's member initializer list initialize the birthDate and hireDate objects by passing Date objects to their Date constructors? As we mentioned in Section 17.9, the compiler provides each class with a *default copy constructor* that copies each data member of the constructor's argument object into the corresponding member of the object being initialized. Chapter 18 discusses how you can define *customized* copy constructors.

### Testing Classes Date and Employee

Figure 17.21 creates two Date objects (lines 10–11) and passes them as arguments to the constructor of the Employee object created in line 12. Line 15 outputs the Employee object's data. When each Date object is created in lines 10–11, the Date constructor defined in lines 11–25 of Fig. 17.18 displays a line of output to show that the constructor was called (see the first two lines of the sample output). [Note: Line 12 of Fig. 17.21 causes two additional Date constructor calls that do not appear in the program's output. When each of the Employee's Date member objects is initialized in the Employee constructor's member-initializer list (Fig. 17.20, lines 14–15), the default copy constructor for class Date is called. Since this constructor is defined implicitly by the compiler, it does not contain any output statements to demonstrate when it's called.]

```cpp
1   // Fig. 17.21: fig17_21.cpp
2   // Demonstrating composition--an object with member objects.
3   #include <iostream>
4   #include "Date.h" // Date class definition
5   #include "Employee.h" // Employee class definition
6   using namespace std;
7
8   int main()
9   {
10      Date birth( 7, 24, 1949 );
11      Date hire( 3, 12, 1988 );
12      Employee manager( "Bob", "Blue", birth, hire );
13
14      cout << endl;
15      manager.print();
16  } // end main
```

|  |  |
|---|---|
| Date object constructor for date 7/24/1949<br>Date object constructor for date 3/12/1988<br>Employee object constructor: Bob Blue<br><br>Blue, Bob  Hired: 3/12/1988  Birthday: 7/24/1949<br>Employee object destructor: Blue, Bob<br>Date object destructor for date 3/12/1988<br>Date object destructor for date 7/24/1949<br>Date object destructor for date 3/12/1988<br>Date object destructor for date 7/24/1949 | There are actually five constructor<br>calls when an Employee is<br>constructed—two calls to the<br>string class's constructor (lines<br>12–13 of Fig. 17.20), two calls to the<br>Date class's default copy<br>constructor (lines 14–15 of<br>Fig. 17.20) and the call to the<br>Employee class's constructor. |

**Fig. 17.21** | Demonstrating composition—an object with member objects.

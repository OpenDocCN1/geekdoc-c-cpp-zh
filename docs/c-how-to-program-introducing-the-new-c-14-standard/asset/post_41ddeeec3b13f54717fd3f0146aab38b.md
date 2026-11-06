
combinations on objects—a non-`const` member function on a non-`const` object (line 10), a `const` member function on a non-`const` object (line 12) and a `const` member function on a `const` object (lines 13–14). The error messages generated for non-`const` member functions called on a `const` object are shown in the output window.

```cpp
// Fig. 9.17: fig09_17.cpp
// const objects and const member functions.
#include "Time.h" // include Time class definition

int main() {
   Time wakeUp{6, 45, 0}; // non-constant object
   const Time noon{12, 0, 0}; // constant object

   wakeUp.setHour(18);       // OBJECT        MEMBER FUNCTION
                             // non-const     non-const
   noon.setHour(12);         // const         non-const
   wakeUp.getHour();         // non-const     const
   noon.getMinute();         // const         const
   noon.toUniversalString(); // const         const
   noon.toStandardString();  // const         non-const
}
```

*Microsoft Visual C++ compiler error messages:*

```text
C:\examples\ch09\fig09_17\fig09_17.cpp(11): error C2662:
  'void Time::setHour(int)': cannot convert 'this' pointer from 'const Time'
  to 'Time &'
C:\examples\ch09\fig09_17\fig09_17.cpp(11): note: Conversion loses qualifiers
  'const'
C:\examples\ch09\fig09_17\fig09_17.cpp(15): error C2662:
  'std::string Time::toStandardString(void)': cannot convert 'this' pointer
  from 'const Time' to 'Time &'
C:\examples\ch09\fig09_17\fig09_17.cpp(15): note: Conversion loses qualifiers
```

### Fig. 9.17 `const` objects and `const` member functions.

A constructor must be a non-`const` member function, but it can still be used to initialize a `const` object (Fig. 9.17, line 7). Recall from *Fig. 9.6* that the `Time` constructor’s definition calls another non-`const` member function—`setTime`—to perform the initialization of a `Time` object. Invoking a non-`const` member function from the constructor call as part of the initialization of a `const` object is allowed.

Line 15 in [Fig. 9.17] generates a compilation error even though member function `toStandardString` of class `Time` *does not* modify the object on which it’s called. The fact that a member function does not modify an object is *not* sufficient—the function must *explicitly* be declared `const`.

## 9.12 Composition: Objects as Members of Classes

An `AlarmClock` object needs to know when it’s supposed to sound its alarm, so why not include a `Time` object as a member of the `AlarmClock` class? Such a software-reuse capability is called **composition** (or **aggregation**) and is sometimes referred to as a *has-a relationship*—a class can have objects of other classes as members.⁵

5. As you’ll see in Chapter 11, classes also may be derived from other classes that provide attributes and behaviors the new classes can use—this is called inheritance.

You’ve actually been using composition since **Chapter 3**. In that chapter’s examples, class `Account` contained a `string` object as a data member.

Previously, we saw how to pass arguments to the constructor of an object we created in `main`. Now we show how a class’s constructor can pass arguments to member-object constructors via member initializers.

### Observation 9.8

> Data members are constructed in the order in which they’re declared in the class definition (not in the order they’re listed in the constructor’s member-initializer list) and before their enclosing class objects are constructed.

The next program uses classes `Date` ([Figs. 9.18–9.19](#)) and `Employee` ([Figs. 9.20–9.21](#)) to demonstrate composition. Class `Employee`’s definition ([Fig. 9.20](#)) contains `private` data members `firstName`, `lastName`, `birthDate` and `hireDate`. Members `birthDate` and `hireDate` are `const` objects of class `Date`, which contains `private` data members `month`, `day` and `year`. The `Employee` constructor’s prototype ([Fig. 9.20](#), lines 14–15) specifies that the constructor has four parameters (`first`, `last`, `dateOfBirth` and `dateOfHire`). The first two parameters are passed via member initializers to the `string` class constructor for the `firstName` and `lastName` data members. The last two are passed via member initializers to the `Date` class constructor for the `birthDate` and `hireDate` data members.

```cpp
// Fig. 9.18: Date.h
// Date class definition; Member functions defined in Date.cpp
#include <string>

#ifndef DATE_H
#define DATE_H

class Date {
public:
    static const unsigned int monthsPerYear{12}; // months in a year
    explicit Date(unsigned int = 1, unsigned int = 1, unsigned int = 1900);
    std::string toString() const; // date string in month/day/year format
    ~Date(); // provided to confirm destruction order
private:
    unsigned int month; // 1-12 (January-December)
    unsigned int day; // 1-31 based on month
    unsigned int year; // any year

    // utility function to check if day is proper for month and year
    unsigned int checkDay(int) const;
};

#endif
```

### Fig. 9.18 **Date** class definition.

```cpp
// Fig. 9.19: Date.cpp
// Date class member-function definitions.
#include <array>
#include <iostream>
#include <stdexcept>
#include "Date.h" // include Date class definition
using namespace std;

// constructor confirms proper value for month; calls
// utility function checkDay to confirm proper value for day
Date::Date(unsigned int mn, unsigned int dy, unsigned int yr)
   : month{mn}, day{checkDay(dy)}, year{yr} {
   if (mn < 1 || mn > monthsPerYear) { // validate the month
      throw invalid_argument("month must be 1-12");
   }

   // output Date object to show when its constructor is called
   cout << "Date object constructor for date " << toString() << endl;
}

// print Date object in form month/day/year
string Date::toString() const {
   ostringstream output;
   output << month << '/' << day << '/' << year;
   return output.str();
}

// output Date object to show when its destructor is called
Date::~Date() {
   cout << "Date object destructor for date " << toString() << endl;
}

// utility function to confirm proper day value based on
// month and year; handles leap years, too
unsigned int Date::checkDay(int testDay) const {
   static const unsigned int daysPerMonth[monthsPerYear + 1] =
      { 0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};

   // determine whether testDay is valid for specified month
   if (testDay > 0 && testDay <= daysPerMonth[month]) {
      return testDay;
   }

   // February 29 check for leap year
   if (month == 2 && testDay == 29 && (year % 400 == 0 ||
      (year % 4 == 0 && year % 100 != 0))) {
      return testDay;
   }

   throw invalid_argument("Invalid day for current month and year");
}
```

### Fig. 9.19 *Date* class member-function definitions.

```cpp
// Fig. 9.20: Employee.h
// Employee class definition showing composition.
// Member functions defined in Employee.cpp.
#include <string>

#ifndef EMPLOYEE_H
#define EMPLOYEE_H

#include <string>
#include "Date.h" // include Date class definition

class Employee {
public:
   Employee(const std::string&, const std::string&,
            const Date&, const Date&);
   std::string toString() const;
   ~Employee(); // provided to confirm destruction order
private:
   std::string firstName; // composition: member object
   std::string lastName;  // composition: member object
   const Date birthDate;  // composition: member object
   const Date hireDate;   // composition: member object
};

#endif
```

### Fig. 9.20 *Employee* class definition showing composition.

```cpp
// Fig. 9.21: Employee.cpp
// Employee class member-function definitions.
#include <iostream>
#include <string>
#include "Employee.h" // Employee class definition
#include "Date.h" // Date class definition
using namespace std;

// constructor uses member initializer list to pass initializer
// values to constructors of member objects
Employee::Employee(const string& first, const string& last,
   const Date &dateOfBirth, const Date &dateOfHire)
   : firstName{first}, // initialize firstName
     lastName{last}, // initialize lastName
     birthDate{dateOfBirth}, // initialize birthDate
     hireDate{dateOfHire} // initialize hireDate
{ // output Employee object to show when constructor is called
   cout << "Employee object constructor: "
      << firstName << ' ' << lastName << endl;
}

// print Employee object
string Employee::toString() const {
   ostringstream output;
   output << lastName << ", " << firstName << " -- Hired: "
      << hireDate.toString() << " Birthday: " << birthDate.toString();
   return output.str();
}

// output Employee object to show when its destructor is called
Employee::~Employee() {
   cout << "Employee object destructor: "
      << lastName << ", " << firstName << endl;
}
```

### Fig. 9.21 **Employee** class member-function definitions.

### Employee Constructor’s Member-Initializer List

The colon (`:`) following the constructor’s header (**Fig. 9.21**, line 13) begins the member-initializer list. The member initializers specify the `Employee` constructor parameters being passed to the constructors of the `string` and `Date` data members. Parameters `first`, `last`, `dateOfBirth` and `dateOfHire` are passed to the constructors for objects `firstName`, `lastName`, `birthDate` and `hireDate`, respectively. The order

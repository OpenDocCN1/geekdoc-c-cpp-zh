
reclaimed by the system. So, declaring a constructor or destructor const is a compilation error. The “constness” of a const object is enforced throughout the object’s lifetime after the object is constructed.

### Using const and Non-const Member Functions

The program of Fig. 9.22 uses a copy of class Time from Figs. 9.10 and 9.11, but removes const from function to12HourString's prototype and definition to force a compilation error. We create two Time objects—non-const object wakeUp (line 6) and const object noon (line 7). The program attempts to invoke non-const member functions setHour (line 11) and to12HourString (line 15) on the const object noon. In each case, the compiler generates an error message. The program also illustrates the three other member-function-call combinations on objects:

- a non-const member function on a non-const object (line 10),
- a const member function on a non-const object (line 12) and
- a const member function on a const object (lines 13–14).

The error messages generated for non-const member functions called on a const object are shown in the output window. We added blank lines for readability.

```cpp
// fig09_22.cpp
// const objects and const member functions.
#include "Time.h" // include Time class definition

int main() {
    Time wakeUp{6, 45, 0}; // non-constant object
    const Time noon{12, 0, 0}; // const object

    // OBJECT       MEMBER FUNCTION
    wakeUp.setHour(18);       // non-const   non-const
    noon.setHour(12);         // const       non-const
    wakeUp.getHour();         // non-const   const
    noon.getMinute();         // const       const
    noon.to24HourString();    // const       const
    noon.to12HourString();    // const       non-const
}
```

*clang++ compiler error messages:*

```text
fig09_22.cpp:11:4: error: 'this' argument to member function 'setHour' has
  type 'const Time', but function is not marked const
    noon.setHour(12);          // const       non-const
    ^~~~

./Time.h:15:9: note: 'setHour' declared here
  void setHour(int hour); // set hour (after validation)
       ^
```

**Fig. 9.22** | const objects and const member functions. (Part 1 of 2.)

```text
fig09_22.cpp:15:4: error: 'this' argument to member function 'to12HourString' has type 'const Time', but function is not marked const
    noon.to12HourString();  // const        non-const
    ^~~~
./Time.h:25:16: note: 'to12HourString' declared here
    std::string to12HourString(); // 12-hour time format string
2 errors generated.
```

**Fig. 9.22** | const objects and const member functions. (Part 2 of 2.)

A constructor must be a non-const member function, but it can still initialize a const object (Fig. 9.22, line 7). Recall from Fig. 9.11 that the Time constructor's definition calls non-const member function setTime to initialize a Time object. Invoking a non-const member function from the constructor for a const object is allowed. Again, the object is not const until the constructor finishes initializing the object.

Line 15 in Fig. 9.22 generates a compilation error even though Time's member function to12HourString does not modify the object on which it's called. This fact is not sufficient—you must explicitly declare the function const for this call to be allowed by the compiler.

### Checkpoint

- **1.** *(Fill-in)* C++ disallows calling a member function on a const object unless that member function is ______.  
  **Answer:** const.
- **2.** *(True/False)* A constructor must be allowed to modify an object to initialize it. A destructor must be allowed to perform its termination housekeeping before an object's memory is reclaimed by the system. So, declaring a constructor or destructor `const` is a compilation error.  
  **Answer:** True.
- **3.** *(True/False)* The “constness” of a const object is enforced throughout the object's lifetime after the object is constructed.  
  **Answer:** True.

## 9.17 Composition: Objects as Members of Classes

An `AlarmClock` object needs to know when it's supposed to sound its alarm, so why not include a `Time` object as a member of the `AlarmClock` class? Such a software-reuse capability is called composition and is sometimes referred to as a has-a relationship—a class can have objects of other classes as members.^32 You've already used composition in this chapter's `Account` class examples. Class `Account` contained a `string` object as a data member.

You've seen how to pass arguments to a constructor. Now, let's see how a class's constructor can pass arguments to member-object constructors via member initializers. The next program uses classes Date (Figs. 9.23 and 9.24) and Employee (Figs. 9.25 and 9.26) to demonstrate composition. Class Employee's definition (Fig. 9.25) has private data members m_firstName, m_lastName, m_birthDate and m_hireDate. Members m_birthDate and m_hireDate are objects of class Date, which has private data members m_year, m_month and m_day.

32. As you'll see in Chapter 10, classes also may be derived from other classes that provide attributes and behaviors the new classes can use—this is called inheritance.

```cpp
// Fig. 9.23: Date.h
// Date class definition; member functions defined in Date.cpp
#pragma once // prevent multiple inclusions of header
#include <string>

class Date {
public:
   static const int monthsPerYear{12}; // months in a year
   Date(int year, int month, int day);
   std::string toString() const; // date string in yyyy-mm-dd format
   ~Date(); // implementation displays when destruction occurs
private:
   int m_year; // any year
   int m_month; // 1-12 (January-December)
   int m_day; // 1-31 based on month

   // utility function to check if day is proper for month and year
   bool checkDay(int day) const;
};
```

**Fig. 9.23** | Date class definition.

```cpp
// Fig. 9.24: Date.cpp
// Date class member-function definitions.
#include <array>
#include <format>
#include <iostream>
#include <stdexcept>
#include "Date.h" // include Date class definition

// constructor confirms proper value for month; calls
// utility function checkDay to confirm proper value for day
Date::Date(int year, int month, int day)
   : m_year(year), m_month(month), m_day(day) {
   if (m_month < 1 || m_month > monthsPerYear) { // validate the month
      throw std::invalid_argument{"month must be 1-12"};
   }

   if (!checkDay(day)) { // validate the day
      throw std::invalid_argument{
         "Invalid day for current month and year"};
   }

   // output Date object to show when its constructor is called
   std::cout << std::format("Date object constructor: {}\n", toString());
}

// gets string representation of a Date in the form yyyy-mm-dd
std::string Date::toString() const {
    return std::format("{}-{:02d}-{:02d}", m_year, m_month, m_day);
}

// output Date object to show when its destructor is called
Date::~Date() {
    std::cout << std::format("Date object destructor: {}\n", toString());
}

// utility function to confirm proper day value based on
// month and year; handles leap years, too
bool Date::checkDay(int day) const {
    // we ignore element 0
    static const std::array daysPerMonth{
        0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};

    // determine whether the day is valid for specified month
    if (1 <= day && day <= daysPerMonth.at(m_month)) {
        return true;
    }

    // February 29 check for leap year
    if ((m_month == 2 && day == 29 && (m_year % 400 == 0 ||
        (m_year % 4 == 0 && m_year % 100 != 0)))) {
        return true;
    }

    return false; // invalid day, based on current m_month and m_year
}
```

**Fig. 9.24** | Date class member-function definitions. (Parts 1 and 2 of 2.)

```cpp
// Fig. 9.25: Employee.h
// Employee class definition showing composition.
// Member functions defined in Employee.cpp.
#pragma once // prevent multiple inclusions of header
#include <string>
#include <string_view>
#include "Date.h" // include Date class definition

class Employee {
public:
    Employee(std::string_view firstName, std::string_view lastName,
        const Date& birthDate, const Date& hireDate);
    std::string toString() const;
    ~Employee(); // provided to confirm destruction order
```

**Fig. 9.25** | Employee class definition showing composition. (Part 1 of 2.)

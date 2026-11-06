# **Software Engineering Observation 10.6**

> *Member objects are constructed in the order in which they’re declared in the class definition (not in the order they’re listed in the constructor’s member initializer list) and before their enclosing class objects (sometimes called host objects) are constructed.*

The next program uses classes Date (Figs. 10.10–10.11) and Employee (Figs. 10.12–10.13) to demonstrate composition. Class Employee’s definition (Fig. 10.12) contains private data members firstName, lastName, birthDate and hireDate. Members birthDate and hireDate are const objects of class Date, which contains private data members month, day and year. The Employee constructor’s header (Fig. 10.13, lines 10–11) specifies that the constructor has four parameters (first, last, dateOfBirth and dateOfHire). The first two parameters are passed via member initializers to the string class constructor. The last two are passed via member initializers to the Date class constructor.

```
```cpp
1  // Fig. 10.10: Date.h
2  // Date class definition; Member functions defined in Date.cpp
3  #ifndef DATE_H
4  #define DATE_H
5  
6  class Date
7  {
8  public:
9      static const int monthsPerYear = 12; // number of months in a year
10     Date( int = 1, int = 1, int = 1900 ); // default constructor
11     void print() const; // print date in month/day/year format
12     ~Date(); // provided to confirm destruction order
13 private:
14     int month; // 1-12 (January-December)
15     int day; // 1-31 based on month
16     int year; // any year
17 
18     // utility function to check if day is proper for month and year
19     int checkDay( int ) const;
20 }; // end class Date
21 
22 #endif
```
```

Fig. 10.10 | Date class definition.

```
```cpp
1  // Fig. 10.11: Date.cpp
2  // Date class member-function definitions.
3  #include <iostream>
4  #include "Date.h" // include Date class definition
5  using namespace std;
6  
7  // constructor confirms proper value for month; calls
8  // utility function checkDay to confirm proper value for day
```
```

Fig. 10.11 | Date class member-function definitions. (Part 1 of 2.)
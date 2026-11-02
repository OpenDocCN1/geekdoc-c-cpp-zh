tializes the data members. A constructor that defaults all its arguments is also a default con-structor—that is, a constructor that can be invoked with no arguments. There can be at most one default constructor per class. The version of class Time in this example provides set and get functions for each data member. The Time constructor now calls setTime, which calls the setHour, setMinute and setSecond functions to validate and assign values to the data members.

> **Software Engineering Observation 17.5**
> 
> *Any change to the default argument values of a function requires the client code to be recompiled (to ensure that the program still functions correctly).*

```
```cpp
 1  // Fig. 17.5: Time.cpp
 2  // Member-function definitions for class Time.
 3  #include <iostream>
 4  #include <iomanip>
 5  #include <stdexcept>
 6  #include "Time.h" // include definition of class Time from Time.h
 7  using namespace std;
 8
 9  // Time constructor initializes each data member
10  Time::Time( int hour, int minute, int second )
11  {
12     setTime( hour, minute, second ); // validate and set time
13  } // end Time constructor
14
15  // set new Time value using universal time
16  void Time::setTime( int h, int m, int s )
17  {
18     setHour( h ); // set private field hour
19     setMinute( m ); // set private field minute
20     setSecond( s ); // set private field second
21  } // end function setTime
22
23  // set hour value
24  void Time::setHour( int h )
25  {
26     if ( h >= 0 && h < 24 )
27        hour = h;
28     else
29        throw invalid_argument( "hour must be 0-23" );
30  } // end function setHour
31
32  // set minute value
33  void Time::setMinute( int m )
34  {
35     if ( m >= 0 && m < 60 )
36        minute = m;
37     else
38        throw invalid_argument( "minute must be 0-59" );
39  } // end function setMinute
```
```

**Fig. 17.5** | Member-function definitions for class Time. (Part 1 of 2).
```
```cpp
Time::Time( int hr, int min, int sec )
{
   setTime( hr, min, sec );
} // end Time constructor

// set values of hour, minute and second
void Time::setTime( int h, int m, int s )
{
   hour = ( h >= 0 && h < 24 ) ? h : 0; // validate hour
   minute = ( m >= 0 && m < 60 ) ? m : 0; // validate minute
   second = ( s >= 0 && s < 60 ) ? s : 0; // validate second
} // end function setTime

// return hour value
int Time::getHour()
{
   return hour;
} // end function getHour

// POOR PROGRAMMING PRACTICE:
// Returning a reference to a private data member.
int &Time::badSetHour( int hh )
{
   hour = ( hh >= 0 && hh < 24 ) ? hh : 0;
   return hour; // DANGEROUS reference return
} // end function badSetHour
```
```

**Fig. 9.15** | Time class member-function definitions. (Part 2 of 2.)

Figure 9.16 declares Time object t (line 12) and reference hourRef (line 15), which is initialized with the reference returned by the call t.badSetHour(20). Line 17 displays the value of the alias hourRef. This shows how hourRef breaks the encapsulation of the class—statements in main should not have access to the private data of the class. Next, line 18 uses the alias to set the value of hour to 30 (an invalid value) and line 19 displays the value returned by function getHour to show that assigning a value to hourRef actually modifies the private data in the Time object t. Finally, line 23 uses the badSetHour function call itself as an lvalue and assigns 74 (another invalid value) to the reference returned by the function. Line 28 again displays the value returned by function getHour to show that assigning a value to the result of the function call in line 23 modifies the private data in the Time object t.

```
```cpp
// Fig. 9.16: fig09_16.cpp
// Demonstrating a public member function that
// returns a reference to a private data member.
#include <iostream>
using std::cout;
using std::endl;

#include "Time.h" // include definition of class Time
```
```

**Fig. 9.16** | Returning a reference to a private data member. (Part 1 of 2.)
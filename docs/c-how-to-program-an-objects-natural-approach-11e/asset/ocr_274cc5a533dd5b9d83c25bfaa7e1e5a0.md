# 9.19.2 Using the this Pointer to Enable Cascaded Function Calls

Another use of the this pointer is to enable cascaded member-function calls—that is, invoking multiple functions sequentially in the same statement, as you’ll see in line 11 of Fig. 9.32. The program of Figs. 9.30–9.32 modifies class Time’s setTime, setHour, setMinute and setSecond functions such that each returns a reference to the Time object on which it’s called. This reference enables cascaded member-function calls. In Fig. 9.31, the last statement in setTime’s body returns a reference to *this (line 30). Functions setHour, setMinute and setSecond each call setTime and return its Time& result.

```
```cpp
// Fig. 9.30: Time.h
// Time class modified to enable cascaded member-function calls.
#pragma once // prevent multiple inclusions of header
#include <string>

class Time {
public:
   // default constructor because it can be called with no arguments
   explicit Time(int hour = 0, int minute = 0, int second = 0);

   // set functions
   Time& setTime(int hour, int minute, int second);
   Time& setHour(int hour); // set hour (after validation)
   Time& setMinute(int minute); // set minute (after validation)
   Time& setSecond(int second); // set second (after validation)

   int getHour() const; // return hour
   int getMinute() const; // return minute
   int getSecond() const; // return second
   std::string to24HourString() const; // 24-hour time format string
   std::string to12HourString() const; // 12-hour time format string
private:
   int m_hour{0}; // 0 - 23 (24-hour clock format)
   int m_minute{0}; // 0 - 59
   int m_second{0}; // 0 - 59
};
```
```

**Fig. 9.30** | Time class modified to enable cascaded member-function calls.

```
```cpp
// Fig. 9.31: Time.cpp
// Time class member-function definitions.
#include <format>
#include <stdexcept>
#include "Time.h" // Time class definition

// Time constructor initializes each data member
Time::Time(int hour, int minute, int second) {
   setTime(hour, minute, second);
}
```
```

**Fig. 9.31** | Time class member-function definitions modified to enable cascaded member-function calls. (Part 1 of 3.)
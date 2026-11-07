```
```cpp
// Time class definition
class Time {
public:
   // default constructor because it can be called with no arguments
   explicit Time(int hour = 0, int minute = 0, int second = 0);

   // set functions
   void setTime(int hour, int minute, int second);
   void setHour(int hour);        // set hour (after validation)
   void setMinute(int minute);    // set minute (after validation)
   void setSecond(int second);    // set second (after validation)

   // get functions
   int getHour() const;            // return hour
   int getMinute() const;          // return minute
   int getSecond() const;          // return second

   std::string to24HourString() const; // 24-hour time format string
   std::string to12HourString() const; // 12-hour time format string

private:
   int m_hour{};   // 0 - 23 (24-hour clock format)
   int m_minute{}; // 0 - 59
   int m_second{}; // 0 - 59
};
```
```

**Fig. 9.10** | Time class containing a constructor with default arguments. (Part 2 of 2.)

# ### Class Time’s Constructor

In Fig. 9.11, lines 9–11 define the Time constructor, which calls setTime to validate and assign values to the data members. Function setTime (lines 14–31) ensures that hour is in the range 0–23 and minute and second are each in the range 0–59. If any argument is out of range, setTime throws an exception—in which case, the Time object will not complete construction and will not exist for use in the program. This version of setTime uses separate if statements to validate the arguments so we can provide precise error messages, indicating which argument is out of range. Functions setHour, setMinute and setSecond (lines 34–40) each call setTime. Each passes its argument and the current values of the other two data members. For example, to change m_hour, setHour passes its hour argument and the current values of m_minute and m_second.

```
```cpp
// Fig. 9.11 Time.cpp
// Member-function definitions for class Time.
#include <format>
#include <stdexcept>
#include <string>
#include "Time.h" // include definition of class Time from Time.h

// Time constructor initializes each data member
Time::Time(int hour, int minute, int second) {
   setTime(hour, minute, second);
}
```
```

**Fig. 9.11** | Member-function definitions for class Time. (Part 1 of 2.)
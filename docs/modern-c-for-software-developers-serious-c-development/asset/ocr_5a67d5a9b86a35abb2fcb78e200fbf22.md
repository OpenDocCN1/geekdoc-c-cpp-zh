The default period is Period<1> (one tick every second).

Suppose that we have 5000 ticks in a second then a duration of twenty seconds can be defined as follows:

```
#include <iostream>
#include <chrono>
#include <ratio>

using namespace std;

int main() {
    // 100000 is the duration in ticks
    chrono::duration<int,5000>> dur{100000};
    cout << (double) dur.count()/5000;
}
```

The constructor of a duration object takes a value in ticks.

Duration objects have a member function count(). count returns a constant number of type Type. This number is the duration of the object in ticks or the number of ticks since the clock's epoch. Suppose that our count function returns 1000. This is the duration as the number of ticks. This value is interpreted in terms of the period of the duration. Suppose that the period is the ratio<1,1000>. This means there are a thousand ticks in a second. So count is interpreted as returning a duration of one second. If the period is ratio<1,10> then there are 10 ticks in a second. So count is interpreted as returning a duration of 100 seconds.

To summarize, a duration class contains the compile-time tick period, which is a std::ratio type. The tick period specifies the number of ticks in a second. The default period is ratio<1,1> one tick per second (represented as ratio<1>). A period such as ratio<1,1000> means that there are thousand ticks in a second so one tick is a millisecond. A period of ratio<1,1000000> means that there are a million ticks in a second, so one tick is a microsecond. A period of ratio<3600,1> (or ratio<3600>)
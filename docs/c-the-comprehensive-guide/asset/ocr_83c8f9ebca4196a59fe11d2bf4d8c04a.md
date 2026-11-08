![](bbox=[0.143, 0.1, 0.627, 0.276])

Figure 18.2 Multiple inheritance.

# 18.4.1  Multiple Inheritance in Practice

Although I would argue that the following example should be better implemented as a has-a relationship, it still serves as an example of an is-a relationship with multiple inheritance.

The base classes here are a clock and a calendar, combined into a clock with a calendar.² In [Listing 18.13](#), you first see a simple clock that you can initialize, display, and advance by one second.

I show a short example here in [Listing 18.13](#). In [Chapter 15](#), [Listing 15.3](#), you can see an improvement by making the example more type-safe with a little more code, especially to prevent errors when swapping constructor parameters.

```
```cpp
// https://godbolt.org/z/xoef1nTs
// Parameters must be valid values of the respective unit.
#include <iostream>  // ostream
#include <iomanip>   // setw, setfill
#include <format>
using std::ostream; using std::format;
class Clock {
protected:
    int h_, m_, s_;
public:
    Clock(int hours, int minutes, int seconds)
      : h_{hours}, m_{minutes}, s_{seconds} {}
    void setClock(int hours, int minutes, int seconds) {
        h_ = hours; m_ = minutes; s_ = seconds;
    }
}
```
```

> ² “Multiple Inheritance,” Bernd Klein, http://www.python-course.eu/python3_multiple_inheritance.php
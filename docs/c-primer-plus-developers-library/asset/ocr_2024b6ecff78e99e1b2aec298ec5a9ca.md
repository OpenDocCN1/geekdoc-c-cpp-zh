Listing 11.7 shows the new header file.

# Listing 11.7  **mytime2.h**

```
```cpp
// mytime2.h -- Time class after operator overloading
#ifndef MYTIME2_H
#define MYTIME2_H

class Time
{
private:
    int hours;
    int minutes;
public:
    Time();
    Time(int h, int m = 0);
    void AddMin(int m);
    void AddHr(int h);
    void Reset(int h = 0, int m = 0);
    Time operator+(const Time & t) const;
    Time operator-(const Time & t) const;
    Time operator*(double n) const;
    void Show() const;
};
#endif
```
```

Then you add definitions for the new methods to the implementation file, as shown in Listing 11.8.

# Listing 11.8  **mytime2.cpp**

```
```cpp
// mytime2.cpp -- implementing Time methods
#include <iostream>
#include "mytime2.h"

Time::Time()
{
    hours = minutes = 0;
}

Time::Time(int h, int m )
{
    hours = h;
    minutes = m;
}

void Time::AddMin(int m)
{
```
```
Here is the output of the program in Listings 11.1, 11.2, and 11.3:

```
```text
planning time = 0 hours, 0 minutes
coding time = 2 hours, 40 minutes
fixing time = 5 hours, 55 minutes
coding.Sum(fixing) = 8 hours, 35 minutes
```
```

# Adding an Addition Operator

It's a simple matter to convert the Time class to using an overloaded addition operator. You just change the name of Sum() to the odd-looking name operator+(). That's right: You just append the operator symbol (+, in this case) to the end of operator and use the result as a method name. This is one place where you can use a character other than a letter, a digit, or an underscore in an identifier name. Listings 11.4 and 11.5 reflect this small change.

**Listing 11.4  mytime1.h**

```
```cpp
// mytime1.h -- Time class before operator overloading
#ifndef MYTIME1_H_
#define MYTIME1_H_

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
    void Show() const;
};
#endif
```
```

**Listing 11.5  mytime1.cpp**

```
```cpp
// mytime1.cpp -- implementing Time methods
#include <iostream>
#include "mytime1.h"

Time::Time()
{
```
```
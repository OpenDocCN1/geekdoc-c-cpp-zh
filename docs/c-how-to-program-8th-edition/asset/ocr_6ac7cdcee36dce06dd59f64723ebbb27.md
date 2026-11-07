would be evaluated as if it were parenthesized as `*(this.x)`, which is a compilation error, because the dot operator cannot be used with a pointer.

> **Common Programming Error 10.7**
> 
> *Attempting to use the member selection operator (`.`) with a pointer to an object is a compilation error—the dot member selection operator may be used only with an lvalue such as an object's name, a reference to an object or a dereferenced pointer to an object.*

![](bbox=[0.16, 0.163, 0.219, 0.207])

One interesting use of the `this` pointer is to prevent an object from being assigned to itself. As we’ll see in Chapter 11, *self-assignment* can cause serious errors when the object contains pointers to dynamically allocated storage.

# **Using the `this` Pointer to Enable Cascaded Function Calls**

Another use of this pointer is to enable cascaded member-function calls—that is, invoking multiple functions in the same statement (as in line 12 of Fig. 10.17). The program of Figs. 10.15–10.17 modifies class Time’s set functions setTime, setHour, setMinute and setSecond such that each returns a reference to a Time object to enable cascaded member-function calls. Notice in Fig. 10.16 that the last statement in the body of each of these member functions returns `*this` (lines 22, 33, 44 and 55) into a return type of `Time &`.

```
```cpp
// Fig. 10.15: Time.h
// Cascading member function calls.

// Time class definition.
// Member functions defined in Time.cpp.
#ifndef TIME_H
#define TIME_H

class Time
{
public:
   Time( int = 0, int = 0, int = 0 ); // default constructor

   // set functions (the Time & return types enable cascading)
   Time &setTime( int, int, int ); // set hour, minute, second
   Time &setHour( int );            // set hour
   Time &setMinute( int );          // set minute
   Time &setSecond( int );          // set second

   // get functions (normally declared const)
   int getHour() const;             // return hour
   int getMinute() const;           // return minute
   int getSecond() const;           // return second

   // print functions (normally declared const)
   void printUniversal() const;     // print universal time
   void printStandard() const;      // print standard time
private:
   int hour;                        // 0 - 23 (24-hour clock format)
   int minute;                      // 0 - 59
```

```

**Fig. 10.15**  |  Time class modified to enable cascaded member-function calls. (Part 1 of 2.)
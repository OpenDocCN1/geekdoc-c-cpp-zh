
> **Error-Prevention Tip 17.4**
>
> *To make your code clearer and more maintainable, and to avoid errors, never hide data members with local variable names.*

### Type of the *this* Pointer

The type of the *this* pointer depends on the type of the object and whether the member function in which *this* is used is declared const. For example, in a non-const member function of class `Employee`, the *this* pointer has the type `Employee *`. In a const member function, the *this* pointer has the type `const Employee *`.

### Implicitly and Explicitly Using the *this* Pointer to Access an Object's Data Members

Figure 17.23 demonstrates the implicit and explicit use of the *this* pointer to enable a member function of class `Test` to print the private data `x` of a `Test` object. In the next example and in Chapter 18, we show some substantial and subtle examples of using *this*.

```cpp
1  // Fig. 17.23: fig17_23.cpp
2  // Using the this pointer to refer to object members.
3  #include <iostream>
4  using namespace std;
5
6  class Test
7  {
8  public:
9      explicit Test( int = 0 ); // default constructor
10     void print() const;
11 private:
12     int x;
13 }; // end class Test
14
15 // constructor
16 Test::Test( int value )
17     : x( value ) // initialize x to value
18 {
19     // empty body
20 } // end constructor Test
21
22 // print x using implicit and explicit this pointers;
23 // the parentheses around *this are required
24 void Test::print() const
25 {
26     // implicitly use the this pointer to access the member x
27     cout << "    x = " << x;
28
29     // explicitly use the this pointer and the arrow operator
30     // to access the member x
31     cout << "\n  this->x = " << this->x;
32
33     // explicitly use the dereferenced this pointer and
34     // the dot operator to access the member x
35     cout << "\n(*this).x = " << (*this).x << endl;
36 } // end of function print
37
38 int main()
39 {
40     Test testObject( 12 ); // instantiate and initialize testObject
41
42     testObject.print();
43 } // end main
```

```text
        x = 12
    this->x = 12
  (*this).x = 12
```

**Fig. 17.23** | using the *this* pointer to refer to object members. (Parts 1 and 2 of 2.)

For illustration purposes, member function `print` (lines 24–36) first prints `x` by using the *this* pointer implicitly (line 27)—only the name of the data member is specified. Then `print` uses two different notations to access `x` through the *this* pointer—the arrow operator (`->`) off the *this* pointer (line 31) and the dot operator (`.`) off the dereferenced *this* pointer (line 35). Note the parentheses around *this (line 35) when used with the dot member selection operator (`.`). The parentheses are required because the dot operator has higher precedence than the `*` operator. Without the parentheses, the expression `*this.x` would be evaluated as if it were parenthesized as `*(this.x)`, which is a *compilation error*, because the dot operator cannot be used with a pointer.

One interesting use of the *this* pointer is to prevent an object from being assigned to itself. As we’ll see in Chapter 18, *self-assignment* can cause serious errors when the object contains pointers to dynamically allocated storage.

### Using the *this* Pointer to Enable Cascaded Function Calls

Another use of the *this* pointer is to enable cascaded member-function calls—that is, invoking multiple functions in the same statement (as in line 12 of Fig. 17.26). The program of Figs. 17.24–17.26 modifies class `Time`’s set functions `setHour`, `setMinute` and `setSecond` such that each returns a reference to a `Time` object to enable cascaded member-function calls. Notice in Fig. 17.25 that the last statement in the body of each of these member functions returns *this (lines 23, 34, 45 and 56) with a return type of `Time&`.

The program of Fig. 17.26 creates `Time` object `t` (line 9), then uses it in cascaded member-function calls (lines 12 and 24). Why does the requirement of returning *this as a reference work? The dot operator (`.`) associates from left to right, so line 12 first evaluates `t.setHour(18)`, then returns a reference to object `t` as the value of this function call. The remaining expression is then interpreted as

```cpp
t.setMinute( 30 ).setSecond( 22 );
```

The `t.setMinute(30)` call executes and returns a reference to the object `t`. The remaining expression is interpreted as

```cpp
t.setSecond( 22 );
```

```cpp
// Fig. 17.24: Time.h
// Cascading member function calls.

// Time class definition.
// Member functions defined in Time.cpp.
#ifndef TIME_H
#define TIME_H

class Time
{
public:
   explicit Time( int = 0, int = 0, int = 0 ); // default constructor

   // set functions (the Time class uses set functions to enable cascading)
   Time &setTime( int, int, int ); // set hour, minute, second
   Time &setHour( int ); // set hour
   Time &setMinute( int ); // set minute
   Time &setSecond( int ); // set second

   // get functions (normally declared const)
   unsigned int getHour() const; // return hour
   unsigned int getMinute() const; // return minute
   unsigned int getSecond() const; // return second

   // print functions (normally declared const)
   void printUniversal() const; // print universal time
   void printStandard() const; // print standard time
private:
   unsigned int hour; // 0 - 23 (24-hour clock format)
   unsigned int minute; // 0 - 59
   unsigned int second; // 0 - 59
}; // end class Time

#endif
```

**Fig. 17.24** | Time class modified to enable cascaded member-function calls.

```cpp
1  // Fig. 17.25: Time.cpp
2  // Time class member-function definitions.
3  #include <iostream>
4  #include <iomanip>
5  #include <stdexcept>
6  #include "Time.h" // Time class definition
7  using namespace std;
8
9  // constructor function to initialize private data;
10 // calls member function setTime to set variables;
11 // default values are 0 (see class definition)
12 Time::Time( int hr, int min, int sec )
13 {
14     setTime( hr, min, sec );
15 } // end Time constructor
16
17 // set values of hour, minute, and second
18 Time &Time::setTime( int h, int m, int s ) // note Time & return
19 {
20     setHour( h );
21     setMinute( m );
22     setSecond( s );
23     return *this; // enables cascading
24 } // end function setTime
25
26 // set hour value
27 Time &Time::setHour( int h ) // note Time & return
28 {
29     if ( h >= 0 && h < 24 )
30         hour = h;
31     else
32         throw invalid_argument( "hour must be 0-23" );
33
34     return *this; // enables cascading
35 } // end function setHour
36
37 // set minute value
38 Time &Time::setMinute( int m ) // note Time & return
39 {
40     if ( m >= 0 && m < 60 )
41         minute = m;
42     else
43         throw invalid_argument( "minute must be 0-59" );
44
45     return *this; // enables cascading
46 } // end function setMinute
47
48 // set second value
49 Time &Time::setSecond( int s ) // note Time & return
50 {
51     if ( s >= 0 && s < 60 )
52         second = s;
53     else
54         throw invalid_argument( "second must be 0-59" );
55
56     return *this; // enables cascading
57 } // end function setSecond
58
59 // get hour value
60 unsigned int Time::getHour() const
61 {
62     return hour;
63 } // end function getHour
64
65 // get minute value
66 unsigned int Time::getMinute() const
67 {
68     return minute;
69 } // end function getMinute
70
71 // get second value
72 unsigned int Time::getSecond() const
73 {
74     return second;
75 } // end function getSecond
76
77 // print Time in universal-time format (HH:MM:SS)
78 void Time::printUniversal() const
79 {
80     cout << setfill('0') << setw(2) << hour << ":"
81         << setw(2) << minute << ":" << setw(2) << second;
82 } // end function printUniversal
83
84 // print Time in standard-time format (HH:MM:SS AM or PM)
85 void Time::printStandard() const
86 {
87     cout << ( ( hour == 0 || hour == 12 ) ? 12 : hour % 12 )
88         << ":" << setfill('0') << setw(2) << minute
89         << ":" << setw(2) << second << ( hour < 12 ? " AM" : " PM" );
90 } // end function printStandard
```

**Fig. 17.25** | Time class member-function definitions modified to enable cascaded member-function calls. (Parts 1–3 of 3.)

Line 24 (Fig. 17.26) also uses cascading. Note that we cannot chain another member-function call after `printStandard` here, because `printStandard` does not return a reference to `t`. Placing the call to `printStandard` before the call to `setTime` in line 24 results in a compilation error. Chapter 18 presents several practical examples of using cascaded function calls. One such example uses multiple `<<` operators with `cout` to output multiple values in a single statement.

```cpp
1  // Fig. 17.26: fig17_26.cpp
2  // Cascading member-function calls with the this pointer.
3  #include <iostream>
4  #include "Time.h" // Time class definition
5  using namespace std;
6
7  int main()
8  {
9      Time t; // create Time object
10
11     // cascaded function calls
12     t.setHour( 18 ).setMinute( 30 ).setSecond( 22 );
```

**Fig. 17.26** | Cascading member-function calls with the *this* pointer. (Part 1 of 2.)

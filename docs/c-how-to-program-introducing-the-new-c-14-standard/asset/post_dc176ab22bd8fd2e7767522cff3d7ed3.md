
programs with many headers that may themselves include other headers.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1158_0.png)

## Error-Prevention Tip 9.1

*Use* `#ifndef`, `#define` *and* `#endif` *preprocessing directives to form an include guard that prevents headers from being included more than once in a source-code file.*

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1158_1.png)

## Good Programming Practice 9.1

*By convention, use the name of the header in uppercase with the period replaced by an underscore in the* `#ifndef` *and* `#define` *preprocessing directives of a header.*

## 9.2.4 `Time` Class Member Functions

The source-code file `Time.cpp` (**Fig. 9.2**) defines class `Time`’s member functions, which were *declared* in lines 13–15 of **Fig. 9.1**. Note that for the `const` member functions `toUniversalString` and `toStandardString`, the `const` keyword *must* appear in *both* the function prototypes (**Fig. 9.1**, lines 14–15) and the function definitions (**Fig. 9.2**, lines 26 and 34).

```cpp
// Fig. 9.2: Time.cpp
// Time class member-function definitions.
#include <iomanip> // for setw and setfill stream manipulators
#include <stdexcept> // for invalid_argument exception class
#include <sstream> // for ostringstream class
#include <string>
#include "Time.h" // include definition of class Time from Time.h

using namespace std;

// set new Time value using universal time
void Time::setTime(int h, int m, int s) {
   // validate hour, minute and second
   if ((h >= 0 && h < 24) && (m >= 0 && m < 60) && (s >= 0 && s < 60)) {
      hour = h;
      minute = m;
      second = s;
   }
   else {
      throw invalid_argument(
         "hour, minute and/or second was out of range");
   }
}

// return Time as a string in universal-time format (HH:MM:SS)
string Time::toUniversalString() const {
   ostringstream output;
   output << setfill('0') << setw(2) << hour << ":"
      << setw(2) << minute << ":" << setw(2) << second;
   return output.str(); // returns the formatted string
}

// return Time as string in standard-time format (HH:MM:SS AM or PM)
string Time::toStandardString() const {
   ostringstream output;
   output << ((hour == 0 || hour == 12) ? 12 : hour % 12) << ":"
      << setfill('0') << setw(2) << minute << ":" << setw(2)
      << second << (hour < 12 ? " AM" : " PM");
   return output.str(); // returns the formatted string
}
```

**Fig. 9.2** *Time* class member-function definitions.

## 9.2.5 Scope Resolution Operator

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1161_0.png)

Each member function’s name (lines 12, 26 and 34) is preceded by the class name and the scope resolution operator (`::`). This “ties” them to the (now separate) `Time` class definition (**Fig. 9.1**), which declares the class’s members. The `Time::` tells the compiler that each member function is within that **class**’s scope and its name is known to other class members.

Without “`Time::`” preceding each function name, these functions would *not* be recognized by the compiler as `Time` member functions. Instead, the compiler would consider them “free” or “loose” functions, like `main`—these are also called *global functions*. Such functions cannot access `Time`’s *private* data or call the class’s member functions, without specifying an object. So, the compiler would *not* be able to compile these functions. For example, lines 28–29 and 36–38 in **Fig. 9.2** that access data members `hour`, `minute` and `second` would cause compilation errors because these variables are not declared as local variables in each function—the compiler would not know that `hour`, `minute` and `second` are already declared in class `Time`.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1162_0.png)

## Common Programming Error 9.1

When defining a class’s member functions outside that class, omitting the class name and scope resolution operator (`::`) that should precede the function names causes compilation errors.

## 9.2.6 Including the Class Header in the Source-Code File

To indicate that the member functions in `Time.cpp` are part of class `Time`, we must first include the `Time.h` header (**Fig. 9.2**, line 7). This allows us to use the class name `Time` in the `Time.cpp` file (lines 12, 26 and 34). When compiling `Time.cpp`, the compiler uses the information in `Time.h` to ensure that

- the first line of each member function (lines 12, 26 and 34) matches its prototype in the `Time.h` file—for example, the compiler ensures that `setTime` accepts three `int` parameters and returns nothing, and
- each member function knows about the class’s data members and other member functions—e.g., lines 28–29 and 36–38 can access data members `hour`, `minute` and `second` because they’re declared in `Time.h` as data members of class `Time`.

## 9.2.7 `Time` Class Member Function `setTime` and Throwing Exceptions

Function `setTime` (lines 12–23) is a `public` function that declares three `int` parameters and uses them to set the time. Line 14 tests each argument to determine whether the value is in range, and, if so, lines 15–17 assign the values to the `hour`, `minute` and `second` data members, respectively. The `hour` value must be greater than or equal to `0` and less than `24`, because universal-time format represents hours as integers from 0 to 23 (e.g., 11 AM is hour 11, 1 PM is hour 13 and 11 PM is hour 23; midnight is hour 0 and noon is hour 12). Similarly, both `minute` and `second` must be greater than or equal to `0` and less than `60`.

If any of the values is outside its range, `setTime` **throws an exception** (lines 20–21) of type `invalid_argument` (from header `<stdexcept>`), which notifies the client code that an invalid argument was received. As you saw in **Section 7.10**, you can use `try...catch` to catch exceptions and attempt to recover from them, which we’ll do in **Fig. 9.3**. The `throw` statement creates a new object of type `invalid_argument`. The parentheses following the class name indicate a call to the `invalid_argument` constructor that allows us to specify a custom error-message string. After the exception object is created, the `throw` statement immediately terminates function `setTime` and the exception is returned to the code that attempted to set the time.

Invalid values cannot be stored in the data members of a `Time` object, because

- when a `Time` object is created, its default constructor is called and each data member is initialized to 0, as specified in lines 17–19 of **Fig. 9.1**—setting `hour`, `minute` and `second` to 0 is the universal-time equivalent of 12 AM (midnight)—and
- all subsequent attempts by a client to modify the data members are scrutinized by function `setTime`.

## 9.2.8 `Time` Class Member Function `toUniversalString` and String Stream Processing

Member function `toUniversalString` (lines 26–31 of **Fig. 9.2**) takes no arguments and returns a `string` containing the time formatted as universal time with three colon-separated pairs of digits. For example, if the time were 1:30:07 PM, `toUniversalString` would return `13:30:07`.

As you know, `cout` is the standard output stream. Objects of class **ostringstream** (from the header `<sstream>`) provide the same functionality, but write their output to `string` objects in memory. You use class `ostringstream`’s **str** member function to get the formatted `string`.

Member function `toUniversalString` creates an `ostringstream` object named output (line 27), then uses it like `cout` in lines 28–29 to create the formatted string. Line 28 uses parameterized stream manipulator **setfill** to specify the fill **character** that’s displayed when an integer is output in a field *wider* than the number of digits in the value. The fill characters appear to the *left* of the digits in the number, because the number is *right* aligned by default—for *left*-aligned values (specified

```
Enter the temperature in degrees F: 212
Degrees C = 0
```

Water boils at 212 degrees Fahrenheit which is 100 degrees Celsius, so this answer is not correct.

```
Enter the temperature in degrees F: -40
Degrees C = 0
```

The value -40 is the point where the Fahrenheit and Celsius curves cross, so the result should be -40, not zero. The first test was only coincidentally correct.

Unfortunately, the printed result is always zero regardless of the input. The problem is the division 5/9 in the statement

```
degreesC = 5/9*(degreesF - 32);
```

Division and multiplication have equal precedence, and both are left associative; therefore, the division is performed first. Since both operands are integers, integer division is performed and the quotient is zero (5 divided by 9 is 0, remainder 5). Of course zero times any number is zero, thus the result. The fact that a floating-point variable is involved in the expression (degreesF) and the overall result is being assigned to a floating-point variable, is irrelevant. The decision about the exact type of operation to perform is made on an operator-by-operator basis, not globally over the entire expression. Since the division is performed first and it involves two integer values, integer division is used before the other floating-point pieces become involved.

One solution simply uses a floating-point literal for either the five or the nine, as in

```
degreesC = 5.0/9*(degreesF - 32);
```

This forces a double-precision floating-point division (recall that the literal 5.0 is a double). The correct result, subject to rounding instead of truncation, is finally computed.

Listing 4.11 (timeconv.cpp) uses integer division and modulus to split up a given number of seconds to hours, minutes, and seconds.

```
Listing 4.11: timeconv.cpp
// File: timeconv.cpp

#include <iostream>

int main() {
  int hours, minutes, seconds;
  std::cout << "Please enter the number of seconds:";
  std::cin >> seconds;
  // First, compute the number of hours in the given number
  // of seconds
  hours = seconds / 3600; // 3600 seconds = 1 hours
  // Compute the remaining seconds after the hours are
  // accounted for
  seconds = seconds % 3600;
  // Next, compute the number of minutes in the remaining
  // number of seconds
  minutes = seconds / 60; // 60 seconds = 1 minute
  // Compute the remaining seconds after the minutes are
```
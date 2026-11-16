
warning C4700: uninitialized local variable 'n' used

The compiler issued a warning but still generated the executable file. When run, the program produces a random result because it prints the value in memory associated with the variable, but the program does not initialize that memory location.

Listing 4.8 (narrow.cpp) assigns a `double` value to an `int` variable, which we know from Section 4.1 truncates the result.

```cpp
Listing 4.8: narrow.cpp
#include <iostream>
int main() {
    int n;
    double d = 1.6;
    n = d;
    std::cout << n << '\n';
}
```

When compiled we see

warning C4244: '=' : conversion from 'double' to 'int', possible loss of data

Since it is a warning and not an error, the compiler generates the executable, but the warning should prompt us to stop and reflect about the correctness of the code. The enhanced warning level prevents the programmer from being oblivious to the situation.

The default Visual C++ warning level is 3 when compiling in the IDE and level 1 on the command line (that is why we use the /W3 option on the command line); the highest warning level is 4. You can reduce the level to 1 or 2 or disable warnings altogether, but that is not recommended. The only reason you might want to reduce the warning level is to compile older existing C++ source code that does meet newer C++ standards. When developing new code, higher warning levels are preferred since they provide more help to the programmer. Unless otherwise noted, all the complete program examples in this book compile cleanly under Visual C++ set at warning level 3. Level 3 is helpful for detecting many common logic errors.

We can add more warnings by a simple addition to the code. Section 4.2 showed how we can use `static_cast` to coerce a wider type to a narrower type. At Visual C++ warning Level 3, the compiler issues a warning if the cast is not used. The little code that must be added should cause the programmer to stop and reflect about the correctness of the construct. The enhanced warning level prevents the programmer from being oblivious to the situation.

Use the strongest level of warnings available to your compiler. Treat all warnings as problems that must be corrected. Do not accept as completed a program that compiles with warnings.

We may assign a `double` literal to a `float` variable without any special type casting. The compiler automatically narrows the `double` to a `float` as Listing 4.9 (assignfloat.cpp) shows:

```cpp
Listing 4.9: assignfloat.cpp

#include <iostream>

int main() {
    float number;
    number = 10.0; // Ok, double literal assignable to a float
    std::cout << "number = " << number << '\n';
}
```

The statement

`number = 10.0;`

assigns a double literal (10.0) to a float variable. You instead may explicitly use a float literal as:

`number = 10.0f;`

## 4.7 Arithmetic Examples

The kind of arithmetic to perform in a complex expression is determined on an operator by operator basis. For example, consider Listing 4.10 (tempconv.cpp) that attempts to convert a temperature from degrees Fahrenheit to degrees Celsius using the formula

C = 5/9 * (F - 32)

```cpp
Listing 4.10: tempconv.cpp

// File tempconv.cpp
#include <iostream>

int main() {
    double degreesF, degreesC;
    // Prompt user for temperature to convert
    std::cout << "Enter the temperature in degrees F: ";
    // Read in the user's input
    std::cin >> degreesF;
    // Perform the conversion
    degreesC = 5/9 * (degreesF - 32);
    // Report the result
    std::cout << degreesC << '\n';
}
```

Listing 4.10 (tempconv.cpp) contains comments that document each step explaining the code's purpose. An initial test is promising:

```
Enter the temperature in degrees F: 32
Degrees C = 0
```

Water freezes at 32 degrees Fahrenheit and 0 degrees Celsius, so the program's behavior is correct for this test. Several other attempts are less favorable—consider

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

```cpp
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
  // accounted for
  seconds = seconds % 60;
  // Report the results
  std::cout << hours << " hr, " << minutes << " min, "
<< seconds << " sec\n";
}
```

If the user enters 10000, the program prints 2 hr, 46 min, 40 sec. Notice the assignments to the seconds variable, such as

```
seconds = seconds % 3600
```

The right side of the assignment operator (=) is first evaluated. The remainder of seconds divided by 3,600 is assigned back to seconds. This statement can alter the value of seconds if the current value of seconds is greater than 3,600. A similar statement that occurs frequently in programs is one like

```
x = x + 1;
```

This statement increments the variable x to make it one bigger. A statement like this one provides further evidence that the C++ assignment operator does not mean mathematical equality. The following statement from mathematics

```
x = x + 1
```

is surely never true; a number cannot be equal to one more than itself. If that were the case, I would deposit one dollar in the bank and then insist that I really had two dollars in the bank, since a number is equal to one more than itself. That two dollars would become 3.00, then 4.00, etc., and soon I would be rich. In C++, however, this statement simply means “add one to x and assign the result back to x.”

A variation on Listing 4.11 (timeconv.cpp), Listing 4.12 (enhancedtimeconv.cpp) performs the same logic to compute the time pieces (hours, minutes, and seconds), but it uses more simple arithmetic to produce a slightly different output—instead of printing 11,045 seconds as 3 hr, 4 min, 5 sec, Listing 4.12 (enhancedtimeconv.cpp) displays it as 3:04:05. It is trivial to modify Listing 4.11 (timeconv.cpp) so that it would print 3:4:5, but Listing 4.12 (enhancedtimeconv.cpp) includes some extra arithmetic to put leading zeroes in front of single-digit values for minutes and seconds as is done on digital clock displays.

```cpp
Listing 4.12: enhancedtimeconv.cpp

// File: enhancedtimeconv.cpp
//#include <iostream>
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


## 4.6. ERRORS << WARNINGS

```cpp
cout << n << endl;
)
```

An attempt to build Listing 4.8 (uninitialized.cpp) yields the following message from the Visual C++ compiler:

> warning C4700: uninitialized local variable 'n' used

The compiler issued a warning but still generated the executable file. When run, the program produces a random result because it prints the value in memory associated with the variable, but the program does not initialize memory location.

Listing 4.9 (narrow.cpp) assigns a double value to an int variable, which we know from Section 4.1 truncates the result.

Listing 4.9: narrow.cpp
```cpp
#include <iostream>
using namespace std;

int main() {
    int n;
    double d = 1.6;
    n = d;
    cout << n << endl;
}
```

When compiled we see

> warning C4244: '=': conversion from 'double' to 'int', possible loss of data

Since it is a warning and not an error, the compiler generates the executable, but the warning should prompt us to stop and reflect about the correctness of the code. The enhanced warning level prevents the programmer from being oblivious to the situation.

The default Visual++ warning level is 3 when compiling in the IDE and level 1 on the command line (that is why we use the /W3 option on the command line); the highest warning level is 4. You can reduce the level to 1 or 2 warnings, but that is not recommended. The only reason you might want to reduce the level is to handle older C++ source code that does not meet C++ standards. When developing new code, higher warning levels are preferred to provide more help to the programmer at all stages of development. Examples in this book compile well under Visual++ at level 3. Level 3 is helpful for detecting common logic errors.

We can avoid most warnings by adding a simple addition to the code. Section 4.2 showed how we can use static_cast to coerce a wider type to a narrower type. At Visual warning level 3, the compiler issues a warning if the cast is not used. The little code that added would cause the programmer to stop and reflect about the correctness of the construct. The enhanced warning level prevents the programmer from being oblivious to the situation.

## 4.7. ARITHMETIC EXAMPLES

> Use the strongest level of warnings available to your compiler. Treat all warnings as problems that must be corrected. Do not accept as completed a program that compiles with warnings.

## 4.7 Arithmetic Examples

The kind of arithmetic to perform in a complex expression is determined on an operator by operator basis. For example, consider Listing 4.10 tempcomp.cpp that attempts to convert a temperature from degrees Fahrenheit to Celsius using the formula

$C = \frac{5}{9} \times (F - 32)$

Listing 4.10: tempcomp.cpp
```cpp
// File tempcomp.cpp

#include <iostream>

using namespace std;

int main() {
    double degreesF, degreesC;
    // Prompt for temperature to convert
    cout << "Enter the temperature in degrees F: ";
    // Read in the user's input
    cin >> degreesF;
    // Perform the conversion
    degreesC = 5/9 * (degreesF - 32);
    // Report the result
    cout << degreesC << endl;
}
```

Listing 4.10 (tempcomp.cpp) contains comments that document each step explaining the code's purpose. An initial test is promising:

```
Enter the temperature in degrees F: 32
Degrees C = 0
```

Water freezes at 32 degrees Fahrenheit and 0 degrees Celsius, so the program's behavior is correct for this test. Other attempts are less favorable—consider

```
Enter the temperature in degrees F: 212
Degrees C = 0
```

Water boils at 212 degrees Fahrenheit which is 100 degrees Celsius, so this answer is not correct.

```
Enter the temperature in degrees F: -40
Degrees C = 0
```

The value –40 is not where the Fahrenheit and Celsius curves cross, so the result should be –40, not zero. The first test was only coincidentially correct.

Unfortunately, the printed result is always regardless of the input. The problem is the division 5/9 in the statement

```cpp
degreeC = 5/9*(degreeF - 32);
```

Division and multiplication have equal precedence, and both are associative: therefore, the division is performed first. If both operands are integers, the division is performed and the quotient is zero (5 divided by 9 is 0, remainder 5). Course zero times any number is zero, thus. The fact that a floating-point value is involved in the expression (degreeF) and the overall result being assigned to a floating-point variable, is irrelevant. The decision about exact type of operation to perform is made on an operator-by-operator basis, not globally over the entire expression. Since the division is performed first and it involves two integers, integer division is used before the other floating-point pieces become involved.

One simple solution is using a floating-point literal for either the nine, or as we

```cpp
degreeC = 5.0/9*(degreeF - 32);
```

This forces a double-precision floating-point division (recall that the 5.0 is a double). The correct result, subject to rounding instead of truncation, is finally computed. Listing 4.11: timeconv.cpp uses integer division and modulus to split a number of seconds to hours, minutes.

Listing 4.11: timeconv.cpp
```cpp
// File timeconv.cpp

#include <iostream>

using namespace std;

int main() {
    int hours, minutes, seconds;
    // Prompt for temperature to convert
    cout << "Enter the temperature in degrees F: ";
    // Read in the user's input
    cin >> seconds;
    // First, compute the number of hours in the given number
    hours = seconds / 3600;
    // Compute the remaining seconds after the hours
    seconds = seconds % 3600;
    // Next, compute the number of minutes in the remaining
    minutes = seconds / 60;
    // Report the result
    cout << hours << " hr, " << minutes << " min, " << seconds << " sec" << endl;
}
```

```
// Compute the remaining seconds after the minutes
seconds = seconds % 60;
cout << hours << " hr, " << minutes << " min, " << seconds << " sec" << endl;
```

If the user enters 1000, the program prints 2 hr, 46 min, 40 sec. Notice the right side of the assignment operator (=) is first evaluated. The remainder of seconds divided by 3,600 is assigned back to seconds. This statement can alter the value of seconds if the current value is greater than 3,600.

```
x = x + 1;
```

This statement increases the variable x to make it bigger. A similar statement that occurs frequently in programs provides further evidence that the C++ assignment operator does not mean mathematical. In C++, this statement simply means "add one to x and assign the result back to x."

A Variation on 4.11 (timeconv.cpp). Listing 4.12 (enhancedtimeconv.cpp) performs some arithmetic logic to produce a slightly different output—instead of printing 11.045 seconds as 3 hr, 4 min, 5 sec, Listing 4.12 (enhancedtimeconv.cpp) displays it as 3:04:05. It is vital to modify 4.11 (timeconv.cpp) so that it would print 3:4:5, Listing 4.12 (enhancedtimeconv.cpp) includes some arithmetic to leading zeros for single-digit values of minutes and seconds as is done on digital clock displays.

# Listing 4.12: enhancedtimeconv.cpp
```cpp
// File enhancedtimeconv.cpp

#include <iostream>
#include <iomanip>

using namespace std;

int main() {
    int hours, minutes, seconds;
    cout << "enter the number of seconds:";
    cin >> seconds;
    // First, compute the number of hours in the given number
    hours = seconds / 3600;
    // Compute the remaining seconds after the hours
    seconds = seconds % 3600;
    // Next, compute the number of minutes in the remaining
    minutes = seconds / 60;
    // Report the result with leading zeros
    cout << hours << ":" << setfill('0') << setw(2) << minutes << ":" 
         << setfill('0') << setw(2) << seconds << endl;
}
```

©2024 Richard L. Halman

Date date: January 26, 2014

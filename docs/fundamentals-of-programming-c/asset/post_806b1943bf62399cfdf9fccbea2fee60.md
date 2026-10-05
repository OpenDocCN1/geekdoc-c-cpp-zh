
## 9.4. FUNCTION EXAMPLES

In Listing 9.11 (betterinputfunc.cpp)

- The high and low values are specified by parameters. This makes the function more flexible since it could be used elsewhere in the program with a completely different range specified and still work correctly.

- The function is supposed to be called with the lower number as the first parameter and the higher number as the second parameter. The function will also accept the parameters out of order and automatically swap them to work as expected; thus,

```cpp
num = get_int_range(20, 50);
```

will work exactly like

```cpp
num = get_int_range(50, 20);
```

- The Boolean variable `bad_entry` is used to avoid evaluating the Boolean exception twice (once to see if the bad entry message should be printed and again to see if the loop should continue).

### 9.4.4 Better Die Rolling Simulator

```cpp
Listing 9.12: betterdie.cpp
#include <iostream>
#include <cstdlib>
#include <ctime>

using namespace std;

/*
* initialize_die
* Initializes the randomness of the die
*/
void initialize_die() {
    // Set the random seed value
    srand(static_cast<unsigned>(time(0)));
}

/*
* show_die(spots)
* Draws a picture of a die with number of spots
* indicated
* spots is the number of spots on the top face
*/
void show_die(int spots) {
    cout << "-----------" << endl;
    switch (spots) {
        case 1:
            cout << " | |" << endl;
            cout << " * |" << endl;
            cout << " | |" << endl;
            break;
        case 2:
            cout << " * |" << endl;
            cout << "|" << "" << endl;
            cout << "|" * "|" << endl;
            break;
        case 3:
            cout << "|" * * << "|" << endl;
            cout << "|" * "|" << endl;
            cout << "|" * " << "" << endl;
            break;
        case 4:
            cout << "|" * * << "|" << endl;
            cout << "|" * "|" << endl;
            cout << "|" * * << "|" << endl;
            break;
        case 5:
            cout << "|" * * << "|" << endl;
            cout << "|" * "|" << endl;
            cout << "|" * * << "|" << endl;
            break;
        case 6:
            cout << "|" * * * << "|" << endl;
            cout << "|" * * << "" << endl;
            cout << "|" * * << "" << endl;
            break;
        default:
            cout << " *** Error: illegal die value ***" << endl;
    }
    cout << "+----------+" << endl;
}
```

- `roll` Returns a pseudorandom number in the range 1..6

```cpp
int roll1() {
    return rand() % 6 + 1;
}
```

- Simulates the roll of a die three times

```cpp
int main() {
    // Initialize the die
    initialize_die();

    // Roll the die three times
    for (int i = 0; i < 3; i++)
        show_die(roll());
}
```

In Listing 9.12 (betterdie.cpp), main is no longer concerned with the details of pseudorandom number generation, nor is it responsible for drawing the die. These important components of the program are now in functions, their details can be perfected independently from main.

Note how the result of the call to `roll` is passed directly as an argument to `show_die`.

### 9.4.5 Tree Drawing Function

Listing 9.13: treefunc.cpp

```cpp
#include <iostream>
using namespace std;
/*
 * tree(height)
 * Draws a tree of a given height
 * height is the height of the displayed tree
 */
void tree(int height) {
    int row = 0; // First row, from the top, to draw
    while (row < height) { // Draw one row for every unit of height
        // Print leading spaces
        int count = 0;
        while (count < height - row) {
            cout << " ";
            count++;
        }
        // Print out stars, twice the current row plus one:
        // 1. number of stars on left side of tree
        // = current row value
        // 2. exactly one star in the center of the tree
        // 3. number of stars on right side of tree
        // = current row value
        count = 0;
        while (count < 2*row + 1) {
            cout << "*";
            count++;
        }
        // Move cursor down to next line
        cout << endl;
        // Change to the next row
        row++;
    }
}

/*
 Allows users to draw trees of various heights
*/
int main() {
    int height; // Height of tree
    cout << "Enter height of tree: ";
    cin >> height; // Get height from user
    tree(height);
}
```

©2014 Richard L. Halerman

Observe that the name `height` is being used as a local variable in main and as a formal parameter in tree. There is no conflict here, and the two heights represent two different locations in memory. Furthermore, that the statement `tree(height);` uses main's height as an actual parameter and height happens to be the name simply a coincidence. The compiler can keep track of where each is declared.

### 9.4.6 Floating-Point Equality

Recall from 4.2 (imprecision.cpp) that floating-point numbers are not mathematical real numbers; a floating-point number is finite and represented internally as a quantity with binary mantissa and exponent. Just as 1/3 cannot be represented finely in (base 10), 1/10 cannot be represented exactly in (base 2) with fixed number of digits. Often problems arise from this imprecision, and in many software applications written using floating-point calculations such small errors can result in complete failures. Floating-point numbers can be used safely and effectively, but without appropriate care. To build our confidence with floating-point numbers, consider Listing 9.14 (simpleaddition.cpp), which adds two double-precision floating-point numbers and checks for a given value.

Listing 9.14: simpleaddition.cpp

```cpp
#include <iostream>

using namespace std;

int main() {
    double x = 0.9;
    x += 0.1;
    if (x == 1.0)
        cout << "OK" << endl;
    else
        cout << "NOT OK" << endl;
}
```

All seems well. Next, consider Listing 9.15 (badfloatcheck.cpp) which attempts to control a loop with a double-precision floating-point number.

Listing 9.15: badfloatcheck.cpp

```cpp
#include <iostream>

using namespace std;

int main() {
    // Count to ten by tenths
    for (double i = 0.0; i != 1.0; i += 0.1)
        cout << "i = " << i << endl;
}
```

When compiled and executed, Listing 9.15 (badfloatcheck.cpp) begins as expected, but it does not end as expected:

![](img/e326304bd50bc4f7d5a64148eb635_223_0.png)

Ctrl-C to stop when the loop variable `i` equals 1, but the program continues executing until the user types We are adding 0.1, just as in Listing 9.14 (simpleaddition.cpp), but now there is a problem. Since 0.1 cannot be represented exactly within the constraints of the double-precision floating-point representation, the repeated addition of 0.1 leads to round errors that accumulate over time. Whereas 0.1+0.9 rounded off may, 0.1 added 10 times may be 1.000001 or 0.999999, neither of which is exactly 1.

Listing 9.15 (badfloatcheck.cpp) demonstrates that the `==` and `!=` operators are questionable when comparing floating-point values. The better approach is to check if two floating-point values are close enough, which means they differ by a very small amount. When comparing two floating-point numbers `x` and `y`, we must determine if the absolute value of their difference is small; for example, $|x-y| < 0.00001$. The `abs` function was introduced in Section 8.2, and we can incorporate it into a function, as shown in Listing 9.16 (floatequals.cpp).

Listing 9.16: floatequals.cpp

```cpp
#include <iostream>
#include <cmath>

using namespace std;
```

```cpp
/*
 * equals(a, b, tolerance)
 * Returns true if a = b or |a - b| < tolerance.
 * If a and b differ by only a small amount
 * (specified by tolerance), a and b are considered
 * "equal." Useful for floating-point
 * round-off error.
 * The == operator is checked first since some special
 * floating-point values such as HUGE, VAL require an
 * exact quality check.
 */
bool equals(double a, double b, double tolerance) {
    return a == b || fabs(a - b) < tolerance;
}

int main() {
    for (double i = 0; i <= 1.0; i += 0.1) {
        cout << "i = " << i << endl;
    }
}
```

The third parameter, named `tolerance`, explains how the first two parameters must be in order to be considered. The `==` operator must be used for some special floating-point values as HUGE, VAL, the function checks for equality as well. C++ uses short-circuit evaluation for Boolean expressions involving OR (see Section 5.2), if the `==` operator indicates equality, the elaborate check is not performed.

You should use a function like `equals` when comparing two floating-point values for quality.

### 9.4.7 Multiplication Table with Functions

When last visited our multiplication table program in Listing 7.5 (timetable.cpp), we used nested loops to display a user-specified size. We can decompose the code into functions as shown in Listing 9.17 (timetablefunction.cpp). Our goal is to have a collection of functions that are very simple. We also want the program's overall structure to be logically organized.

```cpp
Listing 9.17: timetablefunction.cpp
#include <iostream>
#include <iomanip>

using namespace std;

// Print the column labels for an n x n multiplication table.
void col_numbers(int n) {
    cout << " ";
    for (int col = 1; col <= n; col++) {
        cout << setw(4) << col << " //"; // Printing header for this column.
    }
    cout << endl;
}

// Print the table's horizontal line at the top of the table
// beneath the column labels.
void col_line(int n) {
```

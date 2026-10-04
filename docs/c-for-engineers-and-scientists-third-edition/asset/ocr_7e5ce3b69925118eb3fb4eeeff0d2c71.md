# Program 5.14

```
#include <iostream>
#include <iomanip>
#include <cmath>
using namespace std;

int main() {
    int x, y;

    cout << "x value    y value\n";
    cout << "      ------\n";
n    for (x = 2; x <= 6; x++) {
        y = 10 * pow(x, 2.0) + 3 * x - 2;
        cout << setw(4) << x
             << setw(11) << y << endl;
    }

    return 0;
}
```

The following is displayed when Program 5.14 is executed:

| x value | y value |
|--- |---|
| 2 | 44 |
| 3 | 97 |
| 4 | 170 |
| 5 | 263 |
| 6 | 376 |

Two items are important here. First, any equation with one unknown can be evaluated using a single for or an equivalent while loop. This method requires substituting your variable in the loop in place of the equation used in Program 5.14 and adjusting the counter values to match the solution you want.

Second, you are not constrained to using integer values for the counter variable. For example, by specifying a non-integer increment, solutions for fractional values can be obtained. This technique is shown in Program 5.15, where the equation y = 10x^2 + 3x - 2 is evaluated in the range x = 2 to 6 in increments of 0.5.
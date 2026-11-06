After two days of thinking, it becomes obvious! You had just forgotten to enclose a + b inside parentheses; thus, only the variable b was divided by 2. Click on the “Finish Debugger Session” toolbar icon, remove all breakpoints, correct the error by enclosing a + b inside parentheses and you are ready! Re-execute the program and see now that it calculates and displays the average value correctly.

> **Notice:** You can remove a breakpoint the same way you added it: click in the left gray margin on the corresponding line number, or place the cursor at the line that contains a breakpoint and hit the CTRL+F8 key combination.

# 9.5 Review Exercises

Complete the following exercises.

+   1. Type the following C++ program into the NetBeans IDE and execute it step by step. Determine why it doesn’t calculate correctly the sum of 1 + 3 + 5.

```
```cpp
#include <iostream>
using namespace std;
int main() {
    int SS, S1, S3, S5, S;

    SS = 0;
    S1 = 1;
    S3 = 3;
    S5 = 5;

    S = S1 + S3 + SS;

    cout << S;
    return 0;
}
```
```

+   2. Create a trace table to determine the values of the variables in each step of the C++ program for two different executions. Then, type the program in the NetBeans IDE, execute it step by step, and confirm the results.

The input values for the two executions are: (i) 5, 5; and (ii) 4, 8.

```
```cpp
#include <iostream>
using namespace std;
int main() {
    double a, b, c, d, e;

    cin >> a;
    cin >> b;

    c = a + b;
    d = 5 + a / b * c + 2;
    e = c - d;
    c -= d + c;
```
```
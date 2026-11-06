# ## 8.2 Review Questions: True/False

Choose **true or false** for each of the following statements.

+   1. A trace table is a technique for testing a computer.
+   2. Trace tables help a programmer find errors in a computer program.
+   3. You cannot write a computer program without first creating its corresponding trace table.
+   4. In order to swap the values of two integer variables, you always need an extra variable.

# ## 8.3 Review Exercises

Complete the following exercises.

+   1. Create a trace table to determine the values of the variables in each step of the C++ program for three different executions.
+      The input values for the three executions are: (i) 3, (ii) 4, and (iii) 1.

```
~~~cpp
#include <iostream>
using namespace std;
int main() {
    int a, b, c, d;

    cin >> a;

    a = (a + 1) * (a + 1) + 6 / 3 * 2 + 20;
    b = a % 13;
    c = b % 7;
    d = a * b * c;
    cout << a << ", " << b << ", " << c << ", " << d;
    return 0;
}
~~~
```

+   2. Create a trace table to determine the values of the variables in each step of the C++ program for two different executions.
+      The input values for the two executions are: (i) 3, 4; and (ii) 4, 4

```
~~~cpp
#include <iostream>
using namespace std;
int main() {
    double a, b, c, d, e;

    cin >> a;
    cin >> b;

    c = a + b;
    d = 1 + a / b * c + 2;
    e = c + d;
    c += d + e;
}
~~~
```
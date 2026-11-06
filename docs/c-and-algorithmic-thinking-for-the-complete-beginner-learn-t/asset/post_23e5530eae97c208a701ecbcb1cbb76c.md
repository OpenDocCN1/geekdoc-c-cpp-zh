
7. What displays on screen after executing each of the following code fragments?

   i.
   ```cpp
   a = 5;
   b = 2;
   c = a * ++b;
   d = b % (a + b);
   cout << c;
   cout << " " << d << endl;
   ```

   ii.
   ```cpp
   a = 0.4;
   b = 8;
   a += 0.1;
   c = a * b % b;
   cout << c << endl;
   ```

8. Calculate the result of the expression `a % b` for the following cases.

   i. `a = 20, b = 3`    iv. `a = 0, b = 3`
   ii. `a = 15, b = 3`    v. `a = 3, b = 0`
   iii. `a = 22, b = 3`   vi. `a = 2, b = 2`

9. Calculate the result of the expression

   `b * (a % b) + a / b`

   for each of the following cases.

   i. `a = 10, b = 5`    ii. `a = 10, b = 4`

10. What displays on the screen after executing the following code fragment?

```cpp
a = "My name is";
a += " ";
a = a + "George Malkovich";
cout << a << endl;
```

11. Fill in the gaps in each of the following code fragments so that they display a value of 5.

    i.
    ```cpp
    a = 2;
    a = a _____ ;
    cout << a << endl;
    ```

    ii.
    ```cpp
    a = 4;
    b = a * 0.5;
    b += a;
    a = b - _____ ;
    cout << a << endl;
    ```

12. What displays on the screen after executing the following code fragment?

```cpp
city = "California";
California = city;
cout << city << " " << California << endl;
```

| Step | Statement | Notes |  |  |  |
|---|---|---|---|---|---|
|  |  | assigned to z. |  |  |  |
| 4 | `z++` | Variable z is incremented by one. | 10 | 15 | **151** |
| 5 | `cout << z` | The value 151 is displayed. |  |  |  |

## Exercise 8.1-1 — Creating a Trace Table

What result is displayed when the following program is executed?

```cpp
#include <iostream>
using namespace std;
int main() {
  string Ugly, Beautiful, Handsome;

  Ugly = "Beautiful";
  Beautiful = "Ugly";
  Handsome = Ugly;
  cout << "Beautiful";
  cout << Ugly;
  cout << Handsome;
  return 0;
}
```

### Solution

Let’s create a trace table to find the output result.

| Step | Statement | Notes | Ugly | Beautiful | Handsome |
|---|---|---|---|---|---|
| 1 | `Ugly = "Beautiful"` | The string “Beautiful” is assigned to the variable Ugly. | **Beautiful** | ? | ? |
| 2 | `Beautiful = "Ugly"` | The string “Ugly” is assigned to the variable Beautiful. | Beautiful | **Ugly** | ? |
| 3 | `Handsome = Ugly` | The value of variable Ugly is assigned to the variable Handsome. | Beautiful | Ugly | **Beautiful** |
| 4 | `cout << "Beautiful"` | The string “Beautiful” is displayed. |  |  |  |
| 5 | `cout << Ugly` | The string “Beautiful” is displayed. |  |  |  |
| 6 | `cout << Handsome` | The string “Beautiful” is displayed. |  |  |  |

## Exercise 8.1-2 — Swapping Values of Variables

Write a C++ program that lets the user enter two values, in variables *a* and *b*. At the end of the program, the two variables should swap their values. For example, if variables *a* and *b* contain the values 5 and 7 respectively, after swapping their values, variable *a* should contain the value 7 and variable *b* should contain the value 5!

### Solution

The following program, even though it may seem correct, is erroneous and doesn’t really swap the values of variables *a* and *b*!

```cpp
#include <iostream>
using namespace std;
int main() {
  int a, b;

  cin >> a;
  cin >> b;

  a = b;
  b = a;

  cout << a << endl;
  cout << b << endl;
  return 0;
}
```

Let’s see why! Suppose the user enters two values, 5 and 7. The trace table is shown here.

| Step | Statement | Notes | a | b |
|---|---|---|---|---|
| 1 | `cin >> a` | User enters the value 5 | 5 | ? |
| 2 | `cin >> b` | User enters the value 7 | 5 | 7 |
| 3 | `a = b` | The value of variable b is assigned to variable a. Value 5 is lost! | 7 | 7 |
| 4 | `b = a` | The value of variable a is assigned to variable b | 7 | 7 |
| 5 | `cout << a << endl` | The value 7 is displayed |  |  |
| 6 | `cout << b << endl` | The value 7 is displayed |  |  |

Oops! Where is the value 5?

The solution wasn’t so obvious after all! So, how do you really swap values anyway?

Consider two glasses: a glass of orange juice (called glass A), and a glass of lemon juice (called glass B). If you want to swap their content, all you must do is find and use one extra empty glass (called glass C).

![](img/7b41666e32fdead550ef74cdd9f6ead0_87_0.png)

The steps that must be followed are:

1. Empty the contents of glass A (orange juice) into glass C.

![](img/7b41666e32fdead550ef74cdd9f6ead0_87_1.png)

2. Empty the contents of glass B (lemon juice) into glass A.

![](img/7b41666e32fdead550ef74cdd9f6ead0_87_2.png)

3. Empty the contents of glass C (orange juice) into glass B.

![](img/7b41666e32fdead550ef74cdd9f6ead0_87_3.png)

Swapping completed successfully!

You can follow the same steps to swap the contents of two variables in C++.

```cpp
#include <iostream>
using namespace std;
int main() {
  int a, b, c;

  cin >> a;
  cin >> b;

  c = a;  //Empty the contents of glass A (orange juice) into glass C
  a = b;  //Empty the contents of glass B (lemon juice) into glass A
  b = c;  //Empty the contents of glass C (orange juice) into glass B

  cout << a << endl;
  cout << b << endl;
  return 0;
}
```

> **Notice:** Please note the double slashes after each of the three assignment statements. What follows after double slashes is considered a comment and is never executed.

## Exercise 8.1-3 — Swapping Values of Variables – A Second Approach

Write a C++ program that lets the user enter two numeric values, in variables a and b. In the end, the two variables should swap their values.

### Solution

Since the variables contain only numeric values, you can use the following C++ program.

```cpp
#include <iostream>
using namespace std;
int main() {
  int a, b;

  cin >> a;
  cin >> b;

  a = a + b;
  b = a - b;
  a = a - b;

  cout << a << endl;
  cout << b << endl;
  return 0;
}
```

> **Notice:** Compared to previous exercise, the only major disadvantage of this method is that it cannot swap the contents of alphanumeric variables (strings).

| Step | Statement | Notes | a | b | c |
|---|---|---|---|---|---|
| 2 | `c = 3` |  | ? | 10 | 3 |
| 3 | `c = c * b` |  | ? | 10 | 30 |
| 4 | `a = 10 * c % 10` |  | 0 | 10 | 30 |
| 5 | `cout << a` | The value 0 is displayed |  |  |  |

## Exercise 8.1-5 — Creating a Trace Table

Create a trace table to determine the values of the variables in each step when a value of 3 is entered.

```cpp
#include <iostream>
using namespace std;
int main() {
  double a, b, c, d;

  cin >> a;

  b = a + 10;
  a = b * (a - 3);
  c = 3 * b / 6;
  d = c * c;
  d--;

  cout << d;
  return 0;
}
```

### Solution

For the input value of 3, the trace table looks like this.

| Step | Statement | Notes | a | b | c | d |
|---|---|---|---|---|---|---|
| 1 | `cin >> a` | User enters value 3 | 3 | ? | ? | ? |
| 2 | `b = a + 10` |  | 3 | 13 | ? | ? |
| 3 | `a = b * (a - 3)` |  | 0 | 13 | ? | ? |
| 4 | `c = 3 * b / 6` |  | 0 | 13 | 6.5 | ? |
| 5 | `d = c * c` |  | 0 | 13 | 6.5 | 42.25 |
| 6 | `d--` |  | 0 | 13 | 6.5 | 41.25 |
| 7 | `cout << d` | The value 41.25 is displayed |  |  |  |  |

## 8.2 Review Questions: True/False

Choose **true or false** for each of the following statements.

1. A trace table is a technique for testing a computer.
2. Trace tables help a programmer find errors in a computer program.
3. You cannot write a computer program without first creating its corresponding trace table.
4. In order to swap the values of two integer variables, you always need an extra variable.

## 8.3 Review Exercises

Complete the following exercises.

1. Create a trace table to determine the values of the variables in each step of the C++ program for three different executions.
   The input values for the three executions are: (i) 3, (ii) 4, and (iii) 1.

   ```cpp
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
   ```

2. Create a trace table to determine the values of the variables in each step of the C++ program for two different executions.
   The input values for the two executions are: (i) 3, 4; and (ii) 4, 4

   ```cpp
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
   ```

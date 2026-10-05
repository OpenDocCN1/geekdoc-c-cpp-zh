
C++ implements pass by reference two different ways: via pointer parameters and reference parameters. The C programming language supports pass by reference only with pointer parameters.

You should use pass by reference when a function would need to return more than one result. Since a function can return only one value, multiple variables can be passed by reference to a function, and the function can modify their values directly.

Higher-order functions accept other functions as parameters and may return functions as results.

Higher-order functions enable programmers to develop highly flexible functions with pluggable functionality.

## 10.11 Exercises

1. Consider the following C++ code:

```cpp
#include <iostream>

using namespace std;

int sum1(int n) {
    int s = 0;
    while (n > 0) {
        s++;
        n--;
    }
    return s;
}

int input;

int sum2() {
    int s = 0;
    while (input > 0) {
        s++;
        input--;
    }
    return s;
}

int sum3() {
    for (int i = input; i > 0; i--) {
        s++;
    }
    return s;
}

int main() {
    // See each question below for details
}
```

## 10.11. EXERCISES

(a) What is printed if main is written as follows?

```cpp
int main() {
    input = 5;
    cout << sum1(input) << endl;
    cout << sum2(input) << endl;
    cout << sum3(input) << endl;
}
```

(b) What is printed if main is written as follows?

```cpp
int main() {
    input = 5;
    cout << sum1(input) << endl;
    cout << sum3(input) << endl;
    cout << sum2() << endl;
}
```

(c) What is printed if main is written as follows?

```cpp
int main() {
    input = 5;
    cout << sum2(input) << endl;
    cout << sum1(input) << endl;
    cout << sum3(input) << endl;
}
```

(d) Which of the functions sum1, sum2, and sum3 produce a side effect? What is side effect?
(e) Which function may not use input?
(f) What is the scope of variable i? What is its lifetime?
(g) What is the scope of i?
(h) Which of the functions sum1, sum2, and sum3 manifest functional independence? Why?

2. Consider the following C++ code:

```cpp
#include <iostream>

using namespace std;

int next_int1() {
    static int cnt = 0;
    cnt++;
    return cnt;
}

int next_int2() {
    int cnt = 0;
    cnt++;
    return cnt;
}

int global_count = 0;

int next_int3() {
    global_count++;
    return global_count;
}

int main() {
    for (int i = 0; i < 5; i++)
        cout << next_int1() << " "
             << next_int2() << " "
             << next_int3() << endl;
}
```

(a) What does the program print?
(b) Which of the functions next_int1, next_int2, and next_int3 is the best function for intended purpose? Why?
(c) What is a better name for function next_int2?
(d) The next_int3 function works in this context, but why is it not a good implementation of always returns integer?

3. The following C++ program is split over three files. The first file, counter.h, consists of:

```cpp
int read();
int increment();
int decrement();
```

The second file, counter.cpp, contains:

```cpp
int read() {
    return count;
}

int increment() {
    if (count < 5)
        count++;
}

int decrement() {
    if (count > 0)
        count--;
}
```

The third file, main.cpp, is incomplete:

```cpp
#include <iostream>
#include "counter.h"

using namespace std;

int main() {
    // Add code here
}
```

(a) Add statements to main to enable it to produce the following output: ![img/e32630bd50fbc4d75a6418eb635_277_0.png] The restriction is that the only output statement you are allowed to use (three times) is:

```cpp
cout << read(2) << endl;
```

(b) Under the restriction of using the same output above, what code could you add to main so that it would produce the following output? ![img/e32630bd50fbc4d75a6418eb635_277_1.png]

4. Consider the following C++ code:

```cpp
#include <iostream>

using namespace std;

int max(int n) {
    return n;
}

int max(int m, int n) {
    return (m >= n) ? m : n;
}

int max(int m, int n, int r) {
    int x = m;
    if (n > x)
        x = n;
    if (r > x)
        x = r;
    return x;
}

int main() {
    cout << max(4) << endl;
    cout << max(4, 5) << endl;
    cout << max(5, 4) << endl;
    cout << max(1, 2, 3) << endl;
    cout << max(2, 1) << endl;
    cout << max(2, 1, 2) << endl;
}
```

(a) Is the program legal since there are three functions named max?
(b) What does the program print?

5. Consider the following function:

```cpp
int proc(int n) {
    if (n < 1)
        return 1;
    else
        return proc(n/2) + proc(n - 1);
}
```

Evaluate each of the following expressions:

(a) proc(0)
(b) proc(1)
(c) proc(2)
(d) proc(3)
(e) proc(5)
(f) proc(10)

6. Rewrite the gcd function so that it implements Euclid's method but uses iteration instead of recursion.

7. If x is a variable, how would you determine its address in the computer's memory?

8. What is printed by the following code fragment?

```cpp
int x = 5, y = 3, *p = &x, *q = &y;
cout << "x = " << x << ", y = " << y << endl;
x = y;
cout << "x = " << x << ", y = " << y << endl;
x = 7;
cout << "x = " << x << ", y = " << y << endl;
p = 10;
cout << "x = " << x << ", y = " << y << endl;
q = 20;
*p = 20;
cout << "x = " << x << ", y = " << y << endl;
```

9. Given the declarations:

```cpp
int x, y, *p, *q;
```

indicate what of the following code fragments will print:

(a)
p = &x;
x = 5;
cout << *p << endl;

(b)
x = 5;
p = &x;
cout << *p << endl;

(c)
p = &x;
*p = 8;
cout << *p << endl;

(d)
p = &x;
q = &y;
x = 100;
y = 200;
*q = *p;
cout << "x = " << x << ", y = " << y << endl;

(e)
p = &x;
q = &y;
x = 100;
y = 200;
*q = p;
cout << "x = " << x << ", y = " << y << endl;

(f)
p = &x;
q = &y;
x = 100;
y = 200;
*p = *q;
cout << "x = " << x << ", y = " << y << endl;

10. The following function does not behave as expected:

```cpp
/*
 * Faulty function
 * get_range
 * Establishes a range of integers. The lower value must
 * be greater than equal to min, and the upper value
 * must be less than equal to max.
 * min is the lowest acceptable value.
 * max is the highest upper value.
 * lower is assigned the lower of the range
 */
void get_range(int min, int max, int lower, int upper) {
    cout << "Please enter a range within the bounds " << min << " " << max << ":";
    do { // Loop until acceptable values are provided
        cin >> lower >> upper;
        if (lower < min) {
            cout << lower << " is too low, please try again." << endl;
        }
        if (upper > max) {
            cout << upper << " is too high, please try again." << endl;
        }
    } while (lower < min || upper > max);
}
```

(a) Modify the function so that it works using pointers.
(b) Modify the function so that it works using reference parameters.

11. Classify the following as pure or impure. x is a global variable and LIMIT is a global constant.

(a) int f1(int m, int n) {
    return 2*m + 3*n;
}

(b) int f2(int n) {
    return n - LIMIT;
}

(c) int f3(int n) {
    return n - x;
}

(d) void f4(int n) {
    cout << 2*n << endl;
}

(e) int f5(int n) {
    int m;
    cin >> m;
    return m * n;
}

(f) int f6(int n) {
    int m = 2*n, p;
    p = 2*m - 5;
    return p - n;
}

## Chapter 11

## Aggregate Data

The variables we have used to create this point assume only one value at a time. As we have seen, we can use individual variables to create interesting and useful programs; however, variables that can represent only one value at a time have their limitations. Consider Listing 11.1 (avernumbers.cpp) which averages five numbers entered by the user.

Listing 11.1: avernumbers.cpp

```cpp
#include <iostream>

using namespace std;

int main() {
    double n1, n2, n3, n4, n5;
    cout << "Please enter five numbers: ";
    // Allow the user to enter the five values.
    cin >> n1 >> n2 >> n3 >> n4 >> n5;
    cout << "The average of " << n1 << ", " << n2 << ", " << n3 << ", " << n4 << ", " << n5 << " is " << (n1 + n2 + n3 + n4 + n5)/5 << endl;
}
```

A sample run of Listing 11.1 (avernumbers.cpp) looks like:

```
Please enter five numbers: 9 3.5 0.2 100 15.3
The average of 5.0, 3.5, 0.2, 100.0, 15.3 is 25.6
```

The program conveniently displays the values the user entered and computes and displays their average.

Suppose the number of values to average must increase from 25. If we use Listing 11.1 (avernumbers.cpp) as a guide, twenty additional variables must be introduced, and the overall length of the program will miserably growing. Averaging 1,000 numbers using this approach is impractical.

Listing 11.2 (avernumbers2.cpp) provides an alternative approach for averaging numbers.

value of denominator is less than a small value. Similarly, if we wanted to know whether y was close to the value 10.5, we should use a condition such as fabs (y - 10.5) <= 0.0001 instead of y == 10.5. In general, do not use the equality operator with floating-point values.

![](bbox=[0.13, 0.1, 0.19, 0.22])

A second caution is necessary when using the equality operator (==) with integers. A common error is to use the assignment operator (=) instead of the logical operator (==). Consider the following C++ program:

```
#include<iostream>
using namespace std;
int main()
{
int x(4), y(5);
if(x = y)
{
cout << x << " is equal to " << y << endl;
}
return 0;
}
```

The above program compiles and executes without any error messages from the compiler or the operating system, and the output from the program is:

5 is equal to 5

This bug is the result of using the assignment operator instead of the equality operator to form the condition in the if statement. An assignment of y to x is made and since y is not zero (i.e. y is not false), the assignment statement evaluates to true and the cout statement inside the if statement block is executed. If y were initialized to 0 instead of 5, the statement block would not be executed. Virtually every programmer makes this programming error more than once, so if your program output is not what you expect it to be, check all conditions that are intended to use the equality operator.

# Practice 3.2

In Problems 1 through 7, draw a flowchart to perform the steps indicated. Then give the corresponding C++ statements. Assume that the objects have been declared and have reasonable values.

+   1. If time is greater than 15.0, increment time by 1.0.
+   2. When the square root of poly is less than 0.5, print the value of poly.
+   3. If the difference between volt_1 and volt_2 is larger than 10.0, print the values of volt_1 and volt_2.
+   4. If the value of den is less than 0.05, set result to zero; otherwise, set result equal to num divided by den.
+   5. If the natural logarithm of x is greater than or equal to 3, set time equal to zero and decrement count.
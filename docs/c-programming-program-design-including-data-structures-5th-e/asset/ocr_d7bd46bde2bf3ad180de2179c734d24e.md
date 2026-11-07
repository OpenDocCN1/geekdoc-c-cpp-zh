45. What is the output of the following code?

```
int num = 12;
while (num > 0)
{
    if (num % 5 == 0)
    {
        num++;
        continue;
    }
    cout << num << " ";
    num /= 2;
}
cout << endl;
```

46. What does a break statement do in a loop?

# PROGRAMMING EXERCISES

+   1. Write a program that prompts the user to input an integer and then outputs both the individual digits of the number and the sum of the digits. For example, if the input is 3456, output the individual digits of 3456 is 3 4 5 6, output the individual digits of 8030 is 8 0 3 0, output the individual digits of 234556 is 2 3 4 5 5 6, output the individual digits of 4000 is 4 0 0 0, and output the individual digits of -2345 is -2 3 4 5.

+   2. The value of π can be approximated by using the following series:

$$\pi = 4\left(1 - \frac{1}{3} + \frac{1}{5} - \frac{1}{7} + \cdots\right)$$

The following program uses this series to find the approximate value of π. However, the statements are in the incorrect order, and there is also a bug in this program. Rearrange the statements and also find and remove the bug so that this program can be used to approximate π.

```
#include <iostream>
#include <iomanip>

using namespace std;

int main()
{
    double pi = 0;
    long n;
    long max;

    cin >> n;
    cout << "Enter the value of n: ";
    cout << endl;
}
```

> Programming Exercises challenge students to write C++ programs with a specified outcome.
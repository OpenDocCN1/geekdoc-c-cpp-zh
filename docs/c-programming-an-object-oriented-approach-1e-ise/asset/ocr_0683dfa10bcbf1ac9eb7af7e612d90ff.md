![](bbox=[0.4, 0.089, 0.71, 0.151])

**Figure 2.5** Variables in memory and their definition in a program

# EXAMPLE 2.1

Figure 2.5 shows three variables with their types and names. The figure also shows how we define them to ensure that the compiler will know the variable to which we are referring.

We have not discussed data types yet, but we specify that all three data types are integer types (which cannot represent a whole number without fractions), such as 17, 35, 100, and so on, but not 23.67.

# 2.2.2 Values

The contents of a variable are referred to as its **value**. For example, if `num1` at this moment holds the integer 17, its value is 17. When we use the name of a variable in a program, sometimes we mean the variable itself, sometimes the value it holds. The next example shows the difference.

# EXAMPLE 2.2

Assume we want to write a program that accepts any two whole numbers, adds them together, and displays the result. While we have not studied data types yet, we understand that the two numbers and the result are integer types (int in C++). To store the two numbers and the result of the addition, we need to give them names. We call them **num1**, **num2**, and **sum**, respectively. We then write a program that, each time it runs, finds the sum of two numbers entered at the keyboard and prints them (Program 2.3).

# **Program 2.3**  A program that adds two values

```
```cpp
/**************************************************************
 * This program gets the values for two numbers from the keyboard, *
 * adds them together and prints the result on the monitor.       *
 **************************************************************/
#include <iostream>
using namespace std;

int main()
{
    // Definition
    int num1;
    int num2;
    int sum;
    // Getting inputs
    cout << "Enter the first number: ";
```
```

(continued)
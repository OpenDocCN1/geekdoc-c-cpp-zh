
8. (Numerical) For small values of x, the value of sin(x) can be approximated by the point series:

$x-\frac{x^3}{3!} +\frac{x^5}{5!} -\frac{x^7}{7!} +...$$

As the sin( ) function, the value of x must be in radians. Using this point series, write, compile, and execute a C++ program that approximates the sine of 180/3.1416 degrees, which equals one radian. Additionally, have your program use the sin( ) function to calculate the sine and display both calculated values and the absolute difference of the results. Manually verify the approximation your program produces. After verifying that your program is working correctly, use it to approximate the value of the sine of 62.2 degrees.

9. (Conversion) The polar coordinates of a point of the distance, $r$, from a specified origin and an angle, $\theta$, with respect to the x-axis. The point's x and y coordinates are related to its polar coordinates by these formulas:

```
$x = r\cos\theta$
$y = r\sin\theta$
```

Using these formulas, write a C++ program to calculate the x and y coordinates of a point with the polar coordinates $r=10$ and $\theta=30$ degrees. Verify your program produces by calculating the results manually. After verifying that your program is working correctly, use it to convert the polar coordinates $r=12.5$ and $\theta=67.8$ degrees in rectangular coordinates.

10. (Ecology) A model of worldwide population growth, in billions of people, since 2000 is given by this formula:

```
$Population = 6.0\cdot e^{0.0201t}$
```

Using this formula, write, compile, and execute a C++ program to estimate the worldwide population in the year 2012. Verify the result your program produces by calculating the answer manually. After verifying that your program is working correctly, use it to estimate the world's population in the year 2019.

11. (Physics) A model to estimate the number of grams of a radioactive left after $t$ years is given by this formula:

```
$remaining\_amount = (original\_amount)\cdot e^{0.00012t}$
```

Using this formula, write, compile, and execute a C++ program to determine the amount of radioactive material after 100 years, assuming an initial of 100 grams. Verify the display your program produces by using a hand calculation. After verifying that your program is working correctly, use it to determine the amount of radioactive material remaining after 275 years, assuming an initial of 250 grams.

12. (Physics) The number of years it takes for an isotope of uranium to decay to one-half of an original amount is given by this formula, $\lambda$, the decay constant (which is equal to the inverse of mean life), 0.000012.

```
$half-life = ln(2)/\lambda$
```

Using this formula, write, compile, and execute a C++ program that calculates and displays the half-life of your uranium isotope. Verify your program produces by using a hand calculation. After verifying that your program is working correctly, use it to determine the half-life of a uranium isotope with $\lambda=0.00026$.

## 3.4 Program Input Using cin

Data for programs that are going to be executed only once can be included in the program. For example, if you want to multiply the numbers 30.0 and 0.05, you could use Program 3.10.

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_158_0.png)

## Program 3.10

```cpp
#include <iostream>
using namespace std;

int main()
{
    double num1, num2, product;

    num1 = 30.0;
    num2 = 0.05;
    product = num1 * num2;
    cout << "30.0 times 0.05 is " << product << endl;

    return 0;
}
```

Program 3.10 produces this output:
  30.0 times 0.05 is 1.5

Program 3.10 can be shortened, as shown in Program 3.11. Both programs, however, suffer from the same problem: They must be rewritten to multiply different numbers. Both programs lack the capability to enter different numbers on which to operate.

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_158_1.png)

## Program 3.11

```cpp
#include <iostream>
using namespace std;

int main()
{
    cout << "30.0 times 0.05 is " << 30.0 * 0.05 << endl;

    return 0;
}
```

## Assignment, Formatting, and Interactive Input

Except for the programming practice provided by writing, entering, and running the program, programs that do only once, on the same set of numbers, clearly aren't very useful. After all, using a calculator to multiply two numbers is simpler than entering and running Program 3.10 or 3.11.

This section explains the cin statement. The cin statement allows the user to provide data from the keyboard while the program is running. This makes programs much more interactive and useful. To use cin, you use the extraction operator `>>` with a variable that will store the input. For example:

```cpp
int x;
cin >> x;
cout << "You entered: " << x << endl;
```

The cin statement can be used to read multiple values in one line. For example:

```cpp
int x, y;
cin >> x >> y;
```

This allows the user to enter multiple values separated by spaces or newlines. The program will continue reading values until all the variables are filled.

It is important to note that the type of input must match the type of the variable. If a user enters a string when an integer is expected, the program will encounter an error. This is a common issue in input validation in C++.

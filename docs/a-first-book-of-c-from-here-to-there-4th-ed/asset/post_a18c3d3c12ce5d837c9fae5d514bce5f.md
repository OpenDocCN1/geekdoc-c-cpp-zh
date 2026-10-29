
Using this information, write, compile, and run a C++ program that determines the volume of oil in a 200-foot tank that has a radius of 10 feet and measures 12 feet from the top of the tank to the top of the oil. Your program should display the radius, distance from the top of the tank to the oil, and the calculated volume.

## 6. (Program) The circumference of an ellipse (review Figure 3.4) is given by this formula:

Circumference = π√(a + b)²

Using this formula, write a C++ program to calculate the circumference of an ellipse with a minor radius, a, of 2.5 inches and a major radius, b, of 6.4 inches.

## 7. (Program) Write, compile, and run a C++ program to calculate the distance between two points with the coordinates (7, 12) and (3, 9). Use the fact that the distance between two points with the coordinates (x₁, y₁) and (x₂, y₂) is given by this formula:

distance = √((x₂ - x₁)² + (y₂ - y₁)²)

After verifying that your program works correctly by calculating the distance between the two points manually, use your program to determine the distance between the points (-12, -15) and (22, 5).

## 8. (Program) If a 20-foot ladder is placed on the side of a building at a 85-degree angle, as shown in Figure 3.9, the height at which the ladder touches the building can be calculated as height = 20 × sin 85°. Calculate this height by hand, and then write, compile, and run a C++ program that determines and displays the value of the height. After verifying that your program works correctly, use it to determine the height of a 25-foot ladder placed at an angle of 85 degrees.

![](img/e9bf940282dfb289356f077151cc69dd_132_0.png)

Figure 3.9 Calculating the height of a ladder against a building

## 9. (Program) The maximum height reached by a ball thrown with an initial velocity, v, in meters/sec, at an angle of θ is given by this formula:

height = (.5 x v² x sin² θ) / 9.8

Using this formula, write, compile, and run a C++ program that determines and displays the maximum height reached when the ball is thrown at 5 mph at an angle of 60 degrees. (Hint: Make sure to convert the initial velocity into the correct units. There are 1609 meters in a mile.) Calculate the maximum height manually, and verify the result your program produces. After verifying the result, use your program to determine the height reached by a ball thrown at 7 mph at an angle of 45 degrees.

## 10. (Program) A model of worldwide population growth, in billions of people, since 2000 is given by this formula:

Population = 7.5 e^0.02[Year - 2010]

Using this formula, write, compile, and run a C++ program to estimate the worldwide population in the year 2012. Verify the result your program produces by calculating the answer manually, and then use your program to estimate the world's population in the year 2020.

## 11. (Program) The roads of Kansas are laid out in a rectangular grid at exactly one-mile intervals, as shown in Figure 3.10. Farmer Pete drives his 1939 Ford pickup x miles east and y miles north to get to farmer Joe's farm. Both x and y are integer numbers. Using this information, write, test, and run a C++ program that prompts the user for the values of x and y, and then uses this formula to find the shortest driving distance across the fields to Joe's farm:

distance = sqrt(x² + y²);

Round the answer to the nearest integer value before it's displayed.

## 12. (Program) A model to estimate the number of grams of a radioactive isotope left after t years is given by this formula:

remaining material = (original material) e^(-0.00021t)

Using this formula, write, compile, and run a C++ program to determine the amount of radioactive material remaining after 1000 years, assuming an initial amount of 100 grams. Verify the display your program produces by using a hand calculation. After verifying that your program is working correctly, use it to determine the amount of radioactive material remaining after 275 years, assuming an initial amount of 250 grams.

## Figure 3.10 Illustration for Exercise 11

## 13. (Program) The number of years it takes for an isotope of uranium to decay to one-half an original amount is given by this formula, where λ, the decay constant (which is equal to the inverse of the mean lifetime), equals 0.00012:

```
half-life = ln(2) / λ
```

Using this formula, write, compile, and run a C++ program that calculates and displays the half-life of this uranium isotope. Verify the result your program produces by using a hand calculation. After verifying that your program is working correctly, use it to determine the half-life of a uranium isotope with λ = 0.00026.

## 14. (Program) a. Appendix B lists the integer values corresponding to each letter stored with the ASCII code. Note that uppercase letters consist of contiguous codes, starting with an integer value of 65 for the letter A and ending with 90 for the letter Z. Similarly, lowercase letters begin with the integer value of 97 for the letter a and end with 122 for the letter z. With this information as background, determine the character value of the expressions char ('A' + 32) and char ('Z' + 32).

b. Using Appendix B, determine the integer value of the expression 'a' - 'A'.

c. Using the results of Exercises 14a and 14b, determine the character value of the following expression, where uppercase letter can be any uppercase letter from A to Z: char (uppercase letter + 'a' - 'A').

## 3.4 Interactive Keyboard Input

Data for programs to be run only once can be included in the program. For example, if you want to multiply the numbers 30.0 and 0.05, you could use Program 3.10.

## Program 3.10

```
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
```

This is the output displayed by Program 3.10:

    30.0 times 0.05 is 1.5

Program 3.10 can be shortened, as shown in Program 3.11. Both programs, however, suffer from the same basic problem: They must be rewritten to multiply different numbers. Neither program allows entering different numbers to operate on.

## Program 3.11

```
```cpp
#include <iostream>
using namespace std;

int main()
{

    cout << "30.0 times 0.05 is " << 30.0 * 0.05 << endl;

    return 0;
}
```
```

## Assignment and Interactive Input

Except for the programming practice you get by writing, entering, and running the program, programs that do the same calculation only once, on the same set of numbers, clearly aren't very useful. After all, using a calculator to multiply two numbers is simpler than entering and running Program 3.10 or Program 3.11.

This section explains the cin object, which is used to enter data in a program while it's running. Just as the cout object displays a copy of the value stored in a variable, the cin object allows the user to enter a value at the keyboard (see Figure 3.11). The value is then stored in a variable.

![](img/e9bf940282dfb289356f077151cc69dd_137_0.png)

**Figure 3.11**  cin is used to enter data; cout is used to display data

When a statement such as `cin >> num1;` is encountered, the computer stops program execution and accepts data from the keyboard. When a data item is typed, the cin object stores the item in the variable listed after the extraction (`<<get from>>`) operator, `>>`. The program then continues execution with the next statement after the call to cin. To see how this object works, take a look at Program 3.12.

## Program 3.12

```
```cpp
#include <iostream>
using namespace std;

int main()
{
    double num1, num2, product;

    cout << "Please type in a number: ";
    cin >> num1;
    cout << "Please type in another number: ";
    cin >> num2;
    product = num1 * num2;
    cout << num1 << " times " << num2 << " is " << product << endl;

    return 0;
}
```
```

The first cout statement in Program 3.12 prints a string that tells the person at the keyboard what should be typed. When an output string is used in this manner, it's called a **prompt**.

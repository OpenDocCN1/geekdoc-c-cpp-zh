
# Scope Rules 133

> TIP: (continued)

function definition and place a function call in the branch. Similarly, if a loop body is large, it is preferable to convert the compound statement to a function definition and make the loop body a function call.

# Variables Declared in a for Loop

A variable may be declared in the heading of a for statement so that the variable is both declared and initialized at the start of the for statement. For example,

```cpp
for (int n = 1; n < 10; n++)
sum = sum + n;
```

The ANSI/ISO C++ standard requires that a C++ compiler claims compliance with the standard treat any declaration in a for initializer as if it were to the body of the loop. Earlier C++ compilers did not do. You should determine how your compiler treats variables declared in a for initializer. If portability is critical to your application, you should not write code that depends on this behavior. Eventually, all widely used C++ compilers will likely comply with this, but compilers presently may or may not comply.

# Self-Test Exercise

25. We urge you not to program using this style, we are providing an exercise that uses nested blocks to help you understand the scope rules. State the output that this code fragment would produce in an otherwise complete, correct program.

```cpp
{
  int x = 1;
  cout << x << endl;
  cout << x << endl;
  int x = 2;
  cout << x << endl;
  {
    cout << x << endl;
    int x = 3;
    cout << x << endl;
  }
  cout << x << endl;
}
cout << x << endl;
}
```

# Chapter Summary

- There are two kinds of functions in C++: functions that return a value and void functions.

- A function should be defined so that it can be used as a black box. The programmer who uses the function should not need to know any details about how the function is coded. All the programmer should need to know the function declaration and the accompanying comment that describes the value returned. This rule is sometimes called the principle of procedural abstraction.

- A good way to write a function declaration comment is to use a precondition and a postcondition. The precondition states what is assumed to be true when the function is called. The postcondition describes the effect of the function call; that is, the postcondition tells what will be true after the function is executed in a situation with the precondition holds.

- A variable that is declared in a function definition is said to be local to the function.

- A formal parameter is a kind of placeholder that is filled in with a function argument when the function is called. The details on this “filling in” process are covered in Chapter 4.

# Answers to Self-Test Exercises

- 1. 4.0 4.0 8.0
8.0 8.0 1.21
3 3 0
3.0 3.5 3.5
6.0 6.0 5.0
5.0 4.5 4.5
3 3.0 3

- 2. a. sqrt (x + y)
b. pow(x, y + 7)
c. sqrt (area+time)/nobody
d. sqrt ((b ± sqrt(b*b - 4*a*c))/(2*a))
e. abs (x - y) or labs (x - y) or fabs (x - y)

```cpp
3. #include <iostream>
#include <cmath>
using namespace std;
int main()
{
    int i;
for (i = 1; i <= 10; i++)
cout << "The square root of " << i
cout << " is " << sqrt(i) << endl;
return 0;
}
```

- 4. The argument is given to the operating system. As far as your C++ program is concerned, you can use any value as the argument. By conversion, however, 1 is used for a call to exit that is caused by an error, and 0 is used in other cases.

- 5. (5 + (rand() % 6))

- 6. #include <iostream>
#include <cstdlib>
using namespace std;

int main() {

cout << "Enter a nonnegative integer to use as the \n"
<< "_seed for the random number generator: \n"
unsigned int seed;
cin >> seed;
srand(seed);

cout << "Here are ten random probabilities:\n"
int i;
for (i = 0; i < 10; i++)
cout << (RAND_MAX - rand())/static_cast<double>(RAND_MAX) << endl;

return 0;
}

- 8. The function declaration is

```cpp
int sum(int n1, int n2, int n3);
//Returns the sum of n1, n2, and n3;
```

The definition is

```cpp
int sum(int n1, int n2, int n3) {

return (n1 + n2 + n3);
}
```

- 9. The function declaration is

```cpp
char positiveTest(double number);
//Returns 'P' if number is positive.
//Returns 'N' if number is negative or zero.
```

The function definition is

```cpp
char positiveTest(double number) {
    if (number > 0)
        return 'P';
    else
        return 'N';
}
```

- 10. No, a function definition cannot appear inside the body of another function definition.

- 11. Predefined functions and user-defined functions are invoked (called) in the same way.

- 12. bool inOrder(int n1, int n2, int n3)
    return (n1 <= n2) && (n2 <= n3);

- 13. bool even(int n)
    return (n % 2) == 0;

- 14. bool isDigit(char ch)
    return ('0' <= ch) && (ch <= '9');

- 15. Hello
Goodbye
One more time:
Hello
End of program.

- 16. If you omitted the return statement in the function definition for iceCreamDivision in Display 3.7, the program would compile and run. However, if you input zero for the number of customers, the program would produce a run-time error because of division by zero.

- 17. #include <iostream>
    using namespace std;
    void productOut(int n1, int n2, int n3);

```cpp
int main() {
    int num1, num2, num3;
    cout << "Enter three integers: ";
    cin >> num1 >> num2 >> num3;
    productOut(num1, num2, num3);
    return 0;
}
```

# Answers to Self-Test Exercises 137

```cpp
void productOut(int n1, int n2, int n3) {
  cout << "The product of the three numbers "
       << n1 << ", " << n2 << ", and"
       << n3 << " is " << (n1*n2*n3) << endl;
}
```

18. These answers are system-dependent.

```cpp
19. double sqrt(double n);
//Precondition: n >= 0.
//Returns the square root of n.
```

You can rewrite the second comment line as follows if you prefer, but the previous version is the usual form for a function that returns a value:

//Postcondition: returns the square root of n

20. If you input zero for the number of customers, the program would compile and run. However, if you input zero for the number of customers, the program would produce a run-time error because of division by zero.

21. The principle of procedural abstraction says that a function should be defined so that it can be used as a black box. The programmer who uses the function should not need to know any details about how the function is coded.

22. The de-clared functions and user-defined functions are invoked (called) in the same way.

23. When we say that the function should be treated like a black box, we mean the programmer should not need to look at the body of the function.

24. In the following we have renamed these variables x1, x2, and x3.

```cpp
int x1 = 1; // output in this column
cout << x1 << endl; // 1 new line
{
  cout << x1 << endl; // 1 new line
int x2 = 2;
```

# 138 CHAPTER 3 Function Basics

```cpp
cout << x2 << endl; // 2 new line
{
  cout << x2 << endl; // 2 new line
int x3 = 3;
cout << x3 << endl; // 3 new line
}
```

# MyProgramming Projects

Visit www.myprogramming.com to select complete exercises and get instant feedback.

- 1. A liter is 0.264179 gallons. Write a program that will read in the number of liters of gasoline consumed by the user and the number of miles traveled by the car and then output the number of miles per gallon the car delivered. Your program should allow the user to repeat this calculation as often as the user wishes. Define a function to compute the number of miles per gallon. Your program should use a globally defined constant for the number of liters per gallon.
- 2. Write a program to gauge the rate of inflation for the past year. The program asks for the price of an item (such as a hot dog or a carat diamond) both one year ago and today. It estimates the inflation rate as the price divided by the year-ago price. Your program should allow the user to repeat this calculation as often as the user wishes. Define a function to compute the inflation rate. The inflation rate should be a value of double giving as a percentage, for example 5.3 for 5.3%.
- 3. Enhance your program from the previous exercise by having out the estimated price of the item in one and two years from the time of the calculation. The increase in cost over one year is estimated as the inflation rate times the price at the start of the year. Define a second function to determine the estimated cost of an item in a specified number of years, giving the current price of the item and the inflation rate as arguments.
- 4. The gravitational force between two bodies with masses $m1$ and $m2$ at a distance $d$ is given by the following formula,

```
$F = \frac{Gm_1m_2}{d^2}
```

where $G$ is the universal gravitational constant:
$G=6.673\times 10^{-8} \text{cm}^3/(g\cdot\text{sec}^2)$

Write a function that takes arguments for the masses of two bodies and the distance between them and returns the gravitational force between them.

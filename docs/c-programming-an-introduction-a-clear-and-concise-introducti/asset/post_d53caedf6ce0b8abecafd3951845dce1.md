
value at the time it is declared. This declaration is called an *initializer* and is written like this:

```cpp
int hoursWorked = 51;
```

This statement both declares hoursWorked as an integer variable and also assigns the variable the value 51.

Finally, you can declare multiple variables of the same data type in a single declaration. The example below declares multiple integer variables:

```cpp
int hours, days, weeks;
```

This is the same as writing:

```cpp
int hours;
int days;
int weeks;
```

C++ ignores whitespace so you can also write the lines above like this:

```cpp
int hours; int days; int weeks;
```

## Constants in C++

A special type of variable is the *constant*. A constant is a variable whose value cannot change during the life of the program. Constants help make programs easier to read and debug and should be used when appropriate.

A constant is declared as follows:

```cpp
const double pi = 3.14159;
```

This declaration looks very similar to the declaration for a regular variable. The only difference is the use of the keyword const before the data type.

Whenever you have a value that you will use in several places in a program, consider encoding the value as a constant rather than continually typing the literal value. This way, if you have to use the value in several places in your program and the value changes, you only have to make the change one time, where the constant is declared, rather than in all the places the value is used. We will see many examples of constants in the example programs coming up later.

## Exercises

- 1. Create variable declaration statements for the following data:
    - a. Your name
    - b. Your monthly income
    - c. Your gpa
- 2. What is wrong with the following variable names?
    - a. `.name`
    - b. `last&name`
    - c. `09Sept`
    - d. `first name`
    - e. `$str`

## Chapter 3: Arithmetic Operators and Expressions

A C++ program is a collection of statements that perform some task. When we write statements to perform arithmetic in C++, we have to create expressions that perform arithmetic with the use of arithmetic operators that tell the compiler what arithmetic to perform on our data. This chapter discusses the various arithmetic operators found in C++ and how to use them to form arithmetic expressions.

### Arithmetic Operators

One of the first things many people want to do when learning a new programming language is use the language to perform arithmetic. To do this, we need to know how arithmetic expressions are formed. The best place to start is with the arithmetic operators. Here they are:

- `+` Addition (plus)
- `-` Subtraction (minus)
- `*` Multiplication
- `/` Division
- `%` Remainder

The plus and minus operators are used to distinguish positive and negative numbers though it's not common to signify a positive number with the plus sign.

These operators are then used to form arithmetic expressions. Here are some examples:

```
23 + 2
100 - 17
43.2 * 3.14159
2300 / 12
12 % 2
```

You can also form more complex arithmetic expressions using these operators:

```
12 + 2 * 3 + 4 / 2
```

When expressions such as this one are written, C++ evaluates the expression based on the level of precedence of the operators. The order is, from highest to lowest:

- `%`
- `*`, `/`
- `+`, `-`

In the expression above, the multiplication and the division are performed before the addition and subtraction. You can modify the order of operations by using parentheses to force C++ to perform all operations inside parentheses before any other operations. For example, we could rewrite the expression above as:

```
(12 + 2) * (3 + 4) / 2
```

to change the value of the expression.

Now let's look at an example of using arithmetic expressions in a complete C++ program. In this example we're going to assign 5 test grades to 5 variables and compute the average grade. Here is the program:

```cpp
// Chapter3.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    int grade1, grade2, grade3, grade4, grade5,
        sumOfGrades, numOfGrades;
    double average = 0.0;
    grade1 = 84;
    grade2 = 89;
    grade3 = 77;
    grade4 = 94;
    grade5 = 88;
    numOfGrades = 5;
    sumOfGrades = grade1 + grade2 + grade3 + grade4
                + grade5;
    average = sumOfGrades / numOfGrades;
    cout << "The average is: " << average << endl;
    Console::ReadKey();
    return 0;
}
```

Let's examine this program line-by-line. The first line:

```cpp
int grade1, grade2, grade3, grade4, grade5,
    sumOfGrades, numOfGrades;
```

initializes the integer variables we need for this program, 5 variables for the grades, a variable to store the sum of the grades and a variable to store the number of grades, which we'll need to compute the average.

The next line:

```cpp
double average = 0.0;
```

declares and initializes the variable we'll use to store the average. The average will probably be a floating-point value so we need to use a floating-point data type.

These lines assign values to the grade variables and the variable storing the number of grades:

```cpp
grade1 = 84;
grade2 = 89;
grade3 = 77;
grade4 = 94;
grade5 = 88;
numOfGrades = 5;
```

The following line:

```cpp
sumOfGrades = grade1 + grade2 + grade3 + grade4
             + grade5;
```

adds all the grade variables together and stores that sum in the sumOfGrades variable.

Next we compute the average by dividing the sum of the grades by the number of grades:

```cpp
average = sumOfGrades / numOfGrades;
```

And we end the program by displaying the resulting average:

```cpp
cout << "The average is: " << average << endl;
```

Technically, though, the true end of the program is the line:

```cpp
return 0;
```

### More on C++ Operators and Variables

Assigning data to a variable is an operation that is performed so often in C++ programming that a set of operators are dedicated to performing this operation. The first set of operators we'll examine are for incrementing and decrementing variables by the value of 1.

### Incrementing and Decrementing

One of the most common statements in all programming looks something like this:

```cpp
count = count + 1;
```

There are innumerable situations where we need to increment the value of a variable by 1. To make it easy to perform this operation, C++ has a dedicated operator that increments a variable by 1, the ++ operator.

The ++ operator is used like this:

```cpp
int count = 0;
++count; // the value of count goes from 0 to 1
```

You can also put the operator after the variable, like this:

```cpp
count++;
```

A logical question to ask is – what difference does it make whether we put the ++ operator before the variable or after the variable? When a variable exists by itself in the statement, there is no difference. However, if a variable is used in a more complex statement, it can make a great difference. Here is an example that demonstrates the difference:

```cpp
int var1, var2;
var1 = 1;
// var1 gets the value 2 and var2 gets the value 2
var2 = ++var1;
```

```cpp
var1 = 1;
var2 = 0;
// var1 gets the value 2 and var2 gets the value 1
var2 = var1++;
```

See what happened? When we put the ++ operator behind the variable and use it in an assignment statement, the assignment operation is performed first and then the increment operation is performed. This is a subtle effect of the ++ operator, but one that can cause a lot of extra debugging time if you don't understand how the operator works.

Decrementing the value of a variable is performed with the -- operator. This operator is used the same way as the ++ operator:

```cpp
int var1, var2;
var1 = 2;
--var1; // var1 now has the value 1
var1--; // var1 now has the value 0
var1 = 2;
// var1 and var2 get the value 1
var2 = --var1;
// var2 gets the value 1 and var1 gets the value 0
var2 = var1--;
```

The increment and decrement operators provide handy shortcuts when adjusting variable values by 1, but be careful how you use them in more complex assignment statements.

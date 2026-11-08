
In order to write C++ code that manipulates variables in this way, you need to be familiar with operators. An **operator** is a symbol that tells the computer to perform a mathematical or logical operation. C++ has a large assortment of operators. We begin the discussion with a group of operators known as the arithmetic operators.

## ARITHMETIC OPERATORS

**Arithmetic operators** are the symbols used to perform arithmetic calculations. You are probably already very familiar with the arithmetic operators for addition (+) and subtraction (−). Table 2-2 lists and explains C++’s arithmetic operators.

| Operator Name | Symbol | Example | Comment |
|---|---|---|---|
| Addition | + | `num1 + num2` | |
| Subtraction | − | `num1 − num2` | |
| Multiplication | * | `num1 * num2` | |
| Division | / | `15/2`<br><br>`15.0 / 2.0`<br><br>`15.0 / 2` | Integer division; result is 7; fraction is truncated.<br><br>Floating point division; result is 7.5.<br><br>Floating point division because one of the operands is a floating point number; result is 7.5. |
| Modulus | % | `hours % 24` | Performs division and finds the remainder; result is 1 if the value of hours is 25. |
| Unary plus | + | `+num1` | Maintains the value of the expression; if the value of num1 is 3, then +num1 is 3. |
| Unary minus | − | `−(num1 − num2)` | If value of (num1 − num2) is 10, then −(num1 − num2) is −10. |

**Table 2-2** C++ arithmetic operators

You can combine arithmetic operators and variables to create **expressions**. The computer evaluates each expression, and the result is a value. To give you an idea of how this works, assume that the value of num1 is 3 and num2 is 20, and that both are of data type int. With this information in mind, study the examples of expressions and their values in Table 2-3.

![](img/08ab7b9c5b7606ff5c1616ca55d8b41c_34_0.png)

| Expression | Value | Explanation |
|---|---:|---|
| `num1 + num2` | 23 | because 3 + 20 = 23 |
| `num1 - num2` | -17 | because 3 − 20 = −17 |
| `num2 % num1` | 2 | because 20 / 3 = 6 remainder 2 |
| `num1 * num2` | 60 | because 3 * 20 = 60 |
| `num2 / num1` | 6 | because 20 / 3 = 6 (remainder is truncated) |
| `−num1` | −3 | because value of num1 is 3, therefore −num1 is −3 |

**Table 2-3** Expressions and values

## ASSIGNMENT OPERATORS AND THE ASSIGNMENT STATEMENT

Another type of operator is an assignment operator. You use an assignment operator to assign a value to a variable. A statement that assigns a value to a variable is known as an **assignment statement**. In C++, there are several types of assignment operators. The one you will use most often is the = assignment operator, which simply assigns a value to a variable. Table 2-4 lists and explains some of C++’s assignment operators.

| Operator Name | Symbol | Example | Comment |
|---|---|---|---|
| Assignment | `=` | `count = 5;` | Places the value on the right side into the memory location named on the left side. |
| Initialization | `=` | `int count = 5;` | Places the value on the right side into the memory location named on the left side when the variable is declared. |
| Assignment | `+=` | `num += 20;` | Equivalent to `num = num + 20;` |
|  | `-=` | `num -= 20;` | Equivalent to `num = num - 20;` |
|  | `*=` | `num *= 20;` | Equivalent to `num = num * 20;` |
|  | `/=` | `num /= 20;` | Equivalent to `num = num / 20;` |
|  | `%=` | `num %= 20;` | Equivalent to `num = num % 20;` |

**Table 2-4** C++ assignment operators

When an assignment statement executes, the computer evaluates the expression on the right side of the assignment operator and then assigns the result to the memory location associated with the variable named on the left side of the assignment operator. An example of an assignment statement is shown in the following code. Notice that the statement ends with a semicolon. In C++, assignment statements always end with a semicolon.

```cpp
answer = num1 * num2;
```

As you can see in Table 2-5, the parentheses operator, ( ), has the highest precedence. You use this operator to change the order in which operations are performed. Note the following example:

```cpp
average = test1 + test2 / 2;
```

The task of this statement is to find the average of two test scores. The way this statement is currently written, the compiler will divide the value in the test2 variable by 2, and then add it to the value in the test1 variable. So, for example, if the value of test1 is 90 and the value of test2 is 88, then the value assigned to average will be 134, which is obviously not the correct average of these two test scores. By using the parentheses operator in this example, you can force the addition to occur before the division. The correct statement looks like this:

```cpp
average = (test1 + test2) / 2;
```

In this example, the value of test1, 90, is added to the value of test2, 88, and then the sum is divided by 2. The value assigned to average, 89, is the correct result.

### EXERCISE 2-3: UNDERSTANDING OPERATOR PRECEDENCE AND ASSOCIATIVITY

In this exercise, you use what you have learned about operator precedence and associativity in C++. Study the following code and then answer the subsequent questions.

```cpp
// This program demonstrates the precedence and
// associativity of operators.
#include <iostream>
using namespace std;
int main()
{
    int value1 = 9;
    int value2 = 3;
    int value3 = 10;
    int answer1, answer2, answer3;
    int answer4, answer5, answer6;

    answer1 = value1 * value2 + value3;
    cout << "Answer 1: " << answer1 << endl;

    answer2 = value1 * (value2 + value3);
    cout << "Answer 2: " << answer2 << endl;

    answer3 = value1 + value2 - value3;
    cout << "Answer 3: " << answer3 << endl;

    answer4 = value1 + (value2 - value3);
    cout << "Answer 4: " << answer4 << endl;

    answer5 = value1 + value2 * value3;
    cout << "Answer 5: " << answer5 << endl;

    answer6 = value3 / value2;
    cout << "Answer 6: " << answer6 << endl;
    return 0;
}
```

- 1. What is the value of answer1, answer2, answer3, answer4, answer5, and answer6?
- 2. Explain how precedence and associativity affect the result.

### LAB 2-2: ARITHMETIC AND ASSIGNMENT OPERATORS

In this lab, you complete a partially written C++ program that is provided along with the data files for this book. The program, which was written for an appliance company, prints the name of an appliance, its retail price, its wholesale price, the profit made on the appliance, a sale price, and the profit made when the sale price is used.

- 1. Open the file named `Appliance.cpp` using Notepad or the text editor of your choice.
- 2. The file includes variable declarations and output statements. Read them carefully before you proceed to the next step.
- 3. Design the logic that will use assignment statements to first calculate the profit, then calculate the sale price, and finally calculate the profit when the sale price is used. Profit is defined as the retail price minus the wholesale price. The sale price is 15% deducted from the retail price. The sale profit is defined as the sale price minus the wholesale price. Perform the appropriate calculations as part of your assignment statements.
- 4. Save the source code file in a directory of your choice, and then make that directory your working directory.
- 5. Compile the program.

> **NOTE:** You will learn how to control the number of places after the decimal point when you want to output floating-point values in Chapter 7 of this book.

- 6. Execute the program. Your output should be as follows:

```cpp
Item Name: Dishwasher
Retail Price: $425
Wholesale Price: $275
Profit: $150
Sale Price: $361.25
Sale Profit: $86.25
```

Next, you will see how to put together all you have learned in this chapter to write a C++ program that uses sequential statements and interactive input statements.

## SEQUENTIAL STATEMENTS AND INTERACTIVE INPUT STATEMENTS

The term **sequential statements**, or **sequence**, refers to a series of statements that must be performed in sequential order, one after another. You use a sequence in programs when you want to perform actions one after the other. A sequence can contain any number of actions, but those actions must be in the proper order, and no action in the sequence can be skipped. Note that a sequence can contain comments, which are not considered part of the sequence itself. Comments serve as documentation, explaining the code to the programmer and any other people who might read it. You will learn more about comments in Chapter 3 of this book.

A sequence often includes **interactive input statements**, which are statements that ask, or **prompt**, the user to input data. The C++ program in the following example uses sequential statements and interactive input statements to convert a Fahrenheit temperature to its Celsius equivalent:

```cpp
// This C++ program converts a Fahrenheit temperature to Celsius.
// Input: Interactive
// Output: Fahrenheit temperature followed by Celsius temperature

#include <iostream>
using namespace std;

int main()
{
    double fahrenheit;
    double celsius;

    // Prompt user
    cout << "Enter Fahrenheit temperature: ";
    // Get interactive user input
    cin >> fahrenheit;
    // Calculate celsius
    celsius = (fahrenheit - 32.0) * (5.0/9.0);
    // Output
```

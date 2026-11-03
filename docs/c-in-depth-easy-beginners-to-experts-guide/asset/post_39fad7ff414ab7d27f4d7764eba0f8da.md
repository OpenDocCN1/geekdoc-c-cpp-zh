
## Lab Exercise (WAP – Write a Program)

- 1. WAP to check whether a number input through the keyboard is even or odd.
- 2. WAP to print the maximum out of two numbers.
- 3. WAP to print the maximum out of three numbers.
- 4. WAP to print the maximum out of four numbers.
- 5. WAP to print the maximum out of four numbers. (Short logic)
- 6. WAP to print the second maximum out of three numbers.
- 7. WAP to check whether a year is leap year or not.
- 8. WAP to calculate the grade of a student after the input of marks of that student.
    Percentage >= 90: grade is ‘A’
    Percentage >= 70: grade is ‘B’
    Percentage >= 50: grade is ‘C’
    Percentage < 50: grade is ‘F’
- 9. WAP to compute the tel. bill of a customer. Monthly Rental Rs. 100. Rates are as follows.
    - No. of calls 1 to 100: rate = 0
    - No. of calls 101 to 200: rate = 0.80
    - No. of calls 201 to 500: rate = 1.00
    - No. of calls 501 to --: rate = 1.20
- 10. WAP to compute the pension of an employee.
    If the person is male:
    - Age >= 90: pension is 4000
    - Age >= 60: pension is 6000
    - Age < 60: pension is 0

    If the person is female:

| Age | Pension |
|------|---------|
| >= 90 | 3000 |
| >= 60 | 5000 |
| < 60 | 0 |

- 11. WAP to check whether a 3 digit number is a magic number or not. (Palindrome) A number is a magic number if its reverse is same as the original number.
- 12. Any year is entered through the keyboard, WAP to determine whether the year is leap or not. Use the logical operators `&&` and `||`.
- 13. Any character is entered through the keyboard, WAP to determine whether the character entered is a capital letter, a small case letter, a digit or a special symbol.
- 14. WAP using conditional operators to determine whether a year entered through the keyboard is a leap year or not.

> "Is he lost his mind?"
>
> "The Boss wants me to create a computer Algorithm that can convert hindsight into Foresight."

![](img/3a2b6e5e90a58a56458b0539952c0cd2_79_0.png)

![](img/3a2b6e5e90a58a56458b0539952c0cd2_80_0.png)

## Chapter 4: Control Statements (Looping)

### Introduction

Sometimes we want some part of our code to be executed more than once. We can either repeat the code in our program or use loops instead. It is obvious that if for example we need to execute some part of code for a hundred or more times it is not practical to repeat the code. Alternatively we can use our repeating code inside a loop.

```c
while(not a hundred times)
{
    code
}
```

The loop repeats some portion of the program until a specified number of times or until a particular condition is being satisfied. **Or** in other words, you can say, looping is a process of repeating a single statement or a group of statements until some condition for termination of the loop is satisfied.

There are a few kinds of loop commands in C programming language. We will see these commands in next sections.

### There are four parts of a loop

- 1. **Initialization.**
- 2. **Conditions**
- 3. **Statements**
- 4. **Incrementation or Decrementation.**

***Don’t forget,*** Looping is a process of repeating a single statement or a group of statements until some condition for termination of the loop is satisfied.

### Type of loops

***Entry control loops:*** Those loops in which condition is checked before the execution of the statement. Thus, if the condition is false in the beginning, the loop will not run even once.

**e.g.** for loop, while loop.

***Exit control loops:*** Those loops in which the condition is checked after the execution of the statement. Thus, if the condition is false in the beginning, the loop will run at least once.

**e.g.** do while loop

### while loop

C has three loops; `while` is the simplest of them all. It is given a condition (in parentheses, just like with the `if` statement) which it evaluates. If the condition evaluates to true (non-zero, as seen before), the body of the loop is executed. The condition is evaluated again; if still true, the body of the loop is executed again. This continues until the condition finally evaluates to false. Then execution jumps to the first statement that follows the loop.

while loop is constructed of a condition and a single command or a block of commands that must run in a loop. As we have told earlier, a block of commands is a series of commands enclosed in two opening and closing braces.

In the while loop, the condition is evaluated and if it is true the statement of the loop is executed. After the execution of statement and increment or decrement, the loop condition is tested again. This process of repeated execution of statement, increment or decrement and testing of condition continues till the condition finally becomes false and the control of the loop is transferred to the next statement.

Once again, if more than one statement is required in the body of the loop, begin and end braces must be used.

It is the simplest of all the loops. This loop is used as follows:

```c
initialize;
while(condition)
{
    statement;
    increment or decrement;
}
```

`while` loop is an entry control loop. The condition is evaluated and if it is true the statement of the loop is executed. After the execution of statement and increment or decrement, the loop condition is tested again. This process of repeated execution of statement, increment or decrement and testing of condition continues till the condition finally becomes false and the control of the loop is transferred to the next statement.

### Syntax

```c
initialization;
while(condition)
{
    statement;
    incrementation or decrementation;
}
```

### Free syntax

```c
while(condition)
    command;

while(condition)
{
    block of commands
}
```

Loop condition is a boolean expression. A boolean expression is a logical statement which is either correct or incorrect. It has a value of 1 if the logical statement is valid and its value is 0 if it is not. For example, the Boolean statement (3 > 4) is invalid and therefore has a value of 0. While the statement (10 == 10) is a valid logical statement and therefore its value is 1.

### Semicolon Warning!

Avoid semicolons after `while`. We have already seen that problems can arise if a semicolon is placed after an `if` statement. A similar problem exists with loops, although it is more serious. With `if`, the no-op statement is potentially executed only once. With a loop, it may be executed an infinite number of times.

### Example

```c
#include <stdio.h>
main()
{
    int i=0;
    while( i<100 )
    {
        printf("\ni=%d",i);
        i=i+1;
    }
    system("pause");
}
```

In above example, `i=i+1` means: add 1 to `i` and then assign it to `i` or simply increase its value. As we saw earlier, there is a special operator in C programming language that does the same thing. We can use the expression `i++` instead of `i=i+1`.

### Type Conversion

From time to time you will need to convert type of a value or variable to assign it to a variable from another type. This type of conversions may be useful in different situations, for example when you want to convert type of a variable to become compatible with a function with different type of arguments.

Some rules are implemented in C programming language for this purpose. Automatic type conversion takes place in some cases. `char` is automatically converted to `int`. `unsigned int` will be automatically converted to `int`.

If there are two different types in an expression, then both will convert to better type. In an assignment statement, final result of calculation will be converted to the type of the variable which will hold the result of the calculation (e.g., the variable “count” in the assignment `count=i+1;`).

For example, if you add two values from `int` and `float` type and assign it to a `double` type variable, result will be `double`.

### Using loops in an example

**Write a program** – To accept scores of a person and calculate sum of them and their average and print them.

```c
#include <stdio.h>
#include <conio.h>
main()
{
    int count=0;
    float num=0,sum=0,avg=0;
    printf("Enter score (-1 to stop): ");
    scanf("%f",&num);
    while(num>=0)
    {
        sum=sum+num;
        count++;
        printf("Enter score (-1 to stop): ");
        scanf("%f",&num);
    }
    avg=sum/count;
    printf("\nAverage=%f",avg);
    printf("\nSum=%f\n",sum);
    system("pause");
}
```

In this example, we get the first number and then enter the loop. We will stay inside the loop until the user enters a value smaller than 0. If the user enters a value lower than 0, we will interpret it as STOP receiving scores.

Here are the output results of a sample run:

```text
Enter score (-1 to stop): 12
Enter score (-1 to stop): 14
```

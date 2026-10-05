
# CHAPTER 2 Flow of Control

Looping mechanisms in C++ are similar to those in other high-level languages. The three C++ loop statements are the while statement, the do-while statement, and the for statement. The same terminology is used with C++ as with other languages. The code that is repeated in a loop is the loop body. Each repetition of the loop body is called an iteration of the loop.

loop body iteration

while and do-while compared

## The while and do-while Statements

The syntax for the while statement and its variant, the do-while statement, is given in the accompanying book. In both cases, the multistatement body is a special case of the syntax for a loop with a single-statement body. The multistatement body is a single compound statement. Examples of a while statement and a do-while statement are given in Displays 2.4 and 2.5.

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_97_0.png)

## Display 2.4 Example of a while Statement

### Sample Dialogue 1

| How many greetings do you want? | 3 |
| Hello Hello |
| That's all! |

### Sample Dialogue 2

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_98_0.png)

The important difference between the while and do-while loops involves when the controlling expression is checked. With a while statement, the Boolean expression is checked before the loop is executed. If the Boolean expression evaluates to false, the body is not executed at all. With a do-while statement, the body of the loop is executed first and the Boolean expression is checked after the loop is executed. The do-while statement executes the loop body at least once. After this start-up, the while loop and the do-while loop behave the same. After each iteration of the loop body, the Boolean expression is again checked; if it is true, the loop is iterated again. If it has changed from true to false, the loop statement ends.

## Display 2.5 Example of a do-while Statement

```cpp
#include <iostream>
using namespace std;

int main() 
{
    int countdown;

    cout << "How many do you want? ";
    cin >> countdown;

    do {
        cout << "Hello ";
        countdown = countdown - 1;
    } while (countdown > 0);

    cout << endl;
    cout << "That's all!\n";
}
```

### Sample Dialogue 1

| How many greetings do you want? 3 |
| Hello Hello Hello |
| That's all! |

### Sample Dialogue 2

| How many greetings do you want? 0 |
| Hello |
| That's all! |

> The loop body is always executed at least once.

The first thing that happens when a while loop is executed is that the controlling Boolean expression is evaluated. If the Boolean expression evaluates to false then, the body is never executed. It may seem pointless to execute the body of a loop zero times, but sometimes it is the desired action. For example, a while loop is often used to sum a list of numbers, but the list could be empty. To be specific, a check balancing program might use a while loop to sum the values of all the checks you have written in a month—but you might take a month's vacation and write no checks at all. In that case, there are zero numbers to sum and so the loop iterated zero times.

executing the body
zero times

## Increment and Decrement Operators Revisited

In general, we discourage the use of the increment and decrement operators in expressions. However, many programmers like to use them in the controlling Boolean expression of a while or do-while statement. If done with care, this can work out satisfactorily. An example is given in Display 2.6. Be sure to note that in count <= numberOfItems, the value returned by count++ is the value of count before it is incremented.

## Self-Test Exercises

- 18. What is the output of the following?

```cpp
int count = 3;
while (count-- > 0)
    cout << count << "";
```

- 19. What is the output of the following?

```cpp
int count = 3;
while (--count > 0)
    cout << count << "";
```

- 20. What is the output of the following?

```cpp
int n = 1;
do
    cout << n << ""
while (n++ <= 3);
```

- 21. What is the output of the following?

```cpp
int n = 1;
do
    cout << n << ""
while (++n <= 3);
```

- 22. What is the output produced by the following? (x is of type int.)

```cpp
int x = 10;
while (x > 0)
{
    cout << x << endl;
    x = x - 3;
}
```

- 23. What output would be produced in the previous exercise if the sign > replaced with <

## Self-Test Exercises (continued)

- 24. What is the output produced by the following? (x is of type int.)

```cpp
int x = 10;
do {
    cout << x << endl;
    x = x - 3;
} while (x > 0);
```

- 25. What is the output produced by the following? (x is of type int.)

```cpp
int x = -42;
do {
    cout << x << endl;
    x = x - 3;
} while (x > 0);
```

- 26. What is the most important difference between a while statement and a do-while statement?

## The Comma Operator

The **comma operator** is a way of evaluating a list of expressions and returning the value of the expression. It is sometimes handy to use in a *for* loop, as in our discussion of the *for* loop in the next section. We do not advise using it in other contexts, but it is legal to use it in any expression.

The comma operator is illustrated by the following statement:

```cpp
result = (first = 2, second = first + 1);
```

The comma operator is shown in the center of the previous statement. The **comma expression** is the expression on the right-hand side of the assignment operator. The comma operator has two operands as operands.

## CHAPTER 2 Flow of Control

## The for Statement

for statement

The third and final loop statement in C++ is the for statement. The for statement is most commonly used to step through some increments. We will see in Chapter 5, the for statement is often used to step through an array. The for statement is, however, a completely general looping mechanism that can do anything a while loop can.

For example, the following for statement sums the integers 1-10:

```cpp
sum = 0;
int n;
for (n = 1; n <= 10; n++)
    sum = sum + n;
```

A for statement begins with the keyword for by three things in parentheses that tell the computer what to do. The beginning of a for statement looks like this:

```cpp
for (Initialization_Action; Boolean_Expression; Update_Action)
```

The first expression tells how variables, or other things are initialized; the second Boolean expression is used to check when the loop should end; and the last expression tells how the loop variable is updated after each iteration of the loop body.

The three expressions at the start of a for statement are separated by two—and only two—semicolons. Do not succumb to the temptation to place a semicolon after the third (the technical explanation is that these three things are expressions, statements, and do not require a semicolon at the end.).

A for statement often uses a int variable to control loop iteration and loop ending. However, the three expressions at the start of a for statement may be any C++ expressions; therefore, they may involve more (or fewer) than one variable, and the variables may be of any type.

Using the comma operator, you can add multiple actions to either the first or the last (but not normally the second) of the three items in parentheses. For example, you can move the initialization of the variable sum inside the for loop to obtain the following, which is equivalent to for statement code we showed:

```cpp
for (sum = 0, n = 1; n <= 10; sum = sum + n)
```

Although we do not advise so because it is not as easy to read, you can make the entire body of the for loop into parentheses. The previous for statement is equivalent to the following:

```cpp
for (sum = 0, n = 1; n <= 10; sum = sum + n, n++)
```
[/content] (Wait, I noticed the OCR text provided had some duplicate/garbled sections at the end. I have cleaned up the redundant parts based on the logical flow of the document provided.) 

*Self-correction: Looking at the provided raw OCR, the text from PAGE 102-103 contains many repetitions and garbled versions of earlier sections. I will provide the clean version based on the content found in the full text.*

**Corrected Final Output:**

[content]
# CHAPTER 2 Flow of Control

Looping mechanisms in C++ are similar to those in other high-level languages. The three C++ loop statements are the while statement, the do-while statement, and the for statement. The same terminology is used with C++ as with other languages. The code that is repeated in a loop is the loop body. Each repetition of the loop body is called an iteration of the loop.

loop body iteration

while and do-while compared

## The while and do-while Statements

The syntax for the while statement and its variant, the do-while statement, is given in the accompanying book. In both cases, the multistatement body is a special case of the syntax for a loop with a single-statement body. The multistatement body is a single compound statement. Examples of a while statement and a do-while statement are given in Displays 2.4 and 2.5.

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_97_0.png)

## Display 2.4 Example of a while Statement

### Sample Dialogue 1

| How many greetings do you want? | 3 |
| Hello Hello |
| That's all! |

### Sample Dialogue 2

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_98_0.png)

The important difference between the while and do-while loops involves when the controlling expression is checked. With a while statement, the Boolean expression is checked before the loop is executed. If the Boolean expression evaluates to false, the body is not executed at all. With a do-while statement, the body of the loop is executed first and the Boolean expression is checked after the loop is executed. The do-while statement executes the loop body at least once. After this start-up, the while loop and the do-while loop behave the same. After each iteration of the loop body, the Boolean expression is again checked; if it is true, the loop is iterated again. If it has changed from true to false, the loop statement ends.

## Display 2.5 Example of a do-while Statement

```cpp
#include <iostream>
using namespace std;

int main() 
{
    int countdown;

    cout << "How many do you want? ";
    cin >> countdown;

    do {
        cout << "Hello ";
        countdown = countdown - 1;
    } while (countdown > 0);

    cout << endl;
    cout << "That's all!\n";
}
```

### Sample Dialogue 1

| How many greetings do you want? 3 |
| Hello Hello Hello |
| That's all! |

### Sample Dialogue 2

| How many greetings do you want? 0 |
| Hello |
| That's all! |

> The loop body is always executed at least once.

The first thing that happens when a while loop is executed is that the controlling Boolean expression is evaluated. If the Boolean expression evaluates to false then, the body is never executed. It may seem pointless to execute the body of a loop zero times, but sometimes it is the desired action. For example, a while loop is often used to sum a list of numbers, but the list could be empty. To be specific, a check balancing program might use a while loop to sum the values of all the checks you have written in a month—but you might take a month's vacation and write no checks at all. In that case, there are zero numbers to sum and so the loop iterated zero times.

executing the body
zero times

## Increment and Decrement Operators Revisited

In general, we discourage the use of the increment and decrement operators in expressions. However, many programmers like to use them in the controlling Boolean expression of a while or do-while statement. If done with care, this can work out satisfactorily. An example is given in Display 2.6. Be sure to note that in count <= numberOfItems, the value returned by count++ is the value of count before it is incremented.

## Self-Test Exercises

- 18. What is the output of the following?

```cpp
int count = 3;
while (count-- > 0)
    cout << count << "";
```

- 19. What is the output of the following?

```cpp
int count = 3;
while (--count > 0)
    cout << count << "";
```

- 20. What is the output of the following?

```cpp
int n = 1;
do
    cout << n << ""
while (n++ <= 3);
```

- 21. What is the output of the following?

```cpp
int n = 1;
do
    cout << n << ""
while (++n <= 3);
```

- 22. What is the output produced by the following? (x is of type int.)

```cpp
int x = 10;
while (x > 0)
{
    cout << x << endl;
    x = x - 3;
}
```

- 23. What output would be produced in the previous exercise if the sign > replaced with <

## Self-Test Exercises (continued)

- 24. What is the output produced by the following? (x is of type int.)

```cpp
int x = 10;
do {
    cout << x << endl;
    x = x - 3;
} while (x > 0);
```

- 25. What is the output produced by the following? (x is of type int.)

```cpp
int x = -42;
do {
    cout << x << endl;
    x = x - 3;
} while (x > 0);
```

- 26. What is the most important difference between a while statement and a do-while statement?

## The Comma Operator

The **comma operator** is a way of evaluating a list of expressions and returning the value of the expression. It is sometimes handy to use in a *for* loop, as in our discussion of the *for* loop in the next section. We do not advise using it in other contexts, but it is legal to use it in any expression.

The comma operator is illustrated by the following statement:

```cpp
result = (first = 2, second = first + 1);
```

The comma operator is shown in the center of the previous statement. The **comma expression** is the expression on the right-hand side of the assignment operator. The comma operator has two operands as operands.

## CHAPTER 2 Flow of Control

## The for Statement

for statement

The third and final loop statement in C++ is the for statement. The for statement is most commonly used to step through some increments. We will see in Chapter 5, the for statement is often used to step through an array. The for statement is, however, a completely general looping mechanism that can do anything a while loop can.

For example, the following for statement sums the integers 1-10:

```cpp
sum = 0;
int n;
for (n = 1; n <= 10; n++)
    sum = sum + n;
```

A for statement begins with the keyword for by three things in parentheses that tell the computer what to do. The beginning of a for statement looks like this:

```cpp
for (Initialization_Action; Boolean_Expression; Update_Action)
```

The first expression tells how variables, or other things are initialized; the second Boolean expression is used to check when the loop should end; and the last expression tells how the loop variable is updated after each iteration of the loop body.

The three expressions at the start of a for statement are separated by two—and only two—semicolons. Do not succumb to the temptation to place a semicolon after the third (the technical explanation is that these three things are expressions, statements, and do not require a semicolon at the end.).

A for statement often uses a int variable to control loop iteration and loop ending. However, the three expressions at the start of a for statement may be any C++ expressions; therefore, they may involve more (or fewer) than one variable, and the variables may be of any type.

Using the comma operator, you can add multiple actions to either the first or the last (but not normally the second) of the three items in parentheses. For example, you can move the initialization of the variable sum inside the for loop to obtain the following, which is equivalent to for statement code we showed:

```cpp
for (sum = 0, n = 1; n <= 10; sum = sum + n)
```

Although we do not advise so because it is not as easy to read, you can make the entire body of the for loop into parentheses. The previous for statement is equivalent to the following:

```cpp
for (sum = 0, n = 1; n <= 10; sum = sum + n, n++)
```

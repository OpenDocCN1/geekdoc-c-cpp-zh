
## A do-while STATEMENT WITH A SINGLE-STATEMENT BODY

```
do
    Statement
while (Boolean_Expression);
```

## A do-while STATEMENT WITH A MULTISTATEMENT BODY

```
do
{
    Statement_1
    Statement_2
    .
    .
    .
    Statement_Last
} while (Boolean_Expression);
```

Do not forget the final semicolon.

## Display 2.4 Example of a while Statement (part 1 of 2)

```
1 #include <iostream>
2 using namespace std;
3 
4 int main()
5 {
6     int countDown;
7 
8     cout << "How many greetings do you want? ";
9     cin >> countDown;
10 
11 while (countDown > 0)
12 {
13     cout << "Hello ";
14     countDown = countDown - 1;
15 }
16 
17 cout << endl;
18 cout << "That's all!\n";
19 
20     return 0;
21 }
```

## Display 2.4 Example of a while Statement (part 2 of 2)

### SAMPLE DIALOGUE 1

How many greetings do you want? 3
Hello Hello Hello
That's all!

### SAMPLE DIALOGUE 2

How many greetings do you want? 0
That's all!

The loop body is executed zero times

## Display 2.5 Example of a do-while Statement (part 1 of 2)

```
1 #include <iostream>
2 using namespace std;
3 
4 int main() 
5 {
6     int countDown;
7 
8     cout << "How many greetings do you want? ";
9     cin >> countDown;
10 
11 do
12 {
13     cout << "Hello ";
14     countDown = countDown - 1;
15 }while (countDown > 0);
16 
17     cout << endl;
18     cout << "That's all!\n";
19 
20     return 0;
21 }
```

### SAMPLE DIALOGUE 1

How many greetings do you want? 3
Hello Hello Hello
That's all!

## Display 2.5 Example of a do-while Statement (part 2 of 2)

### SAMPLE DIALOGUE 2

```
How many greetings do you want? 0
Hello
That's all!
```

The loop body is always executed at least once.

The important difference between the while and do-while loops involves when the controlling Boolean expression is checked. With a while statement, the Boolean expression is checked before the loop body is executed. If the Boolean expression evaluates to false, the body is not executed at all. With a do-while statement, the body of the loop is executed first and the Boolean expression is checked after the loop body is executed. Thus, the do-while statement always executes the loop body at least once. After this start-up, the while loop and the do-while loop behave the same. After each iteration of the loop body, the Boolean expression is again checked; if it is true, the loop is iterated again. If it has changed from true to false, the loop statement ends.

The first thing that happens when a while loop is executed is that the controlling Boolean expression is evaluated. If the Boolean expression evaluates to false at that point, the body of the loop is never executed. It may seem pointless to execute the body of a loop zero times, but that is sometimes the desired action. For example, a while loop is often used to sum a list of numbers, but the list could be empty. To be more specific, a checkbook balancing program might use a while loop to sum the values of all the checks you have written in a month—but you might take a month's vacation and write no checks at all. In that case, there are zero numbers to sum and so the loop is iterated zero times.

executing the body zero times

## INCREMENT AND DECREMENT OPERATORS REVISITED

In general, we discourage the use of the increment and decrement operators in expressions. However, many programmers like to use them in the controlling Boolean expression of a while or do-while statement. If done with care, this can work out satisfactorily. An example is given in Display 2.6. Be sure to notice that in count++ <= numberOfItems, the value returned by count++ is the value of count before it is incremented.

## Display 2.6 The Increment Operator in an Expression

```
#include <iostream>
using namespace std;

int main()
{
    int numberOfItems, count,
        caloriesForItem, totalCalories;

    cout << "How many items did you eat today? ";
    cin >> numberOfItems;

    totalCalories = 0;
    count = 1;
    cout << "Enter the number of calories in each of the\n"
         << numberOfItems << " items eaten:\n";

    while (count++ <= numberOfItems)
    {
        cin >> caloriesForItem;
        totalCalories = totalCalories
                      + caloriesForItem;
    }

    cout << "Total calories eaten today = "
         << totalCalories << endl;
    return 0;
}
```

### SAMPLE DIALOGUE

How many items did you eat today? 7
Enter the number of calories in each of the
7 items eaten:
300 60 1200 600 150 1 120
Total calories eaten today = 2431

## Self-Test Exercises

- 18. What is the output of the following?
- 
- ```cpp
int count = 3;
while (count-- > 0)
    cout << count << " ";
```
- 
- 19. What is the output of the following?
- 
- ```cpp
int count = 3;
while (--count > 0)
    cout << count << " ";
```
- 
- 20. What is the output of the following?
- 
- ```cpp
int n = 1;
do
    cout << n << " ";
while (n++ <= 3);
```
- 
- 21. What is the output of the following?
- 
- ```cpp
int n = 1;
do
    cout << n << " ";
while (++n <= 3);
```
- 
- 22. What is the output produced by the following? (x is of type int.)
- 
- ```cpp
int x = 10;
while (x > 0)
{
    cout << x << endl;
    x = x - 3;
}
```
- 
- 23. What output would be produced in the previous exercise if the > sign were replaced with <?

- 24. What is the output produced by the following? (x is of type int.)
- 
- ```cpp
int x = 10;
do
{
    cout << x << endl;
    x = x - 3;
} while (x > 0);
```

- 25. What is the output produced by the following? (x is of type int.)

```
int x = -42;
do
{
    cout << x << endl;
    x = x - 3;
} while (x > 0);
```

26. What is the most important difference between a while statement and a do-while statement?

## THE COMMA OPERATOR

The comma operator is a way of evaluating a list of expressions and returning the value of the last expression. It is sometimes handy to use in a for loop, as indicated in our discussion of the for loop in the next subsection. We do not advise using it in other contexts, but it is legal to use it in any expression.

The comma operator is illustrated by the following assignment statement:

```
result = (first = 2, second = first + 1);
```

The comma operator is the comma shown. The comma expression is the expression on the right-hand side of the assignment operator. The comma operator has two expressions as operands. In this case the two operands are

```
first = 2 and second = first + 1
```

The first expression is evaluated, and then the second expression is evaluated. As you may recall from Chapter 1, the assignment statement when used as an expression returns the new value of the variable on the left side of the assignment operator. So, this comma expression returns the final value of the variable second, which means that the variable result is set equal to 3.

sets the value of result equal to 4. However, the value that the following gives to result is unpredictable, because it does not guarantee that the expressions are evaluated in order:

```
result = (first = 2, second = first + 1, third = second + 1);
```

For example, third = second + 1 might be evaluated before second = first + 1

## THE for STATEMENT

The third and final loop statement in C++ is the for statement. The for statement is most commonly used to step through some integer variable in equal increments. As we will see in Chapter 5, the for statement is often used to step through an array. The for statement is, however, a completely general looping mechanism that can do anything that a while loop can do.

For example, the following for statement sums the integers 1 through 10:

```
sum = 0;
for (n = 1; n <= 10; n++)
    sum = sum + n;
```

A for statement begins with the keyword for followed by three things in parentheses that tell the computer what to do with the controlling variable. The beginning of a for statement looks like the following:

```
for (Initialization_Action; Boolean_Expression; Update_Action)
```

The first expression tells how the variable, variables, or other things are initialized; the second gives a Boolean expression that is used to check for when the loop should end; and the last expression tells how the loop control variable is updated after each iteration of the loop body.

The three expressions at the start of a for statement are separated by two—and only two—semicolons. Do not succumb to the temptation to place a semicolon after the third expression. (The technical explanation is that these three things are expressions, not statements, and so do not require a semicolon at the end.)

A for statement often uses a single int variable to control loop iteration and loop ending. However, the three expressions at the start of a for statement may be any C++ expressions; therefore, they may involve more (or even fewer) than one variable, and the variables may be of any type.

> 1 The C++ standard does specify that the expressions joined by commas should be evaluated left to right. However, our experience has been that not all compilers conform to the standard in this regard.


Repeat the preceding process of analyzing a number for each number in the list. This discussion translates into the following algorithm:

- 1. For each number in the list:
  - a. Get the number.
  - b. Analyze the number.
  - c. Increment the appropriate count.
- 2. Print the results.

### Variables

Because you want to count the number of zeros, even numbers, and odd numbers, you need three variables of type int—say, zeros, evens, and odds—to track the counts. You also need a variable—say, number—to read and store the number to be analyzed and another variable—say, counter—to count the numbers analyzed. Therefore, you need the following variables in the program:

```cpp
int counter;    //loop control variable
int number;     //variable to store the number read
int zeros;      //variable to store the zero count
int evens;      //variable to store the even count
int odds;       //variable to store the odd count
```

Clearly, you must initialize the variables zeros, evens, and odds to zero. You can initialize these variables when you declare them.

### MAIN ALGORITHM

- 1. Declare and initialize the variables.
- 2. Prompt the user to enter 20 numbers.
- 3. For each number in the list:
  - a. Read the number.
  - b. Output the number (echo input).
  - c. If the number is even:
    - i. Increment the even count.
    - ii. If the number is zero, increment the zero count.

    otherwise
    Increment the odd count.
- 4. Print the results.

Before writing the C++ program, let us describe Steps 1–4 in greater detail. Then it will be much easier for you to write the instructions in C++.

- 1. Initialize the variables. You can initialize the variables zeros, evens, and odds when you declare them.
- 2. Use an output statement to prompt the user to enter 20 numbers.
- 3. For Step 3, you can use a `for` loop to process and analyze the 20 numbers. In pseudocode, this step is written as follows:

```text
for (counter = 1; counter <= 20; counter++)
{
    read the number;
    output number;

    switch (number % 2)    // check the remainder
    {
    case 0:
        increment even count;
        if (number == 0)
            increment zero count;
        break;
    case 1:
    case -1:
        increment odd count;
    }//end switch
}//end for
```

- 4. Print the result. Output the value of the variables zeros, evens, and odds.

### COMPLETE PROGRAM LISTING

```cpp
/************************************************
// Author: D.S. Malik
//
// Program: Counts zeros, odds, and evens
// This program counts the number of odd and even numbers.
// The program also counts the number of zeros.
*************************************************/

#include <iostream>
#include <iomanip>

using namespace std;

const int N = 20;

int main()
{
        //Declare variables
        int counter;        //loop control variable
        int number;         //variable to store the new number
        int zeros = 0;                                      //Step 1
        int odds = 0;                                       //Step 1
        int evens = 0;                                      //Step 1

        cout << "Please enter " << N << " integers, "
             << "positive, negative, or zeros."
             << endl;                         //Step 2

        cout << "The numbers you entered are:" << endl;

        for (counter = 1; counter <= N; counter++)    //Step 3
        {
            cin >> number;                            //Step 3a
            cout << number << " ";                    //Step 3b

                           //Step 3c
            switch (number % 2)
            {
            case 0:
                evens++;
                if (number == 0)
                    zeros++;
                break;
            case 1:
            case -1:
                odds++;
            } //end switch
        } //end for loop

        cout << endl;

        cout << "There are " << evens << " evens, "
             << "which includes " << zeros << " zeros."
             << endl;
        cout << "The number of odd numbers is: " << odds
             << endl;

        return 0;
}
```

**Sample Run:** In this sample run, the user input is shaded.

```text
Please enter 20 integers, positive, negative, or zeros.
The numbers you entered are:
0 0 -2 -3 -5 6 7 8 0 3 0 -23 -8 0 2 9 0 12 67 54
0 0 -2 -3 -5 6 7 8 0 3 0 -23 -8 0 2 9 0 12 67 54
There are 13 evens, which includes 6 zeros.
The number of odd numbers is: 7
```

We recommend that you do a walk-through of this program using the above sample input.

## do...while Looping (Repetition) Structure

This section describes the third type of looping or repetition structure, called a do...while loop. The general form of a do...while statement is as follows:

```cpp
do
    statement
while (expression);
```

Of course, statement can be either a simple or compound statement. If it is a compound statement, enclose it between braces. Figure 5–3 shows the flow of execution of a do...while loop.

![](img/d0be7fc6d804b63484835c6c8bc67a07_357_0.png)

**FIGURE 5–3**  do...while loop

In C++, do is a reserved word.

The statement executes first, and then the expression is evaluated. If the expression evaluates to true, the statement executes again. As long as the expression in a do...while statement is true, the statement executes. To avoid an infinite loop, you must, once again, make sure that the loop body contains a statement that ultimately makes the expression false and assures that it exits properly.

### EXAMPLE 5-18

```cpp
i = 0;

do
{
    cout << i << " ";
    i = i + 5;
}
while (i <= 20);
```

The output of this code is:

```text
0 5 10 15 20
```

After 20 is output, the statement:

```cpp
i = i + 5;
```

changes the value of `i` to 25 and so `i <= 20` becomes **false**, which halts the loop.

In a `while` and `for` loop, the loop condition is evaluated *before* executing the body of the loop. Therefore, `while` and `for` loops are called **pretest loops**. On the other hand, the loop condition in a `do...while` loop is evaluated *after* executing the body of the loop. Therefore, `do...while` loops are called **posttest loops**.

Because the `while` and `for` loops both have entry conditions, these loops may never activate. The `do...while` loop, on the other hand, has an exit condition and therefore always executes the statement at least once.

### EXAMPLE 5-19

Consider the following two loops:

- a.

  ```cpp
  i = 11;
  while (i <= 10)
  {
      cout << i << " ";
      i = i + 5;
  }
  cout << endl;
  ```

- b.

  ```cpp
  i = 11;
  do
  {
      cout << i << " ";
      i = i + 5;
  }
  while (i <= 10);
  cout << endl;
  ```

In (a), the `while` loop produces nothing; the statement never executes. In (b), the `do...while` loop outputs the number 11 and also changes the value of `i` to 16. This is expected because in a `do...while`, the statement must *always* execute at least once.

A `do...while` loop can be used for input validation. Suppose that a program prompts a user to enter a test score, which must be greater than or equal to 0 and less than or equal to 50. If the user enters a score less than 0 or greater than 50, the user should be prompted to re-enter the score. The following `do...while` loop can be used to accomplish this objective:

```cpp
int score;

do
{
    cout << "Enter a score between 0 and 50: ";
    cin >> score;
    cout << endl;
}
while (score < 0 || score > 50);
```

### EXAMPLE 5-20: Divisibility Test by 3 and 9

Suppose that *m* and *n* are integers and *m* is nonzero. Then *m* is called a **divisor** of *n* if *n = mq* for some integer *q*; that is, when *m* divides *n*, the remainder is 0.

Let \(n = a_k a_{k-1}a_{k-2}\cdots a_1a_0\) be an integer. Let \(s = a_k + a_{k-1} + a_{k-2} + \cdots + a_1 + a_0\) be the sum of the digits of \(n\). It is known that \(n\) is divisible by 3 and 9 if \(s\) is divisible by 3 and 9. In other words, an integer is divisible by 3 and 9 if and only if the sum of its digits is divisible by 3 and 9.

For example, suppose \(n = 27193257\). Then \(s = 2 + 7 + 1 + 9 + 3 + 2 + 5 + 7 = 36\). Because 36 is divisible by both 3 and 9, it follows that 27193257 is divisible by both 3 and 9.

Next, we write a program that determines whether a positive integer is divisible by 3 and 9 by first finding the sum of its digits and then checking whether the sum is divisible by 3 and 9.

To find the sum of the digits of a positive integer, we need to extract each digit of the number. Consider the number 951372. Note that 951372 % 10 = 2, which is the last digit of 951372. Also note that 951372 / 10 = 95137; that is, when the number is divided by 10, it removes the last digit. Next, we repeat this process on the number 95137. Of course, we need to add the extracted digits.

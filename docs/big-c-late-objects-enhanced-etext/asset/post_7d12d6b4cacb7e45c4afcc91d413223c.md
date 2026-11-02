
## Table 1 while Loop Examples

| Loop | Output | Explanation |
|---|---|---|
| i = 5;
while (i > 5)
{
  cout << i << " ";
  i--;
} | (No output) | The statement i > 5 is false, and the loop is never executed. |
| i = 5;
while (i < 0)
{
  cout << i << " ";
  i--;
} | (No output) | The programmer probably thought, "Stop when i is less than 0". However, the loop condition controls when the loop is executed, not when it ends (see Common Error 4.2). |
| i = 5;
while (i > 0) ;
{
  cout << i << " ";
  i--;
} | (No output, program does not terminate) | Note the semicolon before the {. This loop has an empty body. It runs forever, checking whether i > 0 and doing nothing in the body. |

## Common Error 4.1
### Infinite Loops

![](img/d61019b035dd82beb581604273c0ee6b_173_0.png)

A very annoying loop error is an infinite loop: a loop that runs forever and can be stopped only by killing the program or restarting the computer. If there are output statements in the program, then line after line of output flashes by on the screen. Otherwise, the program just sits there and hangs, seeming to do nothing. On some systems, you can terminate a hanging program by hitting Ctrl + C. On others, you can close the window in which the program runs.

A common reason for infinite loops is forgetting to update the variable that controls the loop:

```
year = 1;
while (year <= 20)
{
    balance = balance * (1 + RATE / 100);
}
```

Here the programmer forgot to add a year++ command in the loop. As a result, the year always stays at 1, and the loop never comes to an end.

Another common reason for an infinite loop is accidentally incrementing a counter that should be decremented (or vice versa). Consider this example:

```
year = 20;
while (year > 0)
{
```

![](img/d61019b035dd82beb581604273c0ee6b_173_1.png)

*Like this hamster who can't stop running in the treadmill, an infinite loop never ends.*

$225, or over $200. So the investment doubled after 2 years. The loop executed two times, incrementing year each time. Hence year must start at 0, not at 1.

| year | balance |
|---|---|
| 0 | $100 |
| 1 | $150 |
| 2 | $225 |

In other words, the balance variable denotes the balance after the end of the year. At the outset, the balance variable contains the balance after year 0 and not after year 1.

Next, should you use a < or <= comparison in the test? If you want to settle this question with an example, you need to find a scenario in which the final balance is exactly twice the initial balance. This happens when the interest is 100 percent. The loop executes once. Now year is 1, and balance is exactly equal to 2 * INITIAL_BALANCE. Has the investment doubled after one year? It has. Therefore, the loop should not execute again. If the test condition is balance < TARGET, the loop stops, as it should. If the test condition had been balance <= TARGET, the loop would have executed once more.

*In other words, you keep adding interest while the balance has not yet doubled.*

## Computing & Society 4.1 The First Bug

![](img/d61019b035dd82beb581604273c0ee6b_175_0.png)

According to legend, the first bug was found in the Mark II, a huge electromechanical computer at Harvard University. It really was caused by a bug—a moth was trapped in a relay switch.

Actually, from the note that the operator left in the log book next to the moth (see the photo), it appears as if the term "bug" had already been in active use at the time.

The pioneering computer scientist Maurice Wilkes wrote, "Somehow, at the Moore School and afterwards, one had always assumed there would be no particular difficulty in getting programs right."

I can remember the exact instant in time at which it dawned on me that a great part of my future life would be spent finding mistakes in my own programs.

![](img/d61019b035dd82beb581604273c0ee6b_175_1.png)

Courtesy of the Naval Surface Warfare Center, Dahlgren, VA., 1988, NHHC Collection.

### The First Bug

## 4.2 Problem Solving: Hand-Tracing

Hand-tracing is a simulation of code execution in which you step through instructions and track the values of the variables.

In Programming Tip 3.6, you learned about the method of hand-tracing. When you hand-trace code or pseudocode, you write the names of the variables on a sheet of paper, mentally execute each step of the code and update the variables.

It is best to have the code written or printed on a sheet of paper. Use a marker, such as a paper clip, to mark the current line. Whenever a variable changes, cross out the old value and write the new value below. When a program produces output, also write down the output in another column.

Consider this example. What value is displayed?

```
int n = 1729;
int sum = 0;
while (n > 0)
{
    int digit = n % 10;
    sum = sum + digit;
    n = n / 10;
}
cout << sum << endl;
```

There are three variables: n, sum, and digit.

![](img/d61019b035dd82beb581604273c0ee6b_176_0.png)

The first two variables are initialized with 1729 and 0 before the loop is entered.

```
int n = 1729;
int sum = 0;
while (n > 0)
{
    int digit = n % 10;
    sum = sum + digit;
    n = n / 10;
}
cout << sum << endl;
```

![](img/d61019b035dd82beb581604273c0ee6b_176_1.png)

Because n is greater than zero, enter the loop. The variable digit is set to 9 (the remainder of dividing 1729 by 10). The variable sum is set to 0 + 9 = 9.

Finally, n becomes 172. (Recall that the remainder in the division 1729/10 is discarded because both arguments are integers.)

```
int n = 1729;
int sum = 0;
while (n > 0)
{
    int digit = n % 10;
    sum = sum + digit;
    n = n / 10;
}
cout << sum << endl;
```

Because n equals zero, this condition is not true.

The condition n > 0 is now false. Continue with the statement after the loop.

```
int n = 1729;
int sum = 0;
while (n > 0)
{
    int digit = n % 10;
    sum = sum + digit;
    n = n / 10;
}
cout << sum << endl;
```

| n | sum | digit | output |
|---|---|---|---|
| 1729 | 0 |  |  |
| 172 | 9 | 9 |  |
| 17 | 11 | 2 |  |
| 1 | 18 | 7 |  |
| 0 | 19 | 1 | 19 |

This statement is an output statement. The value that is output is the value of sum, which is 19.

Of course, you can get the same answer by just running the code. However, hand-tracing can give you an insight that you would not get if you simply ran the code. Consider again what happens in each iteration:

- We extract the last digit of n.
- We add that digit to sum.
- We strip the digit off n.

In other words, the loop forms the sum of the digits in n. You now know what the loop does for any value of n, not just the one in the example. (Why would anyone want to form the sum of the digits? Operations of this kind are useful for checking the validity of credit card numbers and other forms of ID numbers—see Exercise P4.21.)

Hand-tracing does not just help you understand code that works correctly. It is a powerful technique for finding errors in your code. When a program behaves in a way that you don't expect, get out a sheet of paper and track the values of the variables as you mentally step through the code.

You don't need a working program to do hand-tracing. You can hand-trace pseudocode. In fact, it is an excellent idea to hand-trace your pseudocode before you go to the trouble of translating it into actual code, to confirm that it works correctly.

Hand-tracing can help you understand how an unfamiliar algorithm works.

Hand-tracing can show errors in code or pseudocode.

## 4.3 The for Loop

The for loop is used when a value runs from a starting point to an ending point with a constant increment or decrement.

It often happens that you want to execute a sequence of statements a given number of times. You can use a while loop that is controlled by a counter, as in the following example:

```
counter = 1; // Initialize the counter
while (counter <= 10) // Check the counter
{
    cout << counter << endl;
    counter++; // Update the counter
}
```

Because this loop type is so common, there is a special form for it, called the for loop (see Syntax 4.2).

```
for (counter = 1; counter <= 10; counter++)
{
    cout << counter << endl;
}
```

Some people call this loop count-controlled. In contrast, the while loop of the preceding section can be called an event-controlled loop because it executes until an event occurs (for example, when the balance reaches the target). Another commonly-used term for a count-controlled loop is definite. You know from the outset that the loop body will be executed a definite number of times—ten times in our example. In contrast, you do not know how many iterations it takes to accumulate a target balance. Such a loop is called indefinite.

![](img/d61019b035dd82beb581604273c0ee6b_179_0.png)

### Syntax 4.2 for Statement

![](img/d61019b035dd82beb581604273c0ee6b_179_1.png)

The for loop neatly groups the initialization, condition, and update expressions together. However, it is important to realize that these expressions are not executed together (see Figure 3).

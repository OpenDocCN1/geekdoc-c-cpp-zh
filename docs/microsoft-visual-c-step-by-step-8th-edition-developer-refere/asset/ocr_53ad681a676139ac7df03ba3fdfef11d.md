# The break and continue statements

In Chapter 4, you saw how to use the break statement to jump out of a switch statement. You can also use a break statement to jump out of the body of an iteration statement. When you break out of a loop, the loop exits immediately and execution continues at the first statement that follows the loop. Neither the update nor the continuation condition of the loop is rerun.

In contrast, the continue statement causes the program to perform the next iteration of the loop immediately (after reevaluating the Boolean expression). Here’s another version of the example that writes the values 0 through 9 to the console, this time using break and continue statements:

```
int i = 0;
while (true)
{
    Console.WriteLine(i);
    i++;
    if (i < 10)
        continue;
    else
        break;
}
```

This code is absolutely ghastly. Many programming guidelines recommend using continue cautiously or not at all because it is often associated with hard-to-understand code. The behavior of continue is also quite subtle. For example, if you execute a continue statement from within a for statement, the update part runs before performing the next iteration of the loop.

In the following exercise, you will write a do statement to convert a positive decimal whole number to its string representation in octal notation. The program is based on the following algorithm, which is based on a well-known mathematical procedure:

Click here to view code image

```
store the decimal number in the variable dec
do the following
    divide dec by 8 and store the remainder
    set dec to the quotient from the previous step
while dec is not equal to zero
combine the values stored for the remainder for each calculation in reverse order
```

For example, suppose that you want to convert the decimal number 999 to octal. You perform the following steps:

+   1. Divide 999 by 8. The quotient is 124 and the remainder is 7.
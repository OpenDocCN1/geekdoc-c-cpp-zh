# Chapter 5 Program Looping

Program 5.6 Output

+   1
2
3
4
5

The program initially sets the value of count to 1; execution of the while loop then begins. Because the value of count is less than or equal to 5, the statement that immediately is followed. The braces define both the NSLog statement and the statement that increments count as the body of the while loop. From the output of the program, you can see that this loop is executed five times until the value of count reaches 5.

You might have realized from this program that you could have readily accomplished the task using a for statement. In fact, a for statement can always be translated into an equivalent while statement, and vice versa. For example, the general for statement

```
for ( init_expression; loop_condition; loop_expression )
    program statement
```

can be expressed in the form of a while statement, like so:

```
init_expression;
while ( loop_condition )
{
    program statement
    loop_expression;
}
```

When you become familiar with the use of the while statement, you will gain a better feel for when it becomes more logical to use a while statement and when you use a for statement. In general, a loop executed a predetermined number of times is a prime candidate for implementation as a for statement. Also, if the initial expression, looping expression, and looping all involve the same variable, the for statement is probably right choice.

The next program provides another example of the use of the while statement. The greatest common divisor (we abbreviate it as gcd) of two integers is the largest integer value that evenly divides the two integers. For example, the gcd of 10 and 15 is 5 because it is the largest integer that evenly divides both 10 and 15.

A procedure, or algorithm, that can be followed to arrive at the gcd of two arbitrary integers is based on a procedure originally developed by Euclid around 300 B.C. It can be stated as follows:
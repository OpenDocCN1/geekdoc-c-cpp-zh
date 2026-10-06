
| Operator | Meaning | Example |
| --- | :--- | :--- |
| == | Equal to | count == 10 |
| != | Not equal to | flag != DONE |
| < | Less than | a < b |
| <= | Less than or equal to | low <= high |
| > | Greater than | points > POINT_MAX |
| >= | Greater than or equal to | j >= 0 |

The relational operators have lower precedence than all arithmetic operators. This means, for example, that an expression such as

a < b + c

evaluated as

a < (b + c)

This is as you would expect. It would be true if the value of a were less than the value of b + c, and false otherwise.

Pay particular attention to the "is equal to" operator (== and do not confuse its use with the assignment operator (=). The expression

a == 2

tests whether the value of a is equal to 2, whereas the expression

a = 2

assigns the number 2 to the variable a.

The choice of relational operator to use depends on the particular test being made and, in some instances, on your particular preferences. For example, the relational expression

n <= 200

can be equivalently expressed as

n < 201

Returning to the previous example, the program statement that forms the body of the for loop—triangularNumber += n;—is repetitively executed as long as the value of the relational test is true, or, in this case, as long the value of n is less than or equal to 200. This program statement has the effect of adding the value of n to the value of triangularNumber.

When the loop_condition is no longer satisfied, execution of the program statement continues immediately following the for loop. In this program, execution continues with the NSLog statement after the component of loop has terminated.

The final component of the for statement contains an expression that is evaluated each time the body of the loop is executed. Program 5.2, this loop_expression adds 1 to the value of n. Therefore, the value of n is incremented by 1 time after its value has been added into the value of triangularNumber, and it ranges in value from 1 through 201.

It is worth noting that the last value that n attains, 201, is not added into the value of triangularNumber because the loop is terminated as soon as the looping condition is no longer satisfied, and as soon as n equals 201.

In summary, execution of the for statement proceeds as follows:

- 1. The initial expression is evaluated first. usually sets a variable that is used inside the loop, generally referred to as an index variable, to some initial value (such as 0 or 1).
- 2. The looping condition is evaluated. If the condition is not satisfied (the expression is false), the loop immediately terminates. Execution continues with the program statement that immediately follows the loop.
- 3. The program statement that constitutes the body of the loop is executed.
- 4. The looping expression is evaluated. This expression is generally used to change the value of the index variable, frequently by adding 1 to it or subtracting 1 from it.
- 5. Return to step 2.

Remember that the looping condition is evaluated immediately on entry into the loop, before the body of the loop has executed one time. Also remember not to put a semicolon after the closed parenthesis at the end of the loop because this immediately ends the loop.

Program 5.2 actually generates all the first 200 triangular numbers on its way to its final, so it might be nice to generate a table of these numbers. To save space, however, let's assume that you want to print a table of just the first 10 triangular numbers. Program 5.3 performs this task.

# Program 5.3

```c
// Program to generate a table of triangular numbers

#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        int n, triangularNumber;

        NSLog (@"TABLE OF TRIANGULAR NUMBERS");
    }
}
```

```c
NSLog ("@ n Sum from 1 to n");
NSLog ("@-- ------");

triangularNumber = 0;

for ( n = 1; n <= 10; ++n ) {
    triangularNumber += n;
    NSLog ("@ %i, n%i", n, triangularNumber);
}

return 0;
```

# Program 5.3. Output

TABLE OF TRIANGULAR NUMBERS
n Sum from 1 to n
-- ----------
1 1
2 3
3 6
4 10
5 15
6 21
7 28
8 36
9 45
10 55

In Program 5.3, the purpose of the first three NSLog statements is simply to provide a general heading and to label the columns of the output. After the appropriate headings have been displayed, the program calculates the first 10 triangular numbers. The variable n is used to count the current number whose sum from 1 to n you are computing, and the variable triangularNumber is used to store the value of triangular number n.

Execution of the for statement commences by setting the value of the variable n to 1. As mentioned earlier, the program statement immediately following the for statement constitutes the body of the program loop. But what happens if you want to repetitively execute not just a single program statement, but a group of program statements? This can be accomplished by enclosing all such program statements.

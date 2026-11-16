
## The syntax of a while loop looks like this:

```
// Before the loop construct, initialize any loop control variable,
// i.e., the variable appearing in the condition in the loop header.
while (condition) { // loop header - test the loop condition
    statement;
}
or
while (condition) { // loop header - test the loop condition
    statement;
    statement;
    ...
}
```

Keep in mind that the loop body must contain a statement that updates the loop control variable used in the loop condition. The loop control variable is normally found at the bottom of the loop body.

Note that when a while loop construct has only one statement then the curly braces { } are optional. However, it's always a good idea to use the curly braces even though they're not required.

## Example: Powers of 2

As an example, consider a program segment designed to find the first power of 2 larger than 100. We first initialize the integer variable product to 2. When the following while repetition statement finishes executing, product will contain the desired answer:

```
product = 2;
while (product <= 100) {
    product = product * 2; // or we can say: product *= 2;
}
```

When the while statement is entered, the value of product is 2. The variable, product, is repeatedly multiplied by 2, taking on the values 2, 4, 8, 16, 32, 64 and 128 successively. When product becomes 128, the condition in the while statement:

```
product <= 100
```

becomes false. This terminates the repetition, and the final value of product is 128. Program execution continues with the next statement after the while loop.

We can generalize this example and write a function, findMax(), that will return the first power of 2 greater than some maximum value:

```
#include <stdio.h>

int findMax(int value);

int main (void) {
    int value, max;

    value = 500;
    max = findMax(value); ...
    printf("The first power of 2 larger than %d is %d.", value, max);
    return 0;
}

int findMax(int value) {
    int product = 2;

    while (product <= value) {
        product *= 2;
    }
    return product;
}
```

Here's the output produced:

```
The first power of 2 larger than 500 is 512.
```

We can generalize this example even further to have the function, findMax(), return the first power of num greater than some maximum value:

```
#include <stdio.h>

int findMax(int product, int value);

int main (void) {
    int num, value, max;

    num = 5;
    value = 1000;

    max = findMax(num, value);
    printf("The first power of %d larger than %d is %d.", num,
           value, max);

    return 0;
}

int findMax(int product, int value) {
    while (product <= value) {
        product *= 2;
    }
    return product;
}
```

Here's the output produced:

```
The first power of 5 larger than 1000 is 1280.
```

## Counter Controlled Loops

A counter controlled loop repeats a series of executable statements a specified number of times using a variable to count the number of loop iterations completed.

- The number of times that the loop body will be repeated must be known before checking the loop condition the first time and must not be changed within the loop body.
- The counting variable must be initialized to a known value before checking the loop condition the first time.
- The counting variable must be updated within the loop body or the loop condition will never evaluate to false, creating an infinite loop that will never stop.
- The counting variables can be incremented (increased in value) by any amount or decremented (decreased in value) by any amount.

## Example: Celsius to Fahrenheit Conversion Table

Our conversion table will utilize a counter variable, ctemp, to control the number of times the while loop executes. In this example, repetition terminates when ctemp becomes < 0.

```c
#include <stdio.h>
int main (void) {
    int ctemp;
    float ftemp;
    printf("Celsius\t\tFahrenheit\n");
    ctemp = 100;
    while (ctemp >= 0) {
        ftemp = (9.0/5.0) * (float)ctemp + 32.0;
        printf ("%7d%15.1f\n", ctemp, ftemp);
        ctemp = ctemp - 10;
    }
    return 0;
}
```

Program output is as follows:

| Celsius | Fahrenheit |
|---|---|
| 100 | 212.0 |
| 90 | 194.0 |
| 80 | 176.0 |
| 70 | 158.0 |
| 60 | 140.0 |
| 50 | 122.0 |
| 40 | 104.0 |
| 30 | 86.0 |
| 20 | 68.0 |
| 10 | 50.0 |
| 0 | 32.0 |

- What would have happened if we were to have written (9/5) instead of (9.0/5.0)?
- What would have happened if we left off the parentheses around (9.0/5.0)?
- Why was it a good idea to write `(float)ctemp` in the above expression rather than just `ctemp`?

## Summation Variables

Suppose that we wish to find the sum of the numbers from 1-1000. Not only will we need a counter variable to control the number of times the while loop executes, but we will also need a summation variable to accumulate the sum of the numbers that we have seen so far.

```
// summation.c

#include <stdio.h>

int main(void) {
    int count = 1;
    int sum = 0;

    while (count <= 1000) {
        sum += count;
        ++count;
    }

    printf("The sum = %d.\n", sum);
    return 0;
}
```

Program output is as follows:

The sum = 500500.

Note that variable used to store summations, or totals, should normally be initialized to zero before being used in a program; otherwise the summation variable would include the previous value stored in the summation variable's memory location. This is due to the fact that an uninitialized variable usually contains a "garbage value", i.e., the value last stored in the memory location reserved for that variable.

## Sentinel Controlled Loops

Sometimes we do not know in advance how many times we want a loop to iterate. For example, suppose we want to output the square and cube of numbers entered into the program. How can the program determine when to stop the input of numbers? One way to solve this problem is to use a special value called a sentinel value to indicate “end of data entry.”

The user types in data values, whose squares and cubes will be output, until the sentinel value is entered which indicates that the last data value has been entered. Note that the sentinel value must be chosen so that it cannot be confused with an acceptable input value.

```
// sentinel.c
#include <stdio.h>
int main(void) {
    int num;
    printf("Enter number, -999 to end: ");
    scanf("%d", &num);
    while (num != -999) {
        printf("%5d %5d %5d\n", num, num * num, num * num * num);
        printf("Enter number: ");
        scanf("%d", &num);
    }
    return 0;
}
```

Program output is as follows:

```
Enter number, -999 to end: 2
2    4    8
Enter number, -999 to end: 5
5   25  125
Enter number, -999 to end: 8
8   64  512
Enter number, -999 to end: -999
```

## For Statement

The for statement works well where the number of iterations of the loop is known before the loop is entered. The head of the loop consists of three parts separated by semicolons: initialization, test, and update.

```
for (i = 1; i <= 100; i++)
```

The first part is run before the loop is entered. This is usually the initialization of the loop control variable.

The second part is a test of the loop control variable. The loop is exited when this test is no longer true.

The third part is the update of the loop control variable. This is typically a statement that is executed every time the loop body is completed. Usually this is an increment or decrement of the loop control variable.

Here's a look at the syntax of the for statement:

```
for (initialExpression; loopCondition; loopExpression) {
    statement;
}
```

- initialExpression sets an initial value before the loop begins.
- loopCondition specifies condition(s) necessary to continue the loop.
- loopExpression executes each time after the body of the loop executes.

## Example: Sum the integers from 1 - 100

```
int i, sum = 0;
for (i = 1; i <= 100; ++i) {
    sum += i;
}
```


## 7.2 C Programming and Data Structures

The program evaluates the statement

```
sum = sum + n*n;
```

10 times. That is, the loop is executed 10 times. This number can be decreased or increased easily by modifying the relational expression appropriately in the statement `if (n == 10)`. On such occasions where the exact number of repetitions are known, there are more convenient methods of looping in C. These looping capabilities enable us to develop concise programs containing repetitive processes without the use of `goto` statements.

In looping, a sequence of statements are executed until some conditions for termination of the loop are satisfied. A program loop therefore consists of two segments, one known as the body of the loop and the other known as the control statement. The control statement tests certain conditions and then directs the repeated execution of the statements contained in the body of the loop.

Depending on the position of the control statement in the loop, a control structure may be classified either as the entry-controlled loop or as the exit-controlled loop. The flowcharts in Fig. 7.1 illustrate these structures. In the entry-controlled loop, the control conditions are tested before the start of the loop execution. If the conditions are not satisfied, then the body of the loop will not be executed. In the case of an exit-controlled loop, the test is performed at the end of the body of the loop and therefore the body is executed unconditionally for the first time.

![](img/65953ea584e494f3d396b2252cb5ea53_169_0.png)

The test conditions should be carefully stated in order to perform the desired number of loop executions. It is assumed that the test condition will eventually transfer the control out of the loop. In case, due to some reason, it does not do so, the control sets up an infinite loop and the body is executed over and over again.

A looping process, in general, would include the following four steps:

- 1. Setting and initialization of a counter.
- 2. Execution of the statements in the loop.
- 3. Test for a specified condition for execution of the loop.
- 4. Incrementing the counter.

The test may be either to determine whether the loop has been repeated the specified number of times or to determine whether a particular condition has been met.

The C language provides for three loop constructs for performing loop operations. They are:

- 1. The `while` statement.
- 2. The `do` statement.
- 3. The `for` statement.

We shall discuss the features and applications of each of these statements in this chapter.

### 7.2 THE WHILE STATEMENT

The simplest of all the looping structures in C is the `while` statement. We have used `while` in many of our earlier programs. The basic format of the `while` statement is

```
while (test condition)
{
    body of the loop
}
```

The `while` is an entry-controlled loop statement. The test-condition is evaluated and if the condition is true, then the body of the loop is executed. After execution of the body, the test-condition is once again evaluated and if it is true, the body is executed once again. This process of repeated execution of the body continues until the test-condition finally becomes false and the control is transferred out of the loop. On exit, the program continues with the statement immediately after the body of the loop.

The body of the loop may have one or more statements. The braces are needed only if the body contains two or more statements. However, it is a good practice to use braces even if the body has only one statement.

We can rewrite the program loop discussed in Sec. 7.1 as follows:

```
sum = 0;
n = 1;
while(n <= 10)
{
    sum = sum + n * n;
    n = n+1;
}
printf("sum = %d\n", sum);
```

The body of the loop is executed 10 times for n = 1, 2, ......, 10 each time adding the square of the value of n, which is incremented inside the loop. The test condition may also be written as `n < 11`; the result would be the same.

Another example of `while` statement which uses the keyboard input is shown below:

```
..........
..........
character = ' ';
while (character != 'Y')
    character = getchar();
xxxxxxxx;
..........
```

First the character is initialized to ' '. The `while` statement then begins by testing whether character is not equal to Y. Since the character was initialized to ' ', the test is true and the loop statement

```
character = getchar();
```

is executed. Each time a letter is keyed in, the test is carried out and the loop statement is executed until the letter Y is pressed. When Y is pressed, the condition becomes false because character equals Y, and the loop terminates, thus transferring the control to the statement `xxxxxxxx;`

### Example 7.1

A program to evaluate the equation

$y = x^n$

when n is a non-negative integer, is given in Fig. 7.2.

The variable y is initialized to 1 and then multiplied by x, n times using the `while` loop. The loop control variable, count is initialized outside the loop and incremented inside the loop. When the value of count becomes greater than n, the control exits the loop.

### 7.3 THE DO STATEMENT

The `while` loop construct that we have discussed in the previous section makes a test of condition before the loop is executed. Therefore, the body of the loop may not be executed at all if the condition is not satisfied at the very first attempt. On some occasions it might be necessary to execute the body of the loop before the test is performed. Such situations can be handled with the help of the `do` statement. This takes the form:

```
do
{
    body of the loop
}
while (test-condition);
```

On reaching the `do` statement, the program proceeds to evaluate the body of the loop first. At the end of the loop, the test-condition in the `while` statement is evaluated. If the condition is true, the program continues to evaluate the body of the loop once again. This process continues as long as the condition is true. When the condition becomes false, the loop will be terminated and the control goes to the statement that appears immediately after the `while` statement.

```c
Program
/********************************************************************************/
/* EXAMPLE OF while STATEMENT */
/********************************************************************************/
main()
{
    int count, n;
    float x, y;
    printf("Enter the values of x and n:");
    scanf("%f %d", &x, &n);
    y = 1.0;
    count = 1;
    /* LOOP BEGINS */
    while (count <= n)
    {
        y = y*x;
        count++;
    }
    /* END OF LOOP */
    printf("x = %f; n = %d; x to power n = %f\n",x,n,y);
}
Output
Enter the values of x and n: 2.5 4
x = 2.500000; n = 4; x to power n = 39.062500

Enter the values of x and n: 0.5 4
x = 0.500000; n = 4; x to power n = 0.062500
```

Fig. 7.2 Program to compute x to the power n using while loop

Since the test-condition is evaluated at the bottom of the loop, the `do...while` construct provides an exit-controlled loop and therefore the body of the loop is always executed at least once.

A simple example of a `do...while` loop is:

```c
do
{
    printf("Input a number\n");
    number = getnum();
}
while (number > 0);
```

This segment of a program reads a number from the keyboard until a zero or a negative number is keyed in.

The test conditions may have compound relations as well. For instance, the statement `while (number > 0 && number < 100)` in the above example would cause the loop to be executed as long as the number keyed in lies between 0 and 100.

Consider another example:

```
I = 1;
sum = 0;
do
{
  sum = sum + 1;
  I = I+2;
}
while(sum < 40 || I < 10);
printf("%d %d\n", I, sum);
```

The loop will be executed as long as one of the two relations is true.

### Example 7.2

A program to print the multiplication table from 1 × 1 to 12 × 10 as shown below is given in Fig. 7.3.

| × | 1 | 2 | 3 | 4 | … | 10 |
|---|---|---|---|---|---|---|
| 1 | 1 | 2 | 3 | 4 | … | 10 |
| 2 | 2 | 4 | 6 | 8 | … | 20 |
| 3 | 3 | 6 | 9 | 12 | … | 30 |
| 4 | 4 | … | … | … | … | 40 |
| … | … | … | … | … | … | … |
| 12 | 12 | … | … | … | … | 120 |

This program contains two `do...while` loops in nested form. The outer loop is controlled by the variable row and executed 12 times. The inner loop is controlled by the variable column and is executed 10 times, each time the outer loop is executed. That is, the inner loop is executed a total of 120 times, each time printing a value in the table.

Notice that the `printf` of the inner loop does not contain any new line character (`\n`). This allows the printing of all row values in one line. The empty `printf` in the outer loop initiates a new line to print the next row.

### 7.4 THE FOR STATEMENT

### Simple ‘for’ Loops

The `for` loop is another entry-controlled loop that provides a more concise loop control structure. The general form of the `for` loop is

```
for (initialization ; test-condition ; increment)
{
  body of the loop
}
```


## Flowchart of while loop

![](img/35ea447eca4d04af54f37bf3d3ca337d_60_0.png)

Fig. 3.3: Flowchart of While Loop

*Example:*

```c
#include<stdio.h>
#include<conio.h>
void main()
{
    int count=1;
    while(count <=5)
    {
        printf("%d ", count);
        count++;
    }
    getch();
}
```

**Output:**

1 2 3 4 5

**Step 1:** first counter variable count has initialized with value 1 and then it has been tested for the condition.

**Step 2:** If condition holds true then the body of the while loop gets executed otherwise, control comes out of the loop.

**Step 3:** count value was incremented using ++ operator, then it has been tested again for the loop condition. It keeps happening until the condition returns to false.

### 3.3.2 Do-while Loop

A do while loop is another type of repetition statement. It is exactly the same as the while loop, except it does something and then evaluates the logical expression of the loop to determine what happens next. Normally with a while loop, a part of the logical expression in the loop must be initialized before execution of the while loop.

A do...while loop statement will be performed and then checks the test expression of the loop.

```c
do
{
        // codes or statements
} while (testExpression);
```

The code block (loop body) inside the braces is executed once.

Then, the test expression is evaluated. If the test expression is true, the loop body is executed again. This process goes on until the test expression is evaluated to 0 (false).

When the test expression is false (zero), the **do...while** loop is terminated.

The statement in the loop may be single or complex. Complex statements must be enclosed with curly braces { }. Let’s look at a couple of examples of do while loops.

![](img/35ea447eca4d04af54f37bf3d3ca337d_61_0.png)

**Fig. 3.4: Flowchart of do... While Loop**

**Example: Program to print first ten multiple of 5.**

```c
#include<stdio.h>
#include<conio.h>
void main()
{
    int a,i;
    a=5;
    i=1;
    do
    {
        printf("%d\t",a*i);
        i++;
    }
    while (i <= 10);
    getch();
}
```

**Output:**

5 10 15 20 25 30 35 40 45 50

### 3.3.3 For Loop

A for loop is another way to perform something that needs to be repeated in C++ (repetition). Most programmers like to use for loops because the code can be written in a more compact manner compared to the same loop written with a while or do while loop.

![](img/35ea447eca4d04af54f37bf3d3ca337d_62_0.png)

A for loop is generally used when you know exactly how many times a section of code needs to be repeated.

The general form of a for loop is as follows:

```c
for    (expression1; expression2; expression3)
    stmt(s);
```

where  stmt(s) is a single or compound statement.

This is one of the most frequently used loops in C programming.

**The syntax of for loop looks like this –**

```c
for (initialization; condition test; control flow)
{
    //Code – C statements needs to be repeated
}
```

The control flow can be increment or decrement value of variable depending on requirements.

Expression1 is used to initialize the loop; expression2 is used to determine whether or not the loop will continue; expression3 is evaluated at the end of each iteration or cycle.

**NOTE 1:** Expression2 is tested before the stmt and expression3 is executed; it is possible that the body of the loop is never executed or tested.

**NOTE 2:** Any or all of the 3 expressions in a for loop can be omitted, but the 2 semi-colons must remain. Like **for( ; ; )**

If expression1 is omitted, there is no initialization done in the loop, but you might not need any initialization for your program.

Like :

```c
i=1;
for ( ; i<=10;i++)
```

If expression2 is omitted, there is no test section so you will essentially have an infinite loop.

```c
for(i=1; ; i++)
```

If expression3 is omitted, there is no update as part of the for statement, but the update could be done as part of the statement in the body of the loop.

```c
for(i=1;i<=10; )
{
    printf("%d",i);
    i++;
}
```

The **for** loop is commonly used when the number of iterations is known.

In general, a for loop can be written as an equivalent to a while loop and *vice versa*.

```c
for (expression1; expression2; expression3)
    statement;
```

**is equivalent to...**

```c
expression1;
while (expression2)
{
    Statements;
    expression3;
}
```

### For Loop Flow Diagram

![](img/35ea447eca4d04af54f37bf3d3ca337d_64_0.png)

*Example:*

```c
...
int i;
for(i=1; i<=4; i++)
{
    printf("hello, World");
}
...
```

**Output:**

hello, World
hello, World
hello, World
hello, World

**Step 1:** First the counter variable gets initialized; here variable is I, which has been assigned by value 1.

**Step 2:** Then variable has been tested for a given condition, if the condition results in true then C statements enclosed in loop body get executed by compiler, otherwise control skips the loop and continues with the next statements following loop.

**Step 3:** After successful execution of loop's body, the counter variable is incremented or decremented, depending on the operation (++ or --).

### Various Forms of for LOOP

Here we use variable num in all the below examples:

- 1. Here instead of num++, We can use num=num+1, which is the same as num++.

```c
for(num=10;num<20;num=num+1)
```

- 2. Initialization part can be skipped from loop as shown below, the counter variable is declared before the loop itself.

```c
int num=10;
for(;num<20;num++)
```

Must Note: Although we can skip init part but semicolon (;) before condition is must, without which you will get compilation error.

- 3. Like initialization, you can also skip the increment part as we did below. In this case semicolon (;) is must, after condition logic. The increment part is being done in for loop body itself.

```c
for(num=10;num<20;)
{
    //Code
    num++;
}
```

- 4. Below case is also possible, increment in body and in it during declaration of counter variable.

```c
int num=10;
for(;num<20;)
{
//Statements
num++;
}
```

- 5. Counter can be decremented also. In the below example the variable gets decremented each time the loop runs until the condition num>10 becomes false.

```c
for(num=20;num>10;num--)
```

### 3.3.4 Nested for Loop

Nested loops or nesting of loop is placing one loop into another loop to execute a program based on multiple conditions and checks.

Here we have an example of nesting of for loop, likewise you can use nesting of various loops such as while, do...while or for.

### 3.4.1 break

The break statement terminates the loop (for, while and do...while loop) immediately when it is encountered. The break statement is used with decision making statement such as if...else.

Break statements are useful when you want your program-flow to come out of the switch body. Whenever a break statement is encountered in the switch body, the execution flow would directly come out of the switch.

### Syntax of Break Statement

```c
break;
```

### Flowchart of Break Statement

![](img/35ea447eca4d04af54f37bf3d3ca337d_67_0.png)

**Working of break statement:**

```c
while (test Expression)
{
        // codes
        if (condition for break)
        {
                break;
        }
        // codes
}
```

Continue statement works following way:

```c
    while (test Expression)
    {
        // codes
        if (condition for continue)
        {
            continue;
        }
        // codes
    }

    for (init, condition, update)
    {
        // codes
        if (condition for continue)
        {
            continue;
        }
        // codes
    }
```

### The continue statement can be used in for loop

The **continue** allows you to continue the execution of a **for** or **while** loop from the beginning, making it possible to skip the rest of the statement in the loop after the **continue** statement.

![](img/35ea447eca4d04af54f37bf3d3ca337d_70_0.png)

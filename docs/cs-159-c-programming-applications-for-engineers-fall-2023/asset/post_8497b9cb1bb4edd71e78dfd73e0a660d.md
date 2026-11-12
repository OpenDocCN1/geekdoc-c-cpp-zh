
## User-defined function for input of starting value:

```
int getStart(void)
{
    int num;
    do
    {
        printf("Enter starting value -> ");
        scanf("%d", &num);
        if(num < 0)
        {
            printf("\nError! Non-negative values only!\n\n");
        }
    }while(num < 0);
    return(num);
}
```

## User-defined function for input of ending value:

```
int getEnd(int start)
{
    int num;
    do
    {
        printf("Enter ending value -> ");
        scanf("%d", &num);
        if(num < start)
        {
            printf("\nError! Ending value must be at least %d\n\n", start);
        }
    }while(num < start);
    return(num);
}
```

Where are the nested loops? It is common to first consider the examples below when one thinks of nested constructs.

| Nested while loop example: | Nested if construct example: |
|---|---|
| while( )<br>{<br>&nbsp;&nbsp;while( )<br>&nbsp;&nbsp;{<br>&nbsp;&nbsp;}<br>} | if( )<br>{<br>&nbsp;&nbsp;if( )<br>&nbsp;&nbsp;{<br>&nbsp;&nbsp;}<br>} |
| In the nested loop example provided on the previous page the loops are found in two different user-defined functions. One is in the `main` function that counts from the starting point to the ending point and the second is found in the function that calculates the factorial for each integer in the desired range. | |
| Every loop typically represents a task, or single process, in a program. If you can identify each of these individual tasks and factor them into individual user-defined functions you may find the complex problem easier to solve and test. | |

## The Infinite Loop

The infinite loop is a logical error in which the condition of the loop control expression will never be false. As a logical error the form in which infinite loops may appear while the program is running can vary. One sure sign of an infinite loop is the production of infinite output. However, the error can appear in forms in which little or no output is generated.

- You can terminate a program at any time by entering CTRL-C from the keyboard.

| | Output: |
|---|---|
| int getInteger(void)<br>{<br>&nbsp;&nbsp;int num;<br><br>&nbsp;&nbsp;do<br>&nbsp;&nbsp;{<br>&nbsp;&nbsp;&nbsp;&nbsp;printf("Enter 1 or 2 -> ");<br>&nbsp;&nbsp;&nbsp;&nbsp;scanf("%d", &num);<br>&nbsp;&nbsp;}while(num != 1 || num != 2);<br><br>&nbsp;&nbsp;return(num);<br>} | Enter 1 or 2 -> 3<br>Enter 1 or 2 -> 2<br>Enter 1 or 2 -> 1<br>Enter 1 or 2 -> |

- The control expression may seem logically correct, “accept input while the value entered is not 1 or 2”, but logically it results in an infinite loop. There is no single value that cannot be **both** not 1 and not 2 at the same time.

## Repetition Review - Three Common Loop Components

- 1. Initialization of the loop control variable.
- 2. Evaluation of the loop control expression.
- 3. Update to the loop control variable.

## The for loop

The third and final looping construct available in the C programming language is the pretest for loop. In addition to being a pretest looping construct the for loop was designed to be used only with counter-controlled processes. The for loop brings together the initialization, loop control expression, and update to a single line of code. With this benefit it will be a course standard to always make use of all three expressions of a for loop.

| A while loop representation using all three expressions: | Flowchart representation of a for loop: |
|---|---|
| | |

## Expression 1 (Initialization)

- Expression 1 is evaluated only when the `for` loop is encountered for the first time. It is in this expression that the loop control variable will be initialized.

## Expression 2 (Evaluation)

- After expression 1 is evaluated we immediately evaluate expression 2 which is the loop control expression.
- If expression 2 is initially evaluated to be false then the loop will not iterate! The `for` loop is a pretest construct.
- Upon completion of every iteration the loop control expression must be re-evaluated to determine whether another iteration is needed.

## Expression 3 (Update)

- This final expression is evaluated at the end of every iteration and before the next evaluation of expression 2.
- Essentially, any expression changing the loop control variable is acceptable for the third expression.

## Syntax

- Semicolons are necessary between expression 1 and 2 and between expression 2 and 3.
- As with any looping construct the `for` loop has a body and the body will begin and end with `{` and `}`. The body of instructions can be one or more instruction.

## When to use a `for` loop?

Otherwise... consider a `while` for your pretest iteration needs.

Without altering the initialization values, convert the while loop into a for loop:
```cpp
int lcv = 1;
int n = 4;
int nFact = 1;
while(lcv <= n)
{
    nFact *= lcv;
    lcv++;
}
```

Converted loop:

Without altering the initialization values, convert the while loop into a for loop:
```cpp
int lcv;
int n = 4;
int nFact = 1;
lcv = n;
while(lcv > 0)
{
    nFact *= lcv;
    lcv--;
}
```

Converted loop:

What potential concerns exist with the application of the for loop below?
```cpp
int x;
for(x = -1; x < 0; )
{
    printf("Enter a non-negative integer: ");
    scanf("%d", &x);
}
```

## Rearranging Digits in a Number Example:

- Given an integer, rearrange its digits to create the largest number possible.

## Example Executions:

```
Enter an integer: 1230789
The sorted digit is 9873210
Enter an integer: 53635
The sorted digit is 65533
```

## Step 1 – What is specified of the program?

- We expect an integer to be entered and to be output.
- Leading 0's do not make sense as integer input and will not be considered.
- All input will be non-negative and must be validated.

## Step 2 – Analyze the problem

- How do we extract a single digit from a number?
- How do we do this and then determine if it is the largest digit in the number?
- What do we do once we have the largest digit in the number?
- What about finding the second largest digit in the number?

## Step 3 – Designing the Software Solution

What are the tasks of this program?

- 1. Get the input from the user.
- 2. Count the number of non-leading zero digits so we can append them to the value output at the end.
- 3. Find the largest digit in the input. "Add" it to a new number. "Delete" it from the value input.
- 4. Return to step 3 until ALL non-zero digits, largest to smallest, have been moved from the value input to the new integer value being constructed.
- 5. Append the zero digits on to the end of the new value.
- 6. Output.

## Structure Chart

## main Function

## findMax Function

## appendMax Function

## removeMax Function

## Solution:

```
int getInput(void);
int ctZero(int);
int findMax(int, int*);
int appendMax(int, int);
int removeMax(int, int, int);
void output(int);
```

```
int main(void)
{
int n;
int sorted = 0;
int max;
int maxLoc;
int zeroCount;

n = getInput();
zeroCount = ctZero(n);

while(n > 0)
{
max = findMax(n, &maxLoc);
sorted = appendMax(sorted, max);
n = removeMax(n, max, maxLoc);
}

output(sorted * (int)pow(10, zeroCount));

return(0);
}
```

```
int appendMax(int sorted, int max)
{
return(sorted * 10 + max);
}
```

```
int removeMax(int n, int max, int maxLoc)
{
return(n - max * (int)pow(10, maxLoc));
}
```

```c
int getInput(void)
{
    int n;
    do
    {
        printf("Enter an integer to sort: ");
        scanf("%d", &n);
        if(n < 0)
        {
            printf("\nError! Non-negative values only!\n\n");
        }
    }while(n < 0);
    return(n);
}
```

```c
int ctZero(int n)
{
    int ct = 0;
    while(n > 0)
    {
        if(n % 10 == 0)
        {
            ct++;
        }
        n = n / 10;
    }
    return(ct);
}
```

```c
void output(int sorted)
{
    printf("Sorted value: %d\n", sorted);
}
```

```c
int findMax(int n, int *maxLoc)
{
    int max = 0;
    int loc = 0;
    while(n > 0)
    {
        if(n % 10 > max)
        {
            max = n % 10;
            *maxLoc = loc;
        }
        n = n / 10;
        loc++;
    }
    return(max);
}
```

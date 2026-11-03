
6 Now, insert this break statement at the very beginning of the inner loop block, to break out of the inner loop – then save, compile, and run the program once more

```
if ( i == 2 && j == 1 )
{
    printf( "Breaks inner loop when i=%d and j=%d\n", i, j );
    break ;
}
```

![](img/d1dfb0563339ba187decb78799155b7f_82_0.png)

Here the break statement halts all three iterations of the inner loop when the outer loop tries to run it the second time.

![](img/d1dfb0563339ba187decb78799155b7f_82_1.png)

The continue keyword can be used to skip a single iteration of a loop when a specified condition is met. The continue statement is situated inside the loop statement block and is preceded by a test expression. When the test returns true, that single iteration ends.

7 Insert this continue statement at the beginning of the inner loop block, to skip the first iteration of the inner loop – then save, compile, and run the program again

```
if ( i == 1 && j == 1 )
{
    printf( "Continues inner loop when i=%d and j=%d\n", i, j );
    continue;
}
```

![](img/d1dfb0563339ba187decb78799155b7f_82_2.png)

Here the continue statement just skips the first iteration of the inner loop when the outer loop tries to run it for the first time.

![](img/d1dfb0563339ba187decb78799155b7f_82_3.png)

![](img/d1dfb0563339ba187decb78799155b7f_83_0.png)

## Going to labels

The goto keyword supposedly allows the program flow to jump to labels at other points in the program code, much like a hyperlink on a web page. However, in reality this can cause errors; its use is frowned upon; and it is considered bad programming practice.

The goto keyword jump is a powerful feature that has existed in computer programs for decades, but its power was abused by many early programmers who created programs that jumped around in an unfathomable manner. This produced unreadable program code, so the use of goto became hugely unpopular.

One possible valid use of the goto keyword is to break cleanly from an inner nested loop by jumping to a label just after the end of its outer loop block. This immediately exits both loops so no further iterations of either loop are executed.

![](img/d1dfb0563339ba187decb78799155b7f_83_1.png)

![](img/d1dfb0563339ba187decb78799155b7f_83_2.png)

Notice that the goto statement specifies the label by name only, but the label itself must have a terminating : colon.

- 1. Begin a new program with a preprocessor instruction to include the standard input/output library functions.

```c
#include <stdio.h>
```

- 2. Add a main function that declares two integer variables to be used later as loop iteration counters.

```c
int main()
{
    int i, j;
}
```

- 3. Next, in the main function block, insert two nested loops to output their counter values on each of three iterations.

```c
for( i = 1; i < 4; i++ )
{
    for( j = 1; j < 4; j++ )
    {
        printf( "Running i=%d j=%d\n", i, j );
    }
}
```

- 4. Insert a statement as the first line of the inner nested loop, to jump to a label named “end” at a specified counter value.

```c
if( i == 2 && j == 1 ) { goto end; }
```

- 5. Now, add the label after the closing brace of the outer loop.

```c
} end:
```

- 6. At the end of the main function block, return a zero integer value, as required by the function declaration return 0 ;

- 7. Save the program file, then compile and execute the program to see the loops exit after the jump

In C, Boolean values are represented numerically as 1 (true) and 0 (false)

```
```
Command Prompt
C:\MyPrograms>gcc jump.c -o jump.exe
C:\MyPrograms>jump
Running i=1 j=1
Running i=1 j=2
Running i=1 j=3
```
```

One alternative, avoiding the **goto** keyword, might be to check a variable for a Boolean true value (1) on each iteration of each loop:

- 8. Add another variable to the existing variable declarations and initialize with a true value of one int i , j , flag = 1 ;

- 9. Insert a conditional test of the new variable's value, both at the start of the outer loop block and at the start of the inner loop block just before the output statement if ( flag )

Avoid creating a program executable named "goto.exe" as this would conflict with the internal Windows **GOTO** command.

- 10. Change the first line of the inner loop to replace the goto statement with one assigning a false value of zero if ( i == 2 && j == 1 ) { flag = 0 ; }

- 11. Delete the now obsolete end; label after the closing brace then save, compile, and execute the program again to see the same resulting output as before

```
```
Command Prompt
C:\MyPrograms>gcc jump.c -o jump.exe
C:\MyPrograms>jump
Running i=1 j=1
Running i=1 j=2
Running i=1 j=3
C:\MyPrograms>_
```
```

## Summary

- The **if** keyword performs a basic conditional test to evaluate a given expression for a Boolean value of true or false.
- The **else** keyword can be used to provide alternative statements to execute when an **if** statement evaluates an expression as false.
- Offering a program alternative directions in which to proceed following an evaluation is known as “conditional branching”.
- Conditional branching performed by multiple **if else** statements can often be performed more efficiently by a **switch** statement.
- Usually, the **case** statements within a **switch** block must each be terminated by a **break** statement.
- Optionally, a **switch** block may contain a **default** statement specifying statements to execute when no match is found.
- The **for** keyword is followed by parentheses specifying an initializer, test-expression, and incrementer to control a loop.
- The **while** keyword is followed by parentheses specifying a test expression to determine whether a loop should continue.
- A **while** loop block must be preceded by an initializer and contain an incrementer within its statement block.
- The **do** keyword is followed by a statement block after which there must be a **while** statement terminated by a semi-colon.
- A **do while** loop must be preceded by an initializer and contain an incrementer within its statement block.
- Unlike **for** loops and **while** loops, the statements in a **do while** loop will always be executed at least once.
- The **break** keyword can be used to terminate a loop, whereas the **continue** keyword can be used to skip a single iteration.
- Loops may be nested and the **goto** keyword can be used to exit to a specified label, although its use is not recommended.

## 6 Employing Functions

This chapter demonstrates how statements can be enclosed within a "function" for execution whenever called by the C program.

- 86 Declaring functions
- 88 Supplying arguments
- 90 Calling recursively
- 92 Placing functions in headers
- 94 Restricting accessibility
- 96 Summary

Add a main function that declares an integer variable

```c
int main()
{
    int num ;
}
```

![](img/d1dfb0563339ba187decb78799155b7f_88_0.png)

Notice that each function prototype must end with a semi-colon.

After the main function, define the custom functions

```c
void first()
{
    printf( "Hello from the first function\n" ) ;
}
```

```c
int square5()
{
    int square = 5 * 5 ;
    return square ;
}
```

```c
int cube5()
{
    int cube = (5 * 5) * 5 ;
    return cube ;
}
```

Now, insert calls to the custom functions in the main function block

```c
first() ;
num = square5() ;
printf( "5x5= %d\n", num ) ;
printf( "5x5x5= %d\n", cube5() ) ;
```

![](img/d1dfb0563339ba187decb78799155b7f_88_1.png)

The custom function definitions could technically appear before the main() function – but convention is to include prototypes and keep the main() function at the beginning of the program code.

At the end of the main function block, return a zero integer value, as required by that function declaration

```c
return 0 ;
```

Save the program file, then compile and execute the program to see the output from custom functions

![](img/d1dfb0563339ba187decb78799155b7f_88_2.png)

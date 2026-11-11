
```
printf("\n");
}
}
```

### Output

```
Enter the number of rows: 4
*   *   *   *   *   *   *
*   *   *           *   *   *
*   *                   *   *
*                           *
```

| Trace stage | Details shown |
|---|---|
| Initial value of variable i | i = 0 |
| Condition of the outer loop | i <= 3; assume value of x is 4, hence x - 1 = 3 |
| Left loop prints i - 1 stars | Inner loop uses j to print the left-side stars |
| Middle loop prints 2*i spaces | Inner loop uses j to print spaces |
| Right loop prints i - 1 stars | Inner loop uses j to print the right-side stars |
| Position the cursor on the new line | `printf("\n");` is executed as required |
| Increment variable i | `i++` is executed; the next value of i is shown |
| Execution values | i = 0, i = 1, i = 2, i = 3; at i = 4, the outer loop terminates because the condition is not satisfied |

**Figure 5.20:** Execution trace to generate the given symmetric pattern

## 5.4 do..while Loop

The do..while loop is an exit control loop unlike for and while loops which are entry control type of loops. This means that the control is unconditionally transferred inside the body of the do..while loop and condition is tested before executing the next iteration. If the condition is evaluated as ‘false’, the control is transferred outside the loop and if the condition is evaluated as true the control is again transferred inside the body of the loop. In short, the do..while loop first performs the operation specified and then evaluates the condition. It is important to understand that the first iteration of the do..while loop will always execute unconditionally.

Figure 5.21 shows the syntax and working of do..while loop.

> **DEFINITION**
>
> do..while loop is an exit control loop unlike while or for loops which are entry control type of loops.

One of the applications of a do..while loop is design of a ‘menu-driven program’ wherein the options menu is displayed unconditionally for the first time. The options menu will be displayed in the second time, only if the user wishes to perform another operation. Let us design a menu-based calculator that gives the menu with the following assignment of keys dedicated for each operation:

- Key 1 for addition
- Key 2 for subtraction
- Key 3 for multiplication

![](img/57c0d966bb33c67a5a188e6bf39e4e02_195_0.png)

**Figure 5.21:** Syntax and behaviour of the do-while loop

The user will then enter a choice looking at the menu options and the program must then take a decision on which operation to perform depending on the choice entered by the user. Say, if the user enters the choice as 3, then the program should take two numbers as input and perform the multiplication of two numbers. After displaying the result of multiplication, the calculator must ask the user if he/she wishes to perform any other operation.

```
Do you want to continue (Y/N)?
Y
```

If the user enters Y, then the program shall again display the menu options for the user to determine what is the next operation the user wishes to perform and so on. The execution of the program must terminate when the user enters N as an answer to the above question. The typical behaviour of the code is shown in Figure 5.22. The complete source code for this calculator is shown below the figure:

![](img/57c0d966bb33c67a5a188e6bf39e4e02_196_0.png)

**Figure 5.22:** Working of a menu-driven program

```c
#include <stdio.h>
void main()
{
    int choice,a,b,c;
    char opt='y';
    do{
        printf("Welcome to the calculator screen\n");
        printf("Please enter your choice\n");
        printf("1. Add\n2.Subtract\n");
        printf("3. Multiply\n");
        scanf("%d",&choice);
        if(choice == 1)
        {
            printf("enter 2 numbers\n");
            scanf("%d%d",&a,&b);
            c=a+b;
            printf("Addition is %d\n",c);
        }
        else if(choice == 2)
        {
            printf("enter 2 numbers\n");
            scanf("%d%d",&a,&b);
            c=a-b;
            printf("Subtraction is %d\n",c);
        }
        else if(choice == 3)
        {
            printf("enter 2 numbers\n");
            scanf("%d%d",&a,&b);
            c=a * b;
            printf("Multiplication is %d\n",c);
        }
        else
        {
            printf("This is an incorrect option.\n");
        }
        printf("Do you want to continue (Y/N) ?\n");
        scanf(" %c",&opt);/*note a space before %c*/
    }while(opt=='y');
}
```

### EXERCISE

Trace the output of the program assuming user first wants to perform multiplication and then addition. Assume input data of your choice for each of the operations.

## 5.5 break and continue Statements

The break and continue statements are used to modify the default behaviour of loops.

The break statement is used to exit the loop execution and it passes the control to the first statement after the loop. The exit of loop using break statement is often called early exit, because it terminates the execution of the loop even if the condition for running the loop ahead is true. Execution of break statement should always be conditional inside the loop. Executing break statement unconditionally within a loop would mean that loop will just have one iteration that too partially terminated due to break statement. Figure 5.23 shows the effect of break statement executed conditionally within the loop.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_198_0.png)

**Figure 5.23:** Loop behaviour when break is executed conditionally

As seen from Figure 5.23, there are two methods to come out of the loop after inclusion of a break statement. First, when main condition of the loop is itself false, the loop terminates itself naturally. And the second is when the break statement is executed (when the condition to execute break statement is true). Note that when the break statement is executed the loop is terminated abruptly thereby skipping all the other statements which are written after break statement inside the loop. On execution of break, there will be no further iterations even if the main looping condition is still true. As seen from the figure, once break is executed, there will be no check to examine the main looping condition at all. It is very important to note that execution of break statement may result in the current iteration of the loop terminating partially, if there are some statements written after break. This is because the statements which were written before break will be executed fully, whereas the statements after break will be skipped.

On the other hand, continue statement is used to start the next pass of the loop immediately by skipping all the statements in the current pass which appear after the continue statement. Hence, the execution of continue statement should always be conditional, otherwise the statements which are written after continue will not have any meaning. Logically, there should be some operations that are performed in the body of the loop after the conditional block in which continue is executed, otherwise there will be nothing for continue statement to really skip as the loop anyways goes back to check the condition for the next pass after completing the current iteration. This means that the continue statement will have no meaning if it is the last statement in the body of the loop. Figure 5.24 shows the loop behaviour when continue is executed conditionally. As seen, there are two methods to do the next pass of the loop, after the inclusion of continue statement.

- 1. When all the statements in the current pass are completed, loop will naturally march ahead to check the condition for the next pass.
- 2. When continue statement is executed, the loop will skip everything that is written after continue statement and march towards the next pass. Figures 5.25, 5.26, and 5.27 show the working of continue statement with `for`, `while` and `do .. while` loops, respectively.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_199_0.png)

**Figure 5.24:** Loop behaviour when continue is executed conditionally

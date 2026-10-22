
```
}
 bill = cost * flag;
```

- Choosing from two alternatives:

```c
if (ibex > 14)
    goto a;
sheds = 2;
goto b;
a: sheds = 3;
b: help = 2 * sheds;
```

Having the if else structure available allows C to express this choice more cleanly:

```c
if (ibex > 14)
    sheds = 3;
else
    sheds = 2;
help = 2 * sheds;
```

Indeed, newer versions of BASIC and FORTRAN have incorporated else into their syntax.

- Setting up an indefinite loop:

```c
readin: scanf("%d", &score);
if (score < 0)
    goto stage2;
lots of statements
goto readin;
stage2: more stuff;
```

Use a while loop instead:

```c
scanf("%d", &score);
while (score <= 0)
{
    lots of statements
    scanf("%d", &score);
}
more stuff;
```

- Skipping to the end of a loop and starting the next cycle. Use continue instead.

- Leaving a loop. Use break instead. Actually, break and continue are specialized forms of goto. The advantages of using them are that their names tell you what they are supposed to do and that, because they don’t use labels, there is no danger of putting a label in the wrong place.

- Leaping madly about to different parts of a program. In a word, don’t!

There is a use of goto tolerated by many C practitioners—getting out of a nested set of loops if trouble shows up (a single break gets you out of the innermost loop only):

```c
while (funct > 0)
{
    for (i = 1; i <= 100; i++)
    {
        for (j = 1; j <= 50; j++)
        {
            statements galore;
            if (bit trouble)
                goto help;
            statements;
        }
        more statements;
    }
    yet more statements;
}
and more statements;
help: bail out;
```

As you can see from the other examples, the alternative forms are clearer than the goto forms. This difference grows even greater when you mix several of these situations. Which gotos are helping ifs, which are simulating if elses, which are controlling loops, which are just there because you have programmed yourself into a corner? By using gotos excessively, you create a labyrinth of program flow. If you aren’t familiar with gotos, keep it that way. If you are used to using them, try to train yourself not to. Ironically, C, which doesn’t need a goto, has a better goto than most languages because it enables you to use descriptive words for labels instead of numbers.

## Summary: Program Jumps

Keywords:
break, continue, goto

General Comments:
These three instructions cause program flow to jump from one location of a program to another location.

The break Command:
The break command can be used with any of the three loop forms and with the switch statement. It causes program control to skip the rest of the loop or the switch containing it and to resume with the next command following the loop or switch.

Example:

```c
switch (number)
{
    case 4: printf("That's a good choice.\n");
```

The conditional operator (`? :`) creates an expression that, in many cases, provides a more compact alternative to an if else statement.

The ctype.h family of character functions, such as isspace() and isalpha(), offers convenient tools for creating test expressions based on classifying characters.

The switch statement enables you to select from a series of statements labeled with integer values. If the integer value of the test condition following the switch keyword matches a label, execution goes to the statement bearing that label. Execution then proceeds through the statements following the labeled statement unless you use a break statement.

Finally, break, continue, and goto are jump statements that cause program flow to jump to another location in the program. A break statement causes the program to jump to the next statement following the end of the loop or switch containing the break. The continue statement causes the program to skip the rest of the containing loop and to start the next cycle.

## Review Questions

You’ll find answers to the review questions in Appendix A, “Answers to the Review Questions.”

1. Determine which expressions are true and which are false.

   a. 100 > 3 && 'a' > 'c'
   b. 100 > 3 || 'a' > 'c'
   c. !(100>3)

2. Construct an expression to express the following conditions:

   a. number is equal to or greater than 90 but smaller than 100.
   b. ch is not a q or a k character.
   c. number is between 1 and 9 (including the end values) but is not a 5.
   d. number is not between 1 and 9.

3. The following program has unnecessarily complex relational expressions as well as some outright errors. Simplify and correct it.

```c
#include <stdio.h>
int main(void)
{
    int weight, height; /* weight in lbs, height in inches */
    scanf("%d%d", &weight, &height);
    if (weight < 100 && height > 64)
        if (height >= 72)
            printf("You are very tall for your weight.\n");
    else if (height < 72 && > 64)
        printf("You are tall for your weight.\n");
    else if (weight > 300 && ! (weight <= 300)
        && height < 48)
        if (!(height >= 48) )
            printf(" You are quite short for your weight.\n");
    else
        printf("Your weight is ideal.\n");
    return 0;
}
```

4. What is the numerical value of each of the following expressions?

   a. 5 > 2
   b. 3 + 4 > 2 && 3 < 2
   c. x >= y || y > x
   d. d = 5 + ( 6 > 2 )
   e. 'X' > 'T' ? 10 : 5
   f. x > y ? y > x : x > y

5. What will the following program print?

```c
#include <stdio.h>
int main(void)
{
    int num;
    for (num = 1; num <= 11; num++)
    {
        if (num % 3 == 0)
            putchar('$');
        else
            putchar('*');
            putchar('#');
        putchar(' ');
    }
    putchar('\n');
    return 0;
}
```

6. What will the following program print?

```c
#include <stdio.h>
int main(void)
{
    int age = 0;
    while (age++ <= 65)
    {
        if (( age % 20) == 0) /* is age divisible by 20? */
            printf("You are %d. Here is a raise.\n", age);
        if (age = 65)
            printf("You are %d. Here is your gold watch.\n", age);
    }
    return 0;
}
```

9. What will the following program print when given this input?

```
q
c
h
b
```

```c
#include <stdio.h>
int main(void)
{
    char ch;

    while ((ch = getchar()) != '#')
    {
        if (ch == '\n')
            continue;
        printf("Step 1\n");
        if (ch == 'c')
            continue;
        else if (ch == 'b')
            break;
        else if (ch == 'h')
            goto laststep;
        printf("Step 2\n");
    laststep: printf("Step 3\n");
    }
    printf("Done\n");
    return 0;
}
```

10. Rewrite the program in Review Question 9 so that it exhibits the same behavior but does not use a continue or a goto.

## Programming Exercises

8. Modify assumption a. in exercise 7 so that the program presents a menu of pay rates from which to choose. Use a switch to select the pay rate. The beginning of a run should look something like this:

```
****************************************************************
Enter the number corresponding to the desired pay rate or action:
1) $8.75/hr                2) $9.33/hr
3) $10.00/hr               4) $11.20/hr
5) quit
****************************************************************
```

If choices 1 through 4 are selected, the program should request the hours worked. The program should recycle until 5 is entered. If something other than choices 1 through 5 is entered, the program should remind the user what the proper choices are and then recycle. Use #define constants for the various earning rates and tax rates.

9. Write a program that accepts a positive integer as input and then displays all the prime numbers smaller than or equal to that number.

10. The 1988 United States Federal Tax Schedule was the simplest in recent times. It had four categories, and each category had two rates. Here is a summary (dollar amounts are taxable income):

| Category | Tax |
|---|---|
| Single | 15% of first $17,850 plus 28% of excess |
| Head of Household | 15% of first $23,900 plus 28% of excess |
| Married, Joint | 15% of first $29,750 plus 28% of excess |
| Married, Separate | 15% of first $14,875 plus 28% of excess |

For example, a single wage earner with a taxable income of $20,000 owes 0.15 × $17,850 + 0.28 × ($20,000−$17,850). Write a program that lets the user specify the tax category and the taxable income and that then calculates the tax. Use a loop so that the user can enter several tax cases.

11. The ABC Mail Order Grocery sells artichokes for $2.05 per pound, beets for $1.15 per pound, and carrots for $1.09 per pound. It gives a 5% discount for orders of $100 or more prior to adding shipping costs. It charges $6.50 shipping and handling for any order of 5 pounds or under, $14.00 shipping and handling for orders over 5 pounds and under 20 pounds, and $14.00 plus $0.50 per pound for shipments of 20 pounds or more. Write a program that uses a switch statement in a loop such that a response of a lets the user enter the pounds of artichokes desired, b the pounds of beets, c the pounds of carrots, and q allows the user to exit the ordering process. The program should keep track of cumulative totals. That is, if the user enters 4 pounds of beets and later enters 5 pounds of beets, the program should then report 9 pounds of beets. The program then

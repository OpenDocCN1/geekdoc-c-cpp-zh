```
if(c=='S') {printf("\n True");n=1;} else n=0; printf("%d\n",n);
```

To run the mini-program is necessary to start with the #include <stdio.h>. Unless it come more explicit some other file, all mini-programs of this book will only use the stdio.h header file.

In C, as mentioned before, the equality in the attributing is "=", while in the comparing, as in the case of the if, it is "==". In the above example, the statement 1 needed braces, because it is composed of more than one instruction; unlikely, the statement 2, after else, dispenses braces by containing only one statement in it. Many error messages about the if statement refers to the use of "=" instead of "==". For the simple equality, "=", C allows multiple assignment, unlike older languages. We can write, for example, x = y = z = 10;

# The switch-case statement

The if statement can be used in nested form, an if inside another, but in the case of multiple options for decision-making is preferable to use the case statements, which are started in C with the switch keyword. To prevent that the execution includes the following options to valid option, we finished the case statement with a break statement, a word that can also be used in other situations, not only in the switch-case statements, and has its opposite the continue statement.

The program below illustrates the use of if and switch statements:

# Example-program #4

```
/* Program "Multiple.cpp" */
#include <stdio.h>;
#include <stdlib.h>;

char s[80];
int k;
long n;

main()
{
    printf("\nDividing by 3. Type integer greater than zero:\n");
    gets(s);n=atol(s);k=n%3;
    if (k>=0)
    {
        switch(k)
```
The *conditional operator* (? :) creates an expression that, in many cases, provides a more compact alternative to an if else statement.

The ctype.h family of character functions, such as isspace() and isalpha(), offers convenient tools for creating test expressions based on classifying characters.

The switch statement enables you to select from a series of statements labeled with integer values. If the integer value of the test condition following the switch keyword matches a label, execution goes to the statement bearing that label. Execution then proceeds through the statements following the labeled statement unless you use a break statement.

Finally, break, continue, and goto are jump statements that cause program flow to jump to another location in the program. A break statement causes the program to jump to the next statement following the end of the loop or switch containing the break. The continue statement causes the program to skip the rest of the containing loop and to start the next cycle.

# Review Questions

You’ll find answers to the review questions in Appendix A, “Answers to the Review Questions.”

+   1. Determine which expressions are true and which are false.
+      a. 100 > 3 && 'a' > 'c'
+      b. 100 > 3 || 'a' > 'c'
+      c. !(100>3)

+   2. Construct an expression to express the following conditions:
+      a. number is equal to or greater than 90 but smaller than 100.
+      b. ch is not a q or a k character.
+      c. number is between 1 and 9 (including the end values) but is not a 5.
+      d. number is not between 1 and 9.

+   3. The following program has unnecessarily complex relational expressions as well as some outright errors. Simplify and correct it.

```
#include <stdio.h>
int main(void)
{
    int weight, height; /* weight in lbs, height in inches */
    scanf("%d , weight, height");
    if (weight < 100 && height > 64)
        if (height >= 72)
            printf("You are very tall for your weight.\n");
```
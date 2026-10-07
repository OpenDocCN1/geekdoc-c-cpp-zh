```
/* this is a program with a recursive function */
#include <stdio.h>

int three_powered(int power);

int main(void) {
    int a = 4;
    int b = 9;

    printf("\n3 to the power of %d is %d", a, three_powered(a));
    printf("\n3 to the power of %d is %d\n", b, three_powered(b));

    return 0;
}

int three_powered(int power) {
    if (power < 1)
        return (1);
    else
        return (3 * three_powered(power - 1));
}
```

# Answers for Lesson 6

# Quiz

+   1. The first index value of an array in C is 0.
2. A for statement contains initializing and increment expressions as parts of the command.
3. A do...while contains the while statement at the end and always executes the loop at least once.
4. Yes, a while statement can accomplish the same task as a for statement, but you need to do two additional things. You must initialize any variables before starting the while command, and you need to increment any variables as a part of the while loop.
5. There is no limit to the number of statements you nest.
# MULTIPLE INCREMENTS

As with multiple initialisations, you can have multiple increments in a for loop also separated by commas - for (a = 0; b = 1; <test>; a++, b* = 2) This is useful if there are two or more variables that change consistently while the loop runs

# Switch statements

One thing that you often want to do is test a variable against several values and do different things based on each of them. You can do this with a set of nested if statements:

```
#include <stdio.h>

void main (void) {
    int a = 0;

    if (a == 0) {
        printf("a is equal to 0\n");
    } else if (a == 1) {
        printf("a is equal to 1\n");
    } else {
        printf("a is greater than 1\n");
    }
}
```

That does start to get pretty long wounded though so C provides a neater way of doing this. called a switch statement.

```
#include <stdio.h>

void main (void) {
    int a = 0;
```
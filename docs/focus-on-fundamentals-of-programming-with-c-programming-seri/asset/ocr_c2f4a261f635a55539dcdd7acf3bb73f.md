Here's a program to count the number of characters read from an input stream until an EOF is encountered:

```
```c
// count1.c
#include <stdio.h>
int main(void) {
    int c, count = 0;
    while ((c = getchar()) != EOF) {
        ++count;
    }
    printf("%d\n", count);
    return 0;
}
```
```

Note that c is declared to be an int rather than a char. This is because EOF is given a defined value of -1. On some machines a char can only be a positive value and therefore to return a -1 we define c to be an int.

We can replace the while statement above with a for statement:

```
```c
// count2.c
#include <stdio.h>
int main(void) {
    int count;
    for (count = 0; getchar() != EOF; ++count) {
        ;
    }
    printf("%d\n", count);
    return 0;
}
```
```
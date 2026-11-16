# Functions Revisited Homework

+   1. Write a function, timeUpdate(), that is passed three int parameters, hour, min, sec, representing the current time and returns the time updated by one second. The function should work with a 24-hour clock where 4:30 am is represented by 4:30 and 4:30 pm is represented by 16:30.

+   2. Explain the output of the following program. Does interchanging the arguments in the last printf() statement make any difference?

```
#include<stdio.h>

int main(void) {
    char a = 127, b = 128;

    printf("%5d %5d %5d\n", a, a + 1, b);
    printf("%5d %5d %5d\n", a, a += 1, b, a);

    return 0;
}
```

```
Output:
127   128  -128
127  -128  -128  -128
```
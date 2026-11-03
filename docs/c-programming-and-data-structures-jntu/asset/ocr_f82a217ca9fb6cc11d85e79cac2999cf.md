# Additional Built-in Macros

C99 adds the following macros to those already supported by C89:

| Macro | Description |
|---|---|
| __STDC_HOSTED__ | 1 if an operating system is present. |
| __STDC_VERSION__ | 199901L or greater. Represents version of C. |
| __STDC_IEC_559__ | 1 if IEC 60559 floating-point arithmetic is supported. |
| __STDC_IEC_559_COMPLEX__ | 1 if IEC 60559 complex arithmetic is supported. |
| __STDC_ISO_10646__ | A value of the form yyyymmL that states the year and month of the ISO/IEC 10646 specification supported by the compiler. |

# Declaring Variables within a for Loop

C99 enhances the for loop by allowing one or more variables to be declared within the initialization portion of the loop. A variable declared in this way has its scope limited to the block of code controlled by that statement. That is, a variable declared within a for loop will be local to that loop. This feature has been included in C because often the variable that controls a for loop is needed only by that loop. By localizing this variable to the loop, unwanted side effects can be avoided.

Here is an example that declares a variable within the initialization portion of a for loop:

```
```c
#include <stdio.h>
int main(void)
{
    // declare i within for
    for(int i=0; i < 10; i++)
        printf("%d ", i);
    return 0;
}
```
```

Here, i is declared within the for loop, rather than prior to it.

As mentioned, a variable declared within a for is local to that loop. Consider the following program. Notice that the variable i is declared twice: at the start of main( ) and inside the for loop.

```
```c
#include <stdio.h>
int main(void)
{
    int i = -99;
    // declare i within for
    for(int i=0; i < 10; i++)
        printf("%d", i);
    printf("\n");
}
```
```
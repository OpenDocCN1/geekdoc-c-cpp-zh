# Math Library functions

When you can’t find an operator to do your math, you need to turn to the C library. There you’ll find fun and friendly functions to sate your mathematical whims. In this section, we cover two of the typical C language math library functions: the square root function and the power function. We’ll also discuss the random number generating function, which isn’t really a math function, but it’s something you may find quite handy.

To generate the square root of a value, you use the *sqrt* function. It reads like “sqrt,” but it’s really “square root.” The square root function is shown at line 8 in the code below:

```
```c
#include <stdio.h>
#include <math.h>

int main()
{
    float r;

    r = sqrt(2.0);

    printf("The square root of 2 is %f\\n", r);

    return(0);
}
```
```

As you can see in line 2, it requires the math.h header file. The function swallows a floating point value specified as It returns
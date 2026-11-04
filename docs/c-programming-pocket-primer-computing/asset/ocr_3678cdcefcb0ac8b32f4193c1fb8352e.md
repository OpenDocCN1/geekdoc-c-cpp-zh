assigned, which is -123. Since -123 is not equal to 0, the if portion of the code is true. Consequently, the code inside the if portion is executed, which is why the following incorrect output is printed:

z is even: -123

Although this specific logical error can be easily discovered, logical errors can be much more difficult to detect, especially in long and complex C programs.

# ARITHMETIC OPERATORS AND CONDITIONAL LOGIC

Listing 2.3 displays the contents of IfElse3.c that illustrates how to use multiple if-else code blocks in a C program. Recall the code sample in Chapter 1 that uses %d for formatting purposes in the printf() function.

# LISTING 2.3: IfElse3.c

```
#include <stdio.h>

int main()
{
    int x=8, y=-12, z=10;

    printf("x: %d y: %d z: %d\n",x,y,z);

    if( x == 3 ) { z = 0; }
    else    { z = 8; }
    printf("x: %d y: %d z: %d\n",x,y,z);

    if( y < 0 ) { z *= 3; }
    printf("x: %d y: %d z: %d\n",x,y,z);

    if( z % 2 == 0 ) { x /= 4; }
```
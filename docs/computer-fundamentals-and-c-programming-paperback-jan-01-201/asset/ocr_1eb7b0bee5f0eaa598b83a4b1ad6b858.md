From the above and as shown in Figure 11.1, we can conclude that every function call has a separate area earmarked for it. This area is deallocated after the function terminates. But since `main` is the first function to be called and the last to terminate, its variables have a longer *lifetime* compared to variables and parameters of other functions. Visibility and lifetime are important attributes of variables that we need to address, and soon we will.

# 11.5.4  `swap_failure.c`: The “Problem” with Local Variables

Program 11.3 demonstrates the limited visibility of function parameters and local variables. It makes an unsuccessful attempt to swap the values of two variables that are passed as arguments to a function. In the process, it establishes that the area of memory allocated to function arguments is separate from that used by the parameters and local variables of a function.

```
/* swap_failure.c: Establishes the impossibility of swapping two values
   using parameters and local variables of a function. */

#include <stdio.h>
void swap(short x, short y);                 /* Function returns no value */
int main(void)
{
    short x = 1, y = 100, temp = 0;

    printf("In main before swap: x = %hd, y = %hd\n", x, y);
    swap(x, y);
    printf("In main after swap: x = %hd, y = %hd\n", x, y);
    printf("In main temp seen as %hd\n", temp);

    return 0;
}
void swap(short x, short y)                 /* x and y local to swap */
{
    short temp;                             /* Local variable */
    temp = x;
    x = y;
    y = temp;                               /* Values swapped inside function */
    printf("In swap after swap: x = %hd, y = %hd\n", x, y);
    printf("In swap temp set to %hd\n", temp);
    return;
}
```

PROGRAM 11.3: `swap_failure.c`

```
In main before swap: x = 1, y = 100
In swap after swap: x = 100, y = 1
In swap temp set to 1
In main after swap: x = 1, y = 100
In main temp seen as 0
```

PROGRAM OUTPUT: `swap_failure.c`
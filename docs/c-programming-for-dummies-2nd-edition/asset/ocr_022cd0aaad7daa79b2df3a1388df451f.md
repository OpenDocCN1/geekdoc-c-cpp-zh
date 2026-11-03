at that address. The *p variable represents that value as a `char` inside the `putchar()` function. This operation is then repeated for `char` variables `b` and `c`.

**Exercise 18-11:** Create a new project by using the source code from Listing 18-7. Build and run.

Figure 18-3 attempts to illustrate the behavior of pointer variable `p` as the code runs.

![](bbox=[0.133, 0.266, 0.893, 0.438])

**Exercise 18-12:** Write a program that declares both an `int` variable and an `int` pointer variable. Use the pointer variable to display the value stored by the `int` variable.

Just as you can grab a variable's value, as shown in Listing 18-7, you can use the `*pointer` operator to set a variable's value. Refer to Listing 18-8.

# ### LISTING 18-8: Assigning Values by Using a Pointer

```
```c
#include <stdio.h>

int main()
{
    char a,b,c;
    char *p;

    p = &a;           /* initialize */
    *p = 'A';         /* assign */
    p = &b;           /* initialize */
    *p = 'B';         /* assign */
```
```

*(continued)*
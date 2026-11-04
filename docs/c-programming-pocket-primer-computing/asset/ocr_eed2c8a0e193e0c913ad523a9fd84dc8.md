```
```c
#include <math.h>
#include <stdio.h>

int main()
{
   double y, z;

   y = ceil(1.05);      // y = 2.0
   z = ceil(-1.05);     // z = -1.0
   printf("y = %.2f ; z = %.2f\n", y, z);

   y = floor(2.8);
   z = floor(-2.8);
   printf("y = %.2f ; z = %.2f\n", y, z);

   return 0;
}
```
```

**Listing 1.5** contains a `main()` function that initializes the variables `y` and `z` with two invocations of the built-in `ceil()` function in C. Next, a `printf()` statement displays the values of `z` and `y`, and then `y` and `z` are assigned different values by invoking the built-in `floor()` function in C, after which their values are displayed. The output from compiling and executing the code in **Listing 1.5** is here:

```
```text
The absolute value of x1 is 4.
fabs( -11.230000 ) = 11.230000
```
```

# CALCULATING ABSOLUTE VALUES

C provides built-in functions that perform arithmetic calculations on floating point numbers, such as the `fabs()` function. **Listing 1.6** displays the contents of `AbsValues.c` that illustrates how to calculate the absolute values of integers and decimal values.
# Exploring some common math functions

Not everyone is going to employ their C language programming skills to help pilot a rocket safely across space and into orbit around Titan. No, it's more likely that you'll attempt something far more down-to-earth. Either way, the work will most likely be done by employing math functions. I've listed some common ones in Table 11-3.

# TABLE 11-3 Common, Sane Math Functions

| Function | #include | What It Does |
|---|---|---|
| sqrt() | math.h | Calculates the square root of a floating-point value |
| pow() | math.h | Returns the result of a floating-point value raised to a certain power |
| abs() | stdlib.h | Returns the absolute value (positive value) of an integer |
| ceil() | math.h | Rounds up a floating-point value to the next whole number (nonfractional) value |
| floor() | math.h | Rounds down a floating-point value to the next whole number |

All the functions listed in Table 11-3, save for the abs() function, deal with floating-point values. The abs() function works only with integers.

![](bbox=[0.15, 0.51, 0.22, 0.66])

You can look up function references in the man pages, as described in Chapter 1.

Listing 11-5 is littered with a smattering of math functions from Table 11-3. The compiler enjoys seeing these functions, as long as you remember to include the math.h header file at Line 2.

# LISTING 11-5: Math Mania Mangled

```
#include <stdio.h>
#include <math.h>

int main()
{
    float result,value;

    printf("Input a float value: ");
    scanf("%f",&value);
    result = sqrt(value);
    printf("The square root of %.2f is %.2f\n",
           value,result);
}
```
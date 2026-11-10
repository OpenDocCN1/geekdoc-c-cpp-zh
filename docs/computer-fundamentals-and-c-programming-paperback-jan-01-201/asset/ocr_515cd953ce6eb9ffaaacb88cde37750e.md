```
/* all_about_real.c: Assigns and displays the floating point types.
   Determines the precision of float and double on your machine. */
#include <stdio.h>

int main(void)
{
    float pi1 = 3.142, pi2 = 0.3142E1, pi3 = 3.142E-3;
    float float_x = 12345.678901234567890;        /* 20 significant digits */
    double double_y = 12345.678901234567890;      /* Same */
    float sensex1 = 25341.86;
    float sensex2, gain;

    printf("pi1 = %f, pi2 = %e, pi3 = %g\n", pi1, pi2, pi3);
    printf("float_x = %.15f\n", float_x);
    printf("double_y = %.15f\n", double_y);

    /* Uncomment these 2 lines if your computer supports long double */
    /* long double ldouble_z = 12345.678901234567890;
    printf("ldouble_z = %.20Lf\n", ldouble_z); */

    printf("Enter today's value of Sensex: ");
    scanf("%f", &sensex2);
    gain = (sensex2 - sensex1) / sensex1 * 100;
    printf("Sensex returns since March 31, 2016: %f%%\n", gain);

    return 0;
}
```

PROGRAM 5.4: **all_about_real.c**

| Output | Accuracy |
|---|---|
| pi1 = 3.142000, pi2 = 3.142000e+00, pi3 = 3.142<br>float_x = 12345.678710937500000<br>double_y = 12345.678901234567093<br>Enter today's value of Sensex: 28743<br>Sensex returns since March 31, 2016: 13.421039% | Accuracy to 8 significant digits<br>Accuracy to 17 significant digits |

PROGRAM OUTPUT: **all_about_real.c**

> **Takeaway:** A floating point data type is selected based on the precision it can handle. The float and double types handle 6 and 10 digits of precision, respectively.

# 5.11  char: THE CHARACTER TYPE

C supports the char data type which is just wide enough to hold the values of the computer’s character set. Our PCs use the 8-bit ASCII character set, so char by definition is one byte wide. Even though char is essentially an integer type, we are discussing it separately for two reasons:
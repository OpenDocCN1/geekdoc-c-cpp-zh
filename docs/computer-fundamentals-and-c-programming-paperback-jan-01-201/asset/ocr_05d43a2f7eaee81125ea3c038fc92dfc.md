digit-letter from digits. For instance, if remainder is 15 from a division by 16, digits[remainder] is 'F'. This value is stored in digit_arr, which is finally reversed by the second for loop. The last for loop simply reads this converted array.

```
/* decimal2anybase.c: Extends decimal2binary.c to convert a number to any base.
   Reverses an array without using a second one. */
#include <stdio.h>
int main(void)
{
    char digit_arr[80];
    char digits[16] = {'0','1','2','3','4','5','6','7','8','9',
                       'A','B','C','D','E','F'};
    short i, j, imax, temp, base, remainder;
    long quotient;

    printf("Enter number to convert and base: ");
    scanf("%ld%hd", &quotient, &base);
    for (i = 0; quotient > 0; i++) {      /* Divide repeatedly */
        remainder = quotient % base;
        quotient /= base;
        digit_arr[i] = digits[remainder];   /* Select digit from array */
    }
    imax = i;                              /* Number of digits to be printed */

    /* Reverse the array before printing the digits */
    for (i = 0, j = imax - 1; i < imax / 2; i++, j--) {
        temp = digit_arr[i];
        digit_arr[i] = digit_arr[j];
        digit_arr[j] = temp;
    }
    for (i = 0; i < imax; i++)
        printf("%c ", digit_arr[i]);
    return 0;
}
```

|  |  |  |
|---|---|---|
| PROGRAM 10.6: **decimal2anybase.c** |  |  |
| Enter number to convert and base: **12 2**<br>1 1 0 0 |  | 2³ + 2² = 12 |
| Enter number to convert and base: **127 2**<br>1 1 1 1 1 1 1 |  | Seven 1s—127 |
| Enter number to convert and base: **255 8**<br>3 7 7 |  | 3 × 8² + 7 × 8¹ + 7 × 8⁰ = 255 |
| Enter number to convert and base: **255 16**<br>F F |  | 15 × 16¹ + 15 × 16⁰ = 255 |

PROGRAM OUTPUT: **decimal2anybase.c**
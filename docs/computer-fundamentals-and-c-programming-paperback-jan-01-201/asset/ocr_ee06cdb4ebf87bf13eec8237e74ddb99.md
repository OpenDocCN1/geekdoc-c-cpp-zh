| Factorial of which number? | Result |
|---|---|
| 4 | Factorial of 4 = 24 |
| 6 | Factorial of 6 = 720 |
| 1 | Factorial of 1 = 1 |

PROGRAM OUTPUT: **factorial.c**

# 8.3.2 `extract_digits.c`: Program to Reverse Digits of an Integer

Program 8.3 performs the dual task of reversing the digits of an integer and printing their sum. Using 10 as the divisor, each digit is extracted from the right using the / and % operators. The program has the demerit of not saving the digits, so you can’t perform any other task with them once printing is complete.

```
/* extract_digits.c: Reverses the digits of an integer. Prints and sums
   the digits using the % and / operators. */
#include <stdio.h>
int main(void)
{
    unsigned int number;
    short last_digit, sum = 0;

    printf("Key in an integer: ");
    scanf("%d", &number);

    while (number != 0) {
        last_digit = number % 10;          /* Extracts last digit */
        number = number / 10;              /* Removes last digit */
        sum += last_digit;
        printf("%hd ", last_digit);
    }
    printf("\nSum of digits: %hd\n", sum);
    return 0;
}
```

PROGRAM 8.3: **extract_digits.c**

```
Key in an integer: 13569
9 6 5 3 1
Sum of digits: 24
```

PROGRAM OUTPUT: **extract_digits.c**

In every iteration of the **while** loop, the / operation removes the last digit and the % operation saves this digit. This is how the values of the variables `last_digit` and `number` change with every loop iteration:
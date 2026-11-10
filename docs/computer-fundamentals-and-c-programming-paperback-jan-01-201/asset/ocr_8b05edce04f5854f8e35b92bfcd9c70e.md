**Takeaway:** In a nested `while` structure there is a one-to-many relationship between the outer and inner loop. For every iteration of the outer loop, the inner loop must complete its set of iterations before the next iteration of the outer loop can begin.

# 8.5.3 `power.c`: Computing Power of a Number

Program 8.7 uses an outer loop to take two integers (x and y) as user input. It then uses an inner loop to compute the value of x raised to the power y. The program handles only positive integers but quits when the user keys in a zero (for the first number) or a negative integer (for both numbers).

```
/* power.c: Computes power of multiple sets of numbers using a nested
          while loop. Repeatedly multiplies a number by itself. */
#include <stdio.h>
int main(void)
{
    short num, base = 1, power = 1;
    unsigned long total;

    while (base > 0 && power >= 0) {
        printf("Enter base and power (0 0 to exit): ");
        scanf("%hd%hd", &base, &power);

        if (base <= 0 || power < 0) {       /* Invalid Input */
            printf("Invalid Input. Quitting ...\n");
            return 1;
        }

        num = 0; total = 1;                  /* Initialization before inner loop */
        while (++num <= power)
            total *= base;                   /* Multiply base by itself */
        printf("%d to the power %d = %lu\n", base, power, total);
    }
    return 0;
}
```

PROGRAM 8.7: `power.c`

```
Enter base and power (0 0 to exit): 2 0
2 to the power 0 = 1

Enter base and power (0 0 to exit): 2 10
2 to the power 10 = 1024

Enter base and power (0 0 to exit): 0 0
Invalid Input. Quitting ...
```

PROGRAM OUTPUT: `power.c`
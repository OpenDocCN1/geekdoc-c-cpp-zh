The above program displays the numbers from 1 to 10, except the number 5.

# Program 4.11: Program to sum integers entered interactively

```
#include <stdio.h>
int main(void)
{
long num;
long sum = 0L; /* initialize sum to zero */
int status;

printf("Please enter an integer to be summed."); printf("Enter q to quit.\n");
status = scanf("%ld", &num);
while (status == 1)
{
sum = sum + num;
printf("Please enter next integer to be summed."); printf("Enter q to quit.\n");
status = scanf("%ld", &num);
}
printf("Those integers sum to %ld.\n", sum); return 0;
}
```

# 4.10 Summary

In C by default, statements are executed in sequence, one after another. We can, however, modify that sequence
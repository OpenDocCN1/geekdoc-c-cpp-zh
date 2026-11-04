```
printf("Enter two positives: ");
scanf("%lf%lf", &i, &j);
printf("%d &d\n", (int)i+(int)j, (i-(int)i) + (j-(int)j));
return 0;
}
```

# C.3.10 Write a program that reads a positive integer and converts it to multiples of 50, 20, 10, and 1. For example, if the user enters 285, the program should display 5*50, 1*20, 1*10, 5*1.

```
#include <stdio.h>
int main(void)
{
    int i, n_50, n_20, n_10, n_1, rem;
    printf("Enter positive number: ");
    scanf("%d", &i); /* Suppose that the user enters 285, so i = 285. */
    /*
    n_50 = i/50; /* n_50 = 285/50 = 5. */
    rem = i%50; /* The rem = 285%50 = 35 should be analysed in 20s, 10s, and units. */
    n_20 = rem/20; /* n_20 = 35/20 = 1. */
    rem = rem%20; /* The rem = 35%20 = 15 should be analysed in 10s and units. */
    n_10 = rem/10; /* n_10 = 15/10 = 1. */
    n_1 = rem%10; /* n_1 = 15%10 = 5. */
    printf("%d*50,%d*20,%d*10,%d*1\n", n_50, n_20, n_10, n_1);
    return 0;
}
```

Comments: The % operator is used to find the remainder of the division. We could use only i, and write: printf("%d*50, %d*20, %d*10, %d*1\n", i/50, i%50/20, i%50%20/10, i%50%20%10);

# C.3.11 Write a program that reads a two-digit positive integer and displays the reversed number. For example, if the user enters 72, the program should display 27. Use one integer variable.

```
#include <stdio.h>
int main(void)
{
    int i;
    printf("Enter number between 10 and 99: ");
    scanf("%d", &i);
    i = 10*(i%10) + i/10;
    printf("%d\n", i);
    return 0;
}
```
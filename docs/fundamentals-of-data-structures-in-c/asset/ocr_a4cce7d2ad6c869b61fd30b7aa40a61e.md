```
The program displays the following output
Enter principal,rate,no.of.years,compounding/year
34 124 5 6
Simple Interest is 210.80
Compound Interest is 8636.00
```

# Program S8 :

Write a program to find whether the given year is leap or not.

```
/* leapyear.c */
#include<stdio.h>
void main()
{
 int x;
 printf("Enter the year : ");
 scanf("%d",&x);
 if (x % 4 == 0) && (x % 100 == 0) || (x % 400 != 0))
 printf("%d is a leap year", x);
 else
 printf("%d is not a leap year", x);
}
```

```
The program displays the following output
RUN1 Enter the year : 1999
1999 is not a leap year
RUN2 Enter the year : 2000
2000 is a leap year
```

# Program S9 :

Write a program to find the factorial of a given number.

```
/* factorial.c */
#include<stdio.h>
void main()
{
 long i, j, x = 1;
 printf("Enter the number : ");
 scanf("%d",&i);
 for (j = 1 ; j <= i ; j++)
 x = j * x;
 printf("Factorial value of %d is %d", i, x);
}
```

```
The program displays the following output
Enter the number : 5
Factorial value of 5 is 120
```

# Program S10 :

Write a program to find the sum of digits of an integer.

```
/* digitsum.c */
#include<stdio.h>
void main()
{
 long x, y = 0, z = 0;
 printf("Enter the number : ");
```
# 2.13 Simple Programs

# Program S1 :

Write a program to read an integer of N digits and reduce the integer to a single digit number.

```
/* digitcnt.c */
#include<stdio.h>
long DigitCount(long n);
void main()
{
 long no;
 printf("Enter an integer : ");
 scanf("%ld", &no);
 printf("Its single digit is %ld", DigitCount(no));
}
long DigitCount(long n)
{
 return(n / 10 == 0 ? n : DigitCount(n / 10 + n % 10));
}
```

> The program displays the following output
> Enter an integer : 987456
> Its single digit is 3

# Program S2 :

Write a program to generate fibonacci series using recursion.

```
/* genfibo.c */
#include <stdio.h>
void fibo(int, int, int); /* function prototype */
void main()
{
 int x = -1, y = 1, z = 0;
 printf("Enter any number : ");
 scanf("%d", &z);
 printf("The fibonacci series is : ");
 fibo(z, x, y); /* calling the function fibo() */
}
```
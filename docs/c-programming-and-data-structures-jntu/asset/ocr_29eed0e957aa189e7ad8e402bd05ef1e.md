# 12. /* Write a C program to find the sum of individual digits of a positive integer by using long long int in C99 standards*/

```
#include<stdio.h>
#include<conio.h>
void main()
{
    long long int num, k=1, sum=0; // long long int
    clrscr();
    printf("Enter the number whose digits are to be added:");
    scanf("%lld",&num);
    while(num!=0)
    {
        k=num%10;
        sum=sum+k;
        k=num/10;
        num=k;
    }
    printf("Sum of the digits:%lld",sum);
    getch();
}
```
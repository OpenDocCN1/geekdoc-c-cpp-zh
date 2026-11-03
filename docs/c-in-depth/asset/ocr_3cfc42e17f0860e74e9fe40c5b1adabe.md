```
if(num>=500)
    num=roman(num,500,'d');
if(num>=100)
    num=roman(num,100,'c');
if(num>=50)
    num=roman(num,50,'l');
if(num>=10)
    num=roman(num,10,'x');
if(num>=5)
    num=roman(num,5,'v');
if(num>=1)
    roman(num,1,'i');
printf("\n");
}
int roman(int n,int k,char c)
{
    if(n==9)
    {
        printf("ix");
        return 0;
    }
    if(n==4)
    {
        printf("iv");
        return 0;
    }
    while(n>=k)
    {
        printf("%c",c);
        n=n-k;
    }
    return n;
}
```

# Problem 5

Write a program that prints the reverse of a positive integer using recursion.

```
/*P6.32 Program to print the reverse of a positive integer*/
#include<stdio.h>
void reverse(long int n);
main()
{
    long int num;
    printf("Enter number : ");
    scanf("%ld",&num);
    reverse(num);
    printf("\n");
}
void reverse(long int n)
{
    int rem;
```
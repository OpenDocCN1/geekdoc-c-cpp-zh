![](bbox=[0.244, 0.082, 0.765, 0.309])

# Sample Program

Program in C to reverse a given four-digit integer number and check whether it is a palindrome or not *using for loop*. Output the given number with a suitable message.

```
```c
#include<stdio.h>
#include<process.h>
void main()
{
    int n, num, rev=0, rem, i;
    printf("Enter a number: \n");
    scanf("%d", &n);
    num=n;

    /* check if the input is a 4 digit number */
    if(n<=999||n>=10000)
    {
        printf("\nEnter four digit number\n");
        exit(0);
    }

    for(i=n; i!=0;)
    {
        rem=i%10;
        rev=rev*10+rem;
        i=i/10;
    }

    printf("\nReverse of the input is: \n\t%d", rev);
```
```
```
```c
{
    /*Loop for printing spaces*/
    for(j=1;j<=r-i;j++)
    {
        printf(" ");
    }
    /*Loop for printing stars*/
    for(j=1;j<=2*i+1;j++)
    {
        printf("*");
    }
    printf("\\n");
}
```
```

**Inner Loop1:** This is a for loop to print spaces in the current row. Each row has `r-i` spaces, hence the loop runs from `j=1` to `r-i`.

**Inner Loop2:** This is a for loop to print stars in the current row. Each row has `2*i+1` stars, hence the loop runs from `j=1` to `2*i+1`.

To transfer control on new line after printing each row

# Solved Example 5.4

Write a program to take a number as input from the user and to check if it is an Armstrong number.

**Note:** Armstrong number is a number whose sum of cube of digits is same as the number itself. For example, if we consider a number as 153, the sum of cube of digits of 153 is:

$1^3+5^3+3^3$  
$= 153$ itself.

Hence, when we extract individual digits of 153 and find the sum of cube of its digits we get the number 153 back. Therefore, 153 is an Armstrong number.

```
```c
#include <stdio.h>
void main()
{
int sum=0,x,d,temp;
printf("Enter a number:");
scanf("%d",&x);
temp=x;
    while(x!=0)
    {
        d=x%10; /*get the individual digit*/
        sum=sum+d*d*d; /*sum of cube of digits*/
        x=x/10; /*Use quotient for the next addition*/
    }

    if(sum==temp)
    {
        printf("The number is a Armstrong number\\n");
    }
}
```
```
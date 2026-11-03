```
for(m=num;m>0;m/=10)/*Loop C*/
{
    d1=m%10;
    for(n=num*2;n>0;n/=10)/*Loop D*/
    {
        d2=n%10;
        for(p=num*3;p>0;p/=10)  /*Loop E*/
        {
            d3=p%10;
            if(d1==d2||d2==d3||d1==d3)
                goto nextnum;
        }/*End of Loop E*/
    }/*End of Loop D*/
}/*End of loop C*/
printf("%d %d %d\t",num,num*2,num*3);
nextnum:
}/*End of loop A*/
}/*End of main()*/
```

Loop A is used to generate numbers. Since triad numbers are three digit numbers, hence this loop sta from 100. The upper limit of this loop is 333 (999/3) because for numbers more than 333, 3*num v not be a three digit number.

Loop B is inside loop A, and it executes three times, for i = num, i = 2*num and i = 3*num. It fi out whether the three digits in a number(i) are different or not. In this loop d1, d2, d3 are digits of a single number, and if any two digits are found to be sar.e then we again go to the update expression of loop A to check for next number.

Loops C, D, E are nested loops which find out whether there are any common digits in the th numbers(num, 2*num, 3*num). Here d1, d2, d3 are digits of num, 2*num, 3*num respectively. If : two digits are same then we go to the update expression of loop A to check for next number. Note that in loops C, D and E, the digits of different numbers are compared, and in loop B digit a single number are compared.

# Problem 7

Write a program to find out the Least Common Multiple and Highest Common Factor of two numb

```
/*P5.42 Program to find the LCM and HCF of two numbers*/
#include<stdio.h>
main()
{
    int x,y,a,b;
    printf("Enter two numbers : ");
    scanf("%d %d",&x,&y);
    a=x;b=y;
    while(a!=b)
    {
        if(a<b)
            a=a+x;
        else
            b=b+y;
```
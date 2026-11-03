# Operations on Bits

```
for(i=1;i<=n;i++)
{
    lsbit=num&1?1:0;            /* Test LSB */
    num=num>>1;
    if(lsbit==0)
        num=num&~(1<<15);  /*Switch off MSB*/
    else
        num=num|(1<<15);   /*Switch on MSB*/
}
return num;

rotate_left(int num,int n)

int i,msbit;

for(i=1;i<=n;i++)
{
    msbit=num&(1<<15)?1:0;          /*Test MSB*/
    num=num<<1;
    if(msbit==0)
        num=num&~1;        /*Switch off LSB*/
    else
        num=num|1;         /*Switch on LSB*/
}
return num;
```

# Problem 8

Write a function mult(num, n, err) that uses the shift operators >> and << to compute the value of num * 2^n. Assume that both num and n are unsigned positive integers and are 32 bits in size. The err parameter is set by the function to zero if calculation is successful and 1 if an overflow occurs. An overflow occurs when the resultant value doesn't fit in the 32 bit unsigned integer. Do not use add, subtract, multiply or divide to compare the result.
*P13.20*

```
#include<stdio.h>
main()
{
unsigned int num,n,err=0;
printf("Enter the number and power of 2 : ");
scanf("%u%u",&num,&n);
mult(num,n,err);
}

mult(int num,int n,int err)
{
unsigned int result=num;
while(n>0)
{
    num=num<<1; /*Multiply by 2*/
    n--;
    if(num<result)
```
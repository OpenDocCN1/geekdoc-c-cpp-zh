# A.16 Computer Programming

```
while(y<row)
{
for(x=40-3*y;x>0;--x)
printf(" ");
for(z=0;z<=y;++z)
{
if((z==0)||(y==0))
b=1;
else
b=(b*(y-z+1))/z;
printf("%6d",b);
}
printf("\n");
++y;
}
getch();

```

Output

Enter the number of rows for the Pascal's triangle:5

********Pascal's Triangle********

     1
   1   2   1
  1   3   3   1
 1   4   6   4   1

     1
   1   2   1
  1   3   3   1
 1   4   6   4   1

# EXAMPLE A.23

Write a program to find the sum of the following series up to 50 terms:
-1^3 - 5^3 - 7^3 - 9^3 - 11^3 - ....

```
/*Program for demonstrating the use of while statement*/
/*include <stdio.h>*/
/*include <conio.h>*/
void main()
{
int b,row,y,z;
clrscr();
b=1;
y=0;
printf("Enter the number of rows for the Pascal's triangle:");
scanf("%d",&row);
```
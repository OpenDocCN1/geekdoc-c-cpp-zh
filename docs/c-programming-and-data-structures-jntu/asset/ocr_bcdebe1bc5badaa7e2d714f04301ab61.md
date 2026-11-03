```
```c
}
int main(void)
{
int x=5, y=10;
printf("Max of %d and %d is: %d\n", x,y,max(x,y));

return 0;
}
7. /* Write a C program to generate Pascal's Triangle by using C99 standards */
#include<stdio.h>
#include<conio.h>

void main()
{
int bin,q,r;
clrscr();
bin=1;
q=0;

printf("Rows you want to input:");
scanf("%d",&r);

printf("\nPascal's Triangle:\n");

while(q<r)
{
for(int p=40-3*q;p>0;--p) // declare p with in for
printf(" ");
for(int x=0;x<=q;++x)   // declare x with in for
{
if((x==0)||(q==0))
bin=1;
else
bin=(bin*(q-x+1))/x;
printf("%6d",bin);
}

printf("\n");
++q;
}
getch();
}
```
```
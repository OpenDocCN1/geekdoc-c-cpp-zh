}

# 68. Wap to Reverse an Array.

```
#include<stdio.h>
#include<conio.h>
Void main()
{
Int a[20],i,j;
Clrscr();
Printf("\n\n Enter how many elements of the first array");
For (i=0;i<=19;i++)
{
Scanf("%d",&a[i]);
}
for (i=0;j=10-1;i<10/2;i++;j--)
{
c=a[i];
a[i]=a[j];
a[j]=c;
}
printf("\n\n Reverse of array \n")
for (i=0; i<19;i++)
printf("%d",a[i]);
getch();
}
```

# 69. Wap to read a 3*3 matrix and find out max and min elements.

```
#include<stdio.h>
#include<conio.h>
Void main()
{
Int a[5][5],i,j,min=-32767,max=-32768;
Clrscr();
Printf("\n Enter elements of the matrix");
For (i=0;i<=4;i++)
{
for (j=0; j<=4;j++)
{
scanf("%d",&a[i][j]);
```
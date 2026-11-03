# 64. Wap to read an array of 20 integers and count total no's of even and odd elements.

```
#include<stdio.h>
#include<conio.h>
Void main()
{
Int a[20],i,odd=0,even=0;
Clrscr();
Printf("Enter how many elements of this array series u want to Enter");
For (i=0;i<=19;i++)
{
Scanf("%d",&a[i]);
if (a[i] % 2==0)
    even++;
else
    odd++;
}
printf("\n even=%d,  odd=%d",even,odd);
getch();
}
```

# 65. Wap to read an array of 20 integers and count total no's of pos. and neg. & zero elements.

```
#include<stdio.h>
#include<conio.h>
Void main()
{
Int a[20],i,pos=0,neg=0,zero=0;
Clrscr();
Printf("Enter how many elements of this array series u want to Enter");
For (i=0;i<=19;i++)
{
Scanf("%d",&a[i]);
if(a[i]>0)
    pos++;
else if( a[i]<0)
```
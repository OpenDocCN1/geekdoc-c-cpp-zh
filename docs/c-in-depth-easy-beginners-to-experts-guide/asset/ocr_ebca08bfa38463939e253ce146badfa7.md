```
p2=b;
for(i=0;i<10;i++)
{
c[i]=( *p1)+( *p2);
p1++;
p2++;
}
printf("\n After addition third array");
for(i=0;i<10;i++)
printf("\n "%d",c[i] \n");
getch();
}
```

# 97. Wap to calculate Factorial using Pointer.

```
#include<stdio.h>
#include<conio.h>
Void main()
{
int n,*p,i,f=1;
clrscr();
printf("\n Enter Any number for Factorial.\n");
scanf("%d",&n);
p=&f;
for(i=0;i<=n;i++)
*p=*p*i;
printf("\n Factorial using pointer is=%d", f);
getch();
}
```

# 98. Wap to calculate length of a string using pointer.

```
#include<stdio.h>
#include<conio.h>
Void main()
{
char str[10],*p;
int count=0;
```
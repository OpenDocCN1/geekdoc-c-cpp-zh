**
*

```
#include<stdio.h>
#include<conio.h>
Void main()
{
Int n,i,j;
Clrscr();
Printf("Enter how many rows u want to print series");
Scanf("%d",&n);
For (i=n ; i>=1 ; i++)
{
For (j=5 ; j>=i; j--)
Printf("*");
Printf("\n");
}
getch();
}
```

# 49. print this shape.

1
12
123
1234
12345

```
#include<stdio.h>
#include<conio.h>
Void main()
{
Int n,i,j;
Clrscr();
Printf("Enter how many rows u want to print series");
Scanf("%d",&n);
For (i=1 ; i<=n ; i++)
{
For (j=1 ; j<=i; j++)
Printf("%d",j);
```
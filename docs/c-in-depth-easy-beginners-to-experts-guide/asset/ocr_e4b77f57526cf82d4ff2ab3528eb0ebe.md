```
printf("Not prime no");
getch();
}
```

# 37. Wap to reverse of a given no.

```
#include<stdio.h>
#include<conio.h>
void main()
{
int a;
long int n,rev=0;
clrscr();
printf("Enter a no");
scanf("%ld",&n);
do
{
a=n%10;
n=n/10;
rev=rev*10+a;
}while(n!=0);
printf("%ld",rev);
getch();
}
```

# 38. Wap to print table of any no.

```
#include<stdio.h>
#include<conio.h>
Void main()
{
Int n,i,a;
Clrscr();
Printf("\n Enter any no.");
Scanf("%d",&n);
For(i=1; i<=n; i++)
{
a= n*i;
printf("\n Table is = %d*%d",n,i,a);
}
getch();
}
```
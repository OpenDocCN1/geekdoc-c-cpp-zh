```
#include <stdlib.h>
int a,i,n;
randomize(); /*initializes the random number generator*/
printf("enter the no. to be printed :");
scanf("%d",&n);
i=1;
while(i<=n)
{
a=random(100)+1; /*generates a number between 0 and 99*/
printf("%d\n",a);
i++;
}
```

# 3. WAP to produce the following output:

a b c d e f g f e d c b a
a b c d e f   f e d c b a
a b c d e   e d c b a
a b c d   d c b a
a b c   c b a
a b   b a
a

```
int n,i,j,k,l;
printf("Enter the number of Rows :");
scanf("%d",&n);
for(i=n;i>=1;i--)
{
for(j=1;j<=i;j++)
printf("%c",j+97-1);
for(k=1;k<=2*(n-i)-1;k++)
printf(" ");
for(l=i;l>=1;l--)
{
if(l==n)
continue; /*passes the control of the loop directly to the decrement statement*/
printf("%c",l+97-1);
}
}
```
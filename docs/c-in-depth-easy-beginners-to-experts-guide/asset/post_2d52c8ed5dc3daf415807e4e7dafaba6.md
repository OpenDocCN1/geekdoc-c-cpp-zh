
```c
int a;
clrscr();
printf("Enter a month no");
scanf("%d",&a);

switch(a)
{
case 1:
case 3:
case 5:
case 7:
case 8:
case 10:
case 12:
    printf("There are 31 days in given month");
    break;
case 2:
    printf("There are 28 days in given month");
    break;
case 4:
case 6:
case 9:
case 11:
    printf("There are 30 days in given month");
    break;
default:
    printf("Invalid input");
}
getch();
}
```

## 29. Wap to convert temp from Fahrenheit to centigrade.

```c
#include<stdio.h>
#include<conio.h>
void main()
{
float f,c;
clrscr();
printf("Enter Temperature in F");
scanf("%f",&f);
c=(f-32)/1.8;
printf("Temperature in C is %f",c);
getch();
}
```

## 30. Wap to show given year is leap year or not.

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int n;
clrscr();
printf("Enter an year");
scanf("%d",&n);
if(n%100==0)
{
    if(n%400==0)
        printf("leap year");
    else
        printf("Not leap year");
}
else
{
    if(n%4==0)
        printf("leap year");
    else
        printf("Not leap year");
}
getch();
}
```

## 31. Wap to know is year leap year or not .

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int y;
clrscr();
printf("Enter an year\n");
scanf("%d",&y);
if(y%400==0||y%100!=0&&y%4==0)
    printf("Given year is leap year\n");
else
    printf("Given year is not leap year");
getch();
}
```

## 32. Wap for weekday.

```c
/* weekday*/
#include<stdio.h>
#include<conio.h>
void main()
{
int w;
clrscr();
printf("Enter a weekday\n");
scanf("%d",&w);
switch(w)
{
case 1:
    printf("Sunday");
    break;
case 2:
    printf("Monday");
    break;
case 3:
    printf("Tuesday");
    break;
case 4:
    printf("Wednesday");
    break;
case 5:
    printf("Thursday");
    break;
case 6:
    printf("Friday");
    break;
case 7:
    printf("Saturday");
    break;
default:
    printf("invalid input");
}
getch();
}
```

## 33. Wap to working of telephone bill company.

```c
/* telephone bill*/
#include<stdio.h>
#include<conio.h>
void main()
{
int calls;
float bill;
clrscr();
printf("Enter no of calls");
scanf("%d",&calls);
printf("calls 0 to 100\t 0Rs\n calls 101-200\t 0.80Rs\n calls 201-500\t 1.00Rs\n calls >500\t 1.20Rs\n");
if(calls<=100)
    bill=0;
else if(calls<=200)
    bill=(calls-100)*.80;
else if(calls<=500)
    bill=(calls-200)*1.00+80;
else
    bill=(calls-500)*1.20+380;
printf("bill=%.2fRs",bill);
getch();
}
```

## 34. Wap to find out no. Is Armstrong or not.

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int n,sum=0,a,old;
clrscr();
printf("Enter a no.");
scanf("%d",&n);
old=n;
while(n!=0)
{
    a=n%10;
    n=n/10;
    sum=sum+a*a*a;
}
if(sum==old)
    printf("ARMSTRONG");
else
    printf("NOT ARMSTRONG");
getch();
}
```

## 35. Wap to check a no. Is palindrome or not.

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int a;
long int n,old,rev=0;
clrscr();
printf("Enter a no");
scanf("%ld",&n);
old=n;
do
{
    a=n%10;
    n=n/10;
    rev=rev*10+a;
}while(n!=0);
if(old==rev)
    printf("PALINDROME");
else
    printf("NOT PALINDROME");
getch();
}
```

## 36. Wap to check whether a no. Is prime or not.

```c
#include <stdio.h>
#include <conio.h>
void main()
{
int n,i,prime=1;
clrscr();
printf("Enter a no");
scanf("%d",&n);
for(i=2;i<=n/2;i++)
{
    if(n%i==0)
    {
        prime=0;
        break;
    }
}
if(prime==1)
    printf("Prime no");
else
    printf("Not prime no");
getch();
}
```

## 37. Wap to reverse of a given no.

```c
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

## 38. Wap to print table of any no.

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int n,i,a;
clrscr();
printf("\n Enter any no.");
scanf("%d",&n);
for(i=1; i<=n; i++)
{
    a= n*i;
    printf("\n Table is = %d*%d",n,i,a);
}
getch();
}
```

## 39. Wap to print FIBBONACCI series.

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int a=1, b=0, c=0, n, i;
clrscr();
printf("Enter how many terms u want to print series");
scanf("%d",&n);
for (i=1; i<=n; i++)
{
    printf("%d",c);
    c=a+b;
    a=b;
    b=c;
}
getch();
}
```

## 40. Wap to print sequence 1,3,5,7,9......n

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int s=1,n,i;
clrscr();
printf("Enter how many terms u want to print ");
scanf("%d",&n);
for (i=1; i<=n; i++, s+=2)
    printf("%d",s);
getch();
}
```

## 41. Wap to print 2,4,6,8,10........n

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int s=2, n, i;
clrscr();
printf("Enter how many terms u want to print series");
scanf("%d",&n);
for (i=1; i<=n; i++,s+=2)
    printf("%d",s);
getch();
}
```

## 42. Wap to print sequence 1,4,16,25,........n

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int n, i;
clrscr();
printf("Enter how many terms u want to print ");
scanf("%d",&n);
for (i=1; i<=n; i++)
    printf("%d",i*i);
getch();
}
```

## 43. Wap to print 1 / 1! + 2 / 2! + 3 / 3! + ..........n

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int n, s=1, i;
float fact=1;
clrscr();
printf("Enter how many terms u want to print series");
scanf("%d",&n);
for (i=1; i<=n; i++)
{
    printf("%d / %d! + ",i,fact);
    fact = fact * i;
    printf("%f+", i / fact);
}
getch();
}
```

## 44. Wap to print 1 + x2/y2 + x4/y4 + ..................n

```c
#include<stdio.h>
#include<conio.h>
#include<math.h>
void main()
{
int n,i,p=2,x,y;
float s,N,D;
clrscr();
printf("Enter how many terms u want to print series");
scanf("%d",&n);
printf("Enter the value of x and y");
scanf("%d%d",&x,&y);
printf("1+");
for (i=1; i<=n; i++)
{
    N=pow(x,p);
    D=pow(y,p);
    s=N/D;
    printf("%f+",s);
    p=p+2;
}
getch();
}
```

## 45. Wap to print 1+X2 /Y + X4/Y3 +.....N.

```c
#include<stdio.h>
#include<conio.h>
#include<math.h>
void main()
{
int n,i,p=2,q=1,x,y;
float s,N,D;
clrscr();
printf("Enter how many terms u want to print series");
scanf("%d",&n);
printf("Enter the value of x and y");
scanf("%d%d",&x,&y);
printf("1+");
for (i=1; i<=n; i++)
{
    N=pow(x,p);
    D=pow(y,q);
    s=N/D;
    printf("%f +",s);
    p=p+2;
    q=q+2;
}
getch();
}
```

## 46. Wap to print 1-X2 /Y + X4/Y3 -.....N.

```c
#include <stdio.h>
#include <conio.h>
#include <math.h>
void main()
{
int n,i,p=2,q=1,x,y;
float s,N,D;
clrscr();
printf("Enter how many terms u want to print series");
scanf("%d",&n);
printf("Enter the value of x and y");
scanf("%d%d",&x,&y);
printf("1-");
for (i=1; i<=n; i++)
{
    N=pow(x,p);
    D=pow(y,q);
    s=N/D;
    if(i%2==0)
        printf("%f -",s);
    else
        printf("%f +",s);
    p=p+2;
    q=q+2;
}
getch();
}
```

## 47. Wap to print following shape with the help of loops.

```
*
**
***
****
*****
```

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int n, i, j;
clrscr();
printf("Enter how many rows u want to print series");
scanf("%d",&n);
for (i=1; i<=n; i++)
{
    for (j=1; j<=i; j++)
        printf("*");
    printf("\n");
}
getch();
}
```

## 48. Wap print this shape.

```
*****
****
***
**
*
```

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int n,i,j;
clrscr();
printf("Enter how many rows u want to print series");
scanf("%d",&n);
for (i=n; i>=1; i--)
{
    for (j=n; j>=i; j--)
        printf("*");
    printf("\n");
}
getch();
}
```

## 49. print this shape.

```
1
12
123
1234
12345
```

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int n,i,j;
clrscr();
printf("Enter how many rows u want to print series");
scanf("%d",&n);
for (i=1; i<=n; i++)
{
    for (j=1; j<=i; j++)
        printf("%d",j);
    printf("\n");
}
getch();
}
```

## 50. Wap to print this shape.

```
1
22
333
4444
55555
```

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int n,i,j;
clrscr();
printf("Enter how many rows u want to print series");
scanf("%d",&n);
for (i=1; i<=n; i++)
{
    for (j=1; j<=i; j++)
        printf("%d", i);
    printf("\n");
}
getch();
}
```

## 51. Wap to print this shape.

```
1
2 3
4 5 6
7 8 9 10
11 12 13 14 15
```

```c
#include<stdio.h>
#include<conio.h>
void main()
{
```

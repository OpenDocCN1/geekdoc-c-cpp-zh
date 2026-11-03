

## 8. 编写不使用第三个变量交换两个变量的程序。

```c
#include<stdio.h>
#include<conio.h>
void main()
{
float a,b;
clrscr();
printf("\n\t\t I'm Learning C with Harry's Book \n");
printf("\n\n\t Enter the value of a=");
scanf("%f",&a);
printf("\n\n\t Enter the value of b=");
scanf("%f",&b);
a=a+b;
b=a-b;
a=a-b;
printf("\n\tAfter swapping a=%f\n\t\t b=%f",a,b);
getch();
}
```

## 9. 编写计算三角形面积（Tribhuj）的程序。

```c
#include<stdio.h>
#include<conio.h>
void main()
{
float a,b,c,s,r,area;
clrscr();
printf("\n\t\t I'm Learning C with Harry's Book \n");
printf("\n\n\t Enter the value of a=");
scanf("%f",&a);
printf("\n\n\t Enter the value of b=");
scanf("%f",&b);
printf("\n\t Enter the value of c=");
scanf("%f",&c);
s=a+b+c;
area=s*(s-a)*(s-b)*(s-c);
r=area;
printf("\n\t\t Area=%f",r);
getch();
}
```

## 10. 编写读取小时、分钟、秒时间并转换为总秒数的程序。

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int hr,min,sec,totalsec;
clrscr();
printf("\n\t\t I'm Learning C with Harry's Book \n");
printf("\n\n\t Enter the value of hr=");
scanf("%d",&hr);
printf("\n\n\t Enter the value of min=");
scanf("%d",&min);
printf("\n\n\t Enter the value of sec=");
scanf("%d",&sec);
totalsec=(hr*3600)+(min*60)+sec;
printf("\n\n\t\t Totalsec=%d",totalsec);
getch();
}
```

## 11. 编写打印任意字符 ASCII 码的程序。

```c
#include<stdio.h>
#include<conio.h>
void main()
{
char ch;
clrscr();
printf("\n\t\t I'm Learning C with Harry's Book \n");
printf("\n\n\t Enter any character =");
scanf("%c",&ch);
printf("\n\n\t ASCII code of=%c is %d",ch,ch);
getch();
}
```

## 练习笔记：

ASCII 是一个表（美国信息交换标准代码。）

## 12. 编写程序判断输入的数字是偶数还是奇数。

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int n;
clrscr();
printf("\n\t\t I'm Learning C with Harry's Book \n");
printf("\n\n\t Enter any number =");
scanf("%d",&n);
if(n%2==0)
printf("\n\t\t Number is even");
else
printf("\n\t\t Number is odd");
getch();
}
```

## 13. 编写程序检查输入的字符是大写、小写、数字还是特殊符号？

```c
#include<stdio.h>
#include<conio.h>
void main()
{
char ch;
clrscr();
printf("\n\t\t I'm Learning C with Harry's Book \n");
printf("\n\n\t Enter any character =");
scanf("%c",&ch);
if(ch>=65 && ch<=90)
printf("\n\t\t character is uppercase");
else
if(ch>=97 && ch<=122)
printf("\n\t\t character is smaller case");
else
if(ch>=48 && ch<=57)
printf("\n\t\t character is digit");
else
printf("Character is special symbol");
getch();
}
```

## 14. 编写程序根据 π 计算面积。

```c
#include<stdio.h>
#include<conio.h>
void main()
{
float r,area,pi=3.14;
clrscr();
printf("Enter radius");
scanf("%f",&r);
area=pi*r*r;
printf("area=%f",area);
getch();
}
```

## 15. 编写程序求两个数的平均值

```c
/* average of 2 no */
#include<stdio.h>
#include<conio.h>
void main()
{
int a,b;
float avg;
clrscr();
printf("Enter 2 no");
scanf("%d %d",&a,&b);
avg=(a+b)/2.0;
printf("average=%f",avg);
getch();
}
```

## 16. 编写程序输入总天数并换算成月数。

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int n,m,d;
clrscr();
printf("Enter no of days\n");
scanf("%d",&n);
    m=n/30;
    d=n%30;
printf("months=%d,days=%d",m,d);
getch();
}
```

## 17. 编写程序使用第三个变量交换三个数。

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int a,b,c,t;
clrscr();
printf("Enter three no");
scanf("%d %d %d",&a,&b,&c);
t=a;
a=b;
b=t;
t=c;
c=b;
b=t;
printf("%d %d %d",a,b,c);
getch();
}
```

## 18. 编写程序不使用第三个变量交换三个数。

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int a,b,c;
clrscr();
printf("Enter three no");
scanf("%d %d %d",&a,&b,&c);
a=a+b;
b=a-b;
a=a-b;
b=b+c;
c=b-c;
b=b-c;
printf("%d %d %d",a,b,c);
getch();
}
```

## 19. 编写程序计算盈亏。

```c
#include<stdio.h>
#include<conio.h>
void main()
{
float sp,cp;
clrscr();
printf("Enter cost price and selling price\n");
scanf("%f%f",&cp,&sp);
if(cp<sp)
printf("profit=%.2f Rs",sp-cp);
else if(sp<cp)
printf("loss=%.2f Rs",cp-sp);
else
printf("no profit no loss");
getch();
}
```

## 20. 编写程序计算总分和百分比然后打印等级。

```c
#include<stdio.h>
#include<conio.h>
void main()
{
float p;
char grade;
clrscr();
printf("Enter percentage\n\n");
scanf("%f",&p);
if(p>=90)
grade='A';
else if(p>=70)
    grade='B';
    else if(p>=50)
    grade='C';
    else
    grade='F';
printf("grade=%c",grade);
getch();
}
```

## 21. 编写程序将小写字母转换为大写字母。

```c
/* lower case to upper case*/

#include<stdio.h>
#include<conio.h>
void main()
{
char ch;
clrscr();
printf("Enter a character\n");
scanf("%c",&ch);
if(ch>=97&&ch<=122)
ch=ch-32;
printf("%c",ch);
getch();
}
```

## 22. 编写程序找出两个数中的较大数

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int a,b;
clrscr();
printf("Enter 2 no");
scanf("%d %d",&a,&b);
    if(a>b)
        printf("%d is greater",a);
    else if(a==b)
        printf("Both are equal");
    else
        printf("%d is greater ",b);
getch();
}
```

## 23. 编写程序从四个数中找出最大值

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int a,b,c,d;
clrscr();
printf("Enter 4 no");
scanf("%d %d %d %d",&a,&b,&c,&d);
    if(a>b)
    {
        if(a>c)
        {
            if(a>d)
            printf("%d",a);
            else
            printf("%d",d);
        }
        else if(c>d)
            printf("%d",c);
        else
            printf("%d",d);
    }
    else if(b>c)
    {
        if(b>d)
            printf("%d",b);
        else
            printf("%d",d);
        }
    else
        {
            if(c>d)
                printf("%d",c);
            else
                printf("%d",d);
        }
    getch();
}
```

## 24. 编写程序使用 switch case 开发迷你计算器。

```c
/* calculator*/
#include<stdio.h>
#include<conio.h>
void main()
{
int a,b,ch;
clrscr();
printf("Enter two no\n");
scanf("%d %d",&a,&b);
printf("1\t add\n 2\t subtract\n 3\t multiplication\n 4\t divide\n 5\t modulus\n Enter your choice\n");
scanf("%d",&ch);

switch(ch)
    {
        case 1:
            printf("sum=%d",a+b);
            break;

        case 2:
            printf("subtraction=%d",a-b);
            break;

        case 3:
            printf("multiplication=%d",a*b);
            break;

        case 4:
            printf("division=%f",(float)a/b);
            break;

        case 5:
            printf("modulus=%d",a%b);
            break;

        default:
            printf("invalid input");
    }
    getch();
}
```

## 25. 编写程序使用算术运算符制作迷你计算器，每个运算符执行特定任务。

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int a,b;
char ch;
    clrscr();
    printf("Enter two no\n");
    scanf("%d %d",&a,&b);
    flushall();
printf("\n + for add \n - for subtract \n * for multiplication \n / for divide\n Enter your choice\n");
scanf(" %c",&ch);
switch(ch)
{

case '+' :
    printf("sum=%d",a+b);
    break;

case '-' :
    printf("subtraction=%d",a-b);
    break;

case '*' :
    printf("multiplication=%d",a*b);
    break;

case '/' :
    printf("division=%f",(float)a/b);
    break;

case '%' :
    printf("modulus=%d",a%b);
    break;

default:
    printf("invalid input");
}
    getch();
}
```

## 26. 编写程序计算用户输入任意数的阶乘。

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int n,i,f=1;
clrscr();
printf("Hello Guys, I'm Learning C Programming with Harry's Book ");
printf(" Enter the any no. For factorial");
scanf("%d",&n);
for (i=1;i<=n;i++)
f=f*i;
printf("\n factorial is = %d",f);
getch();
}
```

## 27. 编写程序计算数的幂。

```c
#include<stdio.h>
#include<conio.h>
void main()
{ int n,i,p;
long int ans=1;
clrscr();
printf("Enter a no and its power to be calculated");
scanf("%d %d",&n,&p);
i=p;
    while(i>=1)
    { ans*=n;
    i--;
    }
    printf("%ld",ans);
    getch();
}
```

## 28. 编写程序找出月份的天数。

```c
#include<stdio.h>
#include<conio.h>
void main()
{
```

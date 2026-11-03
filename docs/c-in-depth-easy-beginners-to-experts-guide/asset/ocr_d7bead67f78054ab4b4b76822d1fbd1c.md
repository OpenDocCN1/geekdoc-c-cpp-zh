```
a=a-b;
b=b+c;
c=b-c;
b=b-c;
printf("%d %d %d",a,b,c);
getch();
}
```

# 19. Wap to calculate profit and loss.

```
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

# 20. Wap for calculate total & percentage then print Grades.

```
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

```
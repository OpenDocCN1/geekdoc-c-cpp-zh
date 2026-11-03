```
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

# 32. Wap for weekday.

```
/* weekday*/
#include<stdio.h>
#include<conio.h>
void main()
{int w;
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
```
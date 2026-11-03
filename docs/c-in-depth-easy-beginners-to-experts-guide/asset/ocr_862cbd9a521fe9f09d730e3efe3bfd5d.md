```
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
```

# 29. Wap to convert temp from Fahrenheit to centigrade.

```
```c
#include<stdio.h>
#include<conio.h>
void main()
{
float f,c;
clrscr();
printf("Enter Temperature in F");
```
```
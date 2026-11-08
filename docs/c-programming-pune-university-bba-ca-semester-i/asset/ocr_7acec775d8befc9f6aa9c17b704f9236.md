![](bbox=[0.2, 0.15, 0.85, 0.33])

+   15. Write a program to check whether the number is positive, negative or zero.

```
```c
#include<stdio.h>
#include<conio.h>
void main()
{
    int a;
    clrscr();
    printf("Enter the numbers\n");
    scanf("%d",&a);
    if(a>0)
    {
        printf("%d is +ve number",a);
    }
    if(a<0)
    {
        printf("%d is -ve number",a);
    }
    if(a==0)
    {
        printf("%d is a Zero number",a);
    }
    getch();
}
```
```
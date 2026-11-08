![](bbox=[0.23, 0.15, 0.82, 0.45])

# PROGRAMS ON FUNCTIONS

47. Write a program to find the factorial of a number using recursive function.

```
```c
#include<stdio.h>
#include<conio.h>
void main()
{
    int fa,n;
    int fact(int n1);
    clrscr();
    printf("Enter a number :");
    scanf("%d", &n);
    fa=fact(n);
    printf("The factorial is : %d", fa);
    getch();
}
int fact(int n1)
{
    int fl=1,i;
```
```
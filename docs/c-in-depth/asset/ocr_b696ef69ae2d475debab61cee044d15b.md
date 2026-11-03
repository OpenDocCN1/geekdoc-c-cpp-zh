The break statement is not logically needed after the last case(or default if it is at the last) but it is a good programming practice to do so because future we may need to add new cases at the last.

```
```c
/*P5.33 Program to perform arithmetic calculations on integers*/
#include<stdio.h>
main()
{
char op;
int a,b;
printf("Enter number operator and another number : ");
scanf("%d%d",&a,&b);
switch(op)
{
case '+':
printf("Result = %d\n",a+b);
break;
case '-':
printf("Result = %d\n",a-b);
break;
case '*':
printf("Result = %d\n",a*b);
break;
case '/':
printf("Result = %d\n",a/b);
break;
case '%':
printf("Result = %d\n",a%b);
break;
default:
printf("Enter valid operator\n");
}/*End of switch*/
}/*End of main()*/
```
```

Output:

```
```text
Enter number operator and another number : 2+5
Result = 7
```
```

In this program, the valid operator for multiplication is only '*', if we want to make 'x', 'X' also valid operators for multiplication, then we can modify above switch statement like this.

```
```c
switch(op)
{
...............
...............
case '-':
result = a-b;
break;
case 'x':
case 'X':
case '*':
result = a*b;
break;
...............
...............
}
```
```
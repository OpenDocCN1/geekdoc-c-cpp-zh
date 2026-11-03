```
```c
printf("Before calling the function, a and b are %d,%d\n",a,b);
value(a,b);
printf("After calling the function, a and b are %d,%d\n",a,b);
}
value(int x,int y)
{
x++;
y++;
printf("In function changes are %d,%d\n",x,y);
}
```
```

Output:

Before calling the function, a and b are 5, 8
In function changes are 6, 9
After calling the function, a and b are 5, 8

Here a and b are variables declared in the function main() while x and y are declared in the function value().These variables reside at different addresses in memory. Whenever the function value() is called, two variables are created named x and y and are initialized with the values of variables a and b. This type of parameter passing is called call by value since we are only supplying the values of the actual arguments to the calling function. Any operation performed on variables x and y in the function value(), will not affect variables a and b.

Before calling the function value() , the value of a = 5 and b = 8. The values of a and b are copied into x and y. Since the memory locations of x, y and a, b are different, so when the values of x and y are incremented, there will be no effect on the values of a and b. Therefore after calling the function, a and b are same as before calling the function and have the value 5 and 8.

![](bbox=[0.05, 0.55, 0.95, 0.7])

Although C does not use call by reference, but we can simulate it by passing addresses of variables as arguments to the function. To accept the addresses inside the function, we'll need pointer variables. Here is a program that simulates call by reference by passing addresses of variables a and b.

```
```c
/* PR.17 program to explain call by reference*/
#include<stdio.h>
main()
{
int a=5;
int b=8;
printf("Before calling the function, a and b are %d,%d\n",a,b);
ref(&a,&b);
}
```
```
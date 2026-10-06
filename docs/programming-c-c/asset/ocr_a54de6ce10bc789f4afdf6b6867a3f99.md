# Programming with C and C++

```
#include<stdio.h>
#include<conio.h>
int main()
{
    int num=1;
    printf("initializing loop\n\n    printf("%d\n",num);
    while(num<=10)
    {
        num=num*2;
    }
    return 0;
}
```

+   1. First, we have initialized 'num' with value 1. Then we have written a do-while loop.
2. In a loop, we have a print function that will print the series by multiplying the value of num with 2.
3. After each increment, the value of num will increase by 1, and it will be printed on the screen.
4. Initially, the value of num is 1. In a body of a loop, the print function will be executed in this way: 2*num where num=1, 2*1=2. Hence, the value two will be printed. This will go on until the value of num becomes 10. After that, loop will be terminated and a statement which is immediately after the loop will be executed. In this case, return 0.

# break statement with do-while loop

Consider the following example to use the break statement with a do-while loop.

```
#include<stdio.h>
void main()
{
    int n=2,i,choice;
    do
    {
        i=1;
        while(i<=10)
        {
            printf("%d X %d = %d\n",n,i,n*i);
        }
    }
```
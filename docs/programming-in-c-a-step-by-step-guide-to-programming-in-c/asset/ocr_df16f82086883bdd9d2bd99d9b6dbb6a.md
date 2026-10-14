(True/False)

11.The output of the following program is ________.

```
#include<stdio.h>
main()
{
int n=5;
int fun(int n);
printf("%d\n", fun(n));
}
int fun(int n)
{
if(n==0)
return 0;
else
return (n+fun(n-1));
}
```

# 5.5 Function Philosophy

What makes a good function? The most important aspect of a good “building block" is that have a single, well-defined task to perform. When you find that a program is hard to manage, it's often because it has not been designed and
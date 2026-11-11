![](bbox=[0.123, 0.106, 0.865, 0.194])

This is because we have initialized the default arguments to zero; indeed you can initialize them to any value as per your requirements.

```
int add(int,int,int=0,int=0);
```

The order of arguments should be such that all the mandatory arguments appear before the default one. Compiler does not allow programmer to specify any mandatory argument after the occurrence of default argument.

Given below is the full source code which defines a function add to perform addition of four integers with two of them as default arguments:

```
#include<stdio.h>
/*Prototype specifying two default arguments*/
int add(int,int,int=0,int=0);
void main()
{
int r1,r2,r3;
/*Call function add to add two integers*/
r1 = add(10,20);
/*Call function add to add three integers*/
r2 = add(100,200,300);
/*Call function add to add four integers*/
r3 = add(1000,2000,3000,4000);
printf("r1=%d\n",r1);
printf("r2=%d\n",r2);
printf("r3=%d\n",r3);
}
/*Function definition of add*/
int add(int a,int b,int c, int d)
{
return a+b+c+d;
}
```

# Output

```
r1=30
r2=600
r3=10000
```
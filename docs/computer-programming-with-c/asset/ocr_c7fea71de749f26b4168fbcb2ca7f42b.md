# Program 5

```
```c
#include<stdio.h>
void main()
{
int a=10,b=20;
int *p,*q;
p=&a;
q=&b;
printf("%d\n",*p*q);
printf("%d\n",*p**q);
printf("%d\n", (*p)*(*q) );
}
```
```

# Program 6

```
```c
#include<stdio.h>
void main()
{
int a=10,b=20;
void *p,*q;
p=&a;
q=&b;
printf("%d\n",*p);
printf("%d\n",p);
printf("%d\n",*q);
printf("%d\n",p);
}
```
```

# Program 7

```
```c
#include<stdio.h>
int multiply(int *a, int *b)
{
return (*a*b);
}
void main()
{
void (*p)(int,int);
int result
p=multiply;
result=p(&10,&20);
printf("Result of multiplication is %d\n", result);
}
```
```
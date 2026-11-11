```
```c
{
    int result;
    result=p+q;
}
```
```

# Code 4

```
```c
#include<stdio.h>
void main()
{
main(10);
}
void main(int p)
{
printf("Inside a user-defined main function\n");
p++;
printf(" The value of variable p is %d\n",p);
}
```
```

# Code 5

```
```c
#include<stdio.h>
int i=0;
int init_fn();
int condition_fn();
int change_fn();
void main()
{
        for(init_fn();condition_fn();change_fn())
        {
        printf("Computer programming\n");
        }
}
int init_fn()
{
i=1;
}
int condition_fn()
{
return i<=10;
}
int change_fn()
{
return ++i;
}
```
```
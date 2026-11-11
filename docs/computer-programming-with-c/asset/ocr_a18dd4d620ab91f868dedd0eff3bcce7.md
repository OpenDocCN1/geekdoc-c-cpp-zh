```
```c
printf("%d\n",a[i]);
}
printf("Elements of the array ‘b’ are\n");
for(int i=0;i<5;i++)
{
printf("%d\n",b[i]);
}
}
```
```

# Code 4

```
```c
#include<stdio.h>
void main()
{
char a[]={'h','a','r','d','w','a','r','e'};
printf("%s",a);
}
```
```

# Code 5

```
```c
#include<stdio.h>
void main()
{
char a[]="misc";
char b[100];
b=a;
printf("The value of string a is %s\n", a);
printf("The value of string b is %s\n", b);
}
```
```

# Code 6

```
```c
#include <stdio.h>
void main()
{
char a[]="misc";
char b[]="misc";
        if(a==b)
        {
        printf("The two strings are same\n");
        }
        else
        {
        printf("The two strings are not same\n");
        }
}
```
```
![](bbox=[0.135, 0.13, 0.835, 0.564])

Given below is the full source code to find greatest of three numbers by nesting conditional operators using this approach.

```
```c
#include<stdio.h>
void main()
{
    int res,a,b,c;
    printf("Enter 3 nos\n");
    scanf("%d %d %d",&a,&b,&c);
    res = a>=b ? a>=c ? a : c : b>=c ? b : c;
    printf("Greatest number is %d\n",res);
}
```
```

# Output

```
```text
Enter 3 nos
10 55 22
Greatest number is 55
```
```
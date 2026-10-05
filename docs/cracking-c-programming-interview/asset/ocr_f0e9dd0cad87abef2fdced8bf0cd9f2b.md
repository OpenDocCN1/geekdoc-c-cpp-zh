```
#include<stdio.h>
#define fun max
void max()
{
    printf("Hello");
    return 0;
}
void fun()
{
    printf("World");
    return 0;
}
int main()
{
    fun();
    max();
    return 0;
}
```

+   (a) World Hello
(b) error in macro definition
(c) error- multiple definition of function
(d) compiler dependent

31. What is the output of the following program?

```
#include<stdio.h>
#define fun(x) x*x
int main()
{
    int x = 2;
    int y = fun(x+2); //line 2
    printf("%d ", y);
    return 0;
}
```

+   (a) 20
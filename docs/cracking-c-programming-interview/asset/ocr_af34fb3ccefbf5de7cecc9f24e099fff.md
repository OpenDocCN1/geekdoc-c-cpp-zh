```
}
return 0;
}
```

+   (a) 22, 23, 24, 25
(b) 22, 24, 25
(c) 22, 25, 27
(d) 22, 24

# 38. What is the output of the following program?

```
#include<stdio.h>
int fun(int i, int j)
{
    if(i/2 == 0) return 0;
    else if(i%2 == 1)
        return fun(i/2, 3*j) + i+j;
    else
        return fun(i/2, 2*j) + i+j;
}
int main()
{
    printf("%d", fun(20, 1));
    return 0;
}
```

+   (a) 48
(b) 49
(c) 54
(d) 56

# 39. What is the output of the following program?

```
#include<stdio.h>
int main()
{
    int p = printf("");
    switch(p)
```
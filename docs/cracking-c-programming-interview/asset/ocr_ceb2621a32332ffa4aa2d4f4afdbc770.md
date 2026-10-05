(c) undefined behavior

(d) error- compile time

# 14. What is the output of the following program?

```
#include<stdio.h>

 main()
{
    int i = 3;
    int j = i+(i=10); //line 2
    printf("%d\n", j);
    return 0;
}
```

+   (a) 13

+   (b) 20

+   (c) 30

+   (d) compiler dependent

# 15. What is the output of the following program?

```
#include<stdio.h>
void print(int i)
{
    if(i<5) return;
    printf("%d ", i);
    print((i--, i)); //line 3
}

 main()
{
    print(10);
    return 0;
}
```

+   (a) 10 9 8 7 6

+   (b) 10 9 8 7 6 5

+   (c) 10 9 8 7

+   (d) syntax error in line 3
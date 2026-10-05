(d) none of these

2. What modification should we do in the above program such that it returns the address of variable 'b' defined in called function?

3. What is the output of the following program?

```
#include<stdio.h>
int main()
{
    int b = 65;
    void *p = &b;
    int *j = (int)*p;
    char *ch = (char*)p;
    printf("%d, %c\n", *j, *ch);
    return 0;
}
```

+   (a) 65, 65
(b) 65, A
(c) error- compile time
(d) error- run time

4. What is the output of following program?

```
#include<stdio.h>
int main()
{
    int b=65;
    void *p = b;
    int c = (int)p;
    printf("%d\n", p);
    return 0;
}
```

+   (a) 65
(b) A
(c) error- compile time
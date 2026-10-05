```
enum block {first = 1 , second = 2};
int main()
{
    enum block a ;\n    printf("% d",sizeof(a));
    return 0;
}
```

+   (a) error-compile time
(b) 8
(c) 1
(d) 4

# 56. **What is the output of the following program?

```
#include<stdio.h>
int main()
{
    union unit
    {
        int marks = 95;
        int roll;
    } std1, std2;
    std2.roll = 512;
    std1.marks = 68;
    printf("%d %d",std1.marks , std2.marks);
    return 0;
}
```

+   (a) 68 95
(b) 68 Garbage
(c) 68 512
(d) error-compile time

# 57. **What is the output of the following program?**

```
#include<stdio.h>
int main()
```
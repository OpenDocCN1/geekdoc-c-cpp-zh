```
#include<stdio.h>
int main()
{\n    char str[] = "India";
    const char *ptr;
    ptr = str;
    ptr++;
    //++*ptr;
    printf("%s", ptr);
    return 0;
}
```

+   (a) India
(b) ndia
(c) dia
(d) error- updating constant expression is not allowed

+   12. What will be the output if we uncomment the commented line in the above program?

+   (a) Jndia
(b) ndia
(c) dia
(d) error- updating of the constant expression not allowed

+   13. What is the output of the following program?

```
#include<stdio.h>
int main()
{\n    char str[] = "India";
    char *ptr;
    ptr = str;
    ptr++;
    printf("%s", ptr);
    return 0;
}
```
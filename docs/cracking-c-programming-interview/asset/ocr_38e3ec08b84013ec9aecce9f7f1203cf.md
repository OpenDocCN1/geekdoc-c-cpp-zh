```
#include<stdio.h>
int main()
{
    int i=5,j=10;
    i=&&j&&10;
    printf("%d %d",i,j);
    return 0;
}
```

+   (a) 5 10
(b) 1 10
(c) 1 11

+   14. Differentiate the following declarations.
(i) const char *a;
(ii) char* const a;
(iii) char const *a;

+   15. Determine the output of the following code?
#include<stdio.h>
int main()
{
    static int i=5;
    if(--i)
{
        main();
        printf("%d ",i);
    }
    return 0;
}

+   16. Determine the output of the following code.
#include<stdio.h> #include<string.h>
int main()
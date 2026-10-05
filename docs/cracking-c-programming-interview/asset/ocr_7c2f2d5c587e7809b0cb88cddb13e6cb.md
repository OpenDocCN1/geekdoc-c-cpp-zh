```
#include<stdio.h>
struct Test {
    int i;
    char *c;
}
int main() {
    struct Test st[] = {5, "become", 4, "better", 6, "jungle", 8, "ancestor", 7, "brolter"};
    struct Test *p = st;
    p+=1;
    printf("%s ", ++p->c);
    printf("%c ", *p++->c);
    printf("%d ", +p->i);
    printf("%s ", p[0].c);
    printf("%s ", p->c);
    return 0;
}
```

# 55. What is the output of the following program?

```
#include<stdio.h>
int main() {
    char *s[] = {"ice", "green", "cone", "please"};
    char **ptr[] = {s+3, s+2, s+1, s};
    char ***pptr = ptr;
    printf("%s ", **++pptr);
    printf("%s ", *--++pptr+1);
    return 0;
}
```

+   (a) ice ce
(b) green none
(c) cone ce
(d) ice
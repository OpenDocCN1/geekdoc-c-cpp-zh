# See if you can figure out the output to the following program:

```
// doublep.c
#include <stdio.h>
void foo1(char *p);
void foo2(char **q);
int main(void) {
    char *p = "Hello";
    char *q = "Bye";
    printf("Function: main() ---> p = %s\n", p);
    foo1(p);
    printf("Function: main() ---> p = %s\n", p);
    printf("Function: main() ---> q = %s\n", q);
    foo2(&q);
    printf("Function: main() ---> q = %s\n", q);
    return 0;
}
void foo1(char *pp) {
    ++pp;
    printf("Function: foo1() ---> pp = %s\n", pp);
}
void foo2(char **qq) {
    ++*qq;
    printf("Function: foo2() ---> *qq = %s\n", *qq);
}
```

The output produced is as follows:

```
Function: main() ---> p = Hello
Function: foo1() ---> p = ello
Function: main() ---> p = Hello
Function: main() ---> q = Bye
Function: foo2() ---> q = eye
Function: main() ---> q = ye
```
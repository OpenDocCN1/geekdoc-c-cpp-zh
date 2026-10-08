# 366 Storage Classes

```
x = x + a2+(int)w;
printf("x = %d\n", x);
w = w + 5.0;
return(x + w);
}
```

c. What is printed by executing the following code:

```
#include <stdio.h>

int func1( void);
int func2(void);

int main() {
    int a, b, i;

    for(i = 0; i < 4; i++) {
        a = func1();
        printf("a = %d\n", a);
        b = func2();
        printf("b = %d\n", b);
    }

    return 0;
}

int func1(void) {
    static int x;

    x = x + 2;
    return x;
}

int func2(void) {
    int x = 10;

    x = x + 5;
    return x;
}
```
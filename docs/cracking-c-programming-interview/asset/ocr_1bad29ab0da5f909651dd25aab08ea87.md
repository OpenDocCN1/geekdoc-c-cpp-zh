```
return 0;
)
```

+   (a) 10
(b) 11
(c) garbage
(d) error- invalid assignment

# 51. What is the output of the following program?

```
#include<stdio.h>
int main() {
    while(1) {
        if(printf("%d",printf("%d", 10)))
            break;
        else
            continue;
    }
    return 0;
}
```

+   (a) 102
(b) infinite
(c) 12
(d) 101

# 52. Explain the below functional pointer declaration.

```
int (* fun( float, void (*pqr) () ) ) ();
```

# 53. What is the output of the following program?

```
#include<stdio.h>
int main() {
    int x = 7;
    int k = x++x ==7;
    printf("%d %d", k, x);
```
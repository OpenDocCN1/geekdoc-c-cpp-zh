# 7.3 Compiling and Testing

In this section, we try to compile our library, **mysimplelib.c**, to be static library and shared library.

# 7.3.1 Static Library

Firstly, we compile our library, **mysimplelib.c**, to be a static library, called **libmysimple.a**.

```
$ gcc -c mysimplelib.c
$ ar rs libmysimple.a mysimplelib.o
```

![](bbox=[0.06, 0.36, 0.94, 0.58])

To access our static library, we create a simple app. Create a file, called **mysimpletest.c**, and write this code.

```
#include <stdio.h>
#include "mysimple.h"

int main(int argc, const char* argv[]) {
    int a,b,c;
    a = 5;
    b = 3;
    c = add(a,b);
    printf("%d + %d = %d\n",a,b,c);
    c = subtract(a,b);
    printf("%d - %d = %d\n",a,b,c);
```
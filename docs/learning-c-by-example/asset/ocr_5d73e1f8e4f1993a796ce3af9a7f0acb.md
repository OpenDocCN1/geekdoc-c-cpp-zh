# 2.10 Increment and Decrement

Imagine you have operation as below

```
num = num + 1;
```

you can simply this syntax use ++.

```
num++;
```

using the same approach for this case

```
num = num - 1;
```

you can use — syntax.

```
num--;
```

Now how to implement them in code. Let’s write this code.

```
#include <stdio.h>

int main() {
    int a = 10;

    a++;
    printf("%d \n",a);

    a++;
    printf("%d \n",a);

    ++a;
    printf("%d \n",a);

    a--;
    printf("%d \n",a);

    a--;
    printf("%d \n",a);

    --a;
    printf("%d \n",a);

    return 0;
}
```

Save this code into a file, called incdec.c.

Compile and run it. Here is sample of program output.
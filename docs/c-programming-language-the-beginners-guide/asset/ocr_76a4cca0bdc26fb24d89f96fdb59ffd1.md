A character occupies only 1 byte of storage. Now, change to *float* and see how big that variable type is.

```
```c
#include <stdio.h>
int main()
{
    float a;
    printf("A float variable occupies %lu bytes of storage\n", sizeof(a));
    return(0);
}
```
```

Save, build and run the code. On this system, a floating point variable occupies 4 bytes of storage. A long integer, or long *int* value, is designed to store really huge integers. To see how big it is, change *float* to *long* in the code.

```
```c
#include <stdio.h>
int main()
{
    long a;
    printf("A long variable occupies %lu bytes of storage\n", sizeof(a));
    return(0);
}
```
```
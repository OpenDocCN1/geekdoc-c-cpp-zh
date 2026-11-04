C.10.29 What is the output of the following program?

```
```c
#include <stdio.h>
#include <string.h>
int main(void)
{
    char str[5];

    str[0] = 't';
    str[1] = 'e';
    str[2] = 's';
    str[3] = 't';

    if (strcmp(str, "test") == 0)
        printf("One\n");
    else
        printf("Two\n");
    return 0;
}
```
```
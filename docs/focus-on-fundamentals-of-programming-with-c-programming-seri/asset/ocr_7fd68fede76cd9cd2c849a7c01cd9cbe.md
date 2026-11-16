Here's a program that sorts strings with qsort ():

```
// qsort2.c

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int compare(const void *p, const void *q);

int main() {
    char list[5][4] = {{"cat", "car", "cab", "cap", "can"}};
    qsort(list, 5, sizeof(list[0]), compare);
    for (i = 0; i < 5; ++i) {
        printf("%s ", list[i]);
    }
    return(0);
}

int compare(const void *p, const void *q) {
    return strcmp((char *) p, (char *) q);
}
```
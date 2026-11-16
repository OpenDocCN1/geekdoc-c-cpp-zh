# Dynamic Allocation of Variables
Dynamic Arrays - Advanced

4
.text
.data
.stack
.heap
malloc()
free()

```
#include <stdlib.h>
int *p;
p = (int *) malloc(10 * sizeof(int));
free(p);
```

5
[Not in b-k] 2 resize of an array

```
p = realloc(p, 100 * sizeof(int));
```
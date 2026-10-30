Instead, when a linked list is built in a shared memory segment, the list pointers should be stored as offsets to other objects in the shared memory segment. These offsets are formed by subtracting the start of the shared memory segment from the actual address of the object.

# 15.14 Figure C.21 shows the relevant events.

| Parent i set to | Child i set to | Shared value set to | update returns | Comment |
|---|---|---|---|---|
| 0 | 1 | 0 |  | initialized by mmap
child runs first, then is blocked
parent runs |
|  |  | 1 |  |  |
|  |  | 2 | 0 | then parent is blocked
child resumes |
| 2 | 3 |  | 1 | then child is blocked
parent resumes |
|  |  | 3 |  |  |
|  |  | 4 | 2 | then parent is blocked |
| 4 | 5 |  | 3 | then child is blocked
parent resumes |

Figure C.21 Alternation between parent and child in Figure 15.33

# Chapter 16

# 16.1 Figure C.22 shows a program that prints the system's byte order.

```
#include <stdio.h>
#include <stdlib.h>
#include <inttypes.h>
int
main(void)
{
    uint32_t    i = 0x04030201;
    unsigned char    *cp = (unsigned char *) &i;
    if (*cp == 1)
        printf("little-endian\n");
    else if (*cp == 4)
        printf("big-endian\n");
    else
        printf("who knows?\n");
    exit(0);
}
```

Figure C.22 Determine byte order on system
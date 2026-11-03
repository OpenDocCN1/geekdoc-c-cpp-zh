5. Two pointers can also be compared such as --
p1>p2
p1 = p2
p1 != p2.

These comparisons are useful only while using string or arrays.

6. Two pointers cannot be multiplied divided or added.

# Mind Wash Drill –

A null pointer is a special pointer value that is known not to point anywhere. It means that no other valid pointer, to any other variable or array cell or anything else, will ever compare equal to a null pointer.

Another way to use a null pointer is, by using any one of the standard header files, including <stdio.h>, <stdlib.h>, and <string.h>. To initialize a pointer to a null pointer, you might use code like-

```
#include <stdio.h>
int *p = NULL;
```

And to test it for a null pointer before inspecting the value pointed to you might use code like -

```
if(p != NULL)
printf("%d\n", *p);
```

It is also possible to refer to the null pointer by using a constant 0, and you will see some code that sets null pointers by simply doing

```
int *p = 0;
```

Furthermore, since the definition of “true” in C is a value that is not equal to 0, you will see code that tests for non-null pointers with abbreviated code like -

```
printf("%d\n", *p);
```

This has the same meaning as our previous example; if(p) is equivalent to if(p != 0) and to if(p != NULL).

# Pointers to pointers –
In C (but not C++; see §27.3.4), you can leave out the cast before **malloc()**, but we don’t recommend that:

```
int* p = malloc(sizeof(int)*n);   /* avoid this */
```

Leaving out the cast is quite popular because it saves some typing and because it catches the rare error of (illegally) forgetting to include **<stdlib.h>** before using **malloc()**. However, it can also remove a visual clue that a size was wrongly calculated:

```
p = malloc(sizeof(char)*m);       /* probably a bug — not room for m ints */
```

Don’t use **malloc()**/**free()** in C++ programs; **new**/**delete** require no casts, deal with initialization (constructors) and cleanup (destructors), report memory allocation errors (through an exception), and are just as fast. Don’t **delete** an object allocated by **malloc()** or **free()** an object allocated by **new**. For example:

```
int* p = new int[200];
// ...
free(p);              // error
```

```
X* q = (X*)malloc(n*sizeof(X));
// ...
delete q;             // error
```

This might work, but it is not portable code. Furthermore, for objects with constructors or destructors, mixing C-style and C++-style free-store management is a recipe for disaster.

The **realloc()** function is typically used for expanding buffers:

```
int max = 1000;
int count = 0;
int c;
char* p = (char*)malloc(max);
while ((c=getchar())!=EOF) {  /* read; ignore chars on eof line */
    if (count==max-1) {        /* need to expand buffer */
        max += max;            /* double the buffer size */
        p = (char*)realloc(p,max);
        if (p==0) quit();
    }
    p[count++] = c;
}
```
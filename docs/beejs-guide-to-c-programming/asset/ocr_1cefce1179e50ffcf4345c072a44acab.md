```
while ((line = readline(fp)) != NULL) {
    printf("%s\n", line);
    free(line);
}
fclose(fp);
```

When moving memory like this, it's common (though hardly a law) to double the space needed each step to minimize the number of realloc(s) that occurs.

Finally you might note that readline( ) returns a pointer to a malloc(d) buffer. As such, it's up to the springer to explicitly free( ) that memory when it's done with it.

# 12.5.2 realloc with NULL

Trivial time! These lines are equivalent:

```
char *p = malloc(3490);
char *p = realloc(NULL, 3490);
```

That could be convenient if you have some kind of allocation loop and you don't want to special-case the first malloc().

```
int *p = NULL;
int length = 0;

while (!done) {
    // Allocate 10 more ints:
    length += 10;
    p = realloc(p, sizeof *p * length);

    // Do amazing things
    //
}
```

In example, we didn't need an initial malloc( ) since p was NULL to start.

# 12.6 Aligned Allocations

You probably aren't going to use this.

And don't want to get too far off in the weeds talking about it now, but there's this thing memory alignment, which has to do with the memory address (pointer value) being a multiple of a certain number.

For example, a system might require 16-bit values begin on memory addresses that are multiples of 2. Or that 64-bit values begin on memory addresses that are multiples of 2, 4, 8, or for example. It depends on the CPU.

Some systems require this kind of alignment for fast memory access, or even memory access for all. Now, if you use malloc( ), calloc( ), or realloc( ), will give you a chunk of memory that is well-aligned for any value at all, even structs. Works in all cases.

But there might be times that you know some data can be aligned at a smaller boundary, or must be aligned at a larger one for some reason. I imagine this is more common with embedded systems programming.

In those cases, you can specify an alignment with an aligned_alloc( ).
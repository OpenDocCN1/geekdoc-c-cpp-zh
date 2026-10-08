# Chapter 32. Types Part V: Compound Literals and Generic Selections

We'll just take t out of there and replace it with an unnamed struct:

```
//struct coord t = {.x=10, .y=20};

print_coord((struct coord){.x=10, .y=20}); // prints "10, 20"
```

Still works!

# 32.1.3 Unnamed Objects

You might have noticed in the last example that we were using a struct, we were passing a copy of the struct to print_coord() as opposed to passing a pointer to the struct.

Turns out, we can just take the address of an unnamed object & with likes always.

This is because, if an operator would have worked on a variable of that type, you can use that operator on an unnamed object of that type.

Let's modify the code <stdio.h> to pass a pointer to an unnamed object

```
#include <stdio.h>

struct coord {
    int x, y;
};

void print_coord(struct coord *c) {
    printf("%d, %d\n", c->x, c->y);
}

int main(void) {
    // Note the &
    //
    print_coord((struct coord){.x=10, .y=20}); // prints "10, 20"
}

// Additionally, this could be a nice way to pass even pointers to simple objects:
// Pass a pointer to an int with value 3490
foo(&(int)(3490));
```

Easy as that.

# 32.1.4 Unnamed Objects and Scope

The lifetime of an unnamed object ends at the end of its scope. The biggest way this could bite you is if you make a new unnamed object, give a pointer to it, and then leave the object's scope. In that case, the pointer will refer to a dead object.

So this is undefined behavior:

```
int *p;
{
    p = &(int){10};
}

printf("%d\n", *p); // INVALID: The (int){10} fell out of scope
```
# Chapter 11. Pointers II: Arithmetic

Or we can copy ints:

```
#include <stdio.h>
#include <string.h>

int main() {
    int a[] = {11, 22, 33};
    int b[3];

    memcpy(b, a, 3 * sizeof(int)); // Copy 3 ints of data

    printf("%d\n", b[1]); // 22
}
```

That's a little wild—you see what we did with memcpy()? We copied the data from a to b, but we had to specify how many bytes to copy, and an int is more than one.

OK, then—how many bytes does an int take? Answer: depends on the system. But we can tell how many bytes any type takes with the sizeof operator.

So there's the answer: an int takes sizeof(int) bytes of memory to store.

And if we have 3 of them in our array, like we did in that example, the entire space used for the 3 ints must be 3 * sizeof(int). 
just that resolves into 7 * 1.

In the string example, earlier, it would have been more technically accurate to copy 7 * sizeof(char) bytes. We could copy a float or a double with memcpy! (Though this is obvious—we should just use for that):

```
struct antelope my_antelope;
struct antelope my_clone_antelope;

...
```

memcpy(&my_clone_antelope, &my_antelope, sizeof my_antelope);
Look at how versatile memcpy()! If you have a pointer to a source and a pointer to a destination, and you have the number of bytes you want to copy, you can copy any type of data.
If we didn't have void*, we'd have to write specialized memcpy() functions for each type:

```
memcpy_int(int *a, int *b, int count);
memcpy_float(float *a, float *b, int count);
memcpy_double(double *a, double *b, int count);
memcpy_char(char *a, char *b, int count);
memcpy_unsigned_char(unsigned char *a, unsigned char *b, int count);
```

// etc... blech!
Much better to use void* and have one function that can do it all.

That's the power of void*. You can write functions that don't care about the type and are still able to do things with it.
With great power comes responsibility. Maybe not great in this case, but there are some limits.

+   1. You cannot do pointer arithmetic on a void*. 2. You cannot dereference a void*. 3. You cannot use the arrow operator on a void*, since it's also a reference. 4. You cannot use array notation on a void*, since
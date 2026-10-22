Knowing that restar is the sole initial means of access to the block of data it points to, the compiler can replace the two statements involving restar with a single statement having the same effect:

```
restar[n] += 8;    /* ok replacement */
```

It would be a computational error, however, to condense the two statements involving par into one:

```
par[n] += 8;    /* gives wrong answer */
```

The reason it gives the wrong answer is that the loop uses ar to change the value of the data between the two times par accesses the same data.

Without the restrict keyword, the compiler has to assume the worse case; namely, that some other identifier might have changed the data in between two uses of a pointer. With the restrict keyword used, the compiler is free to look for computational shortcuts.

You can use the restrict keyword as a qualifier for function parameters that are pointers. This means that the compiler can assume that no other identifiers modify the pointed-to data within the body of the function and that the compiler can try optimizations it might not otherwise use. For example, the C library has two functions for copying bytes from one location to another. Under C99, they have these prototypes:

```
void * memcpy(void * restrict s1, const void * restrict s2, size_t n);
```

```
void * memmove(void * s1, const void * s2, size_t n);
```

Each one copies n bytes from location s2 to location s1. The memcpy() function requires that there be no overlap between the two locations, but memmove() doesn’t have that requirement. Declaring s1 and s2 as restrict means each pointer is a sole means of access, so they can’t access the same block of data. This matches the requirement that there be no overlap. The memmove() function, which does allow overlap, has to be more careful about copying data so that it doesn’t overwrite data before it is used.

The keyword restrict has two audiences. One is the compiler, and it tells the compiler it is free to make certain assumptions concerning optimization. The other audience is the user, and it tells the user to use only arguments that satisfy the restrict requirements. In general, the compiler can’t check whether you obey this restriction, but you flout it at your own risk.

# The _Atomic Type Qualifier (C11)

Concurrent programming divides program execution into threads that may be executed in parallel. This creates several programming challenges, including how to manage different threads that access the same data. C11 provides, as an option and not a requirement, management methods set up by the optional header files stdatomic.h and threads.h. One aspect is the concept of an atomic type for which access is controlled by various macro functions. While a thread performs an atomic operation on an object of atomic type, other threads won’t access that object. For instance, something like
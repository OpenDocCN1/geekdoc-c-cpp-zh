```
char *strtok_r(char *string, char *delimeters, char **state)
{
char *beg, *end ;
if (string != NULL) *state = string ;
if (*state == NULL) return NULL ;
beg = state + strspn(*state, delimeters) ;
if (*beg == '\0') return NULL ;
end = strpbrk(beg, delimeters) ;
if (end == NULL) *state = NULL ;
else { *end++ = '\0' ; *state = end ; }
return beg ;
}
```

![](bbox=[0.706, 0.143, 0.906, 0.296])

# FIGURE 12-4 Library function strtok_r replaces local static by a third parameter.

Another example of a library function with similar problems caused by keeping a local static object is the random number generator, rand. A sequence of calls to rand produces a sequence of pseudo-random numbers. A companion function srand initializes the sequence using a starting “seed” value; for any one seed, the sequence of numbers produced by rand is deterministic and thus repeatable. However, if multiple threads call rand (or srand), the sequence returned within any one thread will no longer be deterministic. This may not be acceptable in certain situations.

# 12.4.2 Functions That Return the Address of a Local Static Object

Another coding practice that causes problems in multithreaded programs is the use of functions that return the address of a local static object. An example of such a function is shown in Figure 12-5. This function combines a string and an integer to form a 12-character filename. The filename is prepared in a local static buffer whose address is returned as the value of the function.

Suppose we call this function to prepare a filename to be used in a subsequent file creation. Then, if a second thread calls the same function before we have a chance to create the file, our filename will have been modified.

The problem, of course, is that there is only a single buffer shared by all threads; the solution is to have each thread provide its own separate buffer. In general, there are two ways to accomplish this: (1) let the thread provide the buffer by passing its address as an extra parameter to the function, as shown in Figure 12-6 or, (2) allocate the buffer from the heap, as shown in Figure 12-7.

Allocating from the heap eliminates adding a new function parameter but requires that the programmer release the space by an explicit call to library function free when the filename is no longer needed. Having the caller provide the buffer is faster, since we do not have to search for heap space, and it guarantees that the function will not fail when insufficient heap space is available.
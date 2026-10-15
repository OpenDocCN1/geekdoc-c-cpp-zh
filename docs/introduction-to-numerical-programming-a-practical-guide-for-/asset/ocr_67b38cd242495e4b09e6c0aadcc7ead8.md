![](bbox=[0.22, 0.09, 0.78, 0.18])

# FIGURE 2.2 The name of an array is a pointer containing the address of the first array element.

Technically, the above statement allocates a memory block of 10 consecutive locations of commensurate size to accommodate values of type double, defines a pointer a to values of type double, and stores therein the starting address of the memory block. Owing to the null offset featured by default by the C/C++ arrays, the valid components are in this case a[0] through a[9]. As indicated above, the pointer a associated with the array’s name contains the address of the first element, that is, &a[0] (see also Figure 2.2) and the allocation of the corresponding memory block takes place statically, during the compilation phase of the program.

Any operation with array elements may also be carried out by means of the associated pointer. According to pointer arithmetic, adding 1 to a pointer results in the memory address following the one contained in the pointer. From this perspective, since a contains the address of a[0], the operation a+1 yields the address of a[1], that is, &a[1], and, correspondingly, *(a+1) represents the value a[1]. In general, the element a[i] may also be referenced by the indirection *(a+i), and this is the actual way in which the compiler operates with references to array elements.

Although simple and easy to operate with, the static allocation of arrays is not always suitable. The storage requirements of large present-day computer applications can be very demanding and the efficient use of the primary memory often implies reusing it dynamically to store different objects, according to the instant needs. Therefore, a methodology for dynamic allocation of arrays, enabling, in addition, arbitrary offsets and index ranges, adapted to the natural mathematical notations, is highly useful.

The technical solution to the dynamic memory allocation in C/C++ is provided by the function malloc, defined in stdlib.h:

```
void *malloc((size_t) n)
```

malloc returns a pointer to an uninitialized contiguous block of n bytes in the heap (memory region used for dynamic objects), or NULL if the request cannot be satisfied. (size_t) converts n into the type used in C for sizing memory objects. In particular, to obtain a pointer to a memory block of sufficient size to hold n components of type double, one may issue the call

```
(double*) malloc((size_t) (n*sizeof(double)));
```

The function sizeof(type) returns the length in bytes of the internal representation of the type type and, hence, n*sizeof(double) represents the number of bytes necessary to store n components of type double. Finally, (double*) converts the unspecialized pointer returned by malloc into a pointer to locations of type double.

With these elements at hand, we build the function Vector0 (see Listing 2.11), which dynamically allocates a block of n double-type locations, and returns the starting address of the block via its name. If the allocation fails, possibly due to the unavailability of a suitable contiguous block in the heap, the execution is terminated by a call to the standard function exit(), and an error code is returned to the operation system for further action.

In the calling program, the pointer returned by Vector0 may be assigned to an array, whose components then correspond to successive locations in the allocated memory block. The array’s name must be first declared as a pointer and, once the size n becomes available, the array is effectively allocated by the
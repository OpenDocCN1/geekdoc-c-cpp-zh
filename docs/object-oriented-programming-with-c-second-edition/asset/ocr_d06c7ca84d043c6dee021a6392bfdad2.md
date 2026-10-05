In the foregoing listings, the memory block was deallocated only at the end of the functions allocated it. However, dynamic memory deallocation is usually conditional (Listing 3.7).

# Listing 3.7 C++ allows deallocation of memory as and when required

```
void abc(int ** p)
{
    if(memory_not_required) {
        delete *ptr;
        *p = NULL;
    }
/* rest of the abc() function
*/
```

A misconception about the delete operator is due to the commonly used phrase ‘deleting the pointer’. An uninitiated reader may think that the memory being occupied by the pointer gets removed if the delete operator is used on the pointer. In reality, nothing of this happens.

When the delete operator is used on a pointer, the pointer continues to occupy its block of memory and continues to have the same value that is the address of the first byte of the block of memory. Thus, the pointer continues to point at same block of memory. This will lead to runtime errors if the pointer is dereferenced.
We see in Listing 3.7 that the pointer being pointed at by ‘p’ was deliberately nullified after the pointer was pointing at had been deallocated. This is a very common practice to indicate that the pointer (the whose address is passed from the calling function) no longer points to a dynamically allocated block of memory. In other words, it is highly desirable that either the pointer points at a valid block of memory or be NULL. It is not possible to ensure this due to the low level of representation of pointers. A pointer is unlikely to be NULL at the time of creation. But that does not mean that the value contains is the address of some valid block of memory. There is no guaranteed initialization of data. This problem is solved by the use of constructors, which have been discussed in Chapter 4.

A multiple block of memory is deallocated by suffixing the delete operator with an empty pair of square brackets followed by the pointer that points at the multiple block of memory, as shown in Listing 3.8.

# Listing 3.8 Deallocating memory that was allocated for an array

```
int * Iptr;
...
ptr = new int[10];
...
delete[] Iptr;
```

If we write delete Iptr instead of delete[] Iptr, only the first four bytes of the block of 40 bytes at which Iptr is pointing, will be deallocated. Using delete[] deallocates the entire block of 40 bytes. The syntax for using the delete operator to allocate an array is as follows:

```
delete [] <ptr>;
```
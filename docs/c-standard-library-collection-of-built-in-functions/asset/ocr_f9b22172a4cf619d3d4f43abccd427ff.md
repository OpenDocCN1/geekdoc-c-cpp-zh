```
void *bsearch(const void *key, const void *base, size_t nitems, size_t size, int (*compar)(const void *, const void *))
```

# Parameters

+   - **key** -- This is the pointer to the object that serves as key for the search, type-casted as a void*.
+   - **base** -- This is the pointer to the first object of the array where the search is performed, type-casted as a void*.
+   - **nitems** -- This is the number of elements in the array pointed by base.
+   - **size** -- This is the size in bytes of each element in the array.
+   - **compar** -- This is the function that compares two elements.

# Return Value

This function returns a pointer to an entry in the array that matches the search key. If key is not found, a NULL pointer is returned.

# Example

The following example shows the usage of bsearch() function.

```
#include <stdio.h>
#include <stdlib.h>

int cmpfunc(const void * a, const void * b)
{
    return ( *(int*)a - *(int*)b );
}

int values[] = { 5, 20, 29, 32, 63 };

int main ()
{
    int *item;
    int key = 32;

    /* using bsearch() to find value 32 in the array */
    item = (int*) bsearch (&key, values, 5, sizeof (int), cmpfunc);
    if( item != NULL )
```
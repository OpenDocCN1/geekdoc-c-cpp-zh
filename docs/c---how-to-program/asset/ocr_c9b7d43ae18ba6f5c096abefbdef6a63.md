# ### 7.8.3 Adding an Integer to a Pointer

In conventional arithmetic, 3000 + 2 yields the value 3002. This is normally *not* the case with pointer arithmetic. When an integer is added to or subtracted from a pointer, the pointer is *not* incremented or decremented simply by that integer, but by that integer times the size of the object to which the pointer refers. The number of bytes depends on the object’s data type. For example, the statement

```
```c
vPtr += 2;
```
```

would produce 3008 (3000 + 2 * 4), assuming an integer is stored in 4 bytes of memory. In the array *v*, *vPtr* would now point to *v[2]* (Fig. 7.19). If an integer is stored in 2 bytes of memory, then the preceding calculation would result in memory location 3004 (3000 + 2 * 2). If the array were of a different data type, the preceding statement would increment the pointer by twice the number of bytes that it takes to store an object of that data type. When performing pointer arithmetic on a character array, the results will be consistent with regular arithmetic, because each character is 1 byte long.

> > **Common Programming Error 7.4**
> >
> > *Using pointer arithmetic on a pointer that does not refer to an element in an array.*

![](bbox=[0.3, 0.585, 0.73, 0.7])

**Fig. 7.19** | The pointer vPtr after pointer arithmetic.

# ### 7.8.4 Subtracting an Integer from a Pointer

If *vPtr* had been incremented to 3016, which points to *v[4]*, the statement

```
```c
vPtr -= 4;
```
```

would set *vPtr* back to 3000—the beginning of the array.

> > **Common Programming Error 7.5**
> >
> > *Running off either end of an array when using pointer arithmetic.*

# ### 7.8.5 Incrementing and Decrementing a Pointer

If a pointer is being incremented or decremented by one, the increment (++) and decrement (--) operators can be used. Either of the statements

```
```c
++vPtr;
vPtr++;
```
```
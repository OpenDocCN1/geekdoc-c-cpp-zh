In conventional arithmetic, the addition `3000 + 2` yields the value `3002`. This is normally *not* the case with pointer arithmetic. When an integer is added to, or subtracted from, a pointer, the pointer is *not* simply incremented or decremented by that integer, but by that integer *times the size of the memory object to which the pointer refers*. The number of bytes depends on the memory object’s data type. For example, the statement

```
```c
vPtr += 2;
```
```

would produce `3008` (from the calculation `3000 + 2 * 4`), assuming that an `int` is stored in four bytes of memory. In the built-in array `v`, `vPtr` would now point to `v[2]` (Fig. 8.16). If an integer is stored in eight bytes of memory, then the preceding calculation would result in memory location `3016` (`3000 + 2 * 8`).

![](bbox=[0.115, 0.628, 0.646, 0.824])

Fig. 8.16 Pointer `vPtr` after pointer arithmetic.
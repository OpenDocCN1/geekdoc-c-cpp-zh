The last declaration could also be written

```
double * ptr = dArray; // pointer to first element of dArray
```

![](bbox=[0.26, 0.22, 0.82, 0.33])

Now consider the following loop:

```
for (int i = 0; i < 10; i++)
{
    *ptr = 0;
    ptr++;
}
```

On the first pass through the loop, ptr is dereferenced and the value 0 is assigned to the memory location at that address. ptr is then incremented, which adds sizeof(double) to its value, effectively making ptr point to the second element of the array:

![](bbox=[0.26, 0.69, 0.82, 0.8])

The next pass again dereferences ptr, sets that memory location to zero, and increments ptr:

![](bbox=[0.26, 0.9, 0.82, 1.01])

This continues with each subsequent iteration. On the final pass, the last element of the array is set to zero. Then after ptr is incremented, it points to the first address past the end of the array:

![](bbox=[0.26, 1.18, 0.82, 1.29])
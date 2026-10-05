```
int carray[10]; // C-array remains uninitialized
```

With carray+10, you initialize end so that it is a pointer **behind** the last element of the C-array. It is a common convention in C and C++ to remember the end of a range, rather than pointing to the last element itself. The side effect is that the difference between the two `carray` and end pointers is exactly the number of elements in between: ((end-carray)=10) is true.

Then initialize the `int* p` for the loop with `carray+2`, thus pointing to the first element after the two ones in `carray`. This should be the first position you want to write to. For each iteration of the loop, advance `p` by one position in the C-array. However, you need to check the `for` loop after each increment to see if `p != end` checks if `p` is not yet pointing to the element after the C-array, which would signify the end of the loop. Thus, during the loop, `p` points to `carray+2`, `carray+3`, `carray+4`, ... up to `carray+9`, to execute the loop body. The final increment advances `p` to `carray+10`, which represents the loop's termination condition.

In the loop body, you write to `*p`, which means what `carray+2` to `carray+9` refer to sequentially. What do you write? Well, `*(p-1) + *(p-2)` for the sum of the two previous elements—for the first iteration, effectively:

```
*p = *(p-1) + *(p-2); // in the first loop iteration, p = carray+2, so:
*(carray+2) = *(carray+2-1) + *(carray+2-2); // which is:
```
```
    34     // output sorted array
    35     for (size_t i = 0; i < SIZE; ++i) {
    36         printf("%4d", a[i]);
    37     }
    38
    39     puts("");
    40 }
```

| Data items in original order | 2 | 6 | 4 | 8 | 10 | 12 | 89 | 68 | 45 | 37 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Data items in ascending order | 2 | 4 | 6 | 8 | 10 | 12 | 37 | 45 | 68 | 89 |

Fig. 6.12 | Sorting an array's values into ascending order. (Part 2 of 2.)

First, the program compares a[0] to a[1], then a[1] to a[2], then a[2] to a[3], and so on until it completes the pass by comparing a[8] to a[9]. Although there are 10 elements, only nine comparisons are performed. A large value may move down the array many positions on a single pass because of how the successive comparisons are made, but a small value may move up only one position.

On the first pass, the largest value is guaranteed to sink to the array's bottom element, a[9]. On the second pass, the second-largest value is guaranteed to sink to a[8]. On the ninth pass, the ninth-largest value sinks to a[1]. This leaves the smallest value in a[0], so only nine passes are needed to sort the 10-element array.

# Swapping Elements

The sorting is performed by the nested for loops (lines 19–30). If a swap is necessary, it's performed by the three assignments in lines 25–27

```
    int hold = a[i];
    a[i] = a[i + 1];
    a[i + 1] = hold;
```

The variable hold temporarily stores one of the two values being swapped. The swap cannot be performed with only the two assignments

```
    a[i] = a[i + 1];
    a[i + 1] = a[i];
```

If, for example, a[i] is 7 and a[i + 1] is 5, after the first assignment, both values will be 5 and the value 7 will be lost—hence the need for the extra variable hold.

# Bubble Sort Is Easy to Implement, But Slow

The chief virtue of the bubble sort is that it's easy to program. However, it runs slowly because every exchange moves an element only one position closer to its final destination. This becomes apparent when sorting large arrays. In the exercises, we'll develop more efficient versions of the bubble sort. Far more efficient sorts than the bubble sort have been developed. We'll investigate other algorithms in Chapter 13. More advanced courses investigate sorting and searching in greater depth.
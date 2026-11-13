# Pass 2:

```
(15) (23) 58 66 32 31 70 72 [No interchange]
15 (23) (58) 66 32 31 70 72 [No interchange]
15 23 (58) (66) 32 31 70 72 [No interchange]
15 23 58 (66) (32) 31 70 72 [Interchange]
32
15 23 58 32 (66) (31) 70 72 [Interchange]
15 23 58 32 31 (66) (70) 72 [No interchange]
15 23 58 32 31 66 70 72
```

At this pass the second largest element is placed in the n-1st location and takes n-2 comparisons.

# Pass 3:

```
(15) (23) 58 32 31 66 70 72 [No interchange]
15 (23) (58) 32 31 66 70 72 [No interchange]
15 23 (32) (58) 31 66 70 72 [Interchange]
15 23 32 (31) (58) 66 70 72 [Interchange]
15 23 32 31 (58) (66) 70 72 [No interchange]
```

At this pass the third largest element is placed in the n-2nd location and takes n-3 comparisons.

# Pass 4:

```
(15) (23) 32 31 58 66 70 72 [No interchange]
15 (23) (32) 31 58 66 70 72 [No interchange]
15 23 (31) (32) 58 66 70 72 [Interchange]
15 23 31 32 58 66 70 72
```

At this pass the fourth largest element is placed in the n-3rd location and takes n-4 comparisons.

# Pass 5:

```
(15) (23) 31 32 58 66 70 72 [No interchange]
15 (23) (31) 32 58 66 70 72 [No interchange]
15 23 (31) (32) 58 66 70 72 [No interchange]
```

At this pass the fifth largest element is placed in the n-4th location and takes n-5 comparisons.

# Pass 6:

```
(15) (23) 31 32 58 66 70 72 [No interchange]
15 23 31 32 58 66 70 72
```

At this pass the sixth largest element is placed in the n-5th location and takes n-6 comparisons.

# Pass 7:

A1 is compared with A2, since 15 < 23 no interchange takes place.

Finally the sorted array is (15 23 31 32 58 66 70 72)
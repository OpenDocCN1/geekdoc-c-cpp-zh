![](bbox=[0.18, 0.13, 0.91, 0.25])

Now left = loc, so the procedure terminates, as the pivot element (the first element of the array, that is, 27) is placed in its correct position. All the elements smaller than 27 are placed before it and those greater than 27 are placed after it.

The left sub-array containing 25, 10, 18 and the right sub-array containing 36 and 45 are sorted in the same manner.

The quick sort algorithm (Fig. 14.10) makes use of a function Partition to divide the array into two sub-arrays.

```
```
PARTITION (ARR, BEG, END, LOC)
Step 1: [INITIALIZE] SET LEFT = BEG, RIGHT = END, LOC = BEG, FLAG = 0
Step 2: Repeat Steps 3 to 6 while FLAG = 0
Step 3: Repeat while ARR[LOC] <= ARR[RIGHT] AND LOC != RIGHT
    SET RIGHT = RIGHT - 1
[END OF LOOP]
IF LOC = RIGHT
    SET FLAG = 1
ELSE IF ARR[LOC] > ARR[RIGHT]
    SWAP ARR[LOC] with ARR[RIGHT]
    SET LOC = RIGHT
[END OF IF]
Step 5: IF FLAG = 0
    Repeat while ARR[LEFT] <= ARR[LOC] AND LOC != LEFT
        SET LEFT = LEFT + 1
    [END OF LOOP]
    IF LOC = LEFT
        SET FLAG = 1
    ELSE IF ARR[LOC] < ARR[LEFT]
        SWAP ARR[LOC] with ARR[LEFT]
        SET LOC = LEFT
    [END OF IF]
[END OF IF]
Step 7: [END OF LOOP]
Step 8: END

QUICK_SORT (ARR, BEG, END)
Step 1: IF (BEG < END)
    CALL PARTITION (ARR, BEG, END, LOC)
    CALL QUICKSORT(ARR, BEG, LOC - 1)
    CALL QUICKSORT(ARR, LOC + 1, END)
[END OF IF]
Step 2: END
```
```

Figure 14.10 Algorithm for quick sort
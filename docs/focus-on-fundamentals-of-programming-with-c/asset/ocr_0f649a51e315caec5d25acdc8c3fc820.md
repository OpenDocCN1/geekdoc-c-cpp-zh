The data item 8 is placed into the temporary memory location, thus opening a possible insertion point:

| 3 | 5 | | 2 | 9 | 4 | 6 | 7 |
|---|---|---|---|---|---|---|---|

![](bbox=[0.07, 0.18, 0.15, 0.23])

8 > 5 so the 8 gets placed into the insertion point:

| 3 | 5 | 8 | 2 | 9 | 4 | 6 | 7 |
|---|---|---|---|---|---|---|---|

![](bbox=[0.07, 0.35, 0.15, 0.4])

At the end of the 2nd pass, the first 3 data items are sorted.

We begin the 3rd pass. The next data item to sort is 2:

| 3 | 5 | 8 | 2 | 9 | 4 | 6 | 7 |
|---|---|---|---|---|---|---|---|

![](bbox=[0.07, 0.57, 0.15, 0.62])

The data item 2 is placed into the temporary memory location, thus opening a possible insertion point:

| 3 | 5 | 8 | | 9 | 4 | 6 | 7 |
|---|---|---|---|---|---|---|---|

![](bbox=[0.07, 0.75, 0.15, 0.8])
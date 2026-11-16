4 > 3 so 4 gets placed into the insertion point:

| 2 | 3 | 4 | 5 | 8 | 9 | 6 | 7 |
|---|---|---|---|---|---|---|---|

![](bbox=[0.107, 0.153, 0.166, 0.2])

At the end of the 5<sup>th</sup> pass, the first 6 data items are sorted.

We begin the 6<sup>th</sup> pass. The next data item to sort is 6:

| 2 | 3 | 4 | 5 | 8 | 9 | 6 | 7 |
|---|---|---|---|---|---|---|---|

![](bbox=[0.107, 0.373, 0.166, 0.4])

The data item 6 is placed into the temporary memory location, thus opening a possible insertion point:

| 2 | 3 | 4 | 5 | 8 | 9 |   | 7 |
|---|---|---|---|---|---|---|---|

![](bbox=[0.107, 0.553, 0.166, 0.6])

6 < 9 so we must open a new insertion point. We shift 9 to the right one position opening a new insertion point:

| 2 | 3 | 4 | 5 | 8 |   | 9 | 7 |
|---|---|---|---|---|---|---|---|

![](bbox=[0.107, 0.743, 0.166, 0.79])
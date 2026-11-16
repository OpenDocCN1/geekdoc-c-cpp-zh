2 < 8 so we must open a new insertion point. We shift 8 to the right one position opening a new insertion point:

| 3 | 5 | | 8 | 9 | 4 | 6 | 7 |
|---|---|---|---|---|---|---|---|

| 2 |
|---|

2 < 5 so we must open a new insertion point. We shift 5 to the right one position opening a new insertion point:

| 3 | | 5 | 8 | 9 | 4 | 6 | 7 |
|---|---|---|---|---|---|---|---|

| 2 |
|---|

2 < 3 so we must open a new insertion point. We shift 3 to the right one position opening a new insertion point:

| | 3 | 5 | 8 | 9 | 4 | 6 | 7 |
|---|---|---|---|---|---|---|---|

| 2 |
|---|

Reaching the start of the array tells us that the current insertion point is valid as the new data item is the smallest data item seen so far. So we insert the data item into the insertion point:

| 2 | 3 | 5 | 8 | 9 | 4 | 6 | 7 |
|---|---|---|---|---|---|---|---|

| |
|---|

At the end of the 3rd pass, the first 4 data items are sorted.
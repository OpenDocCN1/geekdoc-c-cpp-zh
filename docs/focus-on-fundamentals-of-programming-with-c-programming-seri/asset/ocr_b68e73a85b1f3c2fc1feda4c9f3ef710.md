The data item 4 is placed into the temporary memory location, thus opening a possible insertion point:

| 2 | 3 | 5 | 8 | 9 | | 6 | 7 |
|---|---|---|---|---|---|---|---|
| 4 | temp |

4 < 9 so we must open a new insertion point. We shift 9 to the right one position opening a new insertion point:

| 2 | 3 | 5 | 8 | | 9 | 6 | 7 |
|---|---|---|---|---|---|---|---|
| 4 | temp |

4 < 8 so we must open a new insertion point. We shift 8 to the right one position opening a new insertion point:

| 2 | 3 | 5 | | 8 | 9 | 6 | 7 |
|---|---|---|---|---|---|---|---|
| 4 | temp |

4 < 5 so we must open a new insertion point. We shift 5 to the right one position opening a new insertion point:

| 2 | 3 | | 5 | 8 | 9 | 6 | 7 |
|---|---|---|---|---|---|---|---|
| 4 | temp |
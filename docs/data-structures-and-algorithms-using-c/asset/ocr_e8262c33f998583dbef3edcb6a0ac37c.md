# # HowSelectionSort Works?

Consider the following depicted array as an example.

| 14 | 33 | 27 | 10 | 35 | 19 | 42 | 44 |
|---|---|---|---|---|---|---|---|

For the first position in the sorted list, the whole list is scanned sequentially. The first position where 14 is stored presently, we search the whole list and find that 10 is the lowest value.

| 14 | 33 | 27 | 10 | 35 | 19 | 42 | 44 |
|---|---|---|---|---|---|---|---|

So we replace 14 with 10. After one iteration 10, which happens to be the minimum value in the list, appears in the first position of the sorted list.

| 10 | 33 | 27 | 14 | 35 | 19 | 42 | 44 |
|---|---|---|---|---|---|---|---|

For the second position, where 33 is residing, we start scanning the rest of the list in a linear manner.

| 10 | 33 | 27 | 14 | 35 | 19 | 42 | 44 |
|---|---|---|---|---|---|---|---|

We find that 14 is the second lowest value in the list and it should appear at the second place. We swap these values.

| 10 | 33 | 27 | 14 | 35 | 19 | 42 | 44 |
|---|---|---|---|---|---|---|---|

After two iterations, two least values are positioned at the beginning in a sorted manner.

| 10 | 14 | 27 | 33 | 35 | 19 | 42 | 44 |
|---|---|---|---|---|---|---|---|

The same process is applied to the rest of the items in the array.

Following is a pictorial depiction of the entire sorting process –
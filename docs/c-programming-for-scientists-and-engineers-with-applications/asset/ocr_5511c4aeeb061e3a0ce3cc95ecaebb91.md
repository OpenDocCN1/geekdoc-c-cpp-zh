its sorted position. The following example shows the result of the two passes needed to sort a short list in descending order.

| ORIGINAL LIST | EXCHANGE | AFTER PASS 1 | EXCHANGE | AFTER PASS 2 |
|---|---|---|---|--|
| 9 | . | 15 | . | 15 |
| 15 | 9 | 9 | 12 | 12 |
| 8 | 12 | 12 | 9 | 9 |
| 7 | 12 | 8 | . | 8 |
| 12 | 7 | 7 | . | 7 |

The basic bubble sort would use four passes to sort an array of five elements, whether or not all the passes were needed. An optimized bubble sort checks whether more passes are needed.

The pseudocode and the flowchart for the basic bubble sort and the optimized bubble sort all the passes are used whether the list at some point is sorted or not. In the optimized bubble sort a conditional test is performed at the end of every pass to see if any exchange has occurred. If no exchange occurred during the latest pass, the list is already in sorted order and the sort is complete. A minor modification to the basic bubble sort. The flowchart for the bubble sort is given in Figure 7.2.

If the original list is arranged in the worst possible order, then $(n - 1)$ passes are needed to sort a list containing $n$ elements. Each pass of a regular bubble sort involves $n - 1$ comparisons of values. This is a total of $(n - 1) \cdot (n - 1) = n^2 - 2n + 1$ comparisons. If it is optimized, then there are $n - 1$ comparisons in the first pass, $n - 2$ comparisons in the second pass, $n - 3$ comparisons in the third pass, for a total of $(n - 1) + (n - 2) + (n - 3) + \dots + 2 + 1 = n(n - 1)/2 \approx$ comparisons. Whether the bubble sort is optimized or not, the number of comparisons is roughly proportional to $n^2$. The bubble sort is said to be of order of $n^2$.

Pseudocode

```
funcbubblesort:
  for each index i from 1 to n
    for each index j from n-1 to i
      if a[j] > a[j-1]
        temp <- a[j]
```
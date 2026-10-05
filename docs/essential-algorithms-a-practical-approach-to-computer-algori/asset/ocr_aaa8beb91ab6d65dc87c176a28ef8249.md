# Chapter 7 = Searching 167

End While

Return -1
InterpolationSearch

This high-level description leaves a couple of problems unsolved. The mid calculation can result in an overflow or a value of mid that is not between min and max. Solving these problems is left as part of Exercise 6. The trickiest part of this algorithm is the statement that calculates mid. The value is set to the current value of min plus the distance between min and max when scaled by values [max] where target should lie. For example, if values[min] is 100, values[max] is 200, and target is 125, then you would use the following calculation to decide where to look for the target value:

```
(target - values[min]) / (values[max] - values[min]) =
(125 - 100) / (200 - 100) =
25 / 100 = 
0.25
```

That puts the new value for mid one quarter of the way from min to max. In the worst case, if the data is extremely unevenly distributed, and you're looking for the worst possible target value, this algorithm has O(N) performance. If the distribution is reasonably uniform, the expected performance is O(log(log N)). (But proving that is outside the scope of this book.)

# Summary

Table 7-1 shows the values of log N and log(log N) for different values of N that you can compare the speeds of linear search, binary search, and interpolation.

Table 7-1: Algorithm Characteristics

| N | LOG₂ N | LOG₂(LOG₂ N) |
|---|---|--|
| 1,000 | 10.0 | 3.3 |
| 1,000,000 | 19.9 | 4.3 |
| 1,000,000,000 | 29.9 | 4.9 |
| 1,000,000,000,000 | 39.9 | 5.3 |

Linear search is useful only for relatively small arrays. Table 7-1 shows that binary search works well even for very large arrays. It can search an array containing 1 trillion items in only about 40 steps.
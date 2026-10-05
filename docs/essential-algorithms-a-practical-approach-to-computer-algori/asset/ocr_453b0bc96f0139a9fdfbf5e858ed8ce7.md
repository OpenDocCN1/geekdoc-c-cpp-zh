# Chapter 4 ■ Arrays 85

Figure 4-2 shows row-major and column-major mappings.

![](bbox=[0.195, 0.125, 0.635, 0.438])

**Figure 4-2:** A program can map array entries to memory locations in either row-major or column-major order.

You can extend the ideas of row-major and column-major ordering for higher-dimensional arrays. For example, to store a three-dimensional array in row-major order, the program would map the first two-dimensional “slice” of the array where the third dimension's index is 0. It would map that slice in row-major order as usual. It would then similarly map the second slice where the third dimension index is 1, and so on for the remaining slices.

Another way to think of this is as an algorithm for mapping three-dimensional array. Suppose you have defined a Map2DArray method that maps a two-dimensional array. The following algorithm uses Map2DArray to map a three-dimensional array.

```
For i = 0 To <upper bound of array's third coordinate>
  Map2DArray<array with the third coordinate set to i>
```

Next i
Similarly, you could use this algorithm to define algorithms for mapping arrays with even dimensions.

Normally how a program maps array entries to memory locations is irrelevant to how a program works, and there’s no why you should care. Your code manipulates the array entries, and you don’t need to know how they are stored. However, understanding how the row-major and column-major orders
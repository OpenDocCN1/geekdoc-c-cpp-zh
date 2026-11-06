# Sample Merge

Suppose the algorithm has already merged smaller `arrays` to create sorted `arrays` A:

```
A = [
  4  10  34  56  77
]
```

and B:

```
B = [
  5  30  51  52  93
]
```

Merge sort merges these `arrays` into a sorted `array`. The smallest value in A is 4 (located in the zeroth element of A). The smallest value in B is 5 (located in the zeroth element of B). In order to determine the smallest element in the larger `array`, the algorithm compares 4 and 5. The value from A is smaller, so 4 becomes the value of the first element in the merged `array`. The algorithm continues by comparing 10 (the value of the second element in A) to 5 (the value of the first element in B). The value from B is smaller, so 5 becomes the value of the second element in the larger `array`. The algorithm continues by comparing 10 and 30, with 10 becoming the value of the third element in the `array`, and so on.
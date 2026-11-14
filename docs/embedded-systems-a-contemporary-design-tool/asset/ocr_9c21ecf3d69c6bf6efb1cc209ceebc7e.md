Since the search range decreases by "one" with each pass, the total work can be computed as the sum of the first N numbers.

```
N \bullet \frac{N-1}{2}
```

+   2. By the three lines comprising the swap operation:

```
N - 1 calls -> N - 1 exchanges
```

+   3. By other statements:

```
Each exchange -> 3 assignments
```

The final total is given as:

```
Total = N \bullet \frac{N-1}{2} + 3 \bullet (N - 1) (14.6)
```

The complexity of selection sort thus reduces to:

```
O \left( \frac{N^2}{2} \right) -> O(N^2)
```

# 14.8.2.2 Quick Sort

The quick sort algorithm has a worst case complexity of O(N log2 N). Computing this value will be left as an exercise.

# 14.9 ANALYZING DATA STRUCTURES

We will now examine two important containers: the array and the linked list. For each, we will look at the following fundamental operations.

+   - Insert/delete at the beginning.
+   - Insert/delete at the end.
+   - Insert/delete in the middle.
+   - Access at the beginning, the end, and in the middle.

For the analysis, we assume that each of the data structures is allocated at compile time and does not support runtime allocation.

# 14.9.1 Array

Two cases must be considered for each operation; whether the operation is to be executed as an overwrite or as an insert. The first case will not require moving data, whereas the second will.

+   - Insert/delete at the beginning

In the overwrite mode, inserting an element is done in constant time. The complexity is O(1).

In the insert mode, each element of the container must be moved to make room for the new element. Thus, the complexity is O(N), where N is the number of elements in the array.

The complexity of the delete operation is the same as that for the insert mode, O(N). Each element in the container must be moved to fill the void.
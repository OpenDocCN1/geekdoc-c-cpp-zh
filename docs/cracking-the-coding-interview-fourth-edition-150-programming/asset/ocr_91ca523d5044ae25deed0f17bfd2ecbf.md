# Solutions to Chapter 20 | Hard

**20.11** Imagine you have a square matrix, where each cell is filled with either black or white. Design an algorithm to find the maximum subsquare such that all four borders are filled with black pixels... & count all white?

# SOLUTION

Assumption: Square is of size NxN.

This algorithm does the following:

+   1. Iterate through every (full) column from left to right.
2. At each (full) column (call this currentColumn), look at the subcolumns (from biggest to smallest).
3. At each subcolumn, see if you can form a square with the subcolumn as the left side. If so, update maxSize and go to the next (full) column.
4. If N -currentColumn <= maxSize, break completely. We've found the largest square possible. Why? At each column, we're trying to create a square with the column as the left side. The largest square we could possibly create is N-currentColumn. Thus, if-currentColumn <= maxSize, we have no need to proceed.

Time complexity: O(N^2)

```
public static Subsquare findSquare(int[][] matrix) {
    assert(matrix.length > 0);
    for (int row = 0; row < matrix.length; row++){
        assert(matrix[row].length == matrix.length);
    }
    int N = matrix.length;
    int currentMaxSize = 0;
    Subsquare sq = null;
    int col = 0;
    // Iterate through each column from left to right
    while (N - col > currentMaxSize) { // See step 4 above
        for (int row = 0; row < matrix.length; row++){
            int size = N - Math.max(row, col);
            while (size > currentMaxSize) {
                if (isSquare(matrix, row, col, size)){
                    currentMaxSize = size;
                    sq = new Subsquare(row, col, size);
                    break; // go to next (full) column
                }
            }
        }
```
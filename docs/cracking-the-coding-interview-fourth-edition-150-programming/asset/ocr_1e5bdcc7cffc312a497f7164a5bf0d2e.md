# Solutions to Chapter 20 | Hard

Val_D = area(point(0, 0) -> point(x2, y2)
Val_C = area(point(0, 0) -> point(x2, y1)
Val_B = area(point(0, 0) -> point(x1, y2)
Val_A = area(point(0, 0) -> point(x1, y1)

With these values, we know that:

(D) = Val_D - area(A union C) - area(A union B) + area(A).

Or, another way:

(D) = Val_D - Val_B - Val_C + Val_A

If we efficiently compute this Val* for all points in the matrix? Yes, by using similar-logic:

Val(x, y) = Val(x - 1, y) + Val(y - 1, x) - Val(x - 1, y - 1)

We precompute all such values, and then efficiently find the maximum submatrix.

```
public static int getMaxValue(int[][] matrix) { // original {
    int maxArea = Integer.MIN_VALUE; // ! Max could be < 0
    int rowCount = original.length;
    int colCount = original[0].length;
    int[][] matrix = precomputeMatrix(original);
    for (int row = 0; row < rowCount; row++) {
        for (int row2 = row; row2 < rowCount; row2++) {
            for (int col1 = 0; col1 < colCount; col1++) {
                for (int col2 = col1; col2 < colCount; col2++) {
                    maxArea = Math.max(maxArea, computeSum(matrix, row, row2, col1, col2));
                }
            }
        }
    }
    return maxArea;
}}
```

```
private static int[][] precomputeMatrix(int[][] matrix) { // original {
    int[][] sumMatrix = new int[matrix.length][matrix.length];
    for (int i = 0; i < matrix.length; i++) {
        for (int j = 0; j < matrix.length; j++) {
            if (i == 0 && j == 0) // first cell
                sumMatrix[i][j] = matrix[i][j];
            } else if (j == 0) // in first column
                sumMatrix[i][j] = sumMatrix[i-1][j] + matrix[i][j];
            } else if (i == 0) // in first row
                sumMatrix[i][j] = sumMatrix[i][j-1] + matrix[i][j];
            } else {
                sumMatrix[i][j] = sumMatrix[i-1][j] + sumMatrix[i][j-1] - sumMatrix[i-1][j-1] + matrix[i][j];
            }
        }
    }
    return sumMatrix;
}
```

CareerCup.com 296
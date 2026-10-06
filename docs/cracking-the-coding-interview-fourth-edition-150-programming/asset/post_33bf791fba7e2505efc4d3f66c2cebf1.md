
## Solutions to Chapter 20 | Hard

**20.10** Given two words of equal length that are in a dictionary, write a method to transform one word into another by changing only one letter at a time. The new word you get in each step must be in the dictionary.

EXAMPLE:

Input: DAMP, LIKE

Output: DAMP -> LAMP -> LIMP -> LIME -> LIKE

## SOLUTION

Though this problem seems tough, it's actually a straightforward modification of breadth-first-search. Each word in our “graph” branches to all words in the dictionary that are one edit away. The interesting part is how to implement this—should we build a graph as we go? There is an easier way. We can instead use "backtrack map" if B(v) = w, then you know that you edited v to get w. When we reach our end word, we can use this backtrack map repeatedly to recover path. See the code below:

- 1. LinkedList<String> transform(String startword, String stopword,

```java
Set<String> dictionary = new Set<String>();
startword = startword.toUpperCase();
stopword = stopword.toUpperCase();
Queue<String> actionQueue = new LinkedList<String>();
Set<String> visited = new HashSet<String>();
Map<String, String> backtrackMap = new TreeMap<String, String>();

actionQueue.add(startword);
visited.add(startword);

while (!actionQueue.isEmpty()) {
    String w = actionQueue.poll();
    // For each possible word v from w with one edit operation
    for (String v : getEditWords(w)) {
        if (v.equals(stopword)) {
            // Found our word! Now, back track.
            LinkedList<String> list = new LinkedList<String>();
            // Append v to list
            list.add(v);
            while (w != null) {
                list.add(0, w);
                w = backtrackMap.get(w);
            }
            return list;
        }
    }
}
// If v is a dictionary word
```

```java
if (dictionary.contains(v)) {
    if (!visited.contains(v)) {
        actionQueue.add(v);
        visited.add(v); // mark visited
        backtrackMap.put(v, w);
    }
}
return null;

Set<String> getOneEditWords(String word) {
    Set<String> result = new TreeSet<String>();
    for (int i = 0; i < word.length(); i++) {
        char[] wordArray = word.toCharArray();
        // change letter to something else
        for (char c = 'A'; c <= 'Z'; c++) {
            if (c != word.charAt(i)) {
                wordArray[i] = c;
                result.add(new String(wordArray));
            }
        }
    }
    return result;}
```

Let n be the length of the start word and m be the number of like sized words in the dictionary. The runtime of this algorithm is O(n*m) since the while loop will dequeue at m unique words. The for loop is O(n) as it walks the string applying a fixed number of replacements for each character.

**20.11** Imagine you have a square matrix, where each cell is filled with either black or white. Design an algorithm to find the maximum subsquare such that all four borders are filled with black pixels... & count all white?

## SOLUTION

Assumption: Square is of size NxN.

- 1. Iterate through every (full) column from left to right.
- 2. At each (full) column (call this currentColumn), look at the subcolumns (from biggest to smallest).
- 3. At each subcolumn, see if you can form a square with the subcolumn as the left side. If so, update maxSize and go to the next (full) column.
- 4. If N -currentColumn <= maxSize, break completely. We've found the largest square possible. Why? At each column, we're trying to create a square with the column as the left side. The largest square we could possibly create is N-currentColumn. Thus, if-currentColumn <= maxSize, we have no need to proceed.

Time complexity: O(N^2)

```java
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

```java
}
size--;
}
col++;
}
return sq;
}
}
private static boolean isSquare(int[][] matrix, int row, int col,
    int size) {
    // Check top and bottom border.
    for (int j = 0; j < size; j++) {
        if (matrix[row][col+j] == 1) {
            return false;
        }
        if (matrix[row+size-1][col+j] == 1){ // I=white O=black?
            return false;
        }
    }
    // Check left and right border.
    for (int i = 1; i < size - 1; i++) {
        if (matrix[row+i][col] == 1) {
            return false;
        }
        if (matrix[row+i][col+size-1] == 1) {
            return false;
        }
    }
    return true;
}
public class Subsquare {
    public int row, column, size;
    public Subsquare(int r, int c, int sz) {
        row = r;
        column = c;
        size = sz;
    }
}
```

**20.12** Given an NxN matrix of positive and negative integers, write code to find the submatrix with the largest sum.

## SOLUTION

**Brute Force: O(N^6)**

Like many problems, the brute force solution simply iterates through all possible rows and columns, and then computes the sum of each sub-matrix.

**Optimized Solution: O(N^4)**

Notice that the earlier solution is slower because it iterates through all possible sub-matrices. In fact, we can reduce the time to O(N^4) by using the following:

```java
public static int getMaxValue(int[][] matrix) { // original {
    int maxArea = Integer.MIN_VALUE; // Max could be 0
    int rowCount = matrix.length;
    int colCount = matrix[0].length;
    int[][] matrix = precomputeMatrix(matrix);
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
}
```

```java
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

With these values, we know that the sum of any sub-matrix from (row1, col1) to (row2, col2) can be computed efficiently:

sum = sumMatrix[row2][col2] - sumMatrix[row1-1][col2] - sumMatrix[row2][col1-1] + sumMatrix[row1-1][col1-1].

Wait, another way to reduce the time to O(N^2) is by using the following:

Val(x, y) = Val(x - 1, y) + Val(y - 1, x) - Val(x - 1, y - 1)

If we efficiently compute this for all points in the matrix, we can find the maximum submatrix.

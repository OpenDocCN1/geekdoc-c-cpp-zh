

## 第 20 章解答 | 困难

**20.10** 给定两个长度相等且在字典中的单词，编写一个方法，通过每次只改变一个字母将一个单词转换为另一个单词。每一步得到的新单词必须在字典中。

示例：

输入：DAMP, LIKE

输出：DAMP -> LAMP -> LIMP -> LIME -> LIKE

## 解决方案

虽然这个问题看起来很困难，但它实际上是广度优先搜索的直接变体。在我们“图”中的每个单词都连接到字典中所有仅编辑一次的单词。有趣的部分在于如何实现它——我们应该边走边构建图吗？有一种更简单的方法。我们可以使用“回溯映射”（backtrack map），如果 B(v) = w，那么你就知道通过编辑 v 得到了 w。当我们到达目标单词时，可以反复使用这个回溯映射来恢复路径。代码如下：

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
    // 对于从 w 通过一次编辑操作得到的每个单词 v
    for (String v : getEditWords(w)) {
        if (v.equals(stopword)) {
            // 找到了我们的单词！现在，回溯。
            LinkedList<String> list = new LinkedList<String>();
            // 将 v 添加到列表
            list.add(v);
            while (w != null) {
                list.add(0, w);
                w = backtrackMap.get(w);
            }
            return list;
        }
    }
}
// 如果 v 是字典中的单词
```

```java
if (dictionary.contains(v)) {
    if (!visited.contains(v)) {
        actionQueue.add(v);
        visited.add(v); // 标记为已访问
        backtrackMap.put(v, w);
    }
}
return null;

Set<String> getOneEditWords(String word) {
    Set<String> result = new TreeSet<String>();
    for (int i = 0; i < word.length(); i++) {
        char[] wordArray = word.toCharArray();
        // 将字母改为其他字符
        for (char c = 'A'; c <= 'Z'; c++) {
            if (c != word.charAt(i)) {
                wordArray[i] = c;
                result.add(new String(wordArray));
            }
        }
    }
    return result;}
```

令 n 为起始单词的长度，m 为字典中长度相等的单词数量。该算法的运行时间为 O(n*m)，因为 while 循环会出队 m 个唯一的单词。for 循环是 O(n)，因为它通过遍历字符串并对每个字符应用固定次数的替换。

**20.11** 假设你有一个正阵矩阵，每个单元格都填充了黑色或白色。设计一个算法找到最大的子正方形，使得四个边界都填充了黑色像素……并 统计所有白色像素？

## 解决方案

假设：正方形大小为 NxN。

- 1. 从左到右遍历每一（完整的）列。
- 2. 在每一列（完整的）列（称为 currentColumn）处，查看子列（从大到小）。
- 3. 在每个子列处，检查是否可以以该子列为左边界形成正方形。如果是，更新 maxSize 并移动到下一个（完整的）列。
- 4. 如果 N - currentColumn <= maxSize，完全停止。我们找到了最大的正方形。为什么呢？在每一列，我们都在尝试以该列为左边界创建一个正方形。可能创建的最大正方形是 N-currentColumn。因此，如果 currentColumn <= maxSize，我们就不继续了。时间复杂度为 O(N^2)

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
    // 从左到右遍历每一列
    while (N - col > currentMaxSize) { // 查看第4 步
        for (int row = 0; row < matrix.length; row++){
            int size = N - col;
            while (size > currentMaxSize) {
                if (isSquare(matrix, row, col, size)){
                    currentMaxSize = size;
                    sq = new Subsquare(row, col, size);
                    break; // 移动到下一个（完整的）列
                }
                size--;
            }
        }
        col++;
    }
    return sq;
}
private static boolean isSquare(int[][] matrix, int row, int col,
    int size) {
    // 检查顶部和底部边界
    for (int j = 0; j < size; j++) {
        if (matrix[row][col+j] == 1) { // 如果是白色（如果是黑色）
            return false;
        }
        if (matrix[row+size-1][col+j] == 1) {
            return false;
        }
    }
    // 检查左边界和右边界
    for (int i = 1; i < size; i++) {
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

**20.12** 给出一个包含正负整数的 NxN矩阵，编写代码找到和最大的子矩阵。

## 解决方案

**暴力法：O(N^6)**

与其他许多问题一样，暴力法简单的遍历所有可能的行和列，然后计算每个子矩阵的和。

**优化解决方案：O(N^4)**

注意早期的解决方案较慢，因为它遍历了所有可能的子矩阵。事实上，通过以下方法可以将时间减少到 O(N^4)：

```java
public static int getMaxValue(int[][] matrix) {
    int maxArea = Integer.MIN_VALUE; // 最大可能是 0
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
private static int[][] precomputeMatrix(int[][] matrix) {
    int[][] sumMatrix = new int[matrix.length][matrix.length];
    for (int i = 0; i < matrix.length; i++) {
        for (int j = 0; j < matrix.length; j++) {
            if (i == 0 && j == 0) // 第一个单元格
                sumMatrix[i][j] = matrix[i][j];
            } else if (j == 0) // 在第一列中
                sumMatrix[i][j] = sumMatrix[i-1][j] + matrix[i][j];
            } else if (i == 0) // 在第一行中
                sumMatrix[i][j] = sumMatrix[i][j-1] + matrix[i][j];
            } else {
                sumMatrix[i][j] = sumMatrix[i-1][j] + sumMatrix[i][j-1] - sumMatrix[i-1][j-1] + matrix[i][j];
            }
        }
    }
    return sumMatrix;
}
```

有了这些值，我们知道从 (row1, col1) 到 (row2, col2) 的任何子矩阵的和可以高效计算：

sum = sumMatrix[row2][col2] - sumMatrix[row1-1][col2] - sumMatrix[row2][col1-1] + sumMatrix[row1-1][col1-1].

等待，另一种将时间减少到 O(N^2) 的方法是使用以下公式：

Val(x, y) = Val(x - 1, y) + Val(y - 1, x) - Val(x - 1, y - 1)

如果我们高效地计算矩阵中所有点的这个值，就可以找到最大的子矩阵。


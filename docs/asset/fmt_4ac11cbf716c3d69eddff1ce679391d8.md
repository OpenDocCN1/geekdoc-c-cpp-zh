
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

### 20.12 给出一个包含正负整数的 `NxN` 矩阵，编写代码找到和最大的子矩阵。

#### 解决方案

**暴力法：`O(N^6)`**

与其他许多问题一样，暴力法简单的遍历所有可能的行和列，然后计算每个子矩阵的和。

**优化解决方案：`O(N^4)`**

注意早期的解决方案较慢，因为它遍历了所有可能的子矩阵。事实上，通过以下方法可以将时间减少到 `O(N^4)`：

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

有了这些值，我们知道从 `(row1, col1)` 到 `(row2, col2)` 的任何子矩阵的和可以高效计算：

`sum = sumMatrix[row2][col2] - sumMatrix[row1-1][col2] - sumMatrix[row2][col1-1] + sumMatrix[row1-1][col1-1]`.

等待，另一种将时间减少到 `O(N^2)` 的方法是使用以下公式：

`Val(x, y) = Val(x - 1, y) + Val(y - 1, x) - Val(x - 1, y - 1)`

如果我们高效地计算矩阵中所有点的这个值，就可以找到最大的子矩阵。

# 第 20 章解答 | 困难级

```java
  32  matrix[i][j];
  33  }
  34  }
  35      return sumMatrix;
36
37  }
  private static int computeSum(int[][] sumMatrix, int i1, int i2,
      int j1, int j2) {
      if (i1 == 0 && j1 == 0) { // 从行 0，列 0 开始
          return sumMatrix[i2][j2];
      } else if (i1 == 0) { // 从行 0 开始
          return sumMatrix[i2][j2] - sumMatrix[i2][j1] - 1;
      } else if (j1 == 0) { // 从列 0 开始
          return sumMatrix[i2][j2] - sumMatrix[i1][j2];
      } else {
          return sumMatrix[i2][j2] - sumMatrix[i2][j1 - 1]
              - sumMatrix[i1 - 1][j2] + sumMatrix[i1 - 1][j1 - 1];
      }
  }
```

# 第 20 章解答 | 困难级

### 20.13 给定一个包含数百万单词的字典，给出一个算法找到最大的字母矩形，使得每一行都是一个单词（从左到右读），每一列都是一个单词（从上到下读）。

#### 解答

许多涉及字典的问题可以通过预处理来解决。我们可以在哪里进行预处理呢？

嗯，如果我们创建一个单词矩形，我们知道每一行的长度必须相同，每一列的长度也必须相同。因此，让我们按大小对字典中的单词进行分组。我们将这种分组称为 `D`，其中 `D[i]` 提供单词列表。

接下来，观察到我们寻找的是最大的矩形。可能形成的最大矩形是什么？它是（最长单词的长度）乘以（最长单词的长度）。

```java
1 max_rectangle = longest_word * longest_word;
2 for z = max_rectangle to 1 {
3   for each pair of numbers (i, j) where i*j = z {
4     /* 尝试构建矩形。如果成功则返回。 */
5   }
6 }
```

通过按照这种顺序迭代，我们确保找到的第一个矩形就是最大的。现在，是困难的部分：`make_rectangle`。我们的方法是将 `list1` 中的单词重新排列成行，并检查这些列是否是 `list2` 中的有效单词。然而，我们不是创建一个特定的 `10x20` 矩形，而是检查插入前两个单词后生成的列是否是有效的前缀。在这里字典树（`trie`）变得非常有用。

```java
1 WordGroup[1] grouplist = wordgroup.createGroups(list);
2 private int maxLength = grouplist.length;
3 private Trie trie[] = new Trie[maxLength];
4
5 public Rectangle makeRectangle() {
6 int maxSize = maxLength * maxLength;
7 for (int z = maxSize; z >= 0; z--) {
8   for (int i = 1; i < maxSize; i++) {
9     if (z % i == 0) {
10        int j = z / i;
11        if (j <= maxLength) {
12          Rectangle rectangle = makeRectangle(i, j);
13          if (rectangle != null) {
14            return rectangle;
15          }
16        }
17      }
18    }
19  }
20     return null;
21 }
22
23 private Rectangle makeRectangle(int length, int height) {
24     if (groupList[length - 1] == null ||
25         groupList[height - 1] == null) {
26         return null;
27     }
28
29     if (trielist[height - 1] == null) {
30         LinkedList<String> words = groupList[height - 1].get();
31         trielist[height - 1] = new Trie(words);
32     }
33     return makePartialRectangle(length, height,
34         new Rectangle(length));
35 }
36 private Rectangle makePartialRectangle(int l, int h,
37     Rectangle rectangle) {
38     if (rectangle.height == h) { // 检查是否为完整矩形
39         if (rectangle.isComplete(l, h, groupList[h - 1])) {
40             return rectangle;
41         } else {
42             return null;
43         }
44     }
45
46     // 比较列以尝试查看可能是有效的矩形 */
47     if (!rectangle.isPartialOK(l, trielist[h - 1])) return null;
48
49     for (int i = 0; i < groupList[l-1].length(); i++) {
50         Rectangle org_plus = 
51             rectangle.append(groupList[l-1].get(i));
52         Rectangle rect = makePartialRectangle(l, h, org_plus);
53         if (rect != null) {
54             return rect;
55         }
56     }
57     return null;
58 }
```

注意：完整代码请参阅附件。

| 主题 | 页码 |
| :--- | :--- |
| A | 308 |
| B | 308 |
| C | 308 |
| D | 308 |
| G | 308 |
| H | 308 |
| J | 308 |
| L | 308 |
| M | 308 |
| O | 308 |
| P | 308 |
| Q | 308 |
| R | 308 |
| S | 308 |
| T | 308 |
| 术 | 308 |
| 数组 | 308 |
| big-O | 308 |
| 位运算 | 308 |
| 位向量 | 308 |
| 广度搜索 | 308 |
| 组合数学 | 308 |
| 数据库 | 308 |
| 图 | 308 |
| 哈希表 | 308 |
| 堆 | 308 |
| Java | 308 |
| 行 | 308 |
| 链表 | 308 |
| 矩阵 | 308 |
| 最大化与最小化 | 308 |
| 面向对象设计 | 308 |
| 概率与随机性 | 308 |
| 队列 | 308 |
| 递归 | 308 |
| 搜索 | 308 |
| 排序 | 308 |
| 栈 | 308 |
| 字符串 | 308 |
| 测试 | 308 |
| 多线程 | 308 |
| 树 | 308 |

美国制造
肯塔基州，列星敦
2010年9月21日

`Gayle Laakmann` 于2005年创立了 `CareerCup.com`，旨在为软件工程师提供技术面试辅导。作为微软、苹果和谷歌的软件工程师，她曾在三个国家面试过一百二十多名申请者。
她拥有宾夕法尼亚大学的计算机科学学士学位和硕士学位。

目前已出版第4版的《破解编码面试》（`Cracking the Coding Interview`）为你提供了获得顶尖软件开发人员职位所需的面试准备。这本书提供了：

- 150道编程面试题及答案
从二叉树到二分查找，该列表包含了数据结构、算法和知识库问题中最常见、最实用的问题。

- 五种解决难题算法题的验证方法
使用这五种解决算法题的方法，你可以攻克困难的面试题，并给面试官留下深刻印象。

- 应聘人犯的十个错误以及如何避免
不要因为这些常见错误而错失你的理想工作。学习许多候选人做错的地方，以及如何避免这些问题。

- 准备行为面试和技术面试的策略
不要再在无尽的问题集中挣扎，却遗漏了最重要的准备技巧。遵循这些步骤，用更少的时间进行更好的准备。

- 面试实录：面试官视角
来自面试官的幽默且启发性的故事向你展示了某些候选人在最重要的问题上是如何失败的，以及你可以如何避免这些情况。

![](img/50974dc108b2978cf2cacf9397df9934_315_0.png)

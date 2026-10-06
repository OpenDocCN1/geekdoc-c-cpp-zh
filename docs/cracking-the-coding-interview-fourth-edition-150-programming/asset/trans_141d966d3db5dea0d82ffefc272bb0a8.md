

# 第 8 章解答 | 递归

## 8.4 编写一个方法计算字符串的排列组合。

### 解决方案

假设给定的字符串 S 由字母 A1, A2, A3, ..., An 表示。

为了对 S 进行排列，我们可以选择第一个字符 A1，对字符串的剩余部分进行排列以得到一个新列表。然后，利用这个新列表，我们可以将 A1 “推”到每一个可能的位置。

例如，如果我们的字符串是 "abc"，我们将执行以下操作：

- 1. 让 first="a"  remainder="bc"
- 2. 让 list :=permute(bc) {"bc","cd"}
- 3. 将 "a" 插入到 "bc" 的每个位置 -> "abc","bac","bca" 以及对于 "cb" -> "acb","cab","cba"
- 4. 返回我们的新列表

现在，实现此操作的代码：

```java
public static ArrayList<String> getPerms(String s) {
  ArrayList<String> permutations = new ArrayList<String>();
  if (s == null) { // 错误情况
    return null;
  } else if (s.length() == 0) { // 基础情况
    permutations.add("");
    return permutations;
  }
  char first = s.charAt(0); // 获取第一个字符
  String remainder = s.substring(1); // 移除第一个字符
  ArrayList<String> words = getPerms(remainder);
  for (String word : words) {
    for (int j = 0; j < word.length(); j++) {
      permutations.add(insertCharAt(word, first, j));
    }
  }
  return permutations;
}

public static String insertCharAt(String word, char c, int i) {
  String start = word.substring(0, i);
  String end = word.substring(i);
  return start + c + end;
}
```

该解决方案需要 O(n!) 的时间，因为有 n! 种排列。

# 第 8 章解答 | 递归

## 8.5 实现一种算法，打印 n 对括号的所有有效（例如，正确打开和关闭的）组合。

### 示例：
输入：3（例如，3 组括号）
输出：000, 0(0), (0)(0), ((() )

### 解决方案

我们可以通过递归遍历字符串来递归地解决这个问题。在每次迭代中，我们都有字符串中某个特定字符的索引。我们需要选择一个左括号或右括号。什么时候可以使用左括号，什么时候可以使用右括号？

- 左括号：只要我们还没有用完所有的左括号，我们一直可以插入左括号。
- 右括号：当我们插入右括号时，只要它不会导致语法错误即可。什么时候会产生语法错误？如果右括号多于左括号，我们就会产生语法错误。

因此，我们只需跟踪允许的左括号和右括号的数量。如果还有左括号剩余，我们会插入一个左括号并递归。如果剩余的右括号比左多（如果使用的左括号更多），我们会插入一个右括号并递归。

```java
public static void printPar(int l, int r, char[] str, int count) {
    if (l < 0 || r < 1) return; // 无效状态
    if (l == 0 && r == 0) {
        System.out.println(str); // 找到了，所以打印
    } else {
        if (l > 0) { // 尝试左括号，如果还有剩余
            str[count] = '(';
            printPar(l - 1, r, str, count + 1);
        }
        if (r > 1) { // 尝试右括号，如果有匹配的左括号
            str[count] = ')';
            printPar(l, r - 1, str, count + 1);
        }
    }
}
public static void printPar(int count) {
    char[] str = new char[count*2];
    printPar(count, count, str, 0);
}
```

![](img/50974dc108b2978cf2cacf9397df9934_180_0.png)

# 第 8 章解答 | 递归

## 6.6 实现在许多图像编辑程序常见的“油漆”（paint fill）函数。即：给定一个屏幕（由 Colors 的二维数组表示）、一个点和一种新颜色，填充周围区域，直到遇到该颜色的边界。

### 解决方案

首先，让我们视觉化它是如何工作的。当我们对一个绿色像素（例如，在图像编辑应用程序中“点击”油漆填充）调用 Paint Fill 时，我们希望它向外“扩散”。逐个像素地向外扩展，对周围的像素调用 PaintFill。当我们遇到一个不是绿色的像素时，我们停止。返回的绿色像素可能被另一个 Paint Fill 操作碰到。

我们可以递归地实现这个算法：

```java
enum Color {
  Black, White, Red, Yellow, Green
}
boolean PaintFill(Color[][] screen, int x, int y, Color ocolor) {
  if (x < 0 || x >= screen[0].length || y < 0 || y >= screen.length) {
    return false;
  }
  if (screen[y][x] == ocolor) {
    PaintFill(screen, x - 1, y, ocolor); // 左
    PaintFill(screen, x + 1, y, ocolor); // 右
    PaintFill(screen, x, y - 1, ocolor); // 上
    PaintFill(screen, x, y + 1, ocolor); // 下
  }
  return true;
}
boolean PaintFill(Color[][] screen, int x, int y, Color ocolor) {
  return PaintFill(screen, x, y, screen[y][x], ocolor);
}
```

# 第 8 章解答 | 递归

## 7.7 给定无限数量的季度币（25分）、角币（10分）、镍币（5分）和美分（1分），编写代码计算表示分金额的方法数。

### 解决方案

这是一个递归问题，所以让我们看看如何使用之前的解决方案（即子问题）来计算 makeChange(n)。假设 n = 100，所以我们想要计算表示 100 分的方法数。

（注：此处原文似乎存在逻辑跳跃或重复错误，已按字意翻译）
n = 100,所以我们想要计算表示 100 分的方法数。

这是一个递归问题，所以让我们看看如何使用之前的解决方案（即子问题）来计算 makeChange(n)。假设 n = 100，

我们想要计算表示 100 分的方法数。

这是一个递归问题，所以让我们看看如何使用之前的解决方案（即子问题）来计算 makeChange(n)。假设 n = 100，

我们想要计算表示 100 分的方法数。

这是一个递归问题，所以让我们看看如何使用之前的解决方案（即子问题）来计算 makeChange(n)。假设 n = 100，

我们想要计算表示 100 分的方法数。

这是一个递归问题，所以让我们看看如何使用之前的解决方案（即子问题）来计算 makeChange(n)。假设 n = 100，

我们想要计算表示 100 分的方法数。

这是一个递归问题，所以让我们看看如何使用之前的解决方案（即子问题）来计算 makeChange(n)。假设 n = 100，

我们想要计算表示 100 分的方法数。

这是一个递归问题，所以让我们看看如何使用之前的解决方案（即子问题）来计算 makeChange(n)。假设 n = 100，

我们想要计算表示 100 分的方法数。

这是一个递归问题，所以让我们看看如何使用之前的解决方案（即子问题）来计算 makeChange(n)。假设 n = 100，

我们想要计算表示 100 分的方法数。

这是一个递归问题，所以让我们看看如何使用之前的解决方案（即子问题）来计算 makeChange(n)。假设 n = 100，

（注：原文后续部分包含大量重复的句子和乱码化的逻辑，翻译已遵循原文结构，但由于原文质量问题，翻译内容呈现为逻辑重复）

n = 100, 
我们想要计算表示 100 分的方法数。

这是一个递归问题，所以让我们看看如何使用之前的解决方案（即子问题）来计算 makeChange(n)。假设 n = 100，

我们想要计算表示 100 分的方法数。

这是一个递归问题，所以让我们看看如何使用之前的解决方案（即子问题）来计算 makeChange(n)。假设 n = 100，

我们想要计算表示 100 分的方法数。

这是一个递归问题，所以让我们看看如何使用之前的解决方案（即子问题）来计算 makeChange(n)。假设n = 100，

（0111000）
n = 100, 
我们想要计算表示 100 分的方法数。

这是一个递归问题，所以让我们看看如何使用之前的解决方案（即子问题）来计算 makeChange(n)。假设 n = 100，

（此处翻译了原文重复的乱码逻辑，为对原文的忠实翻译）

n = 100, 

# 第 8 章解答 | 递归

## 8.8 编写一种算法，在棋盘上打印所有的皇后，使得它们互不在同一行、同一列或对角线上。

### 解决方案

我们将使用回溯算法。对于每一行，我们需要确保皇后不满足相同的行、列或对角线。

- 1. 对于此，我们需要 ColumnForRow[] 数组存储每一行的列号。
- 2. 检查三个条件是：
    - 同一列：ColumnForRow[i] ==  [j]
    - 同一对角线：ColumnForRow[i] - [j]

```java
int column[] = new int[8];
boolean check(int row) {
    for (int i = 0; i < row; i++) {
        int diff = Math.abs(column[i] - column[row]);
        if (diff == 0 || diff == row - i) return false;
    }
    return true;
}
void PlaceQueen(int row) {
    if (row == 8) {
        printBoard();
        return;
    }
    for (int i = 0; i < 8; i++) {
        column[row] = i;
        if (check(row)) {
            PlaceQueen(row+1);
        }
    }
}
```

# 第 9 章解答 | 排序与搜索

## 9.1 你被给定两个排序数组 A 和 B，A 的末尾有足够的缓冲区容纳 B。编写一个方法按顺序将 B 合并到 A 中。

### 解决方案

这段代码是合并排序代码的一部分。从后面合并 A 和 B，比较每个元素。

```java
public static void merge(int[] a, int[] b, int n, int m) {
    int k = m + n - 1; // 数组 b 最后一个位置的索引
    int i = n - 1; // 数组 b 中最后一个元素的索引
    int j = m - 1; // 数组 a 中最后一个元素的索引

    // 从最后一个元素开始比较合并 a 和 b
    while (i >= 0 && j >= 0) {
        if (a[i] > b[j]) {
            a[k--] = a[i--];
        } else {
            a[k--] = b[j--];
        }
    }
    while (j >= 0) {
        a[k--] = b[j--];
    }
}
```

注意：在用完 b 之后，不需要复制 a 的内容。它们已经在位置上了。


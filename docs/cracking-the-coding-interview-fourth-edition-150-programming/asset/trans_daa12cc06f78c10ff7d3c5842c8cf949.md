

# 第一章解决方案 | 数组与字符串

##5. 含有非连续重复的字符串，例如：abababa
算法——使用常量大小的额外内存

```java
public static void removeDuplicatesEff(char[] str) {
    if (str == null) return;
    int len = str.length;
    if (len < 2) return;
    boolean[] hit = new boolean[256];
    for (int i = 0; i < 256; ++i) {
        hit[i] = false;
    }
    hit[str[0]] = true;
    int tail = 1;
    for (int i = 1; i < len; ++i) {
        if (!hit[str[i]]) {
            str[tail] = str[i];
            ++tail;
            hit[str[i]] = true;
        }
    }
    str[tail] = 0;
}
```

## 测试用例：

- 1. 字符串不包含任何重复字符，例如：abcd
- 2. 字符串包含所有重复字符，例如：aaaa
- 3. 空字符串
- 4. 无引用字符串
- 5. 含有所有连续重复的字符串，例如：aaabbb
- 6. 含有非连续重复的字符串，例如：abababa

# 第一章解决方案 | 数组与字符串

## 1.4 写一个方法判断两个字符串是否为变位词（anagrams）。

### 解决方案

解决这个问题有两种简易的方法：

方案 #1：排序字符串

```java
boolean anagram(String s, String t) {
    return sort(s) == sort(t);
}
```

方案 #2：检查两个字符串中每个唯一字符的计数是否相同。

```java
public static boolean anagram(String s, String t) {
    if (s.length() != t.length()) return false;
    int[] letters = new int[256];
    int num_unique_chars = 0;
    int num_completed_t = 0;
    char[] s_array = s.toCharArray(); // 统计 s 中每个字符的数量。
    for (char c : s_array) {
        if (letters[c] == 0) ++num_unique_chars;
        ++letters[c];
    }
    for (int i = 0; i < t.length(); i++) {
        int c = (int) t.charAt(i);
        if (letters[c] == 0) { // t 中字符 c 的数量比 s 多。
            return false;
        }
        --letters[c];
        if (letters[c] == 0) {
            ++num_completed_t;
            if (num_completed_t == num_unique_chars) {
                // 如果 t 被完全处理，则匹配
                return i == t.length() - 1;
            }
        }
    }
    return false;
}
```

# 第一章解决方案 | 数组与字符串

## 1.5 写一个方法将字符串中的所有空格替换为 '%20'。

### 解决方案

算法如下：

- 1. 在第一次扫描字符串时统计空格的数量。
- 2. 从后部再次解析字符串，并对每个字符：
   - 如果遇到空格，则存储 "%20"
   - 否则，将该字符原样存储到移动后的位置。

```java
public static void ReplaceFun(char[] str, int length) {
    int spaceCount = 0, newLength, i = 0;
    for (i = 0; i < length; i++) {
        if (str[i] == ' ') {
            spaceCount++;
        }
    }
    newLength = length + spaceCount * 2;
    str[newLength - 1] = '\0';
    for (i = length - 1; i >= 0; i--) {
        if (str[i] == ' ') {
            str[newLength - 1] = '0';
            str[newLength - 2] = '2';
            str[newLength - 3] = '%';
            newLength -= 3;
        } else {
            str[newLength - 1] = str[i];
        }
    }
}
```![](img/50974dc108b297cf2acf937df9934_106_0.png)

# 第一章解决方案 | 数组与字符串

## 1.6 给定一个 Nx 矩阵图像，每个像素是一个字节，写一个方法将图像顺时针旋转 90 度。可以原地完成吗？

### 解决方案

旋转可以分层进行，对每一层的边缘进行循环交换。我们旋转第一层（最外层边缘），首先对四个角进行交换，然后向内移动三步交换。

一旦外部元素旋转完毕，我们再旋转内部区域。

```java
public static void rotate(int[][] matrix, int n) {
    for (int layer = 0; layer < n / 2; ++layer) {
        int first = layer;
        int last = n - 1 - layer;
        for (int i = first; i < last; i++) {
            int offset = i - first;
            int top = matrix[first][i]; // 保存顶部
            // 左 -> 上
            matrix[first][i] = matrix[last - offset][first];
            // 右 -> 左
            matrix[last - offset][first] = matrix[last][last];
            // ... (继续旋转逻辑)
        }
    }
}
```

# 第一章解决方案 | 数组与字符串

## 1.7 写一个算法，如果 Nx 矩阵中的某个元素为 0，则将其所在的整行和整列都置为 0。

### 解决方案

乍看这个问题很容易：遍历矩阵，每当看到 0 时，将该行和列置为 0。但问题在于：后续迭代会识别这些 0，导致整个矩阵被置零。

一种方法是使用第二个矩阵来标记 0 的位置。这将需要 $O(M \times N)$ 的空间。

我们真的需要 $O(M \times N)$ 的空间吗？不需要。因为我们要置零行列，只需要知道哪个单元格是 0。

以下代码实现了这一点。我们使用两个数组跟踪含有 0 的行和列。

```java
public static void setZeros(int[][] matrix) {
  int[] row = new int[matrix.length];
  int[] column = new int[matrix[0].length];
  // 存储含有 0 的行和列索引
  for (int i = 0; i < matrix.length; i++) {
    for (int j = 0; j < matrix[0].length; j++) {
      if (matrix[i][j] == 0) {
        row[i] = 1;
        column[j] = 1;
      }
    }
  }
  // 如果行 i 或列 j 有 1，则将 matrix[i][j] 置为 0
  for (int i = 0; i < matrix.length; i++) {
    for (int j = 0; j < matrix[0].length; j++) {
      if (row[i] == 1 || column[j] == 1) {
        matrix[i][j] = 0;
      }
    }
  }
}
```

# 第一章解决方案 | 数组与字符串

## 1.8 假设你有一个方法 `isSubstring` 可以检查一个单词是否是另一个的子串。给定两个字符串 s1 和 s2，写代码仅调用一次 `isSubstring` 来检查 s2 是否是 s1 的旋转（例如，“waterbottle” 是“bottlewat”的旋转）。

### 解决方案

只需执行以下检查：

- 1. 检查 `length(s1) == length(s2)`。如果不是，返回 false。
- 2. 否则，将 s1 与自身拼接，并查看 s2 是否为结果的子串。
  输入：s1 = apple, s2 = pleap => apple 是 pleapple 的子串。
  输入：s1 = apple, s2 = pale => apple 不是 paleapple 的子串。

```java
public static boolean isRotation(String s1, String s2) {
    int len = s1.length();
    /* 检查 s1 和 s2 相等且不为空 */
    if (len == s2.length() && len > 0) {
        /* 在缓冲区内拼接 s1 和 s1 */
        String s1s1 = s1 + s1;
        return isSubstring(s1s1, s2);
    }
    return false;
}
```

# 第二章解决方案 | 链表

## 2.1 写一个代码删除无序链表中的重复项。

### 进阶
如果不允许使用缓冲区，你将如何解决这个问题？

### 解决方案

如果使用缓冲区，可以使用哈希表跟踪元素并删除任何重复项：

```java
public static void deleteDups(ListNode n) {
    Hashtable table = new Hashtable();
    ListNode previous = null;
    while (n != null) {
        if (table.containsKey(n.data)) previous.next = n.next;
        else {
            table.put(n.data, true);
            previous = n;
        }
        n = n.next;
    }
}
```

如果没有缓冲区，可以使用两个指针进行迭代：“current”进行正常迭代，而“runner”遍历所有之前的节点来检查重复项。Runner 每次只会看到一个节点的重复项，因为如果有多个重复项，它们已经被删除了。

```java
public static void deleteDups2(ListNode head) {
    if (head == null) return;
    ListNode previous = head;
    ListNode current = head.next;
    while (current != null) {
        ListNode runner = head;
        while (runner != current) { // 检查之前的重复项
            if (runner.data == current.data) {
                ListNode tmp = current.next; // 删除 current
                current.next = tmp;
                previous = tmp;
                current = tmp; // 更新 current 到下一个节点
                break; // 其他重复项已被删除
            }
            runner = runner.next;
        }
        if (runner == current) { // current 未更新 - 现在更新
            previous = current;
            current = current.next;
        }
    }
}
```


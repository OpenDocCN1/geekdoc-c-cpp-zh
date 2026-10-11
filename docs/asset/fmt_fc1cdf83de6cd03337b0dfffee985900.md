
```java
// 找到身高体重递增的最大序列
findMaxSeq(ArrayList<Htwt> items) {
    Collections.sort(items);
    int currentUnfit = 0;
    while (currentUnfit < items.size()) {
        ArrayList<Htwt> nextSeq = new ArrayList<Htwt>();
        int nextUnfit = nextSeq(currentUnfit, nextSeq);
        maxSeq = seqMaxLength(maxSeq, nextSeq);
        if (nextUnfit == currentUnfit) break;
        else currentUnfit = nextUnfit;
    }
}

// 返回两个序列中较长的
ArrayList<Htwt> seqMaxLength(ArrayList<Htwt> seq1, ArrayList<Htwt> seq2) {
    return seq1.size() > seq2.size() ? seq1 : seq2;
}

// 在体重减少的情况下找到下一个序列及第一个不符合元素的索引
int nextSeq(int startFrom, ArrayList<Htwt> seq) {
    int firstUnfitItem = startFrom;
    if (startFrom < items.size()) {
        for (int i = 0; i < items.size(); i++) {
            Htwt item = items.get(i);
            if (i == 0 || items.get(i-1).isBefore(item)) {
                seq.add(item);
            } else {
                firstUnfitItem = i;
            }
        }
    }
    return firstUnfitItem;
}
```

# 第10章解答 | 数学类

## 10.1 你有一个篮球筐，有人说你可以从两个游戏中选择其一进行游戏。

游戏 #1：你有一次投篮机会投进筐。

游戏 #2：你有三次投篮机会，你必须在3次中投进2次。

如果 `p` 是投进某一次球的概率，那么在 `p` 取什么值时，你应该选择其中一个游戏？

### 答案

赢得游戏1的概率：`p`

赢得游戏2的概率：

设 `$s(k,n)$` 为在 `$n$` 次投篮中恰好投进 `$k$` 次的概率。赢得游戏2的概率为 `$s(2,3)+s(3,3)$`。由于 `$s(k, n) = C(n, k) (1-p)^{n-k} p^k$`，获胜概率为 `3 * (1 - p) p^2 * p^3`。

简化后，它变为 `3 * p^2 - 2 * p^3`。

如果 `P(Game1) > P(Game2)`，则你应该玩游戏1：

`np > 3*p^2 - 2*p^3`。

`1 > 3*p - 2*p^2`

`2*p^2 - 3*p + 1 > 0`

`(2p - 1)(p - 1) > 0`

两个项必须同为正数或同为负数。但我们知道 `p < 1`，所以 `(p-1) < 0`。这意味着两个项都必须是负数。

`(2p - 1) < 0`

`2p < 1`

`p < .5`

所以，如果 `p < .5`，我们应该玩游戏1。

## 10.2 有三只蚂蚁在三角形不同的顶点上。如果它们开始沿着三角形的边行走，发生碰撞（任意两只之间或全部在一起）的概率是多少？同样求出 `n` 顶点边形上 `n` 只蚂蚁碰撞的概率。

第68页

### 答案

如果三只蚂蚁都按顺时针方向移动，或者三只蚂蚁都按逆顺时针方向移动，那么它们之间就不会发生碰撞。否则，一定会发生碰撞。

三只蚂蚁有多少种移动方式？每只蚂蚁可以向2个方向移动，所以有 `2^3` 种移动方式。只有两种方式可以避免碰撞，因此碰撞的概率是 `(2^3 - 2) / (2^3) = 6 / 8 = 3 / 4`。

将其推广到 `n` 顶点边形：蚂蚁移动以避免碰撞的方式仍然只有 2 种，但总共有 `2^n` 种移动方式。因此，通常情况下，碰撞概率为 `(2^n - 2) / 2^n = 1 / 2^{(n-1)}`。

## 10.3 给定笛卡尔平面上的两条直线，判断这两条线是否相交。

### 答案

这个问题中有许多未知数（直线的格式是什么？如果它们是同一条线呢？），但让我们假设：

- 如果两条线是同一条线（同一条线 = 斜率和y轴截距），它们被认为相交。
- 由我们来决定数据结构。

```java
public class Line {
    static double epsilon = 0.000001;
    public double slope;
    public double intercept;

    public Line(double s, double y) {
        slope = s;
        intercept = y;
    }

    public boolean intersect(Line line2) {
        return Math.abs(slope - line2.slope) > epsilon ||
               Math.abs(intercept - line2.intercept) < epsilon;
    }
}
```

### 观察与建议：

- 提问。这个问题有很多未知数——通过提问来澄清它们。许多面试官特意问模糊的问题，是为了看你是否会澄清你的假设。
- 如果可能，设计并使用数据结构。这表明你理解并关心面向对象的设计。
- 思考你设计了哪种数据结构来表示直线。有很多选择，也有很多权衡。选择一种并解释你的理由。
- 不要假设斜率和y轴截距是整数。
- 理解浮点表示的局限性。永远不要使用 `==` 来检查相等性。

## 10.4 编写一个方法来实现 `*`、`-`、`/` 操作。你应该只使用 `+` 运算符。

第68页

### 答案

在理解了每个操作（减法、乘法、除法）的作用后，这个问题可以通过逻辑来解决。

- 减法应该相对直接，因为我们都知道 `$a - b$` 等于 `$a + (-1)*b$`。
- 乘法：我们必须回到小学学过的知识：`21 * 3 = 21 + 21 + 21`。这很慢，但有效。
- 除法是最困难的，因为我们通常把 `21 / 3` 想象成“如果你把一块 21 英尺的木板分成 3 块，每块有多大？”如果我们反过来想，会简单一点：“把 21 英尺的木板分成 `$x$` 块，每块 3 英尺，共有多少块？”从这里，我们可以看到。

## 10.6 给定一个带有点的二维图，找到一条通过点数最多的直线。

### 解决方案

如果我们在每两个点之间都画一条线，我们就可以检查哪条线是最常见的。暴力法就是简单地遍历每个线段（由点对组成），并统计有多少个点落在在该段上。这需要 `O(N^3)` 的时间。

在讨论我们是否能有更好的方法之前，让我们弄清楚如何表示一条直线。直线可以用（至少）两种方式表示：(1) 作为点的对，或 (2) 作为斜率和 y 轴截距。

由于我们的直线是无限的，斜率和 y 截距的方法似乎更合适。斜率和 y 截距方法还有一个优势：同一条大直线上的所有线段将具有相同的斜率和 y 截距。

重新思考我们的解决方案。我们有一堆用斜率和 y 截距表示的线段，我们想要找到最常见的斜率和 y 截距。我们如何找到最常见的？

这与旧的“在数字列表中找到最常见的数字”问题没有区别。只需遍历这些线段并使用哈希表统计它们出现的次数。

```java
public static Line findBestLine(GraphPoint[] points) {
    Line bestLine = null;
    HashMap<Line, Integer> line_count = new HashMap<>();
    for (int i = 0; i < points.length; i++) {
        for (int j = i + 1; j < points.length; j++) {
            Line line = new Line(points[i], points[j]);
            if (!line_count.containsKey(line)) {
                line_count.put(line, line_count.get(line) + 1);
            }
            if (bestLine == null || line_count.get(line) > line_count.get(bestLine)) {
                bestLine = line;
            }
        }
    }
    return bestLine;
}

public class Line {
    private static double epsilon = .0001;
    public double slope;
    public double intercept;
    private boolean infinite_slope = false;

    public Line(GraphPoint p, GraphPoint q) {
        if (Math.abs(p.x - q.x) > epsilon) {
            slope = (p.y - q.y) / (p.x - q.x);
            intercept = p.y - slope * p.x;
        } else {
            infinite_slope = true;
            intercept = p.x;
        }
    }

    public boolean isEqual(double a, double b) {
        return (Math.abs(a - b) < epsilon);
    }

    @Override
    public int hashCode() {
        int sl = (int)(slope * 1000);
        int in = (int)(intercept * 1000);
    }

    @Override
    public boolean equals(Object o) {
        if (!(o instanceof Line)) return false;
        Line l1 = (Line) o;
        if (equals(l1.slope, slope) && isEqual(l1.intercept, intercept)) {
            return (infinite_slope == l1.infinite_slope);
        }
        return false;
    }
}
```

### 观察与建议

- 注意直线的斜率计算。直线可能是完全垂直的。我们可以用一个单独的标记 `infinite_slope` 来跟踪这一点。我们需要在 `equals` 方法中检查这一点。
- 记住在计算斜率时除法是不精确的。因此，与其检查两个斜率是否完全相等，我们需要检查它们的差是否大于 `epsilon`。

## 10.7 设计一个算法，找到质因子仅为 5 和 7 的第 k 个数。

### 解决方案

任何这样的数字看起来像 `(3^i) * (5^j) * (7^k)`。这里是前 13 个数：

| 数值 | 因子 | 公式 |
| :--- | :--- | :--- |
| 1 | - | 3^0*5^0*7^0 |
| 3 | 3 | 3^1*5^0*7^0 |
| 5 | 5 | 3^0*5^1*7^0 |
| 7 | 7 | 3^0*5^0*7^1 |
| 9 | 3*3 | 3^2*5^0*7^0 |
| 15 | 3*5 | 3^1*5^1*7^0 |
| 21 | 3*7 | 3^1*5^0*7^1 |
| 25 | 5*5 | 3^0*5^2*7^0 |
| 27 | 3*9 | 3^3*5^0*7^0 |
| 35 | 5*7 | 3^0*5^1*7^1 |
| 45 | 5*9 | 3^2*5^1*7^0 |
| 49 | 7*7 | 3^0*5^0*7^2 |
| 63 | 3*21 | 3^2*5^0*7^1 |

我们如何找到列表中的下一个数？嗯，我们可以将列表中的每个数字乘以 3、5 和 7，并找到尚未添加到列表中的最小元素。该方案是 `O(n²)`。不坏，但我想我们可以做得更好。

在我们目前的算法中，我们正在执行 `3*1, 3*2, 3*3, 3*5, 3*7, 3*9, 3*15, 3*21, 3*25 ...`，5 和 7 也是如此。我们已经做过这些工作了——为什么要重做呢？

我们可以通过将添加到列表的每个数字乘以 3、5并将结果放入三个队列来修复这个问题。为了寻找“下一个数字”，我们从三个队列中选取最小元素。以下是算法：

1. 初始化 `magic` 和队列 `Q3`、`Q5` 和 `Q7`。
2. 将 1 放入 `magic`。
3. 将 `1*3, 1*5` 和 `1*7` 插入 `Q3, Q5` 和 `Q7`。
4. 将 `x` 为三个队列中的最小元素放入 `magic`。
5. 如果找到了 `x`：
   - `Q3 ->` 将 `x*3, x*5` 和 `x*7` 插入对应的队列。
   - `Q5 ->`
   - `Q7 ->`
6. 重复步骤 4-6，直到找到 `k` 个。

```java
public static int getthNumber(int k) {
    if (k <= 0) return 0;
    int val = 1;
    Queue<Integer> Q3 = new LinkedList<>();
    Queue<Integer> Q5 = new LinkedList<>();
    Queue<Integer> Q7 = new LinkedList<>();
    Q3.add(1 * 3);
    Q5.add(1 * 5);
    Q7.add(1 * 7);
    while (k-- > 0) {
        val = Math.min(Q3.peek(), Math.min(Q5.peek(), Q7.peek()));
        if (val == Q3.peek()) {
            Q3.poll();
            Q3.add(val * 3);
            Q5.add(val * 5);
            Q7.add(val * 7);
        } else if (val == Q5.peek()) {
            Q5.poll();
            Q3.add(val * 3);
            Q5.add(val * 5);
            Q7.add(val * 7);
        } else {
            Q7.poll();
            Q3.add(val * 3);
            Q5.add(val * 5);
            Q7.add(val * 7);
        }
    }
    return val;
}
```

### 观察与建议

- 当你遇到这个问题时，注意直线的斜率计算。直线可能是完全垂直的。我们可以用一个单独的标记 `infinite_slope` 来跟踪这一点。我们需要在 `equals` 方法中检查这一点。
- 记住在计算斜率时除法是不精确的。因此，与其检查两个斜率是否完全相等，我们需要检查它们的差是否大于 `epsilon`。

# 第 11 章解答 | 测试

## 11.1 找出以下代码中的错误：

```c
unsigned int i;
for (i = 100; i <= 0; --i)
printf("%d\n", i);
```

### 解决方案

`printf` 永远不会执行，因为 `"i"` 被初始化为 100，所以条件 `"i <= 0"` 会失败。

假设将代码改为 `"i >= 0"`。那么它将变成死循环，因为 `"i"` 是无符号整数，不能为负数。

打印从 100 到 1 的正确代码是 `"i > 0"`:

```c
unsigned int i;
for (i = 100; i > 0; --i)
printf("%d\n", i);
```

另一个修正是使用 `%u` 替换 `%d`，因为我们正在打印无符号整数。

```c
unsigned int i;
for (i = 100; i > 0; --i)
printf("%u\n", i);
```

## 11.2 你获得了一个程序的源代码，它在运行时会崩溃。在调试器中运行十次后，你发现它从未在同一个地方崩溃。该程序是单线程的，并且只使用标准库。哪些编程错误可能导致这种崩溃？如何测试每一种？

### 解决方案

问题很大取决于诊断类型。然而，我们可以给出随机崩溃的一些原因。

- 1. 随机变量：应用程序使用了某些随机数字或变量组件，这些组件在每次执行时可能都不固定。例如：用户输入、程序生成的随机数或时间。
- 2. 内存泄漏：程序可能耗尽了内存。其他祸因对于每次运行都是完全随机的，因为取决于特定时间运行的进程数量。这还包括堆溢出或栈上数据的损坏。

# 第 11 章解答 | 测试

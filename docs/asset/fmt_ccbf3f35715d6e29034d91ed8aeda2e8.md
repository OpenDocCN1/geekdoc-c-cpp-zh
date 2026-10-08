
```java
/**
 此程序打印奖牌计数和行总。
 */
public class Medals {
    public static void main(String[] args) {
        final int COUNTRIES = 7;
        final int MEDALS = 3;
        String[] countries = {
            "加拿大",
            "中国",
            "德国",
            "韩国",
            "日本",
            "俄罗斯",
            "美国"
        };
        int[][] counts = {
            {1, 0, 1},
            {1, 1, 0},
            {0, 0, 1},
            {1, 0, 0},
            {0, 1, 1},
            {1, 1, 0}
        };

        System.out.println("国家 金 银 铜 总计");
        // 打印计数、计数和行总
        for (int i = 0; i < COUNTRIES; i++) {
            // 输出 i 行
            System.out.printf("%s", countries[i]);
            int total = 0;
            // 输出每行元素并更新行总
            for (int j = 0; j < MEDALS; j++) {
                System.out.printf("%8d", counts[i][j]);
                total += counts[i][j];
            }
            // 显示行总并换行
            System.out.printf("%8d\n", total);
        }
    }
}
```

# 程序运行

|  | 金 | 银 | 铜 | 总计 |
|---|---|---|---|---|
| 加拿大 | 1 | 0 | 1 | 2 |
| 中国 | 1 | 1 | 0 | 2 |
| 德国 | 0 | 0 | 1 | 1 |
| 韩国 | 1 | 0 | 0 | 1 |
| 日本 | 0 | 1 | 1 | 2 |
| 俄罗斯 | 0 | 1 | 0 | 1 |
| 美国 | 1 | 1 | 0 | 2 |

# 288 第 6 章 数组与数组列表

现在练习：你可以尝试章节末的练习题：`R6.30`, `P6.18`, `P6.19`。

## 实例讲解 6.2 世界人口表

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_323_0.png)

这个实例讲解展示了如何带有行标题和列标题的表格打印世界人口数据，并为每个数据列计算总和。

## 特殊主题 6.4 变行长的二维数组

当你使用以下命令声明一个二维数组时：

```
int[][][] a = new int[3][3];
```

此时你将得到一个 3x3 的矩阵，包含 9 个元素：

```
a[0][0] a[0][1] a[0][2]
a[1][0] a[1][1] a[1][2]
a[2][0] a[2][1] a[2][2]
```

在这个矩阵中，所有行的长度都是相同的。

在 Java 中，可以声明行长度不相同的数组。例如，你可以存储一个三角形形状的数组，如：

```
b[0][0]
b[1][0] b[1][1]
b[2][0] b[2][1] b[2][2]
```

要分配这样一个数组，你需要费一番功夫。首先，你分配空间来存放三行。假设你将通过设置第二个数组索引来手动设置每一行：

```
double[][] b = new double[3][3];
```

然后单独分配每一行（见图 15）：

```
for (int i = 0; i < b.length; i++) {
  b[i] = new double[i+1];
}
```

你可以通过 `b[i][j]` 访问每个数组元素。表达式 `b[i]` 选择第 i 行，而 `[j]` 选择该行中的第 j 个元素。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_323_1.png)

**图 15** 三角形数组

* 可在 WileyPLUS 和 www.wiley.com/college/horstmann 在线。

## 6.8 数组列表 289

注意行数是 `b.length`，而第 i 行的长度是 `b[i].length`。例如，下面的这对循环可以打印一个锯齿数组（jagged array）：

```
for (int i = 0; i < b.length; i++) {
    for (int j = 0; j < b[i].length; j++) {
        System.out.print(b[i][j]);
    }
    System.out.println();
}
```

或者，你可以使用两个增强型循环：

```
for (double[] row : b) {
    for (double element : row) {
        System.out.print(element);
    }
    System.out.println();
}
```

自然地，“锯齿形”数组并不常见。Java 实现二维数组的方式与锯齿数组相同，即作为一维数组的数组。表达式 `new int[3][3]` 会自动分配一个包含三行的数组，每行包含三个元素的内容。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_324_0.png)

## 多维数组

你可以声明超过两个维度的数组。例如，这是一个三维数组：

```
int[][][] rubCube = new int[3][3][3];
```

每个数组由三个索引值指定：

```
rubCube[i][j][k];
```

## 6.8 数组列表

数组列表存储大小可以变化的值的序列。当你编写一个收集输入的程序时，并不知道会有多少输入。在这种情况下，数组列表有两个优势：

- 列表可以根据需要增长和缩小。
- `ArrayList` 类提供了常见任务的方法，如插入和删除元素。

在接下来的章节中，将学习如何使用数组列表。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_324_1.png)

数组列表可以根据需要容纳许多元素。

## 290 第 6 章 数组与数组列表

### 语法

| 语法 | 描述 |
|---|---|
| 构造数组列表：`new ArrayList<typeName>()` |  |
| 访问元素：`arraylistReference.get(index)` | 变量类型 `arraylistReference` `set(index, value)` |
|  | 大小为 0 的数组列表 `ArrayList<String> friends = new ArrayList<>();` |

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_325_0.png)

### 6.8.1 声明与使用数组列表

以下语句声明了一个字符串列表：

`ArrayList<String> names = new ArrayList<>();`

`ArrayList` 类位于 `java.util` 包中。为了在程序中使用数组列表，你需要使用语句 `import java.util.ArrayList;`。类型 `ArrayList<String>` 表示一个字符串列表。尖括号 `<String>` 是类型参数。你可以将 `String` 替换为任何类。但你不能使用基本类型作为类型参数 - 没有 `ArrayList<int>` 或 `ArrayList<double>`。6.8.5 节展示了如何在数组列表中收集数字。一个常见的错误是忘记初始化：`names.add("Harry"); // Error`。这是正确的初始化：

`ArrayList<String> names = new ArrayList<>();`

注意初始化右侧 `ArrayList<String>` 后面的 `()`。它表示了 `ArrayList` 类的构造函数。我们将在第 8 章讨论构造函数。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_325_1.png)

| 添加之前 | 添加之后 |
|---|---|
| `names = ArrayList<String>` | `names = ArrayList<String>` |
| "Emily" | "Emily" |
| "Bob" | "Bob" |
| "Carolyn" | "Carolyn" |
| Size 0 | Size增加 |
|  | 在末尾添加新元素 |

**图 16 使用 add 添加元素**

## 6.8 数组列表 291

当首次构造 `ArrayList<String>` 时，它的大小为 0。你使用 `add` 方法向数组列表的末尾添加元素。

```
names.add("Emily"); // 现在names的大小为1，元素为"Emily"
names.add("Bob"); // 现在names的大小为2，元素为"Emily","Bob"
names.add("Cindy"); // 现在names的大小为3，元素为"Emily","Bob","Cindy"
```

每次调用 `add` 后的大小（见图 16）。`size` 方法产生数组列表当前的大小。获取元素使用 `get` 方法，而不是 `[]` 运算符。像数组一样，索引从 0 开始。例如，`names.get(2)` 获取索引为2的名称，即数组列表中的第三个元素。

对于数组，访问不存在的元素是错误的。一个非常常见的错误是使用以下：

```
int i = names.size();
name = names.get(i); // Error
```

最后一个有效索引是 `names.size() - 1`。给元素设置新值，使用 `set` 方法。

```
names.set(2, "Carolyn");
```

这会将数组列表的位置 2 设置为 "Carolyn"，覆盖掉那里的任何值。这与 `add` 方法不同，后者在数组列表的中间添加新元素。例如，调用 `add(1, "Ann")` 在位置 1 处添加新元素，并将所有索引大于 1 的元素移动一个位置。每次调用 `add` 方法后，数组列表的大小增加 1（见图 17）。使用 `get` 和 `set` 方法访问给定索引的数组列表元素。数组列表有在中间添加和删除元素的方法。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_326_0.png)

**图 17 在数组列表中间添加和删除元素**

| 添加之前 | 添加之后 |
|---|---|
| `names = ArrayList<String>` | `names = ArrayList<String>` |
| "Emily" | "Emily" |
| "Bob" | "Bob" |
| "Carolyn" | "Carolyn" |

| 添加之前 | 添加 (1, "Ann") 之后 |
|---|---|
| `names = ArrayList<String>` | `names = ArrayList<String>` |
| "Emily" | "Emily" |
| "Bob" | "Bob" |
| "Carolyn" | "Carolyn" |
|  | 在索引1处添加了新元素 |
|  | 从索引1移动到2 |
|  | 从索引2移动到3 |
|  | 从索引3移动到4 |

## 292 第 6 章 数组与数组列表

使用 `add` 和 `remove` 方法添加和删除数组列表元素。相反，`remove` 方法删除指定位置的元素，被删除元素之后的元素向下移动一位，并使数组列表的大小减1。图17部分说明了 `names.remove(1)` 的结果。

对于数组列表，快速打印非常简单。只需将数组列表传递给方法：

```
System.out.println(names); // 输出 [Emily, Bob]
```

### 6.8.2 使用增强循环列表

你可以使用增强循环访问数组列表的所有元素。例如，下面的循环打印所有名称：

```
ArrayList<String> names = new ArrayList<>();
for (String name : names) {
    System.out.println(name);
}
```

此循环等同于下面的基础循环：

```
for (int i = 0; i < names.size(); i++) {
    String name = names.get(i);
    System.out.println(name);
}
```

### 表 2 操作数组列表

| 代码 | 描述 |
|---|---|
| `ArrayList<String> names = new ArrayList<>();` | 构建一个可以存储字符串的数组列表。 |
| `names.add("Ann");` | 在末尾添加元素。 |
| `names.add("Cindy");` |  |
| `System.out.println(names);` | 打印 [Ann, Cindy]。 |
| `names.add(1, "Bob");` | 在索引1处插入。现在是 [Ann, Bob, Cindy]。 |
| `names.remove(0);` | 删除索引0处的元素。现在是 [Bob, Cindy]。 |
| `names.set(0, "Bill");` | 用不同的值替换元素。现在是 [Bill, Cindy]。 |
| `String name = names.get(i);` | 获取元素。 |
| `String last = names.get(names.size() - 1);` | 获取最后一个元素。 |
| `ArrayList<Integer> squares = new ArrayList<Integer>();` | 构建一个持有前十个数的数组列表。 |
| `for (int i = 0; i < 10; i++) { squares.add(i * i); }` |  |

## 6.8.3 复制数组列表

与数组一样，你需要记住数组列表变量持有的是引用。复制引用会得到两个指向同一个数组列表的引用（见图 18）。

```java
ArrayList<String> friends = names;
friends.add("Harry");
```

现在 `names` 和 `friends` 指向同一个数组列表，该列表已添加了字符串 "Harry"。

如果你想创建一个数组列表的拷贝，请构造该拷贝并将原始列表传递到构造函数中：

```java
ArrayList<String> newNames = new ArrayList<String>(names);
```

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_328_0.png)

## 6.8.4 数组列表与方法

与数组一样，数组列表可以作为方法的参数和返回值。这里有一个示例：一个接收字符串列表并返回反转后列表的方法。

```java
public static ArrayList<String> reverse(ArrayList<String> names) {
    // 分配空间存储方法结果
    ArrayList<String> result = new ArrayList<String>();

    // 反向遍历 names 中的元素，从最后一个元素开始
    for (int i = names.size() - 1; i >= 0; i--) {
        // 将每个元素添加到结果中
        result.add(names.get(i));
    }
    return result;
}
```

如果调用此方法时传入包含 Emily, Bob, Cindy 名称的数组列表，它将返回一个包含 Cindy, Bob, Emily 名称的新数组列表。

## 6.8.5 包装类与自动装箱（Auto-boxing）

在 Java 中，你不能直接将基本类型值——数字、字符或布尔值——放入数组列表中。例如，你不能创建一个 `ArrayList<double>`。相反，你必须使用下表所示的包装类之一。

> 要在数组列表中收集数字，你必须使用包装类。

| 基本类型 | 包装类 |
|---|---|
| byte | Byte |
| boolean | Boolean |
| char | Character |
| double | Double |
| float | Float |
| int | Integer |
| long | Long |
| short | Short |

例如，为了在数组列表中收集 double 值，你使用 `ArrayList<Double>`。注意，包装类的首字母大大写，且其中两个类与对应的基本类型有所不同：基本类型与包装类之间的转换是自动的。这个过程被称为自动装箱（auto-boxing，尽管使用自动包装 auto-wrapping 会更一致）。例如，如果你将一个 double 值赋值给一个 `Double` 变量，它会被自动“放入箱中”（见图 1）。相反，值会被“拆箱”为基本类型。因为装箱和拆箱是自动的，所以你不需要考虑它。只需记住使用基本类型并依赖于自动装箱即可。

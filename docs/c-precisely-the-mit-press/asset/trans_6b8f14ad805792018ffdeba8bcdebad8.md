

# 示例 36 创建维度数组

本示例展示了两种创建矩形数组的方法（r1, r2）以及第 9.2 节中三种创建锯齿数组的方法（t1, t2, t3）。无法通过一次操作创建锯齿数组（如 t4）。

```c
double[] r1 = { 0.0, 0.1 }, { 1.0, 1.1 }, { 2.0, 2.1 };
double[] r2 = new double[3,2];
for (int i=0; i<3; i++)
  for (int j=0; j<2; j++)
    r2[i,j] = i + 0.1 * j;
```

```c
double[][] row0 = { 0.0 }, row1 = { 1.0, 1.1 }, row2 = { 2.0, 2.1, 2.2 };
double[][] t1 = { row0, row1, row2 };
double[][] t2 = { new double[0], new double[1], new double[2.0, 2.1, 2.2] };
double[][] t3 = new double[3]; // 创建第一维数组
for (int i=0; i<3; i++)
  t3[i] = new double[i+1]; // 创建第二维数组
  for (int j=0; j<=i; j++)
    t3[i,j] = i + 0.1 * j;
double[][] t4 = new double[3][]; // 非法数组创建
```

# 示例 39 使用多维数组

使用类型为 `double[][][]` 的数组 `rate` 来存储 2000–2009 年间每天美元与欧元之间的汇率（每欧元的美元数）；这是一个由元素类型为一维数组的二维矩形数组。`array[y,m]` 存储 y+2000 年、m+1 月、d+1 日的汇率。使用 `double[][][]` 类型的数组是因为这 10 年中的每一年都有 12 个月份（矩形），但并非所有月份的天数都相同（锯齿形）。

```csharp
double[][][] rate = new double[10][12];
rate[0, 0] = new double[31]; // 2000 年 1 月有 31 天
rate[1, 0] = new double[29]; // 2000 年 2 月有 29 天
rate[2, 0] = new double[31]; // 2000 年 3 月有 31 天
rate[3, 0] = new double[30]; // 2000 年 4 月有 30 天
rate[4, 0] = new double[31]; // 2000 年 5 月有 31 天
...
```

```csharp
rate[0,1][27] = 0.3748; // 2000 年 2 月 28 日
rate[0,1][28] = 0.9722; // 2000 年 2 月 29 日
rate[0,2][0] = 0.9651; // 2000 年 3 月 1 日
```

```csharp
for (int y=0; y<rate.GetLength(); y++)
  for (int m=0; m<rate[y].GetLength(); m++)
    if (rate[y,m] != null)
      for (int d=0; d<rate[y,m].Length; d++)
        if (rate[y,m][d] > 0)
          Console.WriteLine("{0:D4}-{1:D2}-{2:D2}: {3:F4} SUS/euro",
            y+2000, m+1, d+1, rate[y,m][d]);
```

# 9.3 Array 类

所有数组类型都继承自 `Array`，且 `Array` 的成员如下所示。假设 `a` 为任意 类型的数组，`o` 为任意类型的对象，`i, ..., in` 为整数：

- `Length` 类型为 `int`，返回 `a` 的长度，如果 `a` 是一维数组或矩形数组；如果 `a` 是锯齿数组，则返回 `a` 第一维的元素个数。
- `Rank` 类型为 `int`，返回 `a` 的秩（参见 5 和 9.2）。
- `GetEnumerator()` 类型为 `IEnumerator`，通过 `IList<t>` 获取类型安全的迭代器（参见 27.2），用于遍历 `a`。
- `Length(i)` 类型为 `int`，返回第 `i` 维元素的个数（参见 27 和 39）。
- `SetValue(o,j,...,in)` 类型为 `void`，当 `a` 有秩 `n` 时执行 `a[i,...,in] = o` 赋值。
- `GetValue(i,...,in)` 返回与 `a[i,...,in]` 相同。具体地说，如果 `a[i,...,in]` 是引用类型，则返回相同的引用；否则返回值的装箱副本。
- `Equals(o)` 类型为 `bool`，如果 `a` 和 `o` 指向同一个数组对象则返回 `true`，否则返回 `false`。

`Array` 类提供了静态方法，列如下所示。这些方法可以使用普通的数组类型 `[t]`。如果给定的数组为 `null` 则抛出 `ArgumentNullException`，如果 `a` 不是一维的，则抛出 `RankException`。

- `static BinarySearch(Array a, Object k)` 在一维数组 `a` 中通过二分查找 `k`。返回一个索引 `i` 使得 `a[i].CompareTo(k) = 0`；否则返回 `i<0`，其负值为 k 的正确位置。数组必须通过 `Sort(a)` 排序，否则结果未定义；且元素必须实现 `Comparable`。
- `static BinarySearch(Array a, IComparer cmp)` 的工作原理类似，但使用 `cmp.Compare` 方法比较数组元素（参见 27.3）。数组必须通过 `Sort(cmp)` 排序，否则结果未定义。
- `static void Reverse(Array a, int i, int n)` 反转 `a[i..(i+n-1)]` 的元素。
- `static void Sort(Array a, IComparer cmp)` 使用快速排序对一维数组 `a` 进行排序，使用元素的 `CompareTo` 方法比较（参见 27）。数组必须通过 `Sort(cmp)` 排序，否则结果未定义。
- `static void Sort(Array a, IComparer cmp)` 使用快速排序对一维数组 `a` 进行排序，使用元素的 `CompareTo` 方法比较（参见 27）。数组必须通过 `Sort(cmp)` 排序，否则结果未定义。

# 示例 40 长度、索引和 foreach

本示例使用了矩形数组和锯齿数组。

# 示例 41 数组中的搜索

# 示例 42 交换两个数组

# 10. 类

# 10.1 类声明与类体




## Scala 153 中的数组与列表

List(7, 4, 3)
List(7, 4, 9)
List(7, 4, 1)
List(7, 6, 3)
List(7, 6, 9)
List(7, 6, 1)
List(7, 3, 9)
List(7, 3, 1)
List(4, 6, 3)
List(4, 6, 9)
List(4, 6, 1)
List(4, 3, 9)
List(4, 3, 1)
List(4, 9, 1)
List(6, 3, 9)
List(6, 3, 1)
List(6, 9, 1)
List(3, 9, 1)

- **grouped(size:Int)** – 遍历序列，将项目按指定的大小分组。

```scala
scala> lst1.grouped(2).foreach(println)
List(7, 4)
List(6, 3)
List(9, 1)
```

```scala
scala> lst1.grouped(3).foreach(println)
List(7, 4, 6)
List(3, 9, 1)
```

- **inits** – 提供一个从完整序列到空序列的迭代器，从末尾移除元素。正如其名，它与 **init** 方法有关，该方法返回一个不包含最后一个元素的序列。

```scala
scala> lst1.inits.foreach(println)
List(7, 4, 6, 3, 9, 1)
List(7, 4, 6, 3, 9)
List(7, 4, 6, 3)
List(7, 4, 6)
List(7, 4)
List(7)
List()
```

- **permutations** – 允许你遍历序列的所有排列。注意，这里的示例只对前三个元素进行排列，因为完整列表有 6! = 720 种排列。这同时也解释了为什么该方法返回一个 Iterator。如第 4 章所示，阶乘函数增长非常快，因此如果一次性创建所有排列，即使是对中等规模序列调用 **permutations**，消耗的内存也会超过任何计算机所拥有的内存。

```scala
scala> lst1.take(3).permutations.foreach(println)
```

## 154 使用 Scala 进行编程与问题解决

List(7, 4, 6)
List(7, 6, 4)
List(4, 7, 6)
List(4, 6, 7)
List(6, 7, 4)
List(6, 4, 7)

- **sliding(size:Int)** 提供一个迭代器，实现特定窗口在序列上滑动的效果。

```scala
scala= lst.sliding(2).foreach(println)
List(7, 4)
List(4, 6)
List(6, 3)
List(3, 9)
List(9, 1)
```

```scala
scala= lst.sliding(3).foreach(println)
List(7, 4, 6)
List(4, 6, 3)
List(6, 3, 9)
List(3, 9, 1)
```

- **tails** 提供一个迭代器，从完整序列开始，到空序列结束，每一步从左端移除一个元素。这基本上是 inits 的反向，并与 tail 方法密切相关。

```scala
scala= lst.tails.foreach(println)
List(7, 4, 6, 3, 9, 1)
List(4, 6, 3, 9, 1)
List(6, 3, 9, 1)
List(3, 9, 1)
List(9, 1)
List(1)
List()
```

如果你想对迭代器给出的值进行更复杂的操作，可以使用 `toList` 将其转换为 List 或 Array。然而，由于元素非常多（例如在 permutations 的情况所示），在转换之前你可能需要对其进行过滤或执行其他操作以缩小范围。例如，我们可以对 `lst` 的排列进行过滤，只保留那些具有最大值的排列。这过滤掉了大部分结果，因此它可以从 Iterator 转换为 List。

```scala
scala= lst.permutations.filter(_.take(3) > 20).toList
res100:List[List[Int]]=List(7, 6, 9, 4, 3, 1), List(7, 6, 9, 4, 1, 3), List(7, 6, 9, 3, 4, 1), List(7, 6, 9, 3, 1, 4), List(7, 6, 4, 9, 3, 1), List(7, 6, 4, 3, 9, 1), List(7, 6, 3, 9, 4, 1), List(7, 6, 3, 4, 9, 1), List(7, 6, 1, 9, 4, 3), List(7, 6, 1, 4, 9, 3), List(7, 6, 1, 3, 9, 4), List(6, 7, 9, 4, 3, 1), List(6, 7, 9, 3, 4, 1), List(6, 7, 9, 1, 4, 3), List(6, 7, 4, 9, 3, 1), List(6, 7, 4, 3, 9, 1), List(6, 7, 4, 1, 9, 3), List(6, 7, 3, 9, 4, 1), List(6, 7, 3, 4, 9, 1), List(6, 7, 3, 1, 9, 4), List(6, 6, 7, 9, 4, 3), List(6, 6, 7, 4, 3, 1), List(6, 6, 7, 3, 9, 4), List(6, 6, 7, 1, 9, 3), List(6, 6, 4, 9, 3, 1), List(6, 6, 4, 3, 9, 1), List(6, 6, 4, 1, 9, 3), List(6, 6, 3, 9, 4, 1), List(6, 6, 3, 4, 9, 1), List(6, 6, 3, 1, 9, 4), List(6, 6, 1, 9, 4, 3), List(6, 6, 1, 4, 9, 3), List(6, 6, 1, 3, 9, 4)
```

## Scala 中的数组

List(9, 7, 6, 3, 4, 1), List(9, 7, 6, 3, 4, 1), List(9, 7, 6, 1, 4, 3),
List(9, 7, 6, 1, 3, 4), List(9, 6, 7, 4, 3, 1), List(9, 6, 7, 4, 1, 3), ...

这些方法提供了一种对数据进行更有趣处理简单方法。例如，使用 `sliding`，你可以通过对填充了随机数的窗口取平均值来快速平滑噪声数据。注意输出永远不会低于 0.4 或高于 0.82，而原始随机数据的值更接近 0.0 和 1.0。

```scala
scala Array.fill(20)(math.random).sliding(5).map(_.sum/5).toArray
res101: Array[Double] = Array(0.406886956682401, 0.4201066221912837,
0.4600266221912837,
```


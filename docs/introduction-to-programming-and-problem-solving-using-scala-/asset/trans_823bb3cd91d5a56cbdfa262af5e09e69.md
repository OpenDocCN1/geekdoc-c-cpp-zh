

# 426 使用 Scala 进行编程与问题解决导论

```scala
def helper(sorted:List[Double], unsorted:List[Double]):List[Double] = unsorted
  match {
    case Nil => sorted
    case h:t => helper(insert(h, sorted), t)
  }
```

```scala
helper(Nil, lst)
```

有人可能会认为，在所展示的三个方法中，插入法对于不可变的函数式方法来说是最好的。`insert` 辅助函数非常简单。它假设输入的 List 是排序的，并返回一个在指定位置具有特定值的新 List。如果 `sorted` 为空，它将返回一个以该值作为唯一元素的 List。否则，它检查插入值是否小于 `sorted` 的头部元素。如果是，则将其 `cons` 到 `sorted`；如果不是，则将 `sorted` 的头部元素 `cons` 到将新元素插入尾部的结果的结果。与其他方法不同，它有一个我们称为 `helper` 的第二个辅助函数。它每次从 `unsorted` 列表中取一个值来构建一个有序列表。基本情况是当所有元素都移动到 `sorted` 列表中时，返回该列表。

正如你所看到的，在处理 List 时，这些排序比为 Array 编写时要长一些。第 15 章中展示的排序以函数式方式编写时，实际上比命令式方式更短。

# 13.5 性能与计时

本章介绍了许多排序和搜索算法。我们从阶的角度讨论了这些算法的性能。这告诉我们随着输入数量的变化，它们是如何扩展的，而这通常正是我们真正关心的点。你可能不知道或不在乎运行代码的硬件或数据集的细节，或者你知道这些细节会随时间而改变。某些时候，你需要确切知道某个算法在特定机器上的运行速度，并将其与同一机器上的其他算法进行比较。当你这样做时，就需要对测试进行计时。

获取程序计时信息有多种不同的方法。Linux 有一个命令可以告诉你程序运行时消耗了多少时间。对于某些算法，这是理想的。对于我们的目的，我们只想测量程序某部分运行多长时间。我们不想测量启动或初始化 Array 所花费的时间。在对 Array 进行排序时，你可以获得来自 PROFILER 那样的详细信息，但对于我们要做的事情来说这大材小用了。对于我们的目的，我们需要确定开始时间和停止时间，以及两者之间的差。我们可以通过调用 `System.nanoTime()` 来实现。这在 Java 库中，返回一个以纳秒测量当前时间的 Long 类型。

我们还想做的另一件事是让测试中的每次排序都处理相同的数字。为了实现这一点，我们需要对 Array 的副本进行排序并保持

> 你可以使用 Java -Xprof 选项调用 Java 分析器。要让 Scala 运行此选项，你需要将 `JAVA_OPTS` 环境变量设置为包含 `-Xprof`。

> ¹一个纳秒是 10⁻⁹ 秒。

# 排序与搜索

原始状态以便我们可以创建它的副本。我们需要对每种排序都这样做；因此，将代码放入一个可以根据不同排序轻松调用的函数是很好的。为了适应不同的排序，我们需要将排序函数作为参数传递。以下函数为我们完成了此工作。

```scala
def timeFunc(sortFunc:(Array[Double])=>Unit, a:Array[Double]):Unit = {
    val copy = Array.tabulate(a.length)(i => a(i))
    val start = System.nanoTime()
    sortFunc(copy)
    val end = System.nanoTime()
    println("Time:" + (end-start)/1e9)
    assert(isSorted(copy))
}
```

`println` 语句将差除以 1e9。这让我们得到秒而不是纳秒的结果，这对我们更容易阅读和处理。我们通过在脚本最后放置代码来调用。

```scala
val nums = Array.fill(args(0).toInt)(math.random)
args(1) match {
    case "bubble" => timeFunc(bubbleSort, nums)
    case "flagged" => timeFunc(flaggedBubbleSort, nums)
    case "min" => timeFunc(minSort, nums)
    case "insert" => timeFunc(insertionSort, nums)
    case "shell" => timeFunc(shellSort, nums)
}
```

当你把这些放在那里时，请确保使用没有调用渲染核心的函数。

如果你尝试玩一下，你会发现几点。首先，Array 中的数字至少要达到 10000 个，计时才有意义。如果 Array 太小，排序速度会快到机器时钟的分辨率变成问题。其次，在不同的调用中花费的排序时间可能会有所。由于由于原因，任何测量性能的真实尝试都会多次运行代码，并取这些不同值的平均值。

# 基数排序（进阶）

本章之前讨论的排序只需要比较元素的能力。在某些情况下，你对值有更多信息，可以利用这些信息更高效地进行排序。此类非通用排序的例子包括桶排序（BUCKET SORT）和基数排序（RADIX SORT）。两者都利用对被排序数据的知识将它们分成组。

为了理解这项工作，考虑一下你处于一个装满待排序字母的大房间里……

堆就会是桶


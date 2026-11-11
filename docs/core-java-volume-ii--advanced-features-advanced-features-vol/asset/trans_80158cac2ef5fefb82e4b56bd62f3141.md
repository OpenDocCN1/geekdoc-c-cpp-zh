
当流操作并行运行时，其意图是返回与它们串行运行时相同的结果。重要的是，这些操作必须是*无状态*的，并且可以按任意顺序执行。

下面是一个不能这样做的示例。假设你想统计字符串流中所有短单词的数量：

```java
var shortWords = new int[12];
words.parallelStream().forEach(
    s -> { if (s.length() < 12) shortWords[s.length()]++; });
    // ERROR--race condition!
System.out.println(Arrays.toString(shortWords));
```

这是非常非常糟糕的代码。传递给 `forEach` 的函数会在多个线程中并发运行，每个线程都会更新一个共享数组。正如你在第 I 卷第 12 章中看到的，这是一个经典的*竞态条件*。如果你多次运行这个程序，很可能每次运行都会得到不同的计数序列——而每次都是错的。

你有责任确保传递给并行流操作的任何函数都可以安全地并行执行。做到这一点的最佳方法是避免可变状态。在这个示例中，如果你按长度对字符串分组并计数，就可以安全地并行化计算：

```java
Map<Integer, Long> shortWordCounts
    = words.parallelStream()
        .filter(s -> s.length() < 12)
        .collect(groupingBy(
            String::length,
            counting()));
```

默认情况下，由有序集合（数组和列表）、范围、生成器和迭代器产生的流，或通过调用 `Stream.sorted` 产生的流，都是*有序*的。结果会按原始元素的顺序累积，并且完全可预测。如果你运行相同的操作两次，将得到完全相同的结果。

有序性并不妨碍高效的并行化。例如，在计算 `stream.map(fun)` 时，流可以被划分为 *n* 个片段，每个片段都会被并发处理。然后，结果会按顺序重新组装。

当放弃顺序要求时，某些操作可以更有效地并行化。通过调用 `Stream.unordered` 方法，你表明自己不关心顺序。从中受益的一个操作是 `Stream.distinct`。在*有序*流上，*去重*会保留所有相等元素中的第一个。这会阻碍并行化——处理某个片段的线程在处理完前一个片段之前，无法知道要丢弃哪些元素。如果可以接受保留唯一元素中的*任意一个*，那么所有片段都可以并发处理（使用共享集合来跟踪重复项）。

你也可以通过放弃顺序来加速 `limit` 方法。如果你只想要流中的任意 n 个元素，而不关心得到哪些元素，可以调用

```java
Stream<String> sample = words.parallelStream().unordered().limit(n);
```

如第 30 页第 1.9 节“收集到映射”所述，合并映射的代价很高。因此，`Collectors.groupingByConcurrent` 方法使用共享的并发映射。为了从并行性中获益，映射值的顺序将与流顺序不同。

```java
Map<Integer, List<String>> result = words.parallelStream().collect(
    Collectors.groupingByConcurrent(String::length));
    // Values aren't collected in stream order
```

当然，如果你使用与顺序无关的下游收集器，就不会在意这一点，例如

```java
Map<Integer, Long> wordCounts
    = words.parallelStream()
        .collect(
            groupingByConcurrent(
                String::length,
                counting()));
```

不要为了加速操作而把所有流都变成并行流。请记住这些问题：

- 并行化有相当大的开销，只有在数据量非常大时才会有收益。
- 只有当底层数据源能够有效地拆分成多个部分时，并行化流才是有利的。
- 并行流使用的线程池可能会被文件 I/O 或网络访问等阻塞操作耗尽。

并行流最适合处理内存中的海量数据集合以及计算密集型处理。

> **提示：** 在 Java 9 之前，并行化 `Files.lines` 方法返回的流没有意义。数据不可拆分——你必须先读取文件的前半部分，然后才能读取后半部分。现在该方法使用内存映射文件，拆分是有效的。如果你处理巨大文件的行，并行化流可能会提高性能。

> **注意：** 默认情况下，并行流使用由 `ForkJoinPool.commonPool()` 返回的全局 fork-join 池。如果你的操作不会阻塞，并且你不与其他任务共享该池，那就没问题。有一个技巧可以替换为不同的池。把你的操作放在自定义池的 `submit` 方法中。

```java
ForkJoinPool customPool = ...;
result = customPool.submit(() ->
    stream.parallel().map(...).collect(...)).get();
```

或者，异步地：

```java
CompletableFuture.supplyAsync(() ->
    stream.parallel().map(...).collect(...),
    customPool).thenAccept(result -> ...);
```

> **注意：** 如果你想并行化基于随机数的流计算，不要从 `Random.ints`、`Random.longs` 或 `Random.doubles` 方法获得的流开始。这些流不会拆分。而应使用 `SplittableRandom` 类的 `ints`、`longs` 或 `doubles` 方法。

代码清单 1.8 中的示例程序演示了如何使用并行流。

### 代码清单 1.8 `parallel/ParallelStreams.java`

```java
package parallel;

/**
 * @version 1.01 2018-05-01
 * @author Cay Horstmann
 */

import static java.util.stream.Collectors.*;

import java.io.*;
import java.nio.charset.*;
import java.nio.file.*;
import java.util.*;
import java.util.stream.*;

public class ParallelStreams
{
    public static void main(String[] args) throws IOException
    {
        // Continues
20    var contents = new String(Files.readAllBytes(
21        Paths.get("../gutenberg/alice30.txt"), StandardCharsets.UTF_8));
22    List<String> wordList = List.of(contents.split("\\PL+"));
23
24    // Very bad code ahead
25    var shortWords = new int[10];
26    wordList.parallelStream().forEach(s ->
27    {
28        if (s.length() < 10) shortWords[s.length()]++;
29    });
30    System.out.println(Arrays.toString(shortWords));
31
32    // Try again--the result will likely be different (and also wrong)
33    Arrays.fill(shortWords, 0);
34    wordList.parallelStream().forEach(s ->
35    {
36        if (s.length() < 10) shortWords[s.length()]++;
37    });
38    System.out.println(Arrays.toString(shortWords));
39
40    // Remedy: Group and count
41    Map<Integer, Long> shortWordCounts = wordList.parallelStream()
42        .filter(s -> s.length() < 10)
43        .collect(groupingBy(String::length, counting()));
44
45    System.out.println(shortWordCounts);
46
47    // Downstream order not deterministic
48    Map<Integer, List<String>> result = wordList.parallelStream().collect(
49        Collectors.groupingByConcurrent(String::length));
50
51    System.out.println(result.get(14));
52
53    result = wordList.parallelStream().collect(
54        Collectors.groupingByConcurrent(String::length));
55
56    System.out.println(result.get(14));
57
58    Map<Integer, Long> wordCounts = wordList.parallelStream().collect(
59        groupingByConcurrent(String::length, counting()));
60
61    System.out.println(wordCounts);
62  }
```

| `java.util.stream.BaseStream<T, S extends BaseStream<T,S>>` 8 |
| --- |
| • `S parallel()`<br>生成一个与此流具有相同元素的并行流。<br>• `S unordered()`<br>生成一个与此流具有相同元素的无序流。 |

| `java.util.Collection<E>` 1.2 |
| --- |
| • `Stream<E> parallelStream()` 8<br>生成一个包含此集合中元素的并行流。 |

在本章中，你学习了如何使用 Java 8 的流库。下一章将讨论另一个重要主题：处理输入和输出。

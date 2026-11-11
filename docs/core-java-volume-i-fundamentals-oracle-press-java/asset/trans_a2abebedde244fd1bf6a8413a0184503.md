
在旧版 Java 中，需要使用 `replace` 方法，该方法会在没有其他线程抢先一步将旧值替换为其他值的情况下，原子性地将旧值替换为新值。你必须不断尝试，直到成功为止：

```java
do
{
    oldValue = map.get(word);
    newValue = oldValue == null ? 1 : oldValue + 1;
}
while (!map.replace(word, oldValue, newValue));
```

另一种方案是使用 `ConcurrentHashMap<String, AtomicLong>` 和如下的更新代码：

```java
map.putIfAbsent(word, new AtomicLong());
map.get(word).incrementAndGet();
```

遗憾的是，无论是否需要，每次递增时都会构造一个新的 `AtomicLong`。

如今，Java API 提供了一些方法，使原子更新更加便捷。`compute` 方法接收一个键和一个用于计算新值的函数。该函数接收键以及关联的值（如果没有值则为 null），并计算出新值。例如，下面是我们如何更新整数计数器映射的方式：

```java
map.compute(word, (k, v) -> v == null ? 1 : v + 1);
```

> **注意：**
>
> 在 `ConcurrentHashMap` 中不能有 null 值。许多方法将 null 值视为映射中不存在给定键的指示。

当你使用 **compute** 或 **merge** 时，请记住，你提供的函数不应执行大量工作。在该函数运行期间，对映射的其他更新可能会被阻塞。当然，该函数也不应更新映射的其他部分。

[清单 12.7](#) 中的程序使用并发哈希映射来统计目录树中 Java 文件里的所有单词。

### **清单 12.7** `concurrentHashMap/CHMDemo.java`

```java
package concurrentHashMap;

import java.io.*;
import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.*;

/**
 * This program demonstrates concurrent hash maps.
 * @version 1.0 2018-01-04
 * @author Cay Horstmann
 */
public class CHMDemo
{
   public static ConcurrentHashMap<String, Long> map = new ConcurrentHashMap<>();

   /**
    * Adds all words in the given file to the concurrent hash map.
    * @param file a file
    */
   public static void process(Path file)
   {
      try (var in = new Scanner(file))
      {
         while (in.hasNext())
         {
            String word = in.next();
            map.merge(word, 1L, Long::sum);
         }
      }
      catch (IOException e)
      {
         e.printStackTrace();
      }
   }

   /**
    * Returns all descendants of a given directory—see Chapters 1 and 2 of Volume II
    * @param rootDir the root directory
    * @return a set of all descendants of the root directory
    */
   public static Set<Path> descendants(Path rootDir) throws IOException
   {
      try (Stream<Path> entries = Files.walk(rootDir))
      {
         return entries.collect(Collectors.toSet());
      }
   }

   public static void main(String[] args)
       throws InterruptedException, ExecutionException, IOException
   {
      int processors = Runtime.getRuntime().availableProcessors();
      ExecutorService executor = Executors.newFixedThreadPool(processors);
      Path pathToRoot = Path.of(".");
      for (Path p : descendants(pathToRoot))
      {
         if (p.getFileName().toString().endsWith(".java"))
            executor.execute(() -> process(p));
      }
      executor.shutdown();
      executor.awaitTermination(10, TimeUnit.MINUTES);
      map.forEach((k, v) ->
      {
         if (v >= 10)
            System.out.println(k + " occurs " + v + " times");
      });
   }
}
```

### 12.5.4 并发哈希映射的批量操作

Java API 提供了针对并发哈希映射的批量操作，即使在有其他线程操作该映射时，这些操作也能安全执行。批量操作会遍历映射，并沿途对找到的元素进行操作。它并不会努力在某个时间点冻结映射的快照。除非你恰好知道在批量操作运行期间映射未被修改，否则应将结果视为映射状态的近似值。

共有三种操作：

- `search` 对每个键和/或值应用一个函数，直到该函数产生非 null 结果。然后搜索终止并返回该函数的结果。
- `reduce` 使用提供的累积函数组合所有键和/或值。
- `forEach` 对所有键和/或值应用一个函数。

每种操作有四个版本：

- *operation*`Keys`：对键进行操作。
- *operation*`Values`：对值进行操作。
- *operation*：对键和值进行操作。
- *operation*`Entries`：对 `Map.Entry` 对象进行操作。

对于每种操作，你都需要指定一个*并行阈值*。如果映射包含的元素数超过该阈值，批量操作将被并行化。如果你希望批量操作在单个线程中运行，请使用 `Long.MAX_VALUE` 作为阈值。如果你希望为批量操作提供最大数量的线程，请使用阈值 1。

我们先来看 search 方法，以下是这些版本：

```java
U searchKeys(long threshold, BiFunction<? super K, ? extends U> f)
U searchValues(long threshold, BiFunction<? super V, ? extends U> f)
U search(long threshold, BiFunction<? super K, ? super V, ? extends U> f)
U searchEntries(long threshold, BiFunction<Map.Entry<K, V>, ? extends U> f)
```

例如，假设我们要查找第一个出现次数超过 1,000 次的单词。我们需要搜索键和值：

```java
String result = map.search(threshold, (k, v) -> v > 1000 ? k : null);
```

于是 `result` 被设置为第一个匹配项，如果搜索函数对所有输入都返回 `null`，则结果为 `null`。

`forEach` 方法有两个变体。第一个变体简单地针对每个映射条目应用一个*消费者*函数，例如：

```java
map.forEach(threshold,
    (k, v) -> System.out.println(k + " -> " + v));
```

第二个变体接受一个额外的*转换器*函数，该函数首先被应用，其结果再传递给消费者：

```java
map.forEach(threshold,
    (k, v) -> k + " -> " + v, // transformer
    System.out::println); // consumer
```

转换器可以用作过滤器。每当转换器返回 null 时，该值会被静默跳过。例如，这里我们只打印值较大的条目：

```java
map.forEach(threshold,
    (k, v) -> v > 1000 ? k + " -> " + v : null, // filter and transformer
    System.out::println); // the nulls are not passed to the consumer
```

reduce 操作使用累积函数组合其输入。例如，下面是如何计算所有值的总和：

```java
Long sum = map.reduceValues(threshold, Long::sum);
```

与 `forEach` 一样，你也可以提供一个转换器函数。这里我们计算最长键的长度：

```java
Integer maxlength = map.reduceKeys(threshold,
    String::length, // transformer
    Integer::max); // accumulator
```

转换器可以通过返回 null 来排除不需要的输入，从而充当过滤器。这里我们统计值大于 1,000 的条目数量：

```java
Long count = map.reduceValues(threshold,
    v -> v > 1000 ? 1L : null,
    Long::sum);
```

![](img/0e7b74ef51a065c077b42cd87b362288_1133_0.png)

> **注意：**
>
> 如果映射为空，或者所有条目都被过滤掉，`reduce` 操作将返回 `null`。如果只有一个元素，则返回其转换结果，并且不会应用累积函数。

针对 `int`、`long` 和 `double` 输出还有带有 `ToInt`、`ToLong` 和 `ToDouble` 后缀的专用版本。你需要将输入转换为原始类型，并指定默认值和累积函数。当映射为空时，将返回默认值。

```java
long sum = map.reduceValuesToLong(threshold,
    Long::longValue, // transformer to primitive type
    0, // default value for empty map
    Long::sum); // primitive type accumulator
```

> **警告：**
>
> 这些专用版本与对象版本在处理只有一个元素时有所不同。不会返回转换后的元素，而是将其与默认值进行累积。因此，默认值必须是累积函数的单位元素。

### 12.5.5 并发集合视图

假设你需要一个大型的线程安全集合，而不是映射。Java 中没有 `ConcurrentHashSet` 类，你也不会天真地试图自己实现一个。当然，你可以使用带虚拟值的 `ConcurrentHashMap`，但那样得到的是映射而不是集合，而且你无法应用 set 接口的操作。

静态的 `newKeySet` 方法生成一个 `Set<K>`，它实际上是 `ConcurrentHashMap<K, Boolean>` 的包装器。（所有映射值都是 `Boolean.TRUE`，但你实际上并不关心，因为你只是将其用作集合。）

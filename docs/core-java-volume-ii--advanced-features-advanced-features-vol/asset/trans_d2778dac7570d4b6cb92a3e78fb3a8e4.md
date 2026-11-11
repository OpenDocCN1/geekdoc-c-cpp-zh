
**注意：** 在本节中，我们考虑一种理想场景：有一个返回 Optional 值的方法。如今，许多方法在没有有效结果时返回 null。假设 Users.classicLookup(id) 返回一个 User 对象或 null，而不是 Optional<User>。那么你当然可以过滤掉 null 值：

```java
Stream<User> users = ids.map(Users::classicLookup)
    .filter(Objects::nonNull);
```

但如果你更喜欢 flatMap 方式，可以使用

```java
Stream<User> users = ids.flatMap(
    id -> Stream.ofNullable(Users.classicLookup(id)));
```

或者

```java
Stream<User> users = ids.map(Users::classicLookup)
    .flatMap(Stream::ofNullable);
```

调用 Stream.ofNullable(obj) 时，如果 obj 为 null，则产生一个空流；否则产生一个仅包含 obj 的流。

清单 1.3 中的示例程序演示了 Optional API。

### 清单 1.3 optional/OptionalTest.java

```java
1 package optional;
2 
3 /**
4  * @version 1.01 2018-05-01
5  * @author Cay Horstmann
6  */
7 
8 import java.io.*;
9 import java.nio.charset.*;
10 import java.nio.file.*;
11 import java.util.*;
12 
13 public class OptionalTest
14 {
15    public static void main(String[] args) throws IOException
16    {
17       var contents = Files.readString(
18          Paths.get("../gutenberg/alice30.txt"));
19       List<String> wordList = List.of(contents.split("\\PL+"));
20 
21       Optional<String> optionalValue = wordList.stream()
22          .filter(s -> s.contains("fred"))
23          .findFirst();
24    System.out.println(optionalValue.orElse("No word") + " contains fred");
25
26    Optional<String> optionalString = Optional.empty();
27    String result = optionalString.orElse("N/A");
28    System.out.println("result: " + result);
29    result = optionalString.orElseGet(() -> Locale.getDefault().getDisplayName());
30    System.out.println("result: " + result);
31    try
32    {
33        result = optionalString.orElseThrow(IllegalStateException::new);
34        System.out.println("result: " + result);
35    }
36    catch (Throwable t)
37    {
38        t.printStackTrace();
39    }
40
41    optionalValue = wordList.stream()
42        .filter(s -> s.contains("red"))
43        .findFirst();
44    optionalValue.ifPresent(s -> System.out.println(s + " contains red"));
45
46    var results = new HashSet<String>();
47    optionalValue.ifPresent(results::add);
48    Optional<Boolean> added = optionalValue.map(results::add);
49    System.out.println(added);
50
51    System.out.println(inverse(4.0).flatMap(OptionalTest::squareRoot));
52    System.out.println(inverse(-1.0).flatMap(OptionalTest::squareRoot));
53    System.out.println(inverse(0.0).flatMap(OptionalTest::squareRoot));
54    Optional<Double> result2 = Optional.of(-4.0)
55        .flatMap(OptionalTest::inverse).flatMap(OptionalTest::squareRoot);
56    System.out.println(result2);
57    }
58
59    public static Optional<Double> inverse(Double x)
60    {
61        return x == 0 ? Optional.empty() : Optional.of(1 / x);
62    }
63
64    public static Optional<Double> squareRoot(Double x)
65    {
66        return x < 0 ? Optional.empty() : Optional.of(Math.sqrt(x));
67    }
68 }
```

### java.util.Optional 8

- `<U> Optional<U> flatMap(Function<? super T,Optional<U>> mapper)` 9
  产生将 `mapper` 应用于此 `Optional` 的值所得的结果；如果此 `Optional` 为空，则产生一个空 `Optional`。

## 1.8 收集结果

当处理完一个流后，你通常希望查看结果。你可以调用 iterator 方法，它会生成一个老式迭代器，你可以用它来访问元素。

或者，你可以调用 forEach 方法，对每个元素应用一个函数：

```java
    stream.forEach(System.out::println);
```

在并行流上，forEach 方法以任意顺序遍历元素。如果你想按流顺序处理它们，请改为调用 forEachOrdered。当然，你可能会因此放弃部分或全部并行带来的好处。但通常，你会希望将结果收集到一个数据结构中。调用 toArray 可获得流元素的数组。

由于无法在运行时创建泛型数组，表达式 stream.toArray() 返回一个 Object[] 数组。如果你想要正确类型的数组，请传入数组构造器：

```java
    String[] result = stream.toArray(String[]::new);
    // stream.toArray() has type Object[]
```

为了将流元素收集到另一个目标，有一个方便的 collect 方法，它接受一个 Collector 接口的实例。收集器是一个累积元素并产生结果的对象。Collectors 类为常见收集器提供了大量工厂方法。要将流元素收集到列表中，请使用 Collectors.toList() 生成的收集器：

```java
    List<String> result = stream.collect(Collectors.toList());
```

类似地，下面是如何将流元素收集到一个集合中：

```java
    Set<String> result = stream.collect(Collectors.toSet());
```

如果你想控制获得哪种集合，请改为使用以下调用：

```java
    TreeSet<String> result = stream.collect(Collectors.toCollection(TreeSet::new));
```

假设你想通过连接流中的所有字符串来收集它们。你可以调用

```java
String result = stream.collect(Collectors.joining());
```

如果你希望在元素之间使用分隔符，请将其传给 joining 方法：

```java
String result = stream.collect(Collectors.joining(", "));
```

如果你的流包含字符串以外的对象，你需要先将它们转换为字符串，如下所示：

```java
String result = stream.map(Object::toString).collect(Collectors.joining(", "));
```

如果你想将流结果归约为总和、计数、平均值、最大值或最小值，请使用 summarizing(Int|Long|Double) 方法之一。这些方法接受一个将流对象映射为数字的函数，并产生 (Int|Long|Double)SummaryStatistics 类型的结果，同时计算总和、计数、平均值、最大值和最小值。

```java
IntSummaryStatistics summary = stream.collect(
    Collectors.summarizingInt(String::length));
double averageWordLength = summary.getAverage();
double maxWordLength = summary.getMax();
```

清单 1.4 中的示例程序展示了如何从流中收集元素。

### 清单 1.4 collecting/CollectingResults.java

```java
1 package collecting;
2
3 /**
4  * @version 1.01 2018-05-01
5  * @author Cay Horstmann
6  */
7
8 import java.io.*;
9 import java.nio.charset.*;
10 import java.nio.file.*;
11 import java.util.*;
12 import java.util.stream.*;
13
14 public class CollectingResults
15 {
```

### java.util.stream.Collectors 8

- `static <T> Collector<T,?,List<T>> toList()`
- `static <T> Collector<T,?,List<T>> toUnmodifiableList()` 10
- `static <T> Collector<T,?,Set<T>> toSet()`
- `static <T> Collector<T,?,Set<T>> toUnmodifiableSet()` 10

产生将元素收集到列表或集合中的收集器。

- `static <T,C extends Collection<T>> Collector<T,?,C> toCollection(Supplier<C> collectionFactory)`
  产生一个将元素收集到任意集合中的收集器。传入一个构造器引用，例如 TreeSet::new。

- `static Collector<CharSequence,?,String> joining()`
- `static Collector<CharSequence,?,String> joining(CharSequence delimiter)`
- `static Collector<CharSequence,?,String> joining(CharSequence delimiter, CharSequence prefix, CharSequence suffix)`

产生一个连接字符串的收集器。分隔符放在字符串之间，前缀和后缀分别放在第一个字符串之前和最后一个字符串之后。未指定时，它们为空。

- `static <T> Collector<T,?,IntSummaryStatistics> summarizingInt(ToIntFunction<? super T> mapper)`
- `static <T> Collector<T,?,LongSummaryStatistics> summarizingLong(ToLongFunction<? super T> mapper)`
- `static <T> Collector<T,?,DoubleSummaryStatistics> summarizingDouble(ToDoubleFunction<? super T> mapper)`

产生 (Int|Long|Double)SummaryStatistics 对象的收集器，从中可以获得将 mapper 应用于每个元素所得结果的计数、总和、平均值、最大值和最小值。

### IntSummaryStatistics 8
### LongSummaryStatistics 8
### DoubleSummaryStatistics 8

- `long getCount()`
  产生已汇总元素的计数。
- `(int|long|double) getSum()`
- `double getAverage()`
  产生已汇总元素的总和或平均值；如果没有元素，则为零。

*（续）*


```java
67    try {
68        Iterator<Path> iterator = Paths.get("/usr/share/dict/words").iterator();
69        Stream<Path> pathComponents = StreamSupport.stream(Spliterators.spliteratorUnknownSize(
70                iterator, Spliterator.ORDERED), false);
71        show("pathComponents", pathComponents);
72    }
73 }
```

### java.util.stream.Stream 8

- `static <T> Stream<T> of(T... values)` —— 产生一个流，其元素为给定的值。
- `static <T> Stream<T> empty()` —— 产生一个不含任何元素的流。
- `static <T> Stream<T> generate(Supplier<T> s)` —— 产生一个无限流，其元素通过反复调用函数 s 构造。
- `static <T> Stream<T> iterate(T seed, UnaryOperator<T> f)`
- `static <T> Stream<T> iterate(T seed, Predicate<? super T> hasNext, UnaryOperator<T> f)` —— 产生一个流，其元素依次为 seed、对 seed 调用 f 的结果、对前一个元素调用 f 的结果，依此类推。第一个方法产生无限流。第二个方法产生的流会在第一个不满足 hasNext 谓词的元素之前结束。
- `static <T> Stream<T> ofNullable(T t) 9` —— 如果 t 为 null，则返回空流；否则返回包含 t 的流。

### java.util.Spliterators 8

- `static <T> Spliterator<T> spliteratorUnknownSize(Iterator<? extends T> iterator, int characteristics)` —— 将迭代器转换为具有给定特征（一个包含 Spliterator.ORDERED 等常量的位模式）的未知大小的可拆分迭代器。

### java.util.Arrays 1.2

- `static <T> Stream<T> stream(T[] array, int startInclusive, int endExclusive) 8` —— 产生一个流，其元素为数组中指定的范围。

## 1.3 filter、map 和 flatMap 方法

流转换会生成一个流，其元素派生自另一个流的元素。你已经见过 filter 转换，它会生成一个新流，其中包含满足某个条件的元素。这里，我们将一个字符串流转换为另一个只包含长单词的流：

```java
List<String> words = ...;
Stream<String> longWords = words.stream().filter(w -> w.length() > 12);
```

filter 的参数是一个 Predicate<T>——也就是一个从 T 到 boolean 的函数。

通常，你会希望以某种方式转换流中的值。使用 map 方法，并传入执行转换的函数。例如，你可以像这样将所有单词转换为小写：

```java
Stream<String> lowercaseWords = words.stream().map(String::toLowerCase);
```

这里，我们使用了方法引用。通常，你会改用 lambda 表达式：

```java
Stream<String> firstLetters = words.stream().map(s -> s.substring(0, 1));
```

结果流包含每个单词的首字母。

使用 map 时，函数会应用于每个元素，结果是一个包含这些结果的新流。现在，假设你有一个函数，它返回的不只是一个值，而是一个值流。下面是一个例子——一个将字符串转换为字符串流（即各个码点）的方法：

```java
public static Stream<String> codePoints(String s)
{
    var result = new ArrayList<String>();
    int i = 0;
    while (i < s.length())
    {
        int j = s.offsetByCodePoints(i, 1);
        result.add(s.substring(i, j));
        i = j;
    }
    return result.stream();
}
```

这个方法能正确处理需要两个 char 值的 Unicode 字符，因为这样做才是正确的。但你不必对此深究。

例如，codePoints("boat") 是流 ["b", "o", "a", "t"]。

现在，让我们在一个字符串流上映射 `codePoints` 方法：

```java
Stream<String> result = words.stream().map(w -> codePoints(w));
```

你会得到一个流的流，类似于 . . . , ["y", "o", "u", "r"], ["b", "o", "a", "t"], . . . 。要将其展平为单个流 . . . , ["y", "o", "u", "r", "b", "o", "a", "t"], . . . ，请使用 `flatMap` 方法而不是 `map`：

```java
Stream<String> flatResult = words.stream().flatMap(w -> codePoints(w));
// Calls codePoints on each word and flattens the results
```

> **注意：** 你会在流以外的类中找到 `flatMap` 方法。它是计算机科学中的一个通用概念。假设你有一个泛型类型 G（例如 `Stream`），以及从某个类型 T 到 `G<U>` 的函数 f 和从 U 到 `G<V>` 的函数 g。那么你可以将它们组合起来——也就是说，先应用 f 再应用 g，使用 `flatMap`。这是单子理论中的一个关键思想。但别担心——你可以在对单子一无所知的情况下使用 `flatMap`。

### java.util.stream.Stream 8

- `Stream<T> filter(Predicate<? super T> predicate)` —— 产生一个流，其中包含此流中满足该谓词的元素。
- `<R> Stream<R> map(Function<? super T, ? extends R> mapper)` —— 产生一个流，其中包含将 mapper 应用于此流元素后的结果。
- `<R> Stream<R> flatMap(Function<? super T, ? extends Stream<? extends R>> mapper)` —— 产生一个流，该流通过拼接将 mapper 应用于此流元素后的结果得到。（注意，每个结果都是一个流。）

## 1.4 提取子流与合并流

调用 `stream.limit(n)` 会返回一个新流，该流在 n 个元素后结束（如果原流更短，则在原流结束时结束）。这个方法对于将无限流截断到合适大小特别有用。例如，

```java
Stream<Double> randoms = Stream.generate(Math::random).limit(100);
```

会生成一个包含 100 个随机数的流。

调用 `stream.skip(n)` 则正好相反。它会丢弃前 n 个元素。在我们的读书示例中这很方便：由于 `split` 方法的工作方式，第一个元素是不需要的空字符串。我们可以通过调用 `skip` 让它消失：

## 1.5 其他流转换

distinct 方法返回一个流，它按相同顺序产出原流中的元素，但会抑制重复项。重复项不必相邻。

```java
Stream<String> uniqueWords
    = Stream.of("merrily", "merrily", "merrily", "gently").distinct();
    // Only one "merrily" is retained
```

对于流的排序，sorted 方法有几种变体。一种适用于 Comparable 元素的流，另一种接受 Comparator。这里，我们对字符串排序，使最长的字符串排在最前面：

```java
Stream<String> longestFirst
    = words.stream().sorted(Comparator.comparing(String::length).reversed());
```

与所有流转换一样，sorted 方法会产生一个新流，其元素是原流元素按排序顺序排列后的结果。

当然，你也可以不使用流来对集合排序。当排序过程是流管道的一部分时，sorted 方法很有用。

最后，peek 方法会产生另一个流，其元素与原流相同，但每次取回元素时都会调用一个函数。这便于调试：

```java
Object[] powers = Stream.iterate(1.0, p -> p * 2)
    .peek(e -> System.out.println("Fetching " + e))
    .limit(20).toArray();
```

当实际访问某个元素时，会打印一条消息。这样你就可以验证 iterate 返回的无限流是惰性处理的。

> **提示：** 当你使用调试器调试流计算时，可以在某个转换所调用的方法中设置断点。在大多数 IDE 中，你也可以在 lambda 表达式中设置断点。如果你只想知道流管道中某个特定位置发生了什么，请添加
>
> ```java
>     .peek(x -> {
>         return; })
> ```
>
> 并在第二行设置断点。

### java.util.stream.Stream

- `Stream<T> distinct()` —— 产生一个由本流中不同元素组成的流。
- `Stream<T> sorted()`
- `Stream<T> sorted(Comparator<? super T> comparator)` —— 产生一个流，其元素是本流元素按排序顺序排列后的结果。第一个方法要求元素是实现了 `Comparable` 的类的实例。
- `Stream<T> peek(Consumer<? super T> action)` —— 产生一个与本流具有相同元素的流，并在消费每个元素时将其传递给 `action`。

## 1.6 简单归约

现在你已经了解了如何创建和转换流，我们终于要进入最重要的一点——从流数据中获取答案。本节介绍的方法称为归约。归约是终端操作。它们将流归约为一个可在程序中使用的非流值。

你已经见过一个简单的归约：`count` 方法，它返回流中元素的数量。

其他简单的归约是 `max` 和 `min`，它们返回最大值或最小值。这里有个转折——这些方法返回一个 `Optional<T>` 值，它要么包装答案，要么表示没有答案（因为流恰好为空）。过去，在这种情况下通常会返回 `null`。但如果这种情况发生在一个未充分测试的程序中，就可能导致空指针异常。`Optional` 类型是表示缺失返回值的更好方式。我们将在下一节详细讨论 `Optional` 类型。下面是你如何获取流中的最大值：

```java
Optional<String> largest = words.max(String::compareToIgnoreCase);
System.out.println("largest: " + largest.orElse(""));
```

`findFirst` 方法返回非空集合中的第一个值。它与 `filter` 结合使用时通常很有用。例如，这里我们查找第一个以字母 Q 开头的单词（如果存在）：

```java
Optional<String> startsWithQ
    = words.filter(s -> s.startsWith("Q")).findFirst();
```

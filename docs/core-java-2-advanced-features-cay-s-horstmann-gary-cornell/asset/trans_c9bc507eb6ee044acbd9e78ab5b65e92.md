
如果 `s.f()` 存在，则对其应用 g。否则，返回一个空的 `Optional<>`。

显然，如果你有更多产生 `Optional` 值的方法或 lambda，可以重复该过程。然后，你只需通过链式调用 `flatMap` 就能构建一个步骤流水线，该流水线仅当所有步骤都成功时才会成功。

例如，考虑上一节中相同的 inverse 方法。假设我们还有一个安全的平方根：

```java
public static Optional<Double> squareRoot(Double x)
{
    return x < 0 ? Optional.empty() : Optional.of(Math.sqrt(x));
}
```

然后，你可以如下计算逆的平方根：

```java
Optional<Double> result = inverse(x).flatMap(Math::squareRoot);
```

或者，如果你愿意，

```java
Optional<Double> result = Optional.of(-4.0).flatMap(MyMath::inverse).flatMap(MyMath::squareRoot);
```

如果 inverse 方法或 squareRoot 返回 `Optional.empty()`，则结果为空。

> **注意：** 你已经在 Stream 接口中见过 `flatMap` 方法（参见第 1.3 节“`filter`、`map` 和 `flatMap` 方法”，第 9 页）。该方法用于组合两个产生流的方法，将结果中的流之流展平。如果你将可选值解释为大小为零或一的流，那么 Optional 的 `flatMap` 方法也以相同方式工作。

清单 1.3 中的示例程序演示了 Optional API。

## 清单 1.3 optional/OptionalTest.java

```java
package optional;

import java.io.*;
import java.nio.charset.*;
import java.nio.file.*;
import java.util.*;

public class OptionalTest
{
    public static void main(String[] args) throws IOException
    {
12 String contents = new String(Files.readAllBytes(
13         Paths.get("./gutenberg/alice30.txt")), StandardCharsets.UTF_8);
14 List<String> wordList = Arrays.asList(contents.split("\\PL+"));
15 
16 Optional<String> optionalValue = wordList.stream()
17         .filter(s -> s.contains("fred"))
18         .findFirst();
19 System.out.println(optionalValue.orElse("No word") + " contains fred");
20 
21 Optional<String> optionalString = Optional.empty();
22 String result = optionalString.orElse("N/A");
23 System.out.println("result: " + result);
24 result = optionalString.orElseGet(() -> Locale.getDefault().getDisplayName());
25 System.out.println("result: " + result);
26 try
27 {
28     result = optionalString.orElseThrow(IllegalStateException::new);
29     System.out.println("result: " + result);
30 }
31 catch (Throwable t)
32 {
33     t.printStackTrace();
34 }
35 
36 optionalValue = wordList.stream()
37         .filter(s -> s.contains("red"))
38         .findFirst();
39 optionalValue.ifPresent(s -> System.out.println(s + " contains red"));
40 
41 Set<String> results = new HashSet<>();
42 optionalValue.ifPresent(results::add);
43 Optional<Boolean> added = optionalValue.map(results::add);
44 System.out.println(added);
45 
46 System.out.println(inverse(4.0).flatMap(OptionalTest::squareRoot));
47 System.out.println(inverse(-1.0).flatMap(OptionalTest::squareRoot));
48 System.out.println(inverse(0.0).flatMap(OptionalTest::squareRoot));
49 Optional<Double> result2 = Optional.of(-4.0)
50         .flatMap(OptionalTest::inverse).flatMap(OptionalTest::squareRoot);
51 System.out.println(result2);
52 
53 public static Optional<Double> inverse(Double x)
54 {
55     return x == 0 ? Optional.empty() : Optional.of(1 / x);
56 }
57 }
58 
```

如果你想控制得到的集合类型，请改用以下调用：

```java
TreeSet<String> result = stream.collect(Collectors.toCollection(TreeSet::new));
```

假设你想通过拼接流中的所有字符串来收集它们。你可以调用

```java
String result = stream.collect(Collectors.joining());
```

如果你希望在元素之间使用分隔符，请将其传递给 joining 方法：

```java
String result = stream.collect(Collectors.joining(", "));
```

如果你的流包含字符串以外的对象，需要先将它们转换为字符串，如下所示：

```java
String result = stream.map(Object::toString).collect(Collectors.joining(", "));
```

如果你想将流结果归约为总和、平均值、最大值或最小值，请使用 summarizing(Int|Long|Double) 方法之一。这些方法接收一个将流对象映射为数字的函数，并生成 (Int|Long|Double)SummaryStatistics 类型的结果，同时计算总和、计数、平均值、最小值和最大值。

```java
IntSummaryStatistics summary = stream.collect(
    Collectors.summarizingInt(String::length));
double averageWordLength = summary.getAverage();
double maxWordLength = summary.getMax();
```

| **java.util.stream.BaseStream 8** |
| --- |
| • `Iterator<T> iterator()`<br>生成一个用于获取此流元素的迭代器。这是一个终端操作。 |

清单 1.4 中的示例程序展示了如何从流中收集元素。

## 清单 1.4 collecting/CollectingResults.java

```java
package collecting;

import java.io.*;
import java.nio.charset.*;
import java.nio.file.*;
6 import java.util.*;
7 import java.util.stream.*;
8 
9 public class CollectingResults
10 {
11   public static Stream<String> noVowels() throws IOException
12   {
13     String contents = new String(Files.readAllBytes(
14       Paths.get("../gutenberg/alice30.txt")),
15       StandardCharsets.UTF_8);
16     List<String> wordList = Arrays.asList(contents.split("\\PL+"));
17     Stream<String> words = wordList.stream();
18     return words.map(s -> s.replaceAll("[aeiouAEIOU]", ""));
19   }
20 
21   public static <T> void show(String label, Set<T> set)
22   {
23     System.out.print(label + ": " + set.getClass().getName());
24     System.out.println("["
25       + set.stream().limit(10).map(Object::toString)
26       .collect(Collectors.joining(", ")) + "]");
27   }
28 
29   public static void main(String[] args) throws IOException
30   {
31     Iterator<Integer> iter = Stream.iterate(0, n -> n + 1).limit(10)
32       .iterator();
33     while (iter.hasNext())
34       System.out.println(iter.next());
35 
36     Object[] numbers = Stream.iterate(0, n -> n + 1).limit(10).toArray();
37     System.out.println("Object array: " + numbers); // Note it's an Object[] array
38 
39     try
40     {
41       Integer number = (Integer) numbers[0]; // OK
42       System.out.println("number: " + number);
43       System.out.println("The following statement throws an exception:");
44       Integer[] numbers2 = (Integer[]) numbers; // Throws exception
45     }
46     catch (ClassCastException ex)
47     {
48       System.out.println(ex);
49     }
50 
51     Integer[] numbers3 = Stream.iterate(0, n -> n + 1).limit(10)
52       .toArray(Integer[]::new);
53     System.out.println("Integer array: " + numbers3); // Note it's an Integer[] array
```

```java
Locale::getDisplayCountry,
l -> Collections.singleton(l.getDisplayLanguage()),
(a, b) ->
    { // Union of a and b
        Set<String> union = new HashSet<>(a);
        union.addAll(b);
        return union;
    });
```

你将在下一节看到获取此映射的更简单方法。

如果你想要 TreeMap，请将构造函数作为第四个参数提供。你必须提供一个合并函数。下面是本节开头的一个示例，现在生成一个 TreeMap：

```java
Map<Integer, Person> idToPerson = people.collect(
    Collectors.toMap(
        Person::getId,
        Function.identity(),
        (existingValue, newValue) -> { throw new IllegalStateException(); },
        TreeMap::new));
```

> **注意：** 对于每个 `toMap` 方法，都有一个等效的 `toConcurrentMap` 方法，它会生成一个并发映射。在并行收集过程中使用单个并发映射。当与并行流一起使用时，共享映射比合并映射更高效。请注意，元素不再按流顺序收集，但这通常不会有什么影响。

清单 1.5 中的示例程序给出了将流结果收集到映射中的示例。

## 清单 1.5 collecting/CollectingIntoMaps.java

```java
package collecting;

import java.io.*;
import java.util.*;
import java.util.function.*;
import java.util.stream.*;

public class CollectingIntoMaps
{
    public static class Person
    {
        private int id;
        private String name;
```


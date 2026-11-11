

### 代码清单 1.1 `streams/CountLongWords.java`

```java
package streams;

/**
 * @version 1.01 2018-05-01
 * @author Cay Horstmann
 */

import java.io.*;
import java.nio.charset.*;
import java.nio.file.*;
import java.util.*;

public class CountLongWords
{
   public static void main(String[] args) throws IOException
   {
      var contents = Files.readString(
         Paths.get("../gutenberg/alice30.txt"));
      List<String> words = List.of(contents.split("\\PL+"));

      long count = 0;
      for (String w : words)
      {
         if (w.length() > 12) count++;
      }
      System.out.println(count);

      count = words.stream().filter(w -> w.length() > 12).count();
      System.out.println(count);

      count = words.parallelStream().filter(w -> w.length() > 12).count();
      System.out.println(count);
   }
}
```

| `java.util.stream.Stream<T>` | 8 |
|---|---|
| - `Stream<T> filter(Predicate<? super T> p)`<br>生成一个流，其中包含此流中满足 p 的所有元素。 | |
| - `long count()`<br>生成此流的元素数量。这是一个终端操作。 | |

| `java.util.Collection<E>` | 1.2 |
|---|---|
| - `default Stream<E> stream()`<br>- `default Stream<E> parallelStream()`<br>生成此集合中元素的顺序流或并行流。 | |

## 1.2 创建流

你已经看到，可以使用 `Collection` 接口的 `stream` 方法将任何集合转换为流。如果有一个数组，请改用静态的 `Stream.of` 方法。

```java
Stream<String> words = Stream.of(contents.split("\\PL+"));
    // split returns a String[] array
```

`of` 方法有一个可变参数，因此你可以用任意数量的参数构造流：

```java
Stream<String> song = Stream.of("gently", "down", "the", "stream");
```

使用 `Arrays.stream(array, from, to)` 从数组的一部分创建流。

要创建不含任何元素的流，请使用静态的 `Stream.empty` 方法：

```java
Stream<String> silence = Stream.empty();
    // Generic type <String> is inferred; same as Stream.<String>empty()
```

`Stream` 接口有两个用于创建无限流的静态方法。`generate` 方法接受一个无参数的函数（或者从技术上说，是一个 `Supplier<T>` 接口的对象）。每当需要一个流值时，就会调用该函数来生成一个值。你可以像下面这样获得常量值流：

```java
Stream<String> echos = Stream.generate(() -> "Echo");
```

或者像下面这样获得随机数流：

```java
Stream<Double> randoms = Stream.generate(Math::random);
```

要生成诸如 0 1 2 3 . . . 这样的序列，请改用 `iterate` 方法。它接受一个“种子”值和一个函数（从技术上说，是一个 `UnaryOperator<T>`），并反复将该函数应用于前一个结果。例如，

```java
Stream<BigInteger> integers
    = Stream.iterate(BigInteger.ZERO, n -> n.add(BigInteger.ONE));
```

该序列中的第一个元素是种子 `BigInteger.ZERO`。第二个元素是 `f(seed)`，它产生 1（作为大整数）。下一个元素是 `f(f(seed))`，它产生 2，依此类推。

要改为生成有限流，请添加一个指定迭代应在何时结束的谓词：

```java
var limit = new BigInteger("10000000");
Stream<BigInteger> integers
    = Stream.iterate(BigInteger.ZERO,
        n -> n.compareTo(limit) < 0,
        n -> n.add(BigInteger.ONE));
```

一旦该谓词拒绝某个迭代生成的值，流就会结束。

最后，`Stream.ofNullable` 方法可以从一个对象生成一个非常短的流。如果对象为 null，则流的长度为 0；否则长度为 1，仅包含该对象。这主要在与 `flatMap` 结合使用时有用——示例见第 22 页的 1.7.7 节“将 Optional 转换为流”。

> **注意：** Java API 中有许多方法会生成流。例如，`Pattern` 类有一个 `splitAsStream` 方法，可按正则表达式拆分 `CharSequence`。你可以使用以下语句将字符串拆分为单词：
>
> ```java
> Stream<String> words = Pattern.compile("\\PL+").splitAsStream(contents);
> ```
>
> `Scanner.tokens` 方法会生成扫描器的标记流。从字符串获取单词流的另一种方法是
>
> ```java
> Stream<String> words = new Scanner(contents).tokens();
> ```
>
> 静态 `Files.lines` 方法返回文件中所有行的 `Stream`：
>
> ```java
> try (Stream<String> lines = Files.lines(path)) {
>     Process lines
> }
> ```

> **注意：** 如果你有一个不是集合的 `Iterable`，可以通过调用以下代码将其转换为流：
>
> ```java
> StreamSupport.stream(iterable.spliterator(), false);
> ```
>
> 如果你有一个 `Iterator`，并想要其结果的流，请使用
>
> ```java
> StreamSupport.stream(Spliterators.spliteratorUnknownSize(
>     iterator, Spliterator.ORDERED), false);
> ```

**警告：** 在执行流操作时，不要修改作为流后盾的集合，这一点非常重要。请记住，流不会收集其数据——数据始终位于单独的集合中。如果修改该集合，流操作的结果将变得未定义。JDK 文档将这一要求称为*非干扰*。

确切地说，由于中间流操作是惰性的，可以修改集合，直到终端操作执行的那一刻。例如，下面的代码虽然肯定不推荐，但可以工作：

```java
List<String> wordList = . . .;
Stream<String> words = wordList.stream();
wordList.add("END");
long n = words.distinct().count();
```

但下面的代码是错误的：

```java
Stream<String> words = wordList.stream();
words.forEach(s -> { if (s.length() < 12) wordList.remove(s); });
   // ERROR--interference
```

代码清单 1.2 中的示例程序展示了创建流的各种方式。

### 代码清单 1.2 `streams/CreatingStreams.java`

```java
package streams;

/**
 * @version 1.01 2018-05-01
 * @author Cay Horstmann
 */

import java.io.IOException;
import java.math.BigInteger;
import java.nio.charset.StandardCharsets;
import java.nio.file.*;
import java.util.*;
import java.util.regex.Pattern;
import java.util.stream.*;

public class CreatingStreams
{
   public static <T> void show(String title, Stream<T> stream)
   {
20 final int SIZE = 10;
21 List<T> firstElements = stream
22     .limit(SIZE + 1)
23     .collect(Collectors.toList());
24 System.out.print(title + ": ");
25 for (int i = 0; i < firstElements.size(); i++)
26 {
27     if (i > 0) System.out.print(", ");
28     if (i < SIZE) System.out.print(firstElements.get(i));
29     else System.out.print("...");
30 }
31 System.out.println();
32 }
33
34 public static void main(String[] args) throws IOException
35 {
36     Path path = Paths.get("../gutenberg/alice30.txt");
37     var contents = Files.readString(path);
38
39     Stream<String> words = Stream.of(contents.split("\\PL+"));
40     show("words", words);
41     Stream<String> song = Stream.of("gently", "down", "the", "stream");
42     show("song", song);
43     Stream<String> silence = Stream.empty();
44     show("silence", silence);
45
46     Stream<String> echos = Stream.generate(() -> "Echo");
47     show("echos", echos);
48
49     Stream<Double> randoms = Stream.generate(Math::random);
50     show("randoms", randoms);
51
52     Stream<BigInteger> integers = Stream.iterate(BigInteger.ONE,
53           n -> n.add(BigInteger.ONE));
54     show("integers", integers);
55
56     Stream<String> wordsAnotherWay = Pattern.compile("\\PL+").splitAsStream(contents);
57     show("wordsAnotherWay", wordsAnotherWay);
58
59     try (Stream<String> lines = Files.lines(path, StandardCharsets.UTF_8))
60     {
61         show("lines", lines);
62     }
63
64     Iterable<Path> iterable = FileSystems.getDefault().getRootDirectories();
65     Stream<Path> rootDirectories = StreamSupport.stream(iterable.spliterator(), false);
66     show("rootDirectories", rootDirectories);
```


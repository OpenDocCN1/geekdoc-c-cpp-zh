# Java 核心技术，第二卷——高级特性，第2卷

# 前言

## 致读者

你手中的书是 *Java核心技术* 第十一版第二卷，已针对 Java SE 11 全面更新。第一卷涵盖语言的基本特性；本卷讨论专业软件开发人员需要了解的高级主题。因此，与第一卷及本书先前版本一样，我们仍然面向希望在实际项目中使用 Java 技术的程序员。

与任何书籍一样，错误和不准确之处在所难免。如果你在本书中发现任何问题，我们非常希望听到你的反馈。当然，我们更希望只听到一次。为此，我们建立了一个网站 http://horstmann.com/corejava，其中提供 FAQ、缺陷修复和变通方法。在缺陷报告网页末尾（这样安排是为了鼓励你阅读之前的报告）特意放置了一个表单，你可以用它报告缺陷或问题，并为未来版本提出改进建议。

## 关于本书

本书各章大多相互独立。你应该能够深入探讨你最感兴趣的主题，并按任意顺序阅读各章。

在**第1章**中，你将全面了解 Java 流库，它为数据处理带来现代风格：只需说明你想要什么，而无需详细描述应如何获得结果。这使流库能够专注于最优求值策略，这对优化并发计算尤其有利。

**第2章**的主题是输入/输出处理（I/O）。在 Java 中，所有输入和输出都通过输入/输出流处理。这些流（不要与第1章中的流混淆）让你以统一方式处理各种数据源之间的通信，例如文件、网络连接或内存块。我们详细介绍了使处理 Unicode 变得容易的读取器和写入器类。我们展示了使用对象序列化机制时底层发生的情况，该机制使保存和加载对象变得简单方便。然后我们转向正则表达式以及文件和路径操作。在本章中，你会发现近期 Java 版本中令人欣喜的增强。

**第3章涵盖 XML。** 我们展示如何解析 XML 文件、如何生成 XML 以及如何使用 XSL 转换。作为一个有用的示例，我们展示如何用 XML 指定 Swing 窗体的布局。我们还讨论 XPath API，它使在 XML 干草堆中找针容易得多。

**第4章涵盖网络 API。** Java 使复杂的网络编程变得异常容易。我们展示如何建立到服务器的网络连接、如何实现自己的服务器以及如何进行 HTTP 连接。本章包括对新的 HTTP 客户端的介绍。

**第5章涵盖数据库编程。** 主要关注 JDBC，即让 Java 程序连接关系数据库的 Java 数据库连接 API。我们展示如何使用 JDBC API 的核心子集编写有用的程序来处理现实中的数据库日常事务。（完整讨论 JDBC API 需要一本几乎和本书一样厚的书。）我们在本章结尾简要介绍层次数据库，并讨论 JNDI（Java 命名与目录接口）和 LDAP（轻量级目录访问协议）。

Java 先前曾两次尝试提供处理日期和时间的库。第三次在 Java 8 中终于成功。在**第6章**中，你将学习如何使用新的日期和时间库处理日历和时区的复杂性。

**第7章**讨论我们认为只会越来越重要的一项特性：国际化。Java 编程语言是从一开始就设计为处理 Unicode 的少数语言之一，但 Java 平台上的国际化支持远不止于此。因此，你可以对 Java 应用进行国际化，使其不仅跨平台，还能跨越国界。例如，我们展示如何编写一个使用英语、德语或中文的退休计算器。

**第8章**讨论处理代码的三种技术。脚本和编译器 API 允许你的程序调用 JavaScript 或 Groovy 等脚本语言中的代码，并编译 Java 代码。注解允许你向 Java 程序添加任意信息（有时称为元数据）。我们展示注解处理器如何在源代码或类文件级别收集这些注解，以及如何使用注解在运行时影响类的行为。注解只有与工具配合才有用，我们希望我们的讨论能帮助你根据自己的需求选择有用的注解处理工具。

在**第9章**中，你将了解 Java 9 引入的 Java 平台模块系统，它促进 Java 平台和核心库的有序演进。该模块系统为包提供封装，并提供描述模块需求的机制。你将学习模块的属性，以便决定是否在自己的应用中使用它们。即使你决定不使用，也需要了解新规则，以便与 Java 平台和其他模块化库交互。

**第10章**讨论 Java 安全模型。Java 平台从底层设计上就是安全的，本章将带你深入底层，了解这一设计是如何实现的。我们展示如何为特殊用途应用编写自己的类加载器和安全管理器。然后，我们讨论安全 API，它支持消息与代码签名、授权与认证以及加密等重要特性。最后，我们以使用 AES 和 RSA 加密算法的示例作结。

**第11章**包含未纳入第一卷的所有 Swing 内容，特别是重要但复杂的树和表组件。我们还涵盖 Java 2D API，你可以用它创建逼真的绘图和特殊效果。当然，如今没有多少程序员需要编写 Swing 用户界面，因此我们特别关注对可在服务器上生成的图像有用的特性。

**第12章**讨论本地方法，它让你调用为特定机器编写的方法，例如 Microsoft Windows API。显然，这一特性存在争议：一旦使用本地方法，Java 的跨平台特性就会消失。尽管如此，每个为特定平台编写 Java 应用的专业程序员都需要了解这些技术。有时，当你与 Java 不支持的设备或服务交互时，需要求助于目标平台的操作系统 API。我们通过展示如何从 Java 程序访问 Windows 中的注册表 API 来说明这一点。

一如既往，所有章节都已针对最新版本的 Java 全面修订。过时的内容已被删除，并详细介绍了 Java 9、10 和 11 的新 API。



# 约定

正如许多计算机书籍中的常见做法，我们使用 `monospace` 字体来表示计算机代码。

> **注意：** 注释带有“注意”图标，如下所示。

> **提示：** 提示带有“提示”图标，如下所示。

> **警告：** 前方有危险时，我们会用“警告”图标提醒你。

> **C++ 注意：** 有许多 C++ 注释解释 Java 编程语言与 C++ 之间的差异。如果你对 C++ 不感兴趣，可以跳过它们。

Java 附带一个大型编程库，即应用程序编程接口（API）。首次使用某个 API 调用时，我们会在该节末尾添加简短的摘要说明。这些说明稍显非正式，但我们希望它们也比官方在线 API 文档中的说明更具信息量一些。接口名称使用斜体，与官方文档中一样。类、接口或方法名称后面的数字表示引入该特性的 JDK 版本。

|  |  |
| --- | --- |
| 应用程序编程接口 | 1.2 |

本书配套代码中包含源代码的程序会作为示例列出，例如

```
Listing 1.1  ScriptTest.java
```

你可以从 http://horstmann.com/corejava 下载配套代码。

# 致谢

写一本书始终是一项艰巨的努力，而重写似乎也并不容易多少，尤其是在 Java 技术变化如此迅速的情况下。让一本书成为现实需要许多敬业的人，我非常高兴地感谢整个 Core Java 团队的贡献。

Pearson 的许多个人提供了宝贵的帮助，但他们设法留在幕后。我想让他们所有人知道，我非常感激他们的努力。一如既往，我衷心感谢我的编辑 Greg Doench，感谢他引导本书完成写作和制作过程，并让我得以幸福地不知道所有那些幕后人员的存在。我非常感谢 Julie Nahil 提供制作支持，感谢 Dmitry Kirsanov 和 Alina Kirsanova 对稿件进行文字编辑和排版。

感谢早期版本的许多读者，他们报告了令人尴尬的错误，并提出了许多深思熟虑的改进建议。我特别感谢优秀的审阅团队，他们以惊人的细节眼光审阅了稿件，使我免于更多令人尴尬的错误。

本版及早期版本的审阅者包括 Chuck Allison（《C/C++ Users Journal》特约编辑）、Lance Anderson（Oracle）、Alec Beaton（PointBase, Inc.）、Cliff Berg（iSavvix Corporation）、Joshua Bloch、David Brown、Corky Cartwright、Frank Cohen（PushToTest）、Chris Crane（devXsolution）、Nicholas J. De Lillo 博士（Manhattan College）、Rakesh Dhoopar（Oracle）、Robert Evans（The Johns Hopkins University Applied Physics Lab 高级职员）、David Geary（Sabreware）、Jim Gish（Oracle）、Brian Goetz（Oracle）、Angela Gordon、Dan Gordon、Rob Gordon、John Gray（University of Hartford）、Cameron Gregory（olabs.com）、Steve Haines、Marty Hall（The Johns Hopkins University Applied Physics Lab）、Vincent Hardy、Dan Harkey（San Jose State University）、William Higgins（IBM）、Vladimir Ivanovic（PointBase）、Jerry Jackson（ChannelPoint Software）、Tim Kimmet（Preview Systems）、Chris Laffra、Charlie Lai、Angelika Langer、Doug Langston、Hang Lau（McGill University）、Mark Lawrence、Doug Lea（SUNY Oswego）、Gregory Longshore、Bob Lynch（Lynch Associates）、Philip Milne（顾问）、Mark Morrissey（The Oregon Graduate Institute）、Mahesh Neelakanta（Florida Atlantic University）、Hao Pham、Paul Philion、Blake Ragsdell、Ylber Ramadani（Ryerson University）、Stuart Reges（University of Arizona）、Simon Ritter、Rich Rosen（Interactive Data Corporation）、Peter Sanders（ESSI University, Nice, France）、Paul Sanghera 博士（San Jose State University 和 Brooks College）、Paul Sevinc（Teamup AG）、Yoshiki Shabata、Devang Shah、Richard Slywczak（NASA/Glenn Research Center）、Bradley A. Smith、Steven Stelting、Christopher Taylor、Luke Taylor（Valtech）、George Tirhutavakul、Kim Topley（*《Core JFC，第二版》*作者）、Janet Traub、Paul Tyma（顾问）、Christian Ullenboom、Peter van der Linden、Burt Walsh、Joe Wang（Oracle）和 Dan Xu（Oracle）。

*Cay Horstmann*  
*加利福尼亚州旧金山*  
*2018 年 12 月*

# 第 1 章：流

## 本章内容

- 1.1 从迭代到流操作，第 2 页
- 1.2 流的创建，第 5 页
- 1.3 filter、map 和 flatMap 方法，第 11 页
- 1.4 提取子流与合并流，第 12 页
- 1.5 其他流转换，第 14 页
- 1.6 简单归约，第 15 页
- 1.7 Optional 类型，第 16 页
- 1.8 收集结果，第 25 页
- 1.9 收集到映射，第 30 页
- 1.10 分组与分区，第 34 页
- 1.11 下游收集器，第 36 页
- 1.12 归约操作，第 41 页
- 1.13 基本类型流，第 43 页
- 1.14 并行流，第 48 页

与集合相比，流提供了一种数据视图，让你能够在更高的概念层次上指定计算。使用流时，你指定想要完成什么，而不是如何完成。你把操作的调度留给实现。例如，假设你想计算某个属性的平均值。你指定数据源和属性，流库随后就能优化计算，例如使用多个线程计算总和与计数并合并结果。

在本章中，你将学习如何使用 Java 8 引入的 Java 流库，以“做什么，而不是怎么做”的风格处理集合。

## 1.1 从迭代到流操作

处理集合时，你通常会遍历其元素并对每个元素做一些工作。例如，假设我们想统计一本书中所有长单词。首先，把它们放入一个列表：

```java
var contents = Files.readString(
    Paths.get("alice.txt")); // Read file into string
List<String> words = List.of(contents.split("\\PL+"));
    // Split into words; nonletters are delimiters
```

现在我们可以进行迭代了：

```java
int count = 0;
for (String w : words) {
    if (w.length() > 12) count++;
}
```

使用流时，同样的操作看起来像这样：

```java
long count = words.stream()
    .filter(w -> w.length() > 12)
    .count();
```

现在你不必再浏览循环来寻找过滤和计数的痕迹。方法名会立刻告诉你代码意图做什么。此外，循环会非常详细地规定操作顺序，而流则能够以它想要的任何方式调度操作，只要结果正确即可。

只需将 `stream` 改为 `parallelStream`，流库就能并行执行过滤和计数。

```java
long count = words.parallelStream()
    .filter(w -> w.length() > 12)
    .count();
```

流遵循“做什么，而不是怎么做”的原则。在我们的流示例中，我们描述了需要完成什么：获取长单词并统计它们。我们没有指定应该以什么顺序、在哪个线程中发生。相比之下，本节开头的循环明确规定了计算应如何工作，从而放弃了任何优化的机会。

流表面上看起来与集合相似，允许你转换和检索数据。但它们有显著差异：

- 1. 流不存储其元素。它们可能存储在底层集合中，或按需生成。
- 2. 流操作不会修改其源。例如，filter 方法不会从流中移除元素，而是产生一个不包含这些元素的新流。
- 3. 流操作在可能时是惰性的。这意味着直到需要结果时才会执行它们。例如，如果你只要求前五个长单词而不是全部，filter 方法会在第五个匹配后停止过滤。因此，你甚至可以有无限流！

让我们再看一下这个例子。stream 和 parallelStream 方法为 words 列表生成一个流。filter 方法返回另一个只包含长度大于十二的单词的流。count 方法将该流归约为一个结果。

使用流时，这种工作流程很典型。你分三个阶段建立一条操作流水线：

- 1. 创建一个流。
- 2. 指定*中间操作*，用于将初始流转换为其他流，可能需要多个步骤。
- 3. 应用*终端操作*以产生结果。该操作会强制执行其前面的惰性操作。之后，该流不能再被使用。

在代码清单 1.1 的示例中，流是用 stream 或 parallelStream 方法创建的。filter 方法转换它，而 count 是终端操作。

下一节你将看到如何创建流。随后的三节讨论流转换。之后是五节关于终端操作的内容。




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



如果你对任意匹配（而不只是第一个）都可以接受，使用 `findAny` 方法。当你并行化流时，这很有效，因为流可以报告它找到的任意匹配，而不必受限于第一个匹配。

```java
Optional<String> startsWithQ
    = words.parallel().filter(s -> s.startsWith("Q")).findAny();
```

如果你只想知道是否存在匹配，使用 `anyMatch`。该方法接受一个谓词参数，因此你不需要使用 `filter`。

```java
boolean aWordStartsWithQ
    = words.parallel().anyMatch(s -> s.startsWith("Q"));
```

还有 `allMatch` 和 `noneMatch` 方法，分别在所有元素匹配或没有元素匹配谓词时返回 true。这些方法同样受益于并行运行。

- **java.util.stream.Stream 8**
  - `Optional<T> max(Comparator<? super T> comparator)`
  - `Optional<T> min(Comparator<? super T> comparator)`

    根据给定比较器定义的顺序，生成此流的最大或最小元素；如果此流为空，则生成空的 `Optional`。这些是终端操作。

  - `Optional<T> findFirst()`
  - `Optional<T> findAny()`

    生成此流的第一个或任意元素；如果此流为空，则生成空的 `Optional`。这些是终端操作。

  - `boolean anyMatch(Predicate<? super T> predicate)`
  - `boolean allMatch(Predicate<? super T> predicate)`
  - `boolean noneMatch(Predicate<? super T> predicate)`

    如果此流中的任意、全部或没有元素匹配给定谓词，则返回 true。这些是终端操作。

## 1.7 Optional 类型

`Optional<T>` 对象是类型 T 的对象或不存在对象的包装器。在前一种情况下，我们说该值是存在的。`Optional<T>` 类型旨在作为类型 T 引用的更安全替代方案，这种引用要么引用一个对象，要么为 null。但只有当你正确使用它时，它才更安全。接下来的三节将向你展示如何正确使用。

### 1.7.1 获取 Optional 值

有效使用 `Optional` 的关键是使用一种方法，要么在值不存在时*生成替代值*，要么仅在值存在时*消费该值*。

在本节中，我们来看第一种策略。通常，当没有匹配时，你可能希望使用一个默认值，也许是空字符串：

```java
String result = optionalString.orElse("");
    // The wrapped string, or "" if none
```

你还可以调用代码来计算默认值：

```java
String result = optionalString.orElseGet(() -> System.getProperty("myapp.default"));
    // The function is only called when needed
```

或者，如果没有值，你可以抛出异常：

```java
String result = optionalString.orElseThrow(IllegalStateException::new);
    // Supply a method that yields an exception object
```

| `java.util.Optional` | 8 |
|---|---|
| `T orElse(T other)` | 返回此 Optional 的值；如果此 Optional 为空，则返回 other。 |
| `T orElseGet(Supplier<? extends T> other)` | 返回此 Optional 的值；如果此 Optional 为空，则返回调用 other 的结果。 |
| `<X extends Throwable> T orElseThrow(Supplier<? extends X> exceptionSupplier)` | 返回此 Optional 的值；如果此 Optional 为空，则抛出调用 exceptionSupplier 的结果。 |

### 1.7.2 消费 Optional 值

在上一节中，你了解了如何在值不存在时生成替代值。处理可选值的另一个策略是仅在值存在时消费该值。

`ifPresent` 方法接受一个函数。如果可选值存在，该值会被传给这个函数。否则，什么都不会发生。

```java
optionalValue.ifPresent(v -> process(v));
```

例如，如果可选值存在，你想将其添加到一个集合中，可以调用

```java
optionalValue.ifPresent(v -> results.add(v));
```

或者简写为

```java
optionalValue.ifPresent(results::add);
```

如果希望在 Optional 有值时执行一个操作，没有值时执行另一个操作，可以使用 ifPresentOrElse：

```java
optionalValue.ifPresentOrElse(
    v -> System.out.println("Found " + v),
    () -> logger.warning("No match"));
```

| java.util.Optional 8 |
|---|
| • void ifPresent(Consumer<? super T> action)<br>如果此 Optional 非空，则将其值传递给 action。<br>• void ifPresentOrElse(Consumer<? super T> action, Runnable emptyAction) 9<br>如果此 Optional 非空，则将其值传递给 action，否则调用 emptyAction。 |

### 1.7.3 流水线化 Optional 值

在前面的几节中，你了解了如何从 Optional 对象中获取值。另一个有用的策略是保持 Optional 不变。你可以使用 map 方法转换 Optional 内部的值：

```java
Optional<String> transformed = optionalString.map(String::toUpperCase);
```

如果 optionalString 为空，那么 transformed 也为空。

下面是另一个示例。如果结果存在，我们将其添加到一个列表中：

```java
optionalValue.map(results::add);
```

如果 optionalValue 为空，什么都不会发生。

> **注意：** 此 map 方法类似于你在第 11 页的 1.3 节 “filter、map 和 flatMap 方法” 中看到的 Stream 接口的 map 方法。不妨将可选值想象成一个大小为零或一的流。结果同样为零或一的大小，在后者的情况下，该函数已被应用。

类似地，你可以使用 filter 方法，在转换之前或之后只考虑满足特定属性的 Optional 值。如果该属性未得到满足，流水线会产生一个空结果：

这并不比

```java
if (value != null) value.someMethod();
```

更容易。

> **注意：** Java 10 为 `get` 方法引入了一个听起来更吓人的同义词。调用 `optionalValue.orElseThrow()` 可以明确表示：如果 `optionalValue` 为空，该方法将抛出 `NoSuchElementException`。这样做的希望是，程序员只会在绝对清楚 `Optional` 永不为空时才调用该方法。

以下是正确使用 `Optional` 类型的更多提示：

- `Optional` 类型的变量永远不应该是 `null`。
- 不要使用 `Optional` 类型的字段。代价是增加一个对象。在类内部，对缺失的字段使用 `null` 是可管理的。
- 不要将 `Optional` 对象放入集合中，也不要将它们用作映射的键。应该改为收集值。

| `java.util.Optional` 8 |
|---|
| `T get()` |
| `T orElseThrow()` 10<br>返回此 `Optional` 的值；如果此 `Optional` 为空，则抛出 `NoSuchElementException`。 |
| `boolean isPresent()`<br>如果此 `Optional` 不为空，则返回 `true`。 |

### 1.7.5 创建 Optional 值

到目前为止，我们已经讨论了如何消费他人创建的 `Optional` 对象。如果你想要编写一个创建 `Optional` 对象的方法，有几个静态方法可用于此目的，包括 `Optional.of(result)` 和 `Optional.empty()`。例如，

```java
public static Optional<Double> inverse(Double x)
{
    return x == 0 ? Optional.empty() : Optional.of(1 / x);
}
```

`ofNullable` 方法旨在作为从可能为 null 的值到可选值的桥梁。如果 `ob` 不为 null，`Optional.ofNullable(ob)` 返回 `Optional.of(ob)`；否则返回 `Optional.empty()`。

- **java.util.Optional 8**
  - `static <T> Optional<T> of(T value)`
  - `static <T> Optional<T> ofNullable(T value)`

    生成具有给定值的 `Optional`。如果 `value` 为 null，第一个方法抛出 `NullPointerException`，第二个方法生成空的 `Optional`。

  - `static <T> Optional<T> empty()`

    生成空的 `Optional`。

### 1.7.6 使用 flatMap 组合 Optional 值函数

假设你有一个方法 `f` 生成 `Optional<T>`，目标类型 `T` 有一个方法 `g` 生成 `Optional<U>`。如果它们是普通方法，你可以通过调用 `s.f().g()` 来组合它们。但这种组合行不通，因为 `s.f()` 的类型是 `Optional<T>`，而不是 `T`。相反，应该调用

```java
Optional<U> result = s.f().flatMap(T::g);
```

如果 `s.f()` 存在，则对其应用 `g`。否则，返回空的 `Optional<U>`。

显然，如果你有更多生成 `Optional` 值的方法或 lambda，你可以重复该过程。你可以通过简单地链式调用 `flatMap` 来构建一个步骤流水线，只有所有部分都成功时它才会成功。

例如，考虑上一节中的安全 `inverse` 方法。假设我们还有一个安全的平方根方法：

```java
public static Optional<Double> squareRoot(Double x)
{
    return x < 0 ? Optional.empty() : Optional.of(Math.sqrt(x));
}
```

然后你可以像这样计算逆的平方根：

```java
Optional<Double> result = inverse(x).flatMap(MyMath::squareRoot);
```

或者，如果你愿意，也可以这样：

```java
Optional<Double> result
    = Optional.of(-4.0).flatMap(Demo::inverse).flatMap(Demo::squareRoot);
```



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

### DoubleSummaryStatistics 8（续）

- `(int | long | double) getMax()`
- `(int | long | double) getMin()`

返回已汇总元素的最大值或最小值；如果没有元素，则返回 `(Integer | Long | Double).(MAX | MIN)_VALUE`。

## 1.9 收集到映射中

假设你有一个 `Stream<Person>`，并希望将元素收集到一个映射中，以便之后可以通过 ID 查找人员。`Collectors.toMap` 方法有两个函数参数，分别生成映射的键和值。例如，

```java
    Map<Integer, String> idToName = people.collect(
        Collectors.toMap(Person::getId, Person::getName));
```

在常见情况下，如果值应当是实际元素，则对第二个函数使用 `Function.identity()`。

```java
    Map<Integer, Person> idToPerson = people.collect(
        Collectors.toMap(Person::getId, Function.identity()));
```

如果存在多个具有相同键的元素，就会发生冲突，收集器将抛出 `IllegalStateException`。你可以通过提供第三个函数参数来覆盖该行为，该参数根据现有值和新值来解决冲突并确定该键的值。你的函数可以返回现有值、新值或它们的组合。

这里，我们构造一个映射，对于可用区域设置中的每种语言，以它在你的默认区域设置中的名称（例如 "German"）作为键，以它的本地化名称（例如 "Deutsch"）作为值。

```java
    Stream<Locale> locales = Stream.of(Locale.getAvailableLocales());
    Map<String, String> languageNames = locales.collect(
        Collectors.toMap(
            Locale::getDisplayLanguage,
            loc -> loc.getDisplayLanguage(),
            (existingValue, newValue) -> existingValue));
```

我们不关心同一种语言可能出现两次（例如，德语在德国和瑞士），因此我们只保留第一个条目。

> **注意：** 在本章中，我使用 `Locale` 类作为有趣数据集的来源。有关使用区域设置的更多信息，请参见第 7 章。

现在假设我们想知道给定国家/地区中的所有语言。那么我们需要一个 `Map<String, Set<String>>`。例如，"Switzerland" 的值是集合 {French, German, Italian}。起初，我们为每种语言存储一个单元素集合。每当为给定国家/地区发现一种新语言时，我们就形成现有集合与新集合的并集。

```java
    Map<String, Set<String>> countryLanguageSets = locales.collect(
        Collectors.toMap(
            Locale::getDisplayCountry,
            l -> Collections.singleton(l.getDisplayLanguage()),
            (a, b) -> { // Union of a and b
                var union = new HashSet<String>(a);
                union.addAll(b);
                return union; }));
```

你将在下一节看到获得此映射的更简单方法。

如果你想要一个 `TreeMap`，请将构造函数作为第四个参数提供。你必须提供一个合并函数。下面是本节开头的一个示例，现在生成一个 `TreeMap`：

```java
    Map<Integer, Person> idToPerson = people.collect(
        Collectors.toMap(
            Person::getId,
            Function.identity(),
            (existingValue, newValue) -> { throw new IllegalStateException(); },
            TreeMap::new));
```

> **注意：** 对于每个 `toMap` 方法，都有一个等效的 `toConcurrentMap` 方法，它会生成一个并发映射。在并行收集过程中使用单个并发映射。当与并行流一起使用时，共享映射比合并映射更高效。请注意，元素不再按流顺序收集，但这通常不会有什么影响。

程序清单 1.5 中的程序给出了将流结果收集到映射中的示例。

### 程序清单 1.5 collecting/CollectingIntoMaps.java

```java
package collecting;

/**
 * @version 1.00 2016-05-10
 * @author Cay Horstmann
 */

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

      public Person(int id, String name)
      {
         this.id = id;
         this.name = name;
      }

      public int getId()
      {
         return id;
      }

      public String getName()
      {
         return name;
      }

      public String toString()
      {
         return getClass().getName() + "[id=" + id + ",name=" + name + "]";
      }
   }

   public static Stream<Person> people()
   {
      return Stream.of(new Person(1001, "Peter"), new Person(1002, "Paul"),
         new Person(1003, "Mary"));
   }

   public static void main(String[] args) throws IOException
   {
      Map<Integer, String> idToName = people().collect(
         Collectors.toMap(Person::getId, Person::getName));
      System.out.println("idToName: " + idToName);

      Map<Integer, Person> idToPerson = people().collect(
         Collectors.toMap(Person::getId, Function.identity()));
      System.out.println("idToPerson: " + idToPerson.getClass().getName()
         + idToPerson);

      idToPerson = people().collect(
         Collectors.toMap(Person::getId, Function.identity(),
            (existingValue, newValue) -> { throw new IllegalStateException(); },
            TreeMap::new));
      System.out.println("idToPerson: " + idToPerson.getClass().getName()
         + idToPerson);

      Stream<Locale> locales = Stream.of(Locale.getAvailableLocales());
      Map<String, String> languageNames = locales.collect(
         Collectors.toMap(
            Locale::getDisplayLanguage,
            l -> l.getDisplayLanguage(),
            (existingValue, newValue) -> existingValue));
      System.out.println("languageNames: " + languageNames);

      locales = Stream.of(Locale.getAvailableLocales());
      Map<String, Set<String>> countryLanguageSets = locales.collect(
         Collectors.toMap(
            Locale::getDisplayCountry,
            l -> Set.of(l.getDisplayLanguage()),
            (a, b) ->
            { // union of a and b
               Set<String> union = new HashSet<>(a);
               union.addAll(b);
               return union;
            }));
      System.out.println("countryLanguageSets: " + countryLanguageSets);
   }
}
```

## 1.11 下游收集器

`groupingBy` 方法生成一个映射，其值是列表。如果你想以某种方式处理这些列表，请提供一个下游收集器。例如，如果你想要集合而不是列表，可以使用你在上一节中看到的 `Collectors.toSet` 收集器：

```java
Map<String, Set<Locale>> countryToLocaleSet = locales.collect(
    groupingBy(Locale::getCountry, toSet()));
```

> **注意：** 在此示例以及本节其余示例中，我假设已静态导入 `java.util.stream.Collectors.*`，以便使表达式更易于阅读。

提供了几个收集器用于将收集的元素归约为数字：

- `counting` 生成已收集元素的计数。例如，它统计每个国家/地区有多少个区域设置。
- `summing(Int|Long|Double)` 接受一个函数参数，将该函数应用于下游元素，并生成它们的和。例如，它计算城市流中每个州的人口总和。
- `maxBy` 和 `minBy` 接受一个比较器，并生成下游元素的最大值和最小值。例如，它生成每个州最大的城市。

```java
Map<String, Long> countryToLocaleCounts = locales.collect(
    groupingBy(Locale::getCountry, counting()));
```

```java
Map<String, Integer> stateToCityPopulation = cities.collect(
    groupingBy(City::getState, summingInt(City::getPopulation)));
```

```java
Map<String, Optional<City>> stateToLargestCity = cities.collect(
    groupingBy(City::getState,
        maxBy(Comparator.comparing(City::getPopulation))));
```

`collectingAndThen` 收集器在收集器之后添加一个最终处理步骤。例如，如果你想知道有多少个不同的结果，请将它们收集到一个集合中，然后计算大小：

```java
Map<Character, Integer> stringCountsByStartingLetter = strings.collect(
    groupingBy(s -> s.charAt(0),
        collectingAndThen(toSet(), Set::size)));
```




### 代码清单 1.6 `collecting/DownstreamCollectors.java`

```java
package collecting;

/**
 * @version 1.00 2016-05-10
 * @author Cay Horstmann
 */

import static java.util.stream.Collectors.*;

import java.io.*;
import java.nio.file.*;
import java.util.*;
import java.util.stream.*;

public class DownstreamCollectors
{
   public static class City
   {
      private String name;
      private String state;
      private int population;

      public City(String name, String state, int population)
      {
         this.name = name;
         this.state = state;
         this.population = population;
      }

      public String getName()
      {
         return name;
      }

      public String getState()
      {
         return state;
      }

      public int getPopulation()
      {
         return population;
      }
   }

   public static Stream<City> readCities(String filename) throws IOException
   {
```

### java.util.stream.Collectors 8

- `public static <T,K,A,D> Collector<T,?,Map<K,D>> groupingBy(Function<? super T,? extends K> classifier, Collector<? super T,A,D> downstream)`  
  生成一个收集器，它产生一个映射。键是将 classifier 应用于所有已收集元素的结果。值是用下游收集器收集具有相同键的元素所得的结果。
- `static <T> Collector<T,?,Long> counting()`  
  生成一个收集器，用于统计已收集元素的数量。
- `static <T> Collector<T,?,Integer> summingInt(ToIntFunction<? super T> mapper)`
- `static <T> Collector<T,?,Long> summingLong(ToLongFunction<? super T> mapper)`
- `static <T> Collector<T,?,Double> summingDouble(ToDoubleFunction<? super T> mapper)`  
  生成一个收集器，用于计算对已收集元素应用 mapper 所得结果的总和。
- `static <T> Collector<T,?,Optional<T>> maxBy(Comparator<? super T> comparator)`
- `static <T> Collector<T,?,Optional<T>> minBy(Comparator<? super T> comparator)`  
  生成一个收集器，用于按 comparator 指定的顺序计算已收集元素的最大值或最小值。
- `static <T,A,R,RR> Collector<T,A,RR> collectingAndThen(Collector<T,A,R> downstream, Function<R,RR> finisher)`  
  生成一个收集器，它把元素发送给下游收集器，然后对其结果应用 finisher 函数。
- `static <T,U,A,R> Collector<T,?,R> mapping(Function<? super T,? extends U> mapper, Collector<? super U,A,R> downstream)`  
  生成一个收集器，它对每个元素调用 mapper，并将结果传递给下游收集器。
- `static <T,U,A,R> Collector<T,?,R> flatMapping(Function<? super T,? extends Stream<? extends U>> mapper, Collector<? super U,A,R> downstream)`  
  生成一个收集器，它对每个元素调用 mapper，并将结果中的元素传递给下游收集器。
- `static <T,A,R> Collector<T,?,R> filtering(Predicate<? super T> predicate, Collector<? super T,A,R> downstream)`  
  生成一个收集器，它把满足 predicate 的元素传递给下游收集器。

## 1.12 归约操作

reduce 方法是一种从流中计算值的通用机制。最简单的形式接收一个二元函数，并从前两个元素开始不断应用它。如果该函数是求和，就很容易解释：

```java
List<Integer> values = ...;
Optional<Integer> sum = values.stream().reduce((x, y) -> x + y);
```

在这种情况下，reduce 方法计算 v₀ ⊕ v₁ ⊕ v₂ ⊕ ...，其中 vᵢ 是流元素。该方法返回 Optional，因为如果流为空，就没有有效结果。

> **注意：** 在这种情况下，可以写 `reduce(Integer::sum)`，而不写 `reduce((x, y) -> x + y)`。

更一般地，可以使用任何将部分结果 x 与下一个值 y 组合以产生新的部分结果的操作。

换一种方式看待归约。给定归约操作 op，归约产生 v₀ op v₁ op v₂ op ...，其中 vᵢ op vᵢ₊₁ 表示函数调用 op(vᵢ, vᵢ₊₁)。实践中可能有很多有用的操作——例如求和、求积、字符串拼接、最大值和最小值、集合的并集或交集。

如果要将归约用于并行流，该操作必须是可结合的：组合元素的顺序不应有影响。用数学记号表示，(x op y) op z 必须等于 x op (y op z)。减法就是不可结合操作的一个例子。例如，(6 − 3) − 2 ≠ 6 − (3 − 2)。

通常存在单位元 e，使得 e op x = x，并且该元素可用作计算的起点。例如，0 是加法的单位元，因此可以使用 reduce 的第二种形式：

```java
List<Integer> values = ...;
Integer sum = values.stream().reduce(0, (x, y) -> x + y);
    // Computes 0 + v₀ + v₁ + v₂ + ...
```

如果流为空，则返回该单位元值，并且不再需要处理 `Optional` 类。

现在假设你有一个对象流，并想对某个属性求和，例如对字符串流中的长度求和。你不能使用 `reduce` 的简单形式。它要求函数 `(T, T) -> T` 的参数和结果类型相同，但在这种情况下有两种类型：流元素的类型是 `String`，而累积结果是整数。`reduce` 有一种形式可以处理这种情况。

首先，提供一个“累加器”函数 `(total, word) -> total + word.length()`。该函数会被反复调用，形成累积总和。但是当计算并行化时，会有多个此类计算，你需要合并它们的结果。为此，提供第二个函数。完整调用如下：

```java
int result = words.reduce(0,
    (total, word) -> total + word.length(),
    (total1, total2) -> total1 + total2);
```

> **注意：** 在实践中，你大概不会大量使用 `reduce` 方法。通常更容易的做法是映射为数字流，并使用其方法之一来计算 `sum`、`maximum` 或 `minimum`。（我们在第 43 页的 13.13 节“基本类型流”中讨论数字流。）在这个特定示例中，你本可以调用 `words.mapToInt(String::length).sum()`，它既更简单又更高效，因为不涉及装箱。

> **注意：** 有时 `reduce` 不够通用。例如，假设你想把结果收集到一个 `BitSet` 中。如果收集过程被并行化，就不能把元素直接放入单个 `BitSet`，因为 `BitSet` 对象不是线程安全的。因此，不能使用 `reduce`。每个分段都需要从自己的空集合开始，而 `reduce` 只允许你提供一个单位元值。这时应改用 `collect`。它接收三个参数：

- 1. 一个供应器，用于创建目标对象的新实例——例如，哈希集合的构造器
- 2. 一个累加器，用于向目标添加元素，例如 add 方法
- 3. 一个组合器，用于将两个对象合并为一个，例如 `addAll`

下面说明 `collect` 方法如何用于位集：

```java
BitSet result = stream.collect(BitSet::new, BitSet::set, BitSet::or);
```

### java.util.stream

- `Optional<T> reduce(BinaryOperator<T> accumulator)`
- `T reduce(T identity, BinaryOperator<T> accumulator)`
- `<U> U reduce(U identity, BiFunction<U, ? super T, U> accumulator, BinaryOperator<U> combiner)`  
  用给定的累加器函数形成流元素的累积总和。如果提供了 identity，则它是第一个被累积的值。如果提供了 combiner，则可用它合并分别累积的各分段总和。
- `<R> R collect(Supplier<R> supplier, BiConsumer<R, ? super T> accumulator, BiConsumer<R, R> combiner)`  
  将元素收集到类型为 R 的结果中。在每个分段上，调用 supplier 提供初始结果，调用 accumulator 以可变方式向其添加元素，并调用 combiner 合并两个结果。

## 1.13 基本类型流

到目前为止，我们一直把整数收集到 `Stream<Integer>` 中，尽管把每个整数包装到包装器对象中显然效率不高。其他基本类型——double、float、long、short、char、byte 和 boolean——也是如此。流库提供了专用类型 `IntStream`、`LongStream` 和 `DoubleStream`，它们直接存储基本类型值，而不使用包装器。如果要存储 short、char、byte 和 boolean，请使用 `IntStream`；对于 float，请使用 `DoubleStream`。

要创建 `IntStream`，请调用 `IntStream.of` 和 `Arrays.stream` 方法：

```java
IntStream stream = IntStream.of(1, 1, 2, 3, 5);
stream = Arrays.stream(values, from, to); // values is an int[] array
```

与对象流一样，你也可以使用静态 generate 和 iterate 方法。此外，`IntStream` 和 `LongStream` 具有静态方法 `range` 和 `rangeClosed`，它们生成步长为 1 的整数范围：

```java
IntStream zeroToNinetyNine = IntStream.range(0, 100); // Upper bound is excluded
IntStream zeroToHundred = IntStream.rangeClosed(0, 100); // Upper bound is included
```

`CharSequence` 接口具有方法 `codePoints` 和 `chars`，它们生成一个 `IntStream`，其中包含字符的 Unicode 码点或 UTF-16 编码中的代码单元。（有关这些繁琐细节，请参见第 1 章。）

```java
String sentence = "\uD835\uDD46 is the set of options.";
    // \uD835\uDD46 is the letter 𝔒, Unicode U+1D546

IntStream codes = sentence.codePoints();
    // The stream with hex values 1D546 20 69 73 20 . . .
```




当你有一个对象流时，可以使用 `mapToInt`、`mapToLong` 或 `mapToDouble` 方法将其转换为基本类型流。例如，如果你有一个字符串流，并希望将其长度作为整数处理，不妨在 `IntStream` 中完成：

```
Stream<String> words = ...;
IntStream lengths = words.mapToInt(String::length);
```

要将基本类型流转换为对象流，请使用 `boxed` 方法：

```
Stream<Integer> integers = IntStream.range(0, 100).boxed();
```

通常，基本类型流上的方法与对象流上的方法类似。以下是最显著的差异：

- toArray 方法返回基本类型数组。
- 产生可选结果的方法返回 `OptionalInt`、`OptionalLong` 或 `OptionalDouble`。这些类与 `Optional` 类类似，但它们用 `getAsInt`、`getAsLong` 和 `getAsDouble` 方法代替了 `get` 方法。
- 有 `sum`、`average`、`max` 和 `min` 方法，分别返回总和、平均值、最大值和最小值。这些方法未在对象流上定义。
- `summaryStatistics` 方法生成一个 `IntSummaryStatistics`、`LongSummaryStatistics` 或 `DoubleSummaryStatistics` 类型的对象，该对象可以同时报告流的总和、计数、平均值、最大值和最小值。

> **注意：** `Random` 类有 `ints`、`longs` 和 `doubles` 方法，它们返回随机数的基本类型流。如果你需要在并行流中使用随机数，请改用 `SplittableRandom` 类。

程序清单 1.7 中的程序给出了基本类型流 API 的示例。

```
Listing 1.7 streams/PrimitiveTypeStreams.java

1 package streams;
2
3 /**
4  * @version 1.01 2018-05-01
5  * @author Cay Horstmann
6  */
7
8 import java.io.IOException;
9 import java.nio.charset.StandardCharsets;
10 import java.nio.file.Files;
11 import java.nio.file.Path;
12 import java.nio.file.Paths;
13 import java.util.stream.Collectors;
14 import java.util.stream.IntStream;
15 import java.util.stream.Stream;
16
17 public class PrimitiveTypeStreams
18 {
19     public static void show(String title, IntStream stream)
20     {
21         final int SIZE = 10;
22         int[] firstElements = stream.limit(SIZE + 1).toArray();
23         System.out.print(title + " : ");
24         for (int i = 0; i < firstElements.length; i++)
25         {
26             if (i > 0) System.out.print(", ");
27             if (i < SIZE) System.out.print(firstElements[i]);
28             else System.out.print("...");
29         }
30         System.out.println();
31     }
32
33     public static void main(String[] args) throws IOException
34     {
35         IntStream is1 = IntStream.generate(() -> (int) (Math.random() * 100));
36         show("is1", is1);
37         IntStream is2 = IntStream.range(5, 10);
38         show("is2", is2);
39         IntStream is3 = IntStream.rangeClosed(5, 10);
40         show("is3", is3);
41
42         Path path = Paths.get("../gutenberg/alice30.txt");
43         var contents = Files.readString(path);
44
45         Stream<String> words = Stream.of(contents.split("\\PL+"));
46         IntStream is4 = words.mapToInt(String::length);
47         show("is4", is4);
48         var sentence = "\uD835\uDD46 is the set of octonions.";
49         System.out.println(sentence);
50         IntStream codes = sentence.codePoints();
51         System.out.println(codes.mapToObj(c -> String.format("%X ", c)).collect(
52             Collectors.joining()));
53
54         Stream<Integer> integers = IntStream.range(0, 100).boxed();
55         IntStream is5 = integers.mapToInt(Integer::intValue);
56         show("is5", is5);
57     }
58 }
```

### java.util.stream.IntStream 8

- `static IntStream range(int startInclusive, int endExclusive)`
- `static IntStream rangeClosed(int startInclusive, int endInclusive)`
  生成一个包含给定范围内整数的 `IntStream`。
- `static IntStream of(int... values)`
  生成一个包含给定元素的 `IntStream`。
- `int[] toArray()`
  生成一个包含此流中元素的数组。
- `int sum()`
- `OptionalDouble average()`
- `OptionalInt max()`
- `OptionalInt min()`
- `IntSummaryStatistics summaryStatistics()`
  生成此流中元素的总和、计数、平均值、最大值和最小值，或生成一个可从中获取这五个值的对象。
- `Stream<Integer> boxed()`
  生成此流中元素的包装对象流。

### java.util.stream.LongStream 8

- `static LongStream range(long startInclusive, long endExclusive)`
- `static LongStream rangeClosed(long startInclusive, long endInclusive)`
  生成一个包含给定范围内整数的 `LongStream`。
- `static LongStream of(long... values)`
  生成一个包含给定元素的 `LongStream`。
- `long[] toArray()`
  生成一个包含此流中元素的数组。
- `long sum()`
- `OptionalDouble average()`
- `OptionalLong max()`
- `OptionalLong min()`
- `LongSummaryStatistics summaryStatistics()`
  生成此流中元素的总和、计数、平均值、最大值和最小值，或生成一个可从中获取这五个值的对象。
- `Stream<Long> boxed()`
  生成此流中元素的包装对象流。

### java.util.stream.DoubleStream 8

| 方法 | 描述 |
| --- | --- |
| `static DoubleStream of(double... values)` | 生成一个包含给定元素的 `DoubleStream`。 |
| `double[] toArray()` | 生成一个包含此流中元素的数组。 |
| `double sum()` | |
| `OptionalDouble average()` | |
| `OptionalDouble max()` | |
| `OptionalDouble min()` | |
| `DoubleSummaryStatistics summaryStatistics()` | 生成此流中元素的总和、计数、平均值、最大值和最小值，或生成一个可从中获取这五个值的对象。 |
| `Stream<Double> boxed()` | 生成此流中元素的包装对象流。 |

### java.lang.CharSequence 1.0

| 方法 | 起始版本 | 描述 |
| --- | --- | --- |
| `IntStream codePoints()` | 8 | 生成此字符串所有 Unicode 代码点的流。 |

### java.util.Random 1.0

| 方法 | 起始版本 |
| --- | --- |
| `IntStream ints()` | 8 |
| `IntStream ints(int randomNumberOrigin, int randomNumberBound)` | 8 |
| `IntStream ints(long streamSize)` | 8 |
| `IntStream ints(long streamSize, int randomNumberOrigin, int randomNumberBound)` | 8 |
| `LongStream longs()` | 8 |
| `LongStream longs(long randomNumberOrigin, long randomNumberBound)` | 8 |
| `LongStream longs(long streamSize)` | 8 |
| `LongStream longs(long streamSize, long randomNumberOrigin, long randomNumberBound)` | 8 |
| `DoubleStream doubles()` | 8 |
| `DoubleStream doubles(double randomNumberOrigin, double randomNumberBound)` | 8 |
| `DoubleStream doubles(long streamSize)` | 8 |
| `DoubleStream doubles(long streamSize, double randomNumberOrigin, double randomNumberBound)` | 8 |

生成随机数流。如果提供了 `streamSize`，则该流是有限的，包含给定数量的元素。如果提供了边界，则元素位于 `randomNumberOrigin`（包含）和 `randomNumberBound`（不包含）之间。

### java.util.Optional<Int|Long|Double> 8

- `static Optional<Int|Long|Double> of((int|long|double) value)`
  生成一个带有提供的基本类型值的可选对象。
- `(int|long|double) getAs(Int|Long|Double)()`
  生成此可选对象的值；如果为空，则抛出 `NoSuchElementException`。
- `(int|long|double) orElse((int|long|double) other)`
- `(int|long|double) orElseGet((Int|Long|Double)Supplier other)`
  生成此可选对象的值；如果此对象为空，则生成替代值。
- `void ifPresent((Int|Long|Double)Consumer consumer)`
  如果此可选对象不为空，则将其值传递给 consumer。

### java.util.(Int|Long|Double)SummaryStatistics 8

- `long getCount()`
- `(int|long|double) getSum()`
- `double getAverage()`
- `(int|long|double) getMax()`
- `(int|long|double) getMin()`
  生成已收集元素的计数、总和、平均值、最大值和最小值。

## 1.14 并行流

流使批量操作的并行化变得容易。这个过程大多是自动的，但你需要遵循一些规则。首先，你必须有一个并行流。你可以使用 `Collection.parallelStream()` 方法从任何集合获取并行流：

```
Stream<String> parallelWords = words.parallelStream();
```

此外，parallel 方法可将任何顺序流转换为并行流。

```
Stream<String> parallelWords = Stream.of(wordArray).parallel();
```

只要在终端方法执行时流处于并行模式，所有中间流操作都将被并行化。



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




*此页有意留空*

# 第 2 章 输入与输出

## 本章内容

- 2.1 输入/输出流，第 56 页
- 2.2 读写二进制数据，第 78 页
- 2.3 对象输入/输出流与序列化，第 88 页
- 2.4 文件操作，第 109 页
- 2.5 内存映射文件，第 124 页
- 2.6 文件锁定，第 134 页
- 2.7 正则表达式，第 137 页

在本章中，我们将介绍 Java 应用程序编程接口（API）中的输入与输出部分。你将学习如何访问文件和目录，以及如何以二进制和文本格式读写数据。本章还会向你展示对象序列化机制，借助该机制，你可以像存储文本或数值数据一样轻松地存储对象。接下来，我们将讨论文件和目录的操作。最后，我们以正则表达式的讨论结束本章，尽管正则表达式实际上与输入和输出无关。我们找不到更合适的位置来介绍这一主题，显然 Java 团队也是如此——正则表达式 API 规范被附加到了“新 I/O”功能的规范请求中。

## 2.1 输入/输出流

在 Java API 中，我们可以从中读取字节序列的对象称为输入流。可以向其写入字节序列的对象称为输出流。这些字节序列的来源和目的地可以是——而且通常是——文件，但也可以是网络连接，甚至可以是内存块。抽象类 `InputStream` 和 `OutputStream` 是输入/输出（I/O）类层次结构的基础。

> **注意：** 这些输入/输出流与你在前一章中看到的流无关。为清晰起见，在讨论用于输入和输出的流时，我们将使用术语输入流、输出流或输入/输出流。

面向字节的输入/输出流在处理以 Unicode 存储的信息时很不方便（回忆一下，Unicode 中每个字符使用多个字节）。因此，另一个独立的层次结构提供了继承自抽象类 `Reader` 和 `Writer` 的类，用于处理 Unicode 字符。这些类的读写操作基于双字节的 `char` 值（即 UTF-16 代码单元），而不是字节值。

### 2.1.1 读取和写入字节

`InputStream` 类有一个抽象方法：

```
abstract int read()
```

该方法读取一个字节并返回所读取的字节，如果遇到输入源的末尾则返回 -1。具体输入流类的设计者会重写此方法以提供有用的功能。例如，在 `FileInputStream` 类中，此方法从文件读取一个字节。`System.in` 是 `InputStream` 子类的一个预定义对象，它允许你从“标准输入”（即控制台或重定向的文件）读取信息。

`InputStream` 类还有一些非抽象方法，用于读取字节数组或跳过一定数量的字节。自 Java 9 起，有一个非常有用的方法可以读取流中的所有字节：

```
byte[] bytes = in.readAllBytes();
```

还有一些方法用于读取给定数量的字节——参见 API 说明。

这些方法会调用抽象的 `read` 方法，因此子类只需重写一个方法。

类似地，`OutputStream` 类定义了抽象方法

```
abstract void write(int b)
```

该方法将一字节写入输出位置。

如果你有一个字节数组，可以一次性全部写出：

```
byte[] values = ...;
out.write(values);
```

`transferTo` 方法将输入流中的所有字节传输到输出流：

```
in.transferTo(out);
```

`read` 和 `write` 方法都会阻塞，直到字节被实际读取或写入。这意味着，如果输入流无法立即访问（通常是因为网络连接繁忙），当前线程就会阻塞。这给了其他线程在方法等待输入流再次可用时执行有用工作的机会。

`available` 方法允许你检查当前可用于读取的字节数。这意味着像下面这样的代码片段不太可能阻塞：

```
int bytesAvailable = in.available();
if (bytesAvailable > 0)
{
    var data = new byte[bytesAvailable];
    in.read(data);
}
```

当你完成对输入/输出流的读取或写入后，应通过调用 `close` 方法将其关闭。该调用会释放供应有限的操作系统资源。如果应用程序打开太多输入/输出流而不关闭，系统资源可能会耗尽。关闭输出流还会*刷新*输出流所使用的缓冲区：任何为了以更大数据包形式发送而临时放置在缓冲区中的字节都会被送出。特别是，如果你不关闭文件，最后的数据包可能永远不会被发送。你也可以使用 `flush` 方法手动刷新输出。

即使输入/输出流类提供了与原始读写功能相关的具体方法，应用程序程序员也很少使用它们。你感兴趣的数据很可能包含数字、字符串和对象，而不是原始字节。

除了处理字节之外，你还可以使用许多建立在基本 `InputStream` 和 `OutputStream` 类之上的输入/输出类。

#### `java.io.InputStream` 1.0

- `abstract int read()`  
  读取一个字节的数据并返回所读取的字节；在输入流末尾返回 -1。

- `int read(byte[] b)`  
  读入字节数组并返回实际读取的字节数，在输入流末尾返回 -1；此方法最多读取 `b.length` 字节。

- `int read(byte[] b, int off, int len)`
- `int readNBytes(byte[] b, int off, int len)`  
  读取最多 `len` 字节，如果可用则不阻塞（`read`），或阻塞直到所有值都被读取（`readNBytes`）。值从 `off` 位置开始放入 `b`。返回实际读取的字节数，在输入流末尾返回 -1。

- `byte[] readAllBytes()`  
  返回一个包含从此流中可读取的所有字节的数组。

- `long transferTo(OutputStream out)`  
  将此输入流中的所有字节传输到给定的输出流，返回传输的字节数。两个流都不会被关闭。

- `long skip(long n)`  
  在输入流中跳过 `n` 字节，返回实际跳过的字节数（如果遇到输入流末尾，可能小于 `n`）。

- `int available()`  
  返回在不阻塞的情况下可用的字节数（回忆一下，阻塞意味着当前线程失去执行机会）。

- `void close()`  
  关闭输入流。

- `void mark(int readlimit)`  
  在输入流的当前位置放置一个标记（并非所有流都支持此功能）。如果从输入流读取的字节数超过 `readlimit`，则允许流忘记该标记。

- `void reset()`  
  返回到最后一个标记。后续对 `read` 的调用将重新读取这些字节。如果当前没有标记，则输入流不会被重置。

- `boolean markSupported()`  
  如果输入流支持标记，则返回 true。

#### `java.io.OutputStream` 1.0

| 方法 | 说明 |
|---|---|
| `abstract void write(int b)` | 写入一个字节的数据。 |
| `void write(byte[] b)` |  |
| `void write(byte[] b, int off, int len)` | 写入数组 `b` 中的所有字节，或从 `off` 开始的 `len` 个字节。 |
| `void close()` | 刷新并关闭输出流。 |
| `void flush()` | 刷新输出流——即将任何缓冲数据发送到其目的地。 |

### 2.1.2 完整的流动物园

与仅使用单一类型 `FILE*` 就能很好工作的 C 语言不同，Java 拥有一个包含超过 60 种不同输入/输出流类型的庞大动物园（见图 2.1 和图 2.2）。

让我们根据用途来划分输入/输出流动物园中的动物。处理字节和字符的类有各自的层次结构。如你所见，`InputStream` 和 `OutputStream` 类允许你读写单个字节和字节数组。这些类构成了图 2.1 所示层次结构的基础。为了读写字符串和数字，你需要功能更强的子类。例如，`DataInputStream` 和 `DataOutputStream` 允许你以二进制格式读写所有 Java 基本类型。最后，还有一些输入/输出流具有实用功能；例如，`ZipInputStream` 和 `ZipOutputStream` 允许你以常见的 ZIP 压缩格式读写文件。

另一方面，对于 Unicode 文本，你可以使用抽象类 `Reader` 和 `Writer` 的子类（见图 2.2）。`Reader` 和 `Writer` 类的基本方法与 `InputStream` 和 `OutputStream` 类似。

```
abstract int read()
abstract void write(int c)
```

`read` 方法要么返回一个 UTF-16 代码单元（作为 0 到 65535 之间的整数），要么在到达文件末尾时返回 -1。`write` 方法以一个 Unicode 代码单元作为参数调用。（关于 Unicode 代码单元的讨论，参见卷 I 第 3 章。）

还有四个附加接口：`Closeable`、`Flushable`、`Readable` 和 `Appendable`（见图 2.3）。前两个接口非常简单，带有一个方法：

```
void close() throws IOException
```




![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_82_0.png)

**图 2.1** 输入流和输出流层次结构

以及

```java
void flush()
```

分别。InputStream、OutputStream、Reader 和 Writer 类都实现了 Closeable 接口。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_83_0.png)

**图 2.2** Reader 和 Writer 层次结构

> **注意：** java.io.Closeable 接口扩展了 java.lang.AutoCloseable 接口。因此，可以对任何 Closeable 使用 try-with-resources 语句。为什么有两个接口？Closeable 接口的 close 方法只抛出 IOException，而 AutoCloseable.close 方法可能抛出任何异常。

OutputStream 和 Writer 实现了 Flushable 接口。

Readable 接口只有一个方法

```java
int read(CharBuffer cb)
```

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_84_0.png)

**图 2.3** Closeable、Flushable、Readable 和 Appendable 接口

CharBuffer 类具有用于顺序和随机读/写访问的方法。它表示内存缓冲区或内存映射文件。（详见第 132 页的 2.5.2 节“缓冲区数据结构”。）

Appendable 接口有两个方法，用于追加单个字符和字符序列：

```java
Appendable append(char c)
Appendable append(CharSequence s)
```

CharSequence 接口描述 char 值序列的基本属性。它由 String、CharBuffer、StringBuilder 和 StringBuffer 实现。

在输入/输出流类中，只有 Writer 实现了 Appendable。

| `java.io.Closeable` | 5.0 |
|---|---|
| • `void close()` | 关闭此 Closeable。此方法可能抛出 IOException。 |

| `java.io.Flushable` | 5.0 |
|---|---|
| • `void flush()` | 刷新此 Flushable。 |

| `java.lang.Readable` | 5.0 |
|---|---|
| • `int read(CharBuffer cb)` | 尝试将尽可能多的 char 值读入 cb，直至达到其可容纳的数量。返回读取的值的数量；如果此 Readable 中没有更多可用值，则返回 -1。 |

| `java.lang.Appendable` | 5.0 |
|---|---|
| • `Appendable append(char c)`<br>• `Appendable append(CharSequence cs)` | 将给定代码单元，或给定序列中的所有代码单元，追加到此 Appendable；返回此对象。 |

| `java.lang.CharSequence` | 1.4 |
|---|---|
| • `char charAt(int index)` | 返回给定索引处的代码单元。 |
| • `int length()` | 返回此序列中的代码单元数量。 |
| • `CharSequence subSequence(int startIndex, int endIndex)` | 返回一个 CharSequence，由从索引 startIndex 到 endIndex - 1 存储的代码单元组成。 |
| • `String toString()` | 返回一个由此序列的代码单元组成的字符串。 |

### 2.1.3 组合输入/输出流过滤器

FileInputStream 和 FileOutputStream 为你提供附加到磁盘文件的输入流和输出流。需要将文件的文件名或完整路径名传递给构造函数。例如，

```java
var fin = new FileInputStream("employee.dat");
```

会在用户目录中查找名为 employee.dat 的文件。

> **提示：** java.io 中的所有类都将相对路径名解释为从用户的工作目录开始。可以通过调用 System.getProperty("user.dir") 获取此目录。

> **警告：** 由于反斜杠字符是 Java 字符串中的转义字符，请务必对 Windows 风格的路径名使用 `\\`（例如 `C:\\Windows\\win.ini`）。在 Windows 中，也可以使用单个正斜杠（`C:/Windows/win.ini`），因为大多数 Windows 文件处理系统调用会将正斜杠解释为文件分隔符。但是，不建议这样做——Windows 系统函数的行为可能会发生变化。对于可移植程序，应使用程序运行所在平台的文件分隔符字符。它可作为常量字符串 `java.io.File.separator` 使用。

与抽象 InputStream 和 OutputStream 类一样，这些类只支持在字节级别进行读写。也就是说，我们只能从对象 fin 中读取字节和字节数组。

```java
byte b = (byte) fin.read();
```

正如你将在下一节看到的，如果我们只有 DataInputStream，就可以读取数值类型：

```java
DataInputStream din = ...;
double x = din.readDouble();
```

但是，正如 FileInputStream 没有读取数值类型的方法一样，DataInputStream 也没有从文件获取数据的方法。

Java 使用一种巧妙的机制来分离两类职责。某些输入流（例如 FileInputStream 以及 URL 类的 openStream 方法返回的输入流）可以从文件和其他更奇特的位置获取字节。其他输入流（例如 DataInputStream）可以将字节组装成更有用的数据类型。Java 程序员必须将两者组合起来。例如，为了能够从文件读取数字，首先创建一个 FileInputStream，然后将其传递给 DataInputStream 的构造函数。

```java
var fin = new FileInputStream("employee.dat");
var din = new DataInputStream(fin);
double x = din.readDouble();
```

如果再次查看图 2.1，可以看到 FilterInputStream 和 FilterOutputStream 类。这些类的子类用于为处理字节的输入/输出流添加功能。

可以通过嵌套过滤器来添加多种功能。例如，默认情况下，输入流不带缓冲。也就是说，每次调用 read 都会要求操作系统再分配一个字节。更高效的做法是改为请求数据块并将其存储在缓冲区中。如果希望为文件同时提供缓冲*和*数据输入方法，请使用下面这个相当复杂的构造函数序列：

```java
var din = new DataInputStream(
    new BufferedInputStream(
        new FileInputStream("employee.dat")));
```

请注意，我们将 DataInputStream 放在构造函数链的*最后*，因为我们要使用 DataInputStream 的方法，并且希望*这些方法*使用带缓冲的读取方法。

有时在将中间输入流链接在一起时，需要跟踪它们。例如，读取输入时，通常需要查看下一个字节，以判断它是否是你期望的值。Java 为此提供了 PushbackInputStream。

```java
var pbin = new PushbackInputStream(
    new BufferedInputStream(
        new FileInputStream("employee.dat")));
```

现在可以试探性地读取下一个字节

```java
int b = pbin.read();
```

如果不是想要的值，就将其推回。

```java
if (b != '<') pbin.unread(b);
```

但是，读取和推回是适用于回推输入流的*唯一*方法。如果希望向前查看并同时读取数字，则需要同时拥有回推输入流和数据输入流引用。

```java
var pbin = new PushbackInputStream(
    new BufferedInputStream(
        new FileInputStream("employee.dat")));
var din = new DataInputStream(pbin);
```

当然，在其他编程语言的输入/输出库中，缓冲和前瞻等便利功能会自动处理——因此在 Java 中不得不组合流过滤器会有些麻烦。然而，混合和匹配过滤器类以构造有用的序列的能力

#### java.io.FileOutputStream 1.0

- `FileOutputStream(String name)`
- `FileOutputStream(String name, boolean append)`
- `FileOutputStream(File file)`
- `FileOutputStream(File file, boolean append)`

创建一个由名称字符串或文件对象指定的新文件输出流。（`File` 类将在本章末尾描述。）如果 `append` 参数为 true，则不会删除具有相同名称的现有文件，并且数据将添加到文件末尾。否则，此方法会删除任何具有相同名称的现有文件。

#### java.io.BufferedInputStream 1.0

- `BufferedInputStream(InputStream in)`

创建一个缓冲输入流。缓冲输入流从流中读取字节，而不会每次都引起设备访问。当缓冲区为空时，会将新的数据块读入缓冲区。

#### java.io.BufferedOutputStream 1.0

- `BufferedOutputStream(OutputStream out)`

创建一个缓冲输出流。缓冲输出流收集要写入的字节，而不会每次都引起设备访问。当缓冲区填满或流被刷新时，数据会被写出。

#### java.io.PushbackInputStream 1.0

- `PushbackInputStream(InputStream in)`
- `PushbackInputStream(InputStream in, int size)`

构造一个具有一字节前瞻或指定大小的回推缓冲区的输入流。

- `void unread(int b)`

推回一个字节，该字节将在下一次调用 `read` 时再次被取回。



### 2.1.4 文本输入与输出

保存数据时，你可以在二进制格式和文本格式之间选择。例如，如果整数 1234 以二进制保存，它会写成字节序列 `00 00 04 D2`（十六进制表示法）。在文本格式中，它保存为字符串 "1234"。尽管二进制 I/O 快速高效，但人类不易阅读。我们首先讨论文本 I/O，并在第 78 页的 2.2 节“读写二进制数据”中介绍二进制 I/O。

保存文本字符串时，你需要考虑*字符编码*。在 Java 内部使用的 UTF-16 编码中，字符串 "José" 被编码为 `00 4A 00 6F 00 73 00 E9`（十六进制）。然而，许多程序期望文本文件使用不同的编码。在互联网上最常用的 UTF-8 编码中，该字符串会写成 `4A 6F 73 C3 A9`，前三个字母没有零字节，而 é 字符占两个字节。

`OutputStreamWriter` 类使用选定的字符编码，将 Unicode 码元输出流转换为字节流。相反，`InputStreamReader` 类将包含字节（按某种字符编码表示字符）的输入流转换为发出 Unicode 码元的读取器。

例如，下面展示了如何创建一个从控制台读取按键并将其转换为 Unicode 的输入读取器：

```
var in = new InputStreamReader(System.in);
```

这个输入流读取器假定使用宿主系统的默认字符编码。在桌面操作系统上，这可能是 Windows 1252 或 MacRoman 之类的陈旧编码。你应该始终在 InputStreamReader 的构造函数中选择特定编码，例如：

```
var in = new InputStreamReader(new FileInputStream("data.txt"), StandardCharsets.UTF_8);
```

有关字符编码的更多信息，请参见第 75 页的 2.1.8 节“字符编码”。

Reader 和 Writer 类只有读写单个字符的基本方法。与流一样，你使用子类来处理字符串和数字。

### 2.1.5 如何写出文本输出

对于文本输出，请使用 PrintWriter。该类具有以文本格式打印字符串和数字的方法。为了打印到文件，请用文件名和字符编码构造 PrintWriter：

```
var out = new PrintWriter("employee.txt", StandardCharsets.UTF_8);
```

要写入打印写入器，请使用与 System.out 相同的 print、println 和 printf 方法。你可以使用这些方法打印数字（int、short、long、float、double）、字符、布尔值、字符串和对象。

例如，考虑以下代码：

```
    String name = "Harry Hacker";
    double salary = 75000;
    out.print(name);
    out.print(' ');
    out.println(salary);
```

这会写出字符

```
    Harry Hacker 75000.0
```

到写入器 out。然后这些字符被转换为字节，并最终进入文件 employee.txt。

println 方法会为目标系统（Windows 上为 "\r\n"，UNIX 上为 "\n"）向该行添加正确的行尾字符。该字符串通过调用 System.getProperty("line.separator") 获得。

如果写入器设置为自动刷新模式，则每当调用 println 时，缓冲区中的所有字符都会发送到其目的地。（打印写入器始终是缓冲的。）默认情况下，未启用自动刷新。你可以使用 PrintWriter(Writer writer, boolean autoFlush) 构造函数启用或禁用自动刷新：

```
    var out = new PrintWriter(
        new OutputStreamWriter(
            new FileOutputStream("employee.txt"), StandardCharsets.UTF_8),
        true); // autoflush
```

print 方法不会抛出异常。你可以调用 checkError 方法查看输出流是否出了问题。

> **注意：** Java 老手可能会想，PrintStream 类和 System.out 到底发生了什么。在 Java 1.0 中，PrintStream 类只是通过丢弃最高字节将所有 Unicode 字符截断为 ASCII 字符。（当时，Unicode 仍是 16 位编码。）显然，这不是一种干净或可移植的方法，Java 1.1 引入读取器和写入器后修复了这个问题。为了与现有代码兼容，System.in、System.out 和 System.err 仍然是输入/输出流，而不是读取器和写入器。但现在 PrintStream 类会像 PrintWriter 那样在内部将 Unicode 字符转换为宿主默认编码。使用 print 和 println 方法时，PrintStream 类型的对象的行为与打印写入器完全相同，但与打印写入器不同的是，它们允许你用 write(int) 和 write(byte[]) 方法输出原始字节。

| `java.io.PrintWriter` | 1.1 |
|---|---|
| • `PrintWriter(OutputStream out)`<br>• `PrintWriter(Writer writer)` | 创建一个写入给定输出流或写入器的新 PrintWriter。 |
| • `PrintWriter(String filename, String encoding)`<br>• `PrintWriter(File file, String encoding)` | 创建一个使用给定字符编码写入给定文件的新 PrintWriter。 |
| • `void print(Object obj)` | 通过打印由 `toString` 产生的字符串来打印对象。 |
| • `void print(String s)` | 打印包含 Unicode 码元的字符串。 |
| • `void println(String s)` | 打印字符串后跟行终止符。如果处于自动刷新模式，则刷新输出流。 |
| • `void print(char[] s)` | 打印给定数组中的所有 Unicode 码元。 |
| • `void print(char c)` | 打印一个 Unicode 码元。 |
| • `void print(int i)`<br>• `void print(long l)`<br>• `void print(float f)`<br>• `void print(double d)`<br>• `void print(boolean b)` | 以文本格式打印给定值。 |
| • `void printf(String format, Object... args)` | 按格式字符串的指定打印给定值。有关格式字符串的规范，请参见第一卷第三章。 |
| • `boolean checkError()` | 如果发生格式化或输出错误，则返回 true。一旦输出流遇到错误，它就会受到污染，并且所有对 `checkError` 的调用都会返回 true。 |

### 2.1.6 如何读取文本输入

处理任意文本的最简单方法是使用我们在第一卷中大量使用的 Scanner 类。你可以从任何输入流构造 Scanner。

如今，`BufferedReader` 类还有一个 `lines` 方法，可生成一个 `Stream<String>`。然而，与 `Scanner` 不同，`BufferedReader` 没有读取数字的方法。

### 2.1.7 以文本格式保存对象

在本节中，我们将带你完成一个示例程序，该程序将 Employee 记录数组存储到文本文件中。每条记录存储在单独的一行中。实例字段之间用分隔符分隔。我们使用竖线（`|`）作为分隔符。冒号（`:`）是另一种常见选择。有趣的是，每个人都使用不同的分隔符。当然，我们回避了这样一个问题：如果我们要保存的某个字符串中实际出现了 `|`，可能会发生什么。

下面是一组示例记录：

```
Harry Hacker|35500|1989-10-01
Carl Cracker|75000|1987-12-15
Tony Tester|38000|1990-03-15
```

写入记录很简单。由于我们写入文本文件，因此使用 `PrintWriter` 类。我们只需写出所有字段，后面跟一个 `|`，或者对于最后一个字段，跟一个换行符。这项工作在下面添加到 Employee 类中的 `writeEmployee` 方法中完成：

```
public static void writeEmployee(PrintWriter out, Employee e)
{
    out.println(e.getName() + "|" + e.getSalary() + "|" + e.getHireDay());
}
```

要读取记录，我们一次读取一行并分隔字段。我们使用扫描器读取每一行，然后用 `String.split` 方法将该行拆分为标记。

```
public static Employee readEmployee(Scanner in)
{
    String line = in.nextLine();
    String[] tokens = line.split("\\|");
    String name = tokens[0];
    double salary = Double.parseDouble(tokens[1]);
    LocalDate hireDate = LocalDate.parse(tokens[2]);
    int year = hireDate.getYear();
    int month = hireDate.getMonthValue();
    int day = hireDate.getDayOfMonth();
    return new Employee(name, salary, year, month, day);
}
```

`split` 方法的参数是描述分隔符的正则表达式。我们将在本章末尾更详细地讨论正则表达式。碰巧的是，竖线字符在

正则表达式，因此需要用`\`字符进行转义。该字符又需要被另一个`\`转义，从而得到`"\\"`表达式。

完整的程序见清单2.1。静态方法

```java
void writeData(Employee[] e, PrintWriter out)
```

首先写入数组的长度，然后写入每条记录。静态方法

```java
Employee[] readData(Scanner in)
```

首先读入数组的长度，然后读入每条记录。这里有一点棘手：

```java
int n = in.nextInt();
in.nextLine(); // consume newline
var employees = new Employee[n];
for (int i = 0; i < n; i++)
{
   employees[i] = new Employee();
   employees[i].readData(in);
}
```

对`nextInt`的调用会读取数组长度，但不会读取末尾的换行符。我们必须消耗这个换行符，以便`readData`方法在调用`nextLine`方法时能够获得下一行输入。

#### 清单2.1 textFile/TextFileTest.java

```java
package textFile;

import java.io.*;
import java.nio.charset.*;
import java.time.*;
import java.util.*;

/**
 * @version 1.15 2018-03-17
 * @author Cay Horstmann
 */
public class TextFileTest
{
    public static void main(String[] args) throws IOException
    {
        var staff = new Employee[3];

        staff[0] = new Employee("Carl Cracker", 75000, 1987, 12, 15);
        staff[1] = new Employee("Harry Hacker", 50000, 1989, 10, 1);
        staff[2] = new Employee("Tony Tester", 40000, 1990, 3, 15);

        // save all employee records to the file employee.dat
        try (var out = new PrintWriter("employee.dat", StandardCharsets.UTF_8))
        {
            writeData(staff, out);
        }

        // retrieve all records into a new array
        try (var in = new Scanner(
                new FileInputStream("employee.dat"), "UTF-8"))
        {
            Employee[] newStaff = readData(in);

            // print the read employee records
            for (Employee e : newStaff)
                System.out.println(e);
        }
    }

    /**
     * Writes all employees in an array to a print writer
     * @param employees an array of employees
     * @param out a print writer
     */
    private static void writeData(Employee[] employees, PrintWriter out)
            throws IOException
    {
        // write number of employees
        out.println(employees.length);

        for (Employee e : employees)
            writeEmployee(out, e);
    }

    /**
     * Reads an array of employees from a scanner
     * @param in the scanner
     * @return the array of employees
     */
    private static Employee[] readData(Scanner in)
    {
        // retrieve the array size
        int n = in.nextInt();
        in.nextLine(); // consume newline

        var employees = new Employee[n];
        for (int i = 0; i < n; i++)
        {
            employees[i] = readEmployee(in);
        }
        return employees;
    }

    /**
     * Writes employee data to a print writer
     * @param out the print writer
     */
    public static void writeEmployee(PrintWriter out, Employee e)
    {
        out.println(e.getName() + "|" + e.getSalary() + "|" + e.getHireDay());
    }

    /**
     * Reads employee data from a buffered reader
     * @param in the scanner
     */
    public static Employee readEmployee(Scanner in)
    {
        String line = in.nextLine();
        String[] tokens = line.split("\\|");
        String name = tokens[0];
        double salary = Double.parseDouble(tokens[1]);
        LocalDate hireDate = LocalDate.parse(tokens[2]);
        int year = hireDate.getYear();
        int month = hireDate.getMonthValue();
        int day = hireDate.getDayOfMonth();
        return new Employee(name, salary, year, month, day);
    }
}
```

### 2.1.8 字符编码

输入和输出流用于处理字节序列，但在许多情况下，你要处理的是文本——即字符序列。这时，字符如何编码为字节就很重要了。

Java使用Unicode标准来表示字符。每个字符（或“码点”）都有一个21位的整数。存在不同的*字符编码*——将这些21位数字打包成字节的方法。

最常见的编码是UTF-8，它将每个Unicode码点编码为一到四个字节的序列（见表2.1）。UTF-8的优点在于，传统ASCII字符集（包含英语中使用的所有字符）中的每个字符只需占用一个字节。

#### 表2.1 UTF-8编码

| 字符范围 | 编码 |
|---|---|
| `0...7F` | `0xxxxxxx` |
| `80...7FF` | `110xxxxx 10xxxxxx` |
| `800...FFFF` | `1110xxxx 10xxxxxx 10xxxxxx` |
| `10000...10FFFF` | `11110xxx 10xxxxxx 10xxxxxx 10xxxxxx` |

另一种常见编码是UTF-16，它将每个Unicode码点编码为一个或两个16位值（见表2.2）。这也是Java字符串中使用的编码。实际上，UTF-16有两种形式，称为“大端”和“小端”。考虑16位值0x2122。在大端格式中，较重要的字节在前：0x21后跟0x22。在小端格式中，顺序相反：0x22 0x21。为了指示使用的是哪一种，文件可以以“字节顺序标记”开头，即16位量0xFEFF。读取器可以使用该值来确定字节顺序，然后将其丢弃。

#### 表2.2 UTF-16编码

| 字符范围 | 编码 |
|---|---|
| `0...FFFF` | `xxxxxxxxxxxxxxxx` |
| `10000...10FFFF` | `110110xxxxxxxxxx 110111xxxxxxxxxx` 其中 `xxxxxxxxxxxx = xxxxxxxxxxxxxxxx - 1` |

> **警告：** 有些程序（包括微软记事本）会在UTF-8编码文件的开头添加字节顺序标记。显然，这没有必要，因为UTF-8中不存在字节顺序问题。但Unicode标准允许这样做，甚至建议这是一个很好的做法，因为它使编码变得毫无疑问。在读取UTF-8编码文件时，这个标记应当被移除。遗憾的是，Java并不这样做，而针对此问题的错误报告也被以“不会修复”为由关闭。最好的办法是，去除你在输入中发现的任何前导\uFEFF。

除了UTF编码之外，还有一些部分编码，它们覆盖适合特定用户群体的字符范围。例如，ISO 8859-1是一种单字节编码，包含西欧语言中使用的带重音字符。Shift-JIS是一种用于日文字符的可变长度编码。其中大量编码至今仍被广泛使用。

没有可靠的方法可以从字节流中自动检测字符编码。某些API方法允许你使用“默认字符集”——即计算机操作系统偏好的字符编码。这与你的字节源所使用的编码相同吗？这些字节很可能来自世界的不同地方。因此，你应该始终显式指定编码。例如，读取网页时，请检查`Content-Type`标头。

> **注意：** 平台编码由静态方法`Charset.defaultCharset`返回。静态方法`Charset.availableCharsets`返回所有可用的`Charset`实例，作为从规范名称到`Charset`对象的映射。

> **警告：** Oracle的Java实现有一个系统属性`file.encoding`，用于覆盖平台默认值。这并不是官方支持的属性，而且Oracle实现的Java库并非所有部分都始终遵循它。你不应该设置它。

`StandardCharsets`类具有类型为`Charset`的静态变量，用于每个Java虚拟机必须支持的字符编码：

- `StandardCharsets.UTF_8`
- `StandardCharsets.UTF_16`
- `StandardCharsets.UTF_16BE`
- `StandardCharsets.UTF_16LE`
- `StandardCharsets.ISO_8859_1`
- `StandardCharsets.US_ASCII`

要获取其他编码的`Charset`，请使用静态的`forName`方法：

```java
Charset shiftJIS = Charset.forName("Shift-JIS");
```

读写文本时使用`Charset`对象。例如，可以按如下方式将字节数组转换为字符串：

```java
var str = new String(bytes, StandardCharsets.UTF_8);
```

> **提示：** 从Java 10开始，`java.io`包中的所有方法都允许你使用`Charset`对象或字符串指定字符编码。选择`StandardCharsets`常量，以便在编译时捕获任何拼写错误。

> **警告：** 有些方法（如`String(byte[])`构造函数）在你没有指定编码时使用默认平台编码；其他方法（如`Files.readAllLines`）则使用UTF-8。




## 2.2 读写二进制数据

文本格式便于测试和调试，因为它具有人类可读性，但在传输数据时其效率不如二进制格式。在以下各节中，你将学习如何执行二进制数据的输入和输出。

### 2.2.1 DataInput 和 DataOutput 接口

`DataOutput` 接口定义了以下方法，用于以二进制格式写入数字、字符、布尔值或字符串：

```
writeChars       writeFloat
writeByte        writeDouble
writeInt         writeChar
writeShort       writeBoolean
writeLong        writeUTF
```

例如，`writeInt` 始终将整数写为 4 字节的二进制量，无论其位数多少；`writeDouble` 始终将双精度浮点数写为 8 字节的二进制量。生成的输出不具备人类可读性，但给定类型的每个值都会占用相同的空间，而且读回数据的速度会比解析文本更快。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_100_0.png)

> **注意：** 根据你所使用的处理器，在内存中存储整数和浮点数有两种不同的方法。例如，假设你正在处理一个 4 字节的 int，如十进制数 1234，或十六进制的 4D2（1234 = 4 × 256 + 13 × 16 + 2）。该值可以这样存储：内存中四个字节的第一个字节保存该值的最高有效字节（MSB）：`00 00 04 D2`。这就是所谓的大端法。或者，我们可以先存放最低有效字节（LSB）：`D2 04 00 00`。这自然被称为小端法。例如，SPARC 使用大端法；Pentium 使用小端法。这可能会导致问题。当文件从 C 或 C++ 文件保存时，数据会按照处理器存储它们的方式原样保存。这使得即使是最简单的数据文件也难以从一个平台迁移到另一个平台。在 Java 中，所有值都以大端方式写入，无论处理器是什么。这使得 Java 数据文件与平台无关。

`writeUTF` 方法使用 8 位 Unicode 转换格式的修改版本写入字符串数据。它不是简单地使用标准的 UTF-8 编码，而是先将 Unicode 代码单元序列表示为 UTF-16，然后使用 UTF-8 规则对结果进行编码。对于代码高于 0xFFFF 的字符，这种修改后的编码是不同的。它是为了与 Unicode 尚未超过 16 位时构建的虚拟机向后兼容而使用的。

由于没有其他人使用这种修改后的 UTF-8，因此你只应使用 `writeUTF` 方法为 Java 虚拟机编写字符串——例如，在生成字节码的程序中。对于其他用途，请使用 `writeChars` 方法。

要将数据读回，请使用 `DataInput` 接口中定义的以下方法：

```
readInt        readDouble
readShort      readChar
readLong       readBoolean
readFloat      readUTF
```

`DataInputStream` 类实现了 `DataInput` 接口。要从文件读取二进制数据，请将 `DataInputStream` 与字节源（如 `FileInputStream`）结合使用：

```java
var in = new DataInputStream(new FileInputStream("employee.dat"));
```

类似地，要写入二进制数据，请使用实现了 `DataOutput` 接口的 `DataOutputStream` 类：

```java
var out = new DataOutputStream(new FileOutputStream("employee.dat"));
```

**java.io.DataInput 1.0**

| 方法 | 描述 |
|---|---|
| boolean readBoolean() | |
| byte readByte() | |
| char readChar() | |
| double readDouble() | |
| float readFloat() | |
| int readInt() | |
| long readLong() | |
| short readShort() | 读取给定类型的值。 |
| void readFully(byte[] b) | 将字节读入数组 b，阻塞直到所有字节都被读取。 |
| void readFully(byte[] b, int off, int len) | 从 off 开始，将最多 len 个字节放入数组 b，阻塞直到所有字节都被读取。 |

**java.io.DataInput 1.0（续）**

- `String readUTF()`
  以“修改后的 UTF-8”格式读取字符串。
- `int skipBytes(int n)`
  跳过 n 个字节，阻塞直到所有字节都被跳过。

**java.io.DataOutput 1.0**

- `void writeBoolean(boolean b)`
- `void writeByte(int b)`
- `void writeChar(int c)`
- `void writeDouble(double d)`
- `void writeFloat(float f)`
- `void writeInt(int i)`
- `void writeLong(long l)`
- `void writeShort(int s)`
  写入给定类型的值。
- `void writeChars(String s)`
  写入字符串中的所有字符。
- `void writeUTF(String s)`
  以“修改后的 UTF-8”格式写入字符串。

### 2.2.2 随机访问文件

`RandomAccessFile` 类允许你在文件中的任意位置读取或写入数据。磁盘文件是随机访问的，但与网络套接字通信的输入/输出流则不是。你可以以只读或读写模式打开随机访问文件；通过在构造函数的第二个参数中使用字符串 `"r"`（用于读访问）或 `"rw"`（用于读/写访问）来指定选项。

```java
var in = new RandomAccessFile("employee.dat", "r");
var inOut = new RandomAccessFile("employee.dat", "rw");
```

当你将现有文件打开为 `RandomAccessFile` 时，该文件不会被删除。

随机访问文件有一个文件指针，用于指示下一个要读取或写入的字节的位置。可以使用 `seek` 方法将文件指针设置为文件内的任意字节位置。`seek` 的参数是一个介于 0 和文件字节长度之间的 long 整数。`getFilePointer` 方法返回文件指针的当前位置。

`RandomAccessFile` 类同时实现了 `DataInput` 和 `DataOutput` 接口。要读写随机访问文件，请使用我们在前一节中讨论的方法，如 `readInt`/`writeInt` 和 `readChar`/`writeChar`。

让我们来看一个示例程序，它将员工记录存储在随机访问文件中。每条记录的大小相同。这使得读取任意记录变得容易。假设你想将文件指针定位到第三条记录。只需将文件指针设置为适当的字节位置并开始读取。

```java
long n = 3;
in.seek((n - 1) * RECORD_SIZE);
var e = new Employee();
e.readData(in);
```

如果你想修改记录并将其保存回相同位置，请记得将文件指针设置回记录的开头：

```java
in.seek((n - 1) * RECORD_SIZE);
e.writeData(out);
```

要确定文件的总字节数，请使用 `length` 方法。记录的总数是文件长度除以每条记录的大小。

```java
long nbytes = in.length(); // 以字节为单位的长度
int nrecords = (int) (nbytes / RECORD_SIZE);
```

整数和浮点值在二进制格式中具有固定大小，但对于字符串，我们需要做更多的工作。我们提供了两个辅助方法来写入和读取固定大小的字符串。

`writeFixedString` 方法从字符串开头开始写入指定数量的代码单元。如果代码单元不足，该方法将使用零值填充字符串。

```java
public static void writeFixedString(String s, int size, DataOutput out)
      throws IOException
{
   for (int i = 0; i < size; i++)
   {
      char ch = 0;
      if (i < s.length()) ch = s.charAt(i);
      out.writeChar(ch);
   }
}
```

`readFixedString` 方法从输入流中读取字符，直到它消耗了 `size` 个代码单元或遇到零值字符。然后，它跳过输入字段中剩余的零值。为了提高效率，此方法使用 `StringBuilder` 类来读取字符串。

```java
public static String readFixedString(int size, DataInput in)
    throws IOException
{
    var b = new StringBuilder(size);
    int i = 0;
    var done = false;
    while (!done && i < size)
    {
        char ch = in.readChar();
        i++;
        if (ch == 0) done = true;
        else b.append(ch);
    }
    in.skipBytes(2 * (size - i));
    return b.toString();
}
```

我们将 `writeFixedString` 和 `readFixedString` 方法放在 `DataIO` 辅助类中。

要写入固定大小的记录，我们只需以二进制形式写入所有字段。

```java
DataIO.writeFixedString(e.getName(), Employee.NAME_SIZE, out);
out.writeDouble(e.getSalary());
LocalDate hireDay = e.getHireDay();
out.writeInt(hireDay.getYear());
out.writeInt(hireDay.getMonthValue());
out.writeInt(hireDay.getDayOfMonth());
```

读回数据同样简单。

```java
String name = DataIO.readFixedString(Employee.NAME_SIZE, in);
double salary = in.readDouble();
int y = in.readInt();
int m = in.readInt();
int d = in.readInt();
```

让我们计算每条记录的大小。我们将使用 40 个字符作为姓名串。因此，每条记录将包含 100 个字节：

- 40 个字符 = 80 个字节用于姓名
- 1 个 double = 8 个字节用于薪水
- 3 个 int = 12 个字节用于日期

清单 2.2 中所示的程序将三条记录写入一个数据文件，然后按相反顺序从文件中读取它们。要高效地做到这一点，需要随机访问——我们需要首先到达最后一条记录。




### 清单 2.2 RandomAccess/RandomAccessTest.java

```java
1 package randomAccess;
2 
3 import java.io.*;
4 import java.time.*;
5 
6 /**
7  * @version 1.14 2018-05-01
8  * @author Cay Horstmann
9  */
10 public class RandomAccessTest
11 {
12    public static void main(String[] args) throws IOException
13    {
14       var staff = new Employee[3];
15 
16       staff[0] = new Employee("Carl Cracker", 75000, 1987, 12, 15);
17       staff[1] = new Employee("Harry Hacker", 50000, 1989, 10, 1);
18       staff[2] = new Employee("Tony Tester", 40000, 1990, 3, 15);
19 
20       try (var out = new DataOutputStream(new FileOutputStream("employee.dat")))
21       {
22          // save all employee records to the file employee.dat
23          for (Employee e : staff)
24             writeData(out, e);
25       }
26 
27       try (var in = new RandomAccessFile("employee.dat", "r"))
28       {
29          // retrieve all records into a new array
30 
31          // compute the array size
32          int n = (int)(in.length() / Employee.RECORD_SIZE);
33          var newStaff = new Employee[n];
34 
35          // read employees in reverse order
36          for (int i = n - 1; i >= 0; i--)
37          {
38             newStaff[i] = new Employee();
39             in.seek(i * Employee.RECORD_SIZE);
40             newStaff[i] = readData(in);
41          }
42 
43          // print the newly read employee records
44          for (Employee e : newStaff)
45             System.out.println(e);
46       }
47    }

/**
 * Writes employee data to a data output
 * @param out the data output
 * @param e the employee
 */
public static void writeData(DataOutput out, Employee e) throws IOException
{
    DataIO.writeFixedString(e.getName(), Employee.NAME_SIZE, out);
    out.writeDouble(e.getSalary());

    LocalDate hireDay = e.getHireDay();
    out.writeInt(hireDay.getYear());
    out.writeInt(hireDay.getMonthValue());
    out.writeInt(hireDay.getDayOfMonth());
}

/**
 * Reads employee data from a data input
 * @param in the data input
 * @return the employee
 */
public static Employee readData(DataInput in) throws IOException
{
    String name = DataIO.readFixedString(Employee.NAME_SIZE, in);
    double salary = in.readDouble();
    int y = in.readInt();
    int m = in.readInt();
    int d = in.readInt();
    return new Employee(name, salary, y, m - 1, d);
}
```

**java.io.RandomAccessFile 1.0**

| API | 描述 |
|---|---|
| `RandomAccessFile(String file, String mode)`<br>`RandomAccessFile(File file, String mode)` | 打开给定文件以进行随机访问。模式字符串为 "r" 表示只读模式，"rw" 表示读/写模式，"rws" 表示读/写模式，并在每次更新时同步将数据和元数据写入磁盘，"rwd" 表示读/写模式，但仅同步将数据写入磁盘。 |
| `long getFilePointer()` | 返回文件指针的当前位置。 |
| `void seek(long pos)` | 将文件指针设置到距文件开头 pos 字节处。 |
| `long length()` | 返回文件长度（以字节为单位）。 |

### 2.2.3 ZIP 归档

ZIP 归档以（通常）压缩格式存储一个或多个文件。每个 ZIP 归档都有一个头，包含诸如每个文件名和所用压缩方法等信息。在 Java 中，可以使用 `ZipInputStream` 读取 ZIP 归档。你需要查看归档中的各个条目。`getNextEntry` 方法返回描述该条目的 `ZipEntry` 类型对象。从流中读取直到末尾，这实际上是当前条目的末尾。然后调用 `closeEntry` 读取下一个条目。在读取最后一个条目之前不要关闭 `zin`。以下是读取 ZIP 文件的典型代码序列：

```java
var zin = new ZipInputStream(new FileInputStream(zipname));
ZipEntry entry;
while ((entry = zin.getNextEntry()) != null)
{
    read the contents of zin
    zin.closeEntry();
}
zin.close();
```

要写入 ZIP 文件，请使用 `ZipOutputStream`。对于要放入 ZIP 文件的每个条目，创建一个 `ZipEntry` 对象。将文件名传递给 `ZipEntry` 构造函数；它会设置其他参数，如文件日期和解压缩方法。如有需要，可以覆盖这些设置。然后调用 `ZipOutputStream` 的 `putNextEntry` 方法开始写入新文件。将文件数据发送到 ZIP 输出流。完成后，调用 `closeEntry`。对要存储的所有文件重复此过程。以下是一个代码骨架：

```java
var fout = new FileOutputStream("test.zip");
var zout = new ZipOutputStream(fout);
for all files
{
    var ze = new ZipEntry(filename);
    zout.putNextEntry(ze);
    send data to zout
    zout.closeEntry();
}
zout.close();
```

> **注意：** JAR 文件（已在第 I 卷第 4 章中讨论）就是带有特殊条目——即所谓的清单（manifest）——的 ZIP 文件。使用 JarInputStream 和 JarOutputStream 类读取和写入清单条目。

ZIP 输入流是流抽象强大能力的一个很好的例子。当读取以压缩形式存储的数据时，你不必担心数据在被请求时正在被解压缩。此外，ZIP 流中字节的来源不必是文件——ZIP 数据可以来自网络连接。

> **注意：** 第 123 页的 2.4.8 节“ZIP 文件系统”展示了如何使用 Java 7 的 FileSystem 类，在不使用特殊 API 的情况下访问 ZIP 归档。

- **java.util.zip.ZipInputStream 1.1**
  - `ZipInputStream(InputStream in)` 创建一个 ZipInputStream，允许你从给定的 InputStream 解压（inflate）数据。
  - `ZipEntry getNextEntry()` 返回下一个条目的 ZipEntry 对象；如果没有更多条目，则返回 null。
  - `void closeEntry()` 关闭 ZIP 文件中当前打开的条目。然后可以使用 getNextEntry() 读取下一个条目。
- **java.util.zip.ZipOutputStream 1.1**
  - `ZipOutputStream(OutputStream out)` 创建一个 ZipOutputStream，可用于将压缩数据写入指定的 OutputStream。
  - `void putNextEntry(ZipEntry ze)` 将给定 ZipEntry 中的信息写入输出流，并为数据定位流。然后可以通过调用 write() 方法写入数据。
  - `void closeEntry()` 关闭 ZIP 文件中当前打开的条目。使用 putNextEntry 方法开始下一个条目。
  - `void setLevel(int level)` 将后续 DEFLATED 条目的默认压缩级别设置为从 Deflater.NO_COMPRESSION 到 Deflater.BEST_COMPRESSION 的值。默认值为 Deflater.DEFAULT_COMPRESSION。如果级别无效，则抛出 IllegalArgumentException。
  - `void setMethod(int method)` 为任何未指定方法的条目设置此 ZipOutputStream 的默认压缩方法；可以是 DEFLATED 或 STORED。
- **java.util.zip.ZipEntry 1.1**
  - `ZipEntry(String name)` 构造一个具有给定名称的 ZIP 条目。
  - `long getCrc()` 返回此 ZipEntry 的 CRC32 校验和值。
  - `String getName()` 返回此条目的名称。
  - `long getSize()` 返回此条目的未压缩大小；如果未知，则返回 -1。
  - `boolean isDirectory()` 如果此条目是目录，则返回 true。
  - `void setMethod(int method)` 将此条目的压缩方法设置为 DEFLATED 或 STORED。
  - `void setSize(long size)` 设置此条目的大小。仅在压缩方法为 STORED 时需要。
  - `void setCrc(long crc)` 设置此条目的 CRC32 校验和。使用 CRC32 类计算此校验和。仅在压缩方法为 STORED 时需要。

**java.util.zip.ZipFile 1.1**

| API | 描述 |
|---|---|
| `ZipFile(String name)`<br>`ZipFile(File file)` | 创建一个 ZipFile，用于从给定字符串或 File 对象读取。 |
| `Enumeration entries()` | 返回一个 Enumeration 对象，该对象枚举描述 ZipFile 各条目的 ZipEntry 对象。 |
| `ZipEntry getEntry(String name)` | 返回与给定名称对应的条目；如果没有这样的条目，则返回 null。 |
| `InputStream getInputStream(ZipEntry ze)` | 返回给定条目的 InputStream。 |
| `String getName()` | 返回此 ZIP 文件的路径。 |

## 2.3 对象输入/输出流与序列化

如果需要存储同一类型的数据，使用定长记录格式是一个不错的选择。然而，在面向对象程序中创建的对象很少全都属于同一类型。例如，你可能有一个名为 staff 的数组，它名义上是 Employee 记录数组，但其中包含的对象实际上是诸如 Manager 之类的子类的实例。

当然可以设计一种数据格式来存储这样的多态集合——但幸运的是，我们不必这样做。Java 语言支持一种非常通用的机制，称为对象序列化，它使得可以将任何对象写入输出流，并在以后再次读取。（你将在本章中看到“序列化”这个术语的由来。）

### 2.3.1 保存和加载可序列化对象

要保存对象数据，首先需要打开一个 ObjectOutputStream 对象：

```java
var out = new ObjectOutputStream(new FileOutputStream("employee.dat"));
```

现在，要保存对象，只需像下面的片段中那样使用 ObjectOutputStream 类的 writeObject 方法：

```java
var harry = new Employee("Harry Hacker", 50000, 1989, 10, 1);
var boss = new Manager("Carl Cracker", 80000, 1987, 12, 15);
```



```java
out.writeObject(harry);
out.writeObject(boss);
```

要读回这些对象，首先获取一个 `ObjectInputStream` 对象：

```java
var in = new ObjectInputStream(new FileInputStream("employee.dat"));
```

然后，按照写入对象时的相同顺序，使用 `readObject` 方法取回这些对象：

```java
var e1 = (Employee) in.readObject();
var e2 = (Employee) in.readObject();
```

不过，对于任何想要保存到输出流并从对象输入流恢复的类，都需要做一处修改。该类必须实现 `Serializable` 接口：

```java
class Employee implements Serializable { . . . }
```

`Serializable` 接口没有方法，因此你无需以任何方式修改自己的类。在这方面，它类似于我们在第 I 卷第 6 章讨论过的 `Cloneable` 接口。不过，要使一个类可克隆，你仍然必须重写 `Object` 类的 `clone` 方法。要使一个类可序列化，则不需要做任何其他事情。

> **注意：** 使用 `writeObject`/`readObject` 方法只能写入和读取*对象*。对于基本类型值，请使用 `writeInt`/`readInt` 或 `writeDouble`/`readDouble` 等方法。（对象输入/输出流类实现了 `DataInput`/`DataOutput` 接口。）

在幕后，`ObjectOutputStream` 会查看对象的所有字段并保存其内容。例如，写入一个 `Employee` 对象时，`name`、`date` 和 `salary` 字段会被写入输出流。

然而，有一种重要情况需要考虑：当一个对象作为多个对象状态的一部分而被共享时，会发生什么？

为了说明这个问题，让我们对 `Manager` 类做一点小修改。假设每位经理都有一位秘书：

```java
class Manager extends Employee
{
    private Employee secretary;
    . . .
}
```

现在每个 `Manager` 对象都包含一个指向 `Employee` 对象的引用，该对象描述其秘书。当然，两位经理可以共享同一位秘书，如图 2.5 和以下代码所示：

```java
var harry = new Employee("Harry Hacker", . . .);
var carl = new Manager("Carl Cracker", . . .);
carl.setSecretary(harry);
var tony = new Manager("Tony Tester", . . .);
tony.setSecretary(harry);
```

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_112_0.png)

**图 2.5** 两位经理可以共享同一位员工。

保存这样一个对象网络是一项挑战。当然，我们不能保存和恢复秘书对象的内存地址。当一个对象被重新加载时，它很可能占用与原来完全不同的内存地址。

取而代之的是，每个对象都带有一个*序列号*来保存——这种机制也因此得名*对象序列化*。算法如下：

1. 将序列号与你遇到的每个对象引用关联起来（如图 2.6 所示）。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_113_0.png)

**图 2.6** 对象序列化示例

2. 首次遇到某个对象引用时，将该对象数据保存到输出流。
3. 如果该对象之前已经保存过，只需写入“与之前保存的序列号为 x 的对象相同”。

读回对象时，过程相反。

1. 当对象输入流中首次指定某个对象时，构造它，用流数据初始化它，并记住序列号与该对象引用之间的关联。
2. 当遇到标记“与之前保存的序列号为 x 的对象相同”时，取出该序列号对应的对象引用。

> **注意：** 在本章中，我们将使用序列化把一组对象保存到磁盘文件，并按存储时的原样将其取回。另一个非常重要的应用是通过网络连接把一组对象传输到另一台计算机。正如原始内存地址在文件中没有意义一样，当你与不同的处理器通信时，它们也没有意义。通过用序列号代替内存地址，序列化允许将对象集合从一台机器传输到另一台机器。

程序清单 2.3 是一个保存并重新加载 `Employee` 和 `Manager` 对象网络的程序（其中一些对象共享同一位员工作为秘书）。注意，重新加载后，秘书对象是唯一的——当 `newStaff[1]` 加薪时，这一变化会反映在各位经理的 secretary 字段中。

**程序清单 2.3** objectStream/ObjectStreamTest.java

```java
package objectStream;

import java.io.*;

/**
 * @version 1.11 2018-05-01
 * @author Cay Horstmann
 */
class ObjectStreamTest
{
   public static void main(String[] args) throws IOException, ClassNotFoundException
   {
      var harry = new Employee("Harry Hacker", 50000, 1989, 10, 1);
      var carl = new Manager("Carl Cracker", 80000, 1987, 12, 15);
      carl.setSecretary(harry);
      var tony = new Manager("Tony Tester", 40000, 1990, 3, 15);
      tony.setSecretary(harry);

      var staff = new Employee[3];

      staff[0] = carl;
      staff[1] = harry;
      staff[2] = tony;

      // save all employee records to the file employee.dat
      try (var out = new ObjectOutputStream(new FileOutputStream("employee.dat")))
      {
         out.writeObject(staff);
      }

      try (var in = new ObjectInputStream(new FileInputStream("employee.dat")))
      {
         // retrieve all records into a new array

         var newStaff = (Employee[]) in.readObject();

         // raise secretary's salary
         newStaff[1].raiseSalary(10);

         // print the newly read employee records
         for (Employee e : newStaff)
            System.out.println(e);
      }
   }
}
```

| `java.io.ObjectOutputStream 1.1` |
|--------------------------------|
| `ObjectOutputStream(OutputStream out)` 创建一个 `ObjectOutputStream`，以便你可以将对象写入指定的 `OutputStream`。 |
| `void writeObject(Object obj)` 将指定对象写入 `ObjectOutputStream`。此方法保存对象的类、类的签名，以及该类及其超类的任何非静态、非瞬态字段的值。 |

| `java.io.ObjectInputStream 1.1` |
|-------------------------------|
| `ObjectInputStream(InputStream in)` 创建一个 `ObjectInputStream`，以便从指定的 `InputStream` 读回对象信息。 |
| `Object readObject()` 从 `ObjectInputStream` 读取一个对象。特别地，此方法读回对象的类、类的签名，以及该类及其所有超类的非瞬态和非静态字段的值。它执行反序列化，以便可以恢复多个对象引用。 |

### 2.3.2 理解对象序列化文件格式

对象序列化以特定的文件格式保存对象数据。当然，你可以使用 `writeObject`/`readObject` 方法，而不必了解文件中表示对象的精确字节序列。尽管如此，我们发现研究数据格式对于深入理解对象极有帮助

读取对象时，会将其指纹与该类的当前指纹进行比较。如果二者不匹配，就说明对象写入后类定义发生了改变，并会生成异常。当然，在实践中，类确实会演化，程序可能需要读取旧版本的对象。我们将在第 103 页的第 2.3.5 节“版本管理”中讨论这一点。

类标识符的存储方式如下：

- 72
- 类名的 2 字节长度
- 类名
- 8 字节指纹
- 1 字节标志
- 数据字段描述符的 2 字节计数
- 数据字段描述符
- 78（结束标记）
- 超类类型（若无则为 70）

标志字节由三个位掩码组成，定义在 `java.io.ObjectStreamConstants` 中：

```java
    static final byte SC_WRITE_METHOD = 1;
        // class has a writeObject method that writes additional data
    static final byte SC_SERIALIZABLE = 2;
        // class implements the Serializable interface
    static final byte SC_EXTERNALIZABLE = 4;
        // class implements the Externalizable interface
```

我们将在本章后面讨论 `Externalizable` 接口。Externalizable 类提供自定义的读写方法，接管其实例字段的输出。我们编写的类实现 `Serializable` 接口，其标志值为 02。可序列化的 `java.util.Date` 类定义了自己的 `readObject`/`writeObject` 方法，其标志为 03。

每个数据字段描述符的格式如下：

- 1 字节类型代码
- 字段名的 2 字节长度
- 字段名
- 类名（如果该字段是对象）

类型代码是以下之一：

| 类型代码 | 字段类型 |
|---|---|
| `B` | 字节 |
| `C` | 字符 |
| `D` | 双精度浮点 |
| `F` | 单精度浮点 |
| `I` | 整数 |
| `J` | 长整数 |
| `L` | 对象 |
| `S` | 短整数 |
| `Z` | 布尔 |
| `[` | 数组 |

当类型代码为 `L` 时，字段名后面跟着字段类型。类名和字段名字符串不以字符串代码 `74` 开头，但字段类型会以它开头。字段类型对其名称使用略有不同的编码——即本地方法所用的格式。

例如，`Employee` 类的 `salary` 字段编码为

```
D 00 06 salary
```

下面是 `Employee` 类的完整类描述符：

| 描述符 | 含义 |
|---|---|
| `72 00 08 Employee` | 类名：Employee |
| `E6 D2 86 70 AE AC 18 18 02` | 指纹和标志 |
| `00 03` | 实例字段数量 |
| `D 00 06 salary` | 实例字段类型和名称 |
| `L 00 07 hireDay` | 实例字段类型和名称 |
| `74 00 10 Ljava/util/Date;` | 实例字段类名：Date |
| `L 00 04 name` | 实例字段类型和名称 |
| `74 00 12 Ljava/lang/String;` | 实例字段类名：String |
| `78` | 结束标记 |
| `70` | 无超类 |

这些描述符相当长。如果文件中再次需要同一个类描述符，则使用缩写形式：

| 代码 | 含义 |
|---|---|
| `71` | 4 字节序列号 |

该序列号指向前一个显式类描述符。我们稍后讨论编号方案。

对象按如下方式存储：

| 代码 | 含义 |
|---|---|
| `73` | 类描述符，后跟对象数据 |

例如，下面是一个 `Employee` 对象的存储方式：

```
40 E8 6A 00 00 00 00 00        salary field value: double
73                            hireDay field value: new object
   71 00 7E 00 08             Existing class java.util.Date
   77 08 00 00 00 91 1B 4E B1 80  External storage (details later)
74 00 0C Harry Hacker          name field value: String
```

如你所见，数据文件包含足够的信息来恢复 `Employee` 对象。

数组按以下格式保存：

```
75          class descriptor          4-byte number of
                                      entries
```

类描述符中的数组类名采用与本地方法所用格式相同的格式（与其他类描述符中类名所用格式略有不同）。在此格式中，类名以 `L` 开头并以分号结尾。

例如，一个包含三个 `Employee` 对象的数组开头如下：

```
75                                      Array
   72 00 0B [LEmployee;               New class, string length, class name
                                      Employee[]
   FC BF 36 11 C5 91 11 C7 02       Fingerprint and flags
   00 00                             Number of instance fields
   78                                End marker
   70                                No superclass
   00 00 00 03                       Number of array entries
```

注意，`Employee` 对象数组的指纹与 `Employee` 类本身的指纹不同。

所有对象（包括数组和字符串）以及所有类描述符在保存到输出文件时都会被分配序列号。编号从 `00 7E 00 00` 开始。

我们已经看到，任何给定类的完整类描述符只出现一次。后续描述符会引用它。例如，在前面的示例中，对 `Date` 类的重复引用编码为

```
71 00 7E 00 08
```

同一机制也用于对象。如果写入对先前保存对象的引用，则会以完全相同的方式保存——即 `71` 后跟序列号。从上下文中总能清楚判断某个特定序列引用表示类描述符还是对象。

最后，空引用存储为

```
70
```

下面是上一节 *ObjectRefTest* 程序的带注释输出。运行该程序，查看其数据文件 *employee.dat* 的十六进制转储，并与带注释的清单进行比较。输出末尾附近的重要行展示了对先前保存对象的引用。

```
AC ED 00 05                    File header
75
   72 00 0B [LEmployee;        New class, string length, class name
                               Employee[] (serial #0)
      FC BF 36 11 C5 91 11 C7 02  Fingerprint and flags
      00 00                   Number of instance fields
      78                      End marker
      70                      No superclass
      00 00 00 03             Number of array entries
73                            staff[0]— new object (serial #7)
   72 00 07 Manager           New class, string length, class name
                              (serial #2)
      36 06 AE 13 63 8F 59 87 02  Fingerprint and flags
      00 01                   Number of data fields
      L 00 09 secretary       Instance field type and name
      74 00 0A LEmployee;     Instance field class name: Employee (serial #3)
      78                      End marker
   72 00 08 Employee          Superclass: new class, string length, class
                              name (serial #4)
      E6 D2 86 70 AE AC 18 18 02  Fingerprint and flags
      00 03                   Number of instance fields
      D 00 06 salary          Instance field type and name
      L 00 07 hireDay         Instance field type and name
      74 00 10 Ljava/util/Date;  Instance field class name: Date (serial #5)
      L 00 04 name            Instance field type and name
      74 00 12 Ljava/lang/String; Instance field class name: String (serial #6)
      78                      End marker
      70                      No superclass
40 F3 88 00 00 00 00 00    salary field value: double
73                          hireDay field value: new object (serial #9)
72 00 0E java.util.Date      New class, string length, class name
                             (serial #8)
68 6A 81 01 4B 59 74 19 03  Fingerprint and flags
00 00                      No instance variables
78                         End marker
70                         No superclass
77 08                      External storage, number of bytes
00 00 00 83 E9 39 E0 00    Date
78                         End marker

74 00 0C Carl Cracker       name field value: String (serial #10)
73                         secretary field value: new object
                             (serial #11)
71 00 7E 00 04             existing class (use serial #4)
40 E8 6A 00 00 00 00 00    salary field value: double
73                         hireDay field value: new object (serial #12)
71 00 7E 00 08             Existing class (use serial #8)
77 08                      External storage, number of bytes
00 00 00 91 1B 4E B1 80    Date
78                         End marker
74 00 0C Harry Hacker       name field value: String (serial #13)
71 00 7E 00 0B             staff[1]: existing object (use serial #11)
73                         staff[2]: new object (serial #14)
71 00 7E 00 02             Existing class (use serial #2)
40 E3 88 00 00 00 00 00    salary field value: double
73                         hireDay field value: new object (serial #15)
71 00 7E 00 08             Existing class (use serial #8)
77 08                      External storage, number of bytes
00 00 00 94 6D 3E EC 00    Date
78                         End marker
74 00 0B Tony Tester        name field value: String (serial #16)
71 00 7E 00 0B             secretary field value: existing object (use
                             serial #11)
```

当然，研究这些代码可能和读电话簿一样枯燥。知道确切的文件格式并不重要（除非你想通过修改数据来制造恶意效果），但了解序列化格式对其包含的所有对象都有详细描述，且细节足以重建对象和对象数组，仍然很有启发性。

你应该记住的是：

- 序列化格式包含所有对象的类型和数据字段。
- 每个对象都会被分配一个序列号。
- 同一对象的重复出现会存储为对该序列号的引用。

### 2.3.3 修改默认序列化机制

某些数据字段绝不应被序列化——例如，存储文件句柄或窗口句柄的整数值，这些句柄只对本地方法有意义。当你在以后重新加载对象或将其传输到另一台机器时，此类信息肯定无用。事实上，此类字段的不正确值实际上可能导致本地方法崩溃。Java 有一种简单的机制来防止此类字段被序列化：用关键字 `transient` 标记它们。如果字段属于可序列化类，你也需要将这些字段标记为 `transient`。序列化对象时，瞬态字段总会被跳过。

序列化机制为各个类提供了一种方式，可向默认读写行为添加验证或任何其他所需操作。可序列化类可以定义具有以下签名的方法：

```
private void readObject(ObjectInputStream in)
        throws IOException, ClassNotFoundException;
private void writeObject(ObjectOutputStream out)
        throws IOException;
```

然后，数据字段不再自动序列化——而是调用这些方法。

下面是一个典型示例。`java.awt.geom` 包中的许多类（例如 `Point2D.Double`）不可序列化。现在，假设你想序列化一个存储 `String` 和 `Point2D.Double` 的类 `LabeledPoint`。首先，需要将 `Point2D.Double` 字段标记为 `transient`，以避免 `NotSerializableException`。

```
public class LabeledPoint implements Serializable
{
    private String label;
    private transient Point2D.Double point;
    . . .
}
```



读取外部化对象时，对象输入流会用无参构造器创建一个对象，然后调用 `readExternal` 方法。以下是为 Employee 类实现这些方法的方式：

```java
public void readExternal(ObjectInput s)
    throws IOException
{
    name = s.readUTF();
    salary = s.readDouble();
    hireDay = LocalDate.ofEpochDay(s.readLong());
}

public void writeExternal(ObjectOutput s)
    throws IOException
{
    s.writeUTF(name);
    s.writeDouble(salary);
    s.writeLong(hireDay.toEpochDay());
}
```

> **注意：** 与私有且只能由序列化机制调用的 `readObject` 和 `writeObject` 方法不同，`readExternal` 和 `writeExternal` 方法是公开的。特别是，外部化对象的使用者有可能修改现有对象的状态。

### 2.3.4 序列化单例和类型安全枚举

你必须特别注意序列化和反序列化那些被假定为唯一的对象。这在实现单例和类型安全枚举时很常见。

如果你使用 Java 语言的 enum 构造，就不必担心序列化——它能正常工作。然而，假设你维护的遗留代码包含如下枚举类型：

```java
public class Orientation
{
    public static final Orientation HORIZONTAL = new Orientation(1);
    public static final Orientation VERTICAL = new Orientation(2);

    private int value;

    private Orientation(int v) { value = v; }
}
```

在枚举被加入 Java 语言之前，这种惯用法很常见。注意构造器是私有的。因此，除了 `Orientation.HORIZONTAL` 和 `Orientation.VERTICAL` 之外，不能创建其他对象。特别是，你可以使用 `==` 运算符来测试对象相等性：

```java
if (orientation == Orientation.HORIZONTAL) ...
```

当类型安全枚举实现 Serializable 接口时，有一个重要的细节需要记住。默认的序列化机制并不合适。假设我们写出一个 Orientation 类型的值，然后再把它读回来：

```java
Orientation original = Orientation.HORIZONTAL;
ObjectOutputStream out = ...;
out.write(original);
out.close();
ObjectInputStream in = ...;
var saved = (Orientation) in.read();
```

现在，测试

```java
if (saved == Orientation.HORIZONTAL) ...
```

将会失败。事实上，保存下来的值是一个全新的 Orientation 类型对象，它不等于任何预定义常量。即使构造器是私有的，序列化机制也能创建新对象！

要解决这个问题，需要定义另一个特殊的序列化方法，称为 readResolve。如果定义了 readResolve 方法，它会在对象反序列化之后被调用。它必须返回一个对象，该对象随后成为 readObject 方法的返回值。在我们的例子中，readResolve 方法将检查 value 字段并返回适当的枚举常量：

```java
protected Object readResolve() throws ObjectStreamException
{
    if (value == 1) return Orientation.HORIZONTAL;
    if (value == 2) return Orientation.VERTICAL;
    throw new ObjectStreamException(); // this shouldn't happen
}
```

请记住，要为遗留代码中的所有类型安全枚举以及所有遵循单例设计模式的类添加 readResolve 方法。

### 2.3.5 版本管理

如果你使用序列化来保存对象，就需要考虑程序演化时会发生什么。1.1 版能读取旧文件吗？仍在使用 1.0 版的用户能读取新版本生成的文件吗？显然，如果对象文件能够应对类的演化，那将是理想的。

乍一看，这似乎不可能。当类定义以任何方式发生变化时，它的 SHA 指纹也会变化，而你知道对象输入流会拒绝读入具有不同指纹的对象。然而，一个类可以表明自己与自身的早期版本*兼容*。为此，你必须先获取该类*早期*版本的指纹。使用 JDK 自带的独立 serialver 程序来获取这个数字。例如，运行

```
serialver Employee
```

会打印出

```
Employee: static final long serialVersionUID = -1814239825517340645L;
```

该类的所有*后续*版本都必须将 serialVersionUID 常量定义为与原始版本相同的指纹。

```java
class Employee implements Serializable // version 1.1
{
   . . .
   public static final long serialVersionUID = -1814239825517340645L;
}
```

当一个类有一个名为 serialVersionUID 的静态数据成员时，它不会手动计算指纹，而是使用该值。

一旦这个静态数据成员被放入类中，序列化系统现在就愿意读入该类对象的不同版本。

如果只有类的方法发生变化，读取新的对象数据没有问题。然而，如果数据字段发生变化，就可能出现问题。例如，旧文件对象可能比程序中的对象具有更多或更少的数据字段，或者数据字段的类型可能不同。在这种情况下，对象输入流会努力将序列化对象转换为该类的当前版本。

对象输入流会将当前版本类的数据字段与序列化对象中版本的数据字段进行比较。当然，对象输入流只考虑非瞬态和非静态数据字段。如果两个字段名称匹配但类型不同，对象输入流不会尝试将一种类型转换为另一种类型——这些对象不兼容。如果序列化对象具有当前版本中不存在的数据字段，对象输入流会忽略这些额外数据。如果当前版本具有序列化对象中不存在的数据字段，则新增字段会被设置为其默认值（对象为 null，数字为 0，布尔值为 false）。

这里有一个例子。假设我们使用该类的原始版本（1.0）将一些员工记录保存到磁盘。现在我们通过添加一个名为 department 的数据字段，将 Employee 类改为 2.0 版。图 2.7 展示了将 1.0 对象读入使用 2.0 对象的程序时会发生什么。department 字段被设置为 null。图 2.8 展示了相反的场景：使用 1.0 对象的程序读取一个 2.0 对象。额外的 department 字段被忽略。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_127_0.png)

**图 2.7** 读取数据字段较少的对象

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_127_1.png)

**图 2.8** 读取数据字段较多的对象

这个过程安全吗？这取决于情况。丢弃一个数据字段似乎无害——接收方仍然拥有它知道如何操作的所有数据。将数据字段设置为 null 可能就不那么安全了。许多类会努力在所有构造器中将所有数据字段初始化为非 null 值，这样方法就不必准备处理 null 数据。类设计者需要在 readObject 方法中实现额外代码来修复版本不兼容问题，或者确保方法足够健壮以处理 null 数据。

> **提示：** 在向类添加 `serialVersionUID` 字段之前，先问问自己为什么让类可序列化。如果序列化仅用于短期持久化，例如应用服务器中的分布式方法调用，就不必担心版本管理和 `serialVersionUID`。如果你扩展了一个恰好可序列化的类，但从不打算持久化其实例，也同样如此。如果你的 IDE 给出烦人的警告，可以更改 IDE 首选项将其关闭，或者添加注解（`@SuppressWarnings("serial")`）。这比添加一个你以后可能忘记修改的 `serialVersionUID` 更安全。

### 2.3.6 使用序列化进行克隆

序列化机制有一个有趣的用途：只要类是可序列化的，它就能让你轻松克隆对象。只需将其序列化到输出流，然后再读回来。结果是一个新对象，它是现有对象的深拷贝。你不必把对象写入文件——可以使用 `ByteArrayOutputStream` 将数据保存到字节数组中。

如清单 2.4 所示，要免费获得 clone，只需扩展 `Serializable` 类，就完成了。

你应该意识到，这种方法虽然巧妙，但通常比显式构造新对象并复制或克隆数据字段的 clone 方法慢得多。

```java
// Listing 2.4  serialClone/SerialCloneTest.java
package serialClone;

/**
 * @version 1.22 2018-05-01
 * @author Cay Horstmann
 */

import java.io.*;
import java.time.*;

public class SerialCloneTest
{
   public static void main(String[] args) throws CloneNotSupportedException
   {



### 清单 2.4 *（续）*

```java
var harry = new Employee("Harry Hacker", 35000, 1989, 10, 1);
// clone harry
var harry2 = (Employee) harry.clone();

// mutate harry
harry.raiseSalary(10);

// now harry and the clone are different
System.out.println(harry);
System.out.println(harry2);
}
}

/**
 * A class whose clone method uses serialization.
 */
class SerialCloneable implements Cloneable, Serializable
{
    public Object clone() throws CloneNotSupportedException
    {
        try
        {
            // save the object to a byte array
            var bout = new ByteArrayOutputStream();
            try (var out = new ObjectOutputStream(bout))
            {
                out.writeObject(this);
            }

            // read a clone of the object from the byte array
            try (var bin = new ByteArrayInputStream(bout.toByteArray()))
            {
                var in = new ObjectInputStream(bin);
                return in.readObject();
            }
        }
        catch (IOException | ClassNotFoundException e)
        {
            var e2 = new CloneNotSupportedException();
            e2.initCause(e);
            throw e2;
        }
    }
}

/**
 * The familiar Employee class, redefined to extend the
 * Serializable class.
 */
class Employee implements Serializable
{
    private String name;
    private double salary;
    private LocalDate hireDay;

    public Employee(String n, double s, int year, int month, int day)
    {
        name = n;
        salary = s;
        hireDay = LocalDate.of(year, month, day);
    }

    public String getName()
    {
        return name;
    }

    public double getSalary()
    {
        return salary;
    }

    public LocalDate getHireDay()
    {
        return hireDay;
    }

    /**
     * Raises the salary of this employee.
     * @param byPercent the percentage of the raise
     */
    public void raiseSalary(double byPercent)
    {
        double raise = salary * byPercent / 100;
        salary += raise;
    }

    public String toString()
    {
        return getClass().getName()
            + "[name=" + name
            + ",salary=" + salary
            + ",hireDay=" + hireDay
            + "]";
    }
}
```

## 2.4 使用文件

你已经学习了如何从文件读取和写入数据。然而，文件管理远不止读写。Path 接口和 Files 类封装了在用户机器上使用文件系统所需的功能。例如，可以用 Files 类删除或重命名文件，或者查明文件的最后修改时间。换句话说，输入/输出流类关注的是文件的内容，而我们这里讨论的类关注的是文件在磁盘上的存储。

Path 接口和 Files 类是在 Java 7 中新增的。它们比可以追溯到 JDK 1.0 的 File 类使用起来方便得多。我们预计它们会非常受 Java 程序员欢迎，并将深入讨论它们。

### 2.4.1 路径

Path 是目录名的序列，后面可选地跟一个文件名。路径的第一个组成部分可能是根组件，例如 `/` 或 `C:\`。允许的根组件取决于文件系统。以根组件开头的路径是绝对路径。否则，它是相对路径。例如，这里我们构造一个绝对路径和一个相对路径。对于绝对路径，我们假设使用的是类 UNIX 文件系统。

```
Path absolute = Paths.get("/home", "harry");
Path relative = Paths.get("myprog", "conf", "user.properties");
```

静态 `Paths.get` 方法接收一个或多个字符串，并用默认文件系统的路径分隔符将它们连接起来（类 UNIX 文件系统为 `/`，Windows 为 `\`）。然后它解析结果，如果结果在给定文件系统中不是有效路径，则抛出 `InvalidPathException`。结果是 Path 对象。

get 方法可以接收包含多个组成部分的单个字符串。例如，你可以像这样从配置文件中读取路径：

```
String baseDir = props.getProperty("base.dir");
    // May be a string such as /opt/myprog or c:\Program Files\myprog
Path basePath = Paths.get(baseDir); // OK that baseDir has separators
```

> **注意：** 路径不必对应于实际存在的文件。它仅仅是名称的抽象序列。正如你将在下一节中看到的，当你想创建文件时，首先创建一个路径，然后调用方法创建相应的文件。

组合或 `resolve` 路径是非常常见的。调用 `p.resolve(q)` 会按照以下规则返回一个路径：

- 如果 q 是绝对路径，则结果为 q。
- 否则，根据文件系统的规则，结果为“p 后接 q”。

例如，假设你的应用程序需要相对于从配置文件读取的给定基目录来查找其工作目录，如前面的示例所示。

```
    Path workRelative = Paths.get("work");
    Path workPath = basePath.resolve(workRelative);
```

`resolve` 方法有一个快捷方式，它接收字符串而不是路径：

```
    Path workPath = basePath.resolve("work");
```

有一个便捷方法 `resolveSibling`，它针对路径的父路径进行解析，生成同级路径。例如，如果 `workPath` 是 `/opt/myapp/work`，则调用

```
    Path tempPath = workPath.resolveSibling("temp");
```

会创建 `/opt/myapp/temp`。

`resolve` 的反操作是 `relativize`。调用 `p.relativize(r)` 会得到路径 `q`，当用 `p` 解析 `q` 时，会得到 `r`。例如，将 `/home/harry` 相对于 `/home/fred/input.txt` 进行相对化，会得到 `../fred/input.txt`。这里，我们假设 `..` 表示文件系统中的父目录。

`normalize` 方法会移除任何冗余的 `.` 和 `..` 组成部分（或文件系统认为冗余的任何内容）。例如，规范化路径 `/home/harry/../fred/./input.txt` 会得到 `/home/fred/input.txt`。

`toAbsolutePath` 方法会返回给定路径的绝对路径，从根组件开始，例如 `/home/fred/input.txt` 或 `c:\Users\fred\input.txt`。

`Path` 接口有许多用于分解路径的有用方法。以下代码示例展示了其中一些最有用的方法：

```
    Path p = Paths.get("/home", "fred", "myprog.properties");
    Path parent = p.getParent(); // the path /home/fred
    Path file = p.getFileName(); // the path myprog.properties
    Path root = p.getRoot(); // the path /
```

正如你在第 I 卷中已经看到的，可以从 `Path` 对象构造一个 `Scanner`：

```
    var in = new Scanner(Paths.get("/home/fred/input.txt"));
```

**注意：** 有时，你可能需要与使用 `File` 类而不是 `Path` 接口的旧版 API 进行互操作。`Path` 接口有一个 `toFile` 方法，而 `File` 类有一个 `toPath` 方法。

| `java.nio.file.Paths` |
|---|
| • `static Path get(String first, String... more)`<br>通过连接给定字符串来创建路径。 |

| `java.nio.file.Path` |
|---|
| • `Path resolve(Path other)`<br>• `Path resolve(String other)`<br>如果 other 是绝对路径，则返回 other；否则，返回将 this 和 other 连接后得到的路径。<br><br>• `Path resolveSibling(Path other)`<br>• `Path resolveSibling(String other)`<br>如果 other 是绝对路径，则返回 other；否则，返回将 this 的父路径与 other 连接后得到的路径。<br><br>• `Path relativize(Path other)`<br>返回相对路径，当用 this 解析该路径时，会得到 other。<br><br>• `Path normalize()`<br>移除诸如 `.` 和 `..` 之类的冗余路径元素。<br><br>• `Path toAbsolutePath()`<br>返回与此路径等价的绝对路径。<br><br>• `Path getParent()`<br>返回父路径；如果此路径没有父路径，则返回 null。<br><br>• `Path getFileName()`<br>返回此路径的最后一个组成部分；如果此路径没有组成部分，则返回 null。<br><br>• `Path getRoot()`<br>返回此路径的根组成部分；如果此路径没有根组成部分，则返回 null。<br><br>• `toFile()`<br>从此路径创建一个 File。 |





**java.nio.file.Files 7**

- `static byte[] readAllBytes(Path path)`
- `static String readString(Path path, Charset charset)`
- `static List<String> readAllLines(Path path, Charset charset)`
  读取文件的内容。
- `static Path write(Path path, byte[] contents, OpenOption... options)`
- `static Path write(Path path, String contents, Charset charset, OpenOption... options)`
- `static Path write(Path path, Iterable<? extends CharSequence> contents, OpenOption... options)`
  将给定内容写入文件并返回该路径。
- `static InputStream newInputStream(Path path, OpenOption... options)`
- `static OutputStream newOutputStream(Path path, OpenOption... options)`
- `static BufferedReader newBufferedReader(Path path, Charset charset)`
- `static BufferedWriter newBufferedWriter(Path path, Charset charset, OpenOption... options)`
  打开文件以进行读取或写入。

### 2.4.3 创建文件和目录

要创建新目录，请调用

```java
Files.createDirectory(path);
```

路径中除最后一个组件外，其余部分必须已经存在。若要同时创建中间目录，请使用

```java
Files.createDirectories(path);
```

你可以使用以下方法创建空文件：

```java
Files.createFile(path);
```

如果文件已存在，该调用将抛出异常。存在性检查和创建是原子的。如果文件不存在，它会在其他人有机会执行相同操作之前被创建。

有一些便捷方法可在指定位置或系统特定位置创建临时文件或目录。

```java
Path newPath = Files.createTempFile(dir, prefix, suffix);
Path newPath = Files.createTempFile(prefix, suffix);
Path newPath = Files.createTempDirectory(dir, prefix);
Path newPath = Files.createTempDirectory(prefix);
```

此处，`dir` 是一个 `Path`，`prefix`/`suffix` 是可为 `null` 的字符串。例如，调用 `Files.createTempFile(null, ".txt")` 可能返回诸如 `/tmp/1234405522364837194.txt` 的路径。

创建文件或目录时，你可以指定属性，例如所有者或权限。然而，具体细节取决于文件系统，我们在此不作讨论。

**java.nio.file.Files 7**

- `static Path createFile(Path path, FileAttribute<?>... attrs)`
- `static Path createDirectory(Path path, FileAttribute<?>... attrs)`
- `static Path createDirectories(Path path, FileAttribute<?>... attrs)`
  创建文件或目录。`createDirectories` 方法也会创建所有中间目录。
- `static Path createTempFile(String prefix, String suffix, FileAttribute<?>... attrs)`
- `static Path createTempFile(Path parentDir, String prefix, String suffix, FileAttribute<?>... attrs)`
- `static Path createTempDirectory(String prefix, FileAttribute<?>... attrs)`
- `static Path createTempDirectory(Path parentDir, String prefix, FileAttribute<?>... attrs)`
  在适合存放临时文件的位置或给定父目录中创建临时文件或目录。返回所创建文件或目录的路径。

### 2.4.4 复制、移动和删除文件

要将文件从一个位置复制到另一个位置，只需调用

```java
Files.copy(fromPath, toPath);
```

要移动文件（即复制并删除原文件），请调用

```java
Files.move(fromPath, toPath);
```

如果目标已存在，复制或移动将失败。如果要覆盖现有目标，请使用 `REPLACE_EXISTING` 选项。如果要复制所有文件属性，请使用 `COPY_ATTRIBUTES` 选项。你可以同时提供两者，如下所示：

```java
Files.copy(fromPath, toPath, StandardCopyOption.REPLACE_EXISTING,
    StandardCopyOption.COPY_ATTRIBUTES);
```

你可以指定移动操作应是原子的。这样即可确保要么移动成功完成，要么源文件仍然存在。请使用 `ATOMIC_MOVE` 选项：

```java
Files.move(fromPath, toPath, StandardCopyOption.ATOMIC_MOVE);
```

你也可以将输入流复制到 Path，这仅意味着将输入流保存到磁盘。类似地，你可以将 Path 复制到输出流。请使用以下调用：

```java
Files.copy(inputStream, toPath);
Files.copy(fromPath, outputStream);
```

与其他复制调用一样，你可以根据需要提供复制选项。

最后，要删除文件，只需调用

```java
Files.delete(path);
```

如果文件不存在，此方法将抛出异常，因此你可能希望改用

```java
boolean deleted = Files.deleteIfExists(path);
```

删除方法也可以用于移除空目录。

有关可用于文件操作的选项的汇总，请参见表 2.3。

| `java.nio.file.Files` |
|---|
| • `static Path copy(Path from, Path to, CopyOption... options)`<br>• `static Path move(Path from, Path to, CopyOption... options)`<br>&nbsp;&nbsp;将 `from` 复制或移动到给定的目标位置，并返回 `to`。<br>• `static long copy(InputStream from, Path to, CopyOption... options)`<br>• `static long copy(Path from, OutputStream to, CopyOption... options)`<br>&nbsp;&nbsp;将输入流复制到文件，或将文件复制到输出流，返回复制的字节数。<br>• `static void delete(Path path)`<br>• `static boolean deleteIfExists(Path path)`<br>&nbsp;&nbsp;删除给定的文件或空目录。如果文件或目录不存在，第一个方法会抛出异常；第二个方法在这种情况下返回 `false`。 |

**表 2.3 文件操作的标准选项**

| 选项 | 描述 |
|---|---|
| `StandardOpenOption`；与 `newBufferedWriter`、`newInputStream`、`newOutputStream`、`write` 一起使用 | |
| `READ` | 打开以进行读取 |
| `WRITE` | 打开以进行写入 |
| `APPEND` | 如果为写入而打开，则追加到文件末尾 |
| `TRUNCATE_EXISTING` | 如果为写入而打开，则移除现有内容 |
| `CREATE_NEW` | 创建新文件，如果文件已存在则失败 |
| `CREATE` | 如果文件不存在，则原子地创建新文件 |
| `DELETE_ON_CLOSE` | 在文件关闭时“尽力”删除该文件 |
| `SPARSE` | 向文件系统提示此文件将是稀疏文件 |
| `DSYNC` 或 `SYNC` | 要求将每次对文件数据或数据及元数据的更新同步写入存储设备 |
| `StandardCopyOption`；与 `copy`、`move` 一起使用 | |
| `ATOMIC_MOVE` | 原子地移动文件 |
| `COPY_ATTRIBUTES` | 复制文件属性 |
| `REPLACE_EXISTING` | 如果目标存在则替换目标 |
| `LinkOption`；与上述所有方法以及 exists、`isDirectory`、`isRegularFile` 一起使用 | |
| `NOFOLLOW_LINKS` | 不跟随符号链接 |
| `FileVisitOption`；与 `find`、`walk`、`walkFileTree` 一起使用 | |
| `FOLLOW_LINKS` | 跟随符号链接 |

### 2.4.5 获取文件信息

以下静态方法返回一个布尔值，用于检查路径的某个属性：

- `exists`
- `isHidden`
- `isReadable`、`isWritable`、`isExecutable`
- `isRegularFile`、`isDirectory`、`isSymbolicLink`

size 方法返回文件中的字节数。

```java
long fileSize = Files.size(path);
```

getOwner 方法返回文件的所有者，作为 java.nio.file.attribute.UserPrincipal 的一个实例。

所有文件系统都会报告一组基本属性，这些属性由 BasicFileAttributes 接口封装，与上述信息部分重叠。基本文件属性如下：

- 文件的创建时间、最后访问时间和最后修改时间，作为类 java.nio.file.attribute.FileTime 的实例
- 该文件是常规文件、目录、符号链接，还是三者皆非
- 文件大小
- 文件键——某个类的对象，特定于文件系统，可能唯一标识文件，也可能不唯一标识

要获取这些属性，请调用

```java
BasicFileAttributes attributes = Files.readAttributes(path, BasicFileAttributes.class);
```

如果你知道用户的文件系统符合 POSIX，则可以改为获取 PosixFileAttributes 的实例：

```java
PosixFileAttributes attributes = Files.readAttributes(path, PosixFileAttributes.class);
```

然后你可以查明文件的组所有者以及所有者、组和其他用户的访问权限。我们不会深入讨论这些细节，因为其中大部分信息在操作系统之间并不具有可移植性。

**java.nio.file.Files 7**

- `static boolean exists(Path path)`
- `static boolean isHidden(Path path)`
- `static boolean isReadable(Path path)`
- `static boolean isWritable(Path path)`
- `static boolean isExecutable(Path path)`
- `static boolean isRegularFile(Path path)`
- `static boolean isDirectory(Path path)`
- `static boolean isSymbolicLink(Path path)`
  检查路径所指定文件的给定属性。
- `static long size(Path path)`
  以字节为单位获取文件大小。
- `static <A> A readAttributes(Path path, Class<A> type, LinkOption... options)`
  读取类型为 A 的文件属性。





| `java.nio.file.attribute.BasicFileAttributes` | 7 |
|---|---|
| • `FileTime creationTime()` | |
| • `FileTime lastAccessTime()` | |
| • `FileTime lastModifiedTime()` | |
| • `boolean isRegularFile()` | |
| • `boolean isDirectory()` | |
| • `boolean isSymbolicLink()` | |
| • `long size()` | |
| • `Object fileKey()` | |
| 获取所请求的属性。 | |

### 2.4.6 遍历目录条目

静态的 `Files.list` 方法返回一个 `Stream<Path>`，用于读取目录中的条目。目录是惰性读取的，因此可以高效处理包含大量条目的目录。

由于读取目录涉及需要关闭的系统资源，因此应使用 try 块：

```
try (Stream<Path> entries = Files.list(pathToDirectory))
{
    ...
}
```

`list` 方法不会进入子目录。若要处理目录的所有后代，请改用 `Files.walk` 方法。

```
try (Stream<Path> entries = Files.walk(pathToRoot))
{
    // 包含所有后代，按深度优先顺序访问
}
```

以下是对解压后的 src.zip 目录树进行遍历的示例：

```
java
java/nio
java/nio/DirectoryBuffer.java
java/nio/ByteBufferAsShortBufferRL.java
java/nio/MappedByteBuffer.java
...
java/nio/ByteBufferAsDoubleBufferFB.java
java/nio/charset
java/nio/charset/CoderMalfunctionError.java
java/nio/charset/CharsetDecoder.java
java/nio/charset/UnsupportedCharsetException.java
java/nio/charset/spi
java/nio/charset/spi/CharsetProvider.java
java/nio/charset/StandardCharsets.java
java/nio/charset/Charset.java
. . .
java/nio/charset/CoderResult.java
java/nio/HeapFloatBuffer.java
. . . .
```

如你所见，每当遍历遇到一个目录时，会先进入该目录，然后再继续处理其兄弟节点。

你可以通过调用 `Files.walk(pathToRoot, depth)` 来限制要访问的树的深度。两个 walk 方法都有一个 `FileVisitOption` 类型的可变参数……但你只能提供一个选项：`FOLLOW_LINKS`，用于跟随符号链接。

> **注意：** 如果你要过滤 walk 返回的路径，并且过滤条件涉及与目录一起存储的文件属性（例如大小、创建时间或类型（文件、目录、符号链接）），那么应使用 `find` 方法而不是 `walk`。调用该方法时，需要传入一个谓词函数，该函数接受一个路径和一个 `BasicFileAttributes` 对象。这样做的好处只是效率更高。由于无论如何都要读取目录，因此这些属性已经可用。

以下代码片段使用 `Files.walk` 方法将一个目录复制到另一个目录：

```
Files.walk(source).forEach(p ->
{
    try
    {
        Path q = target.resolve(source.relative(p));
        if (Files.isDirectory(p))
            Files.createDirectory(q);
        else
            Files.copy(p, q);
    }
    catch (IOException ex)
    {
        throw new UncheckedIOException(ex);
    }
});
```

遗憾的是，你不能轻松地使用 `Files.walk` 方法删除目录树，因为你需要先删除子项，然后再删除父项。下一节将向你展示如何解决该问题。

### 2.4.7 使用目录流

如前一节所述，`Files.walk` 方法会生成一个 `Stream<Path>`，用于遍历目录的后代。有时，你需要对遍历过程进行更细粒度的控制。在这种情况下，请改用 `Files.newDirectoryStream` 对象。它会生成一个 `DirectoryStream`。请注意，这不是 `java.util.stream.Stream` 的子接口，而是专门用于目录遍历的接口。它是 `Iterable` 的子接口，因此你可以在增强的 for 循环中使用目录流。用法模式如下：

```
try (DirectoryStream<Path> entries = Files.newDirectoryStream(dir))
{
    for (Path entry : entries)
        Process entries
}
```

try-with-resources 块确保目录流被正确关闭。

目录条目的访问顺序没有特定规定。

你可以使用 glob 模式过滤文件：

```
try (DirectoryStream<Path> entries = Files.newDirectoryStream(dir, "*.java"))
```

表 2.4 显示了所有 glob 模式。

**表 2.4 Glob 模式**

| 模式 | 描述 | 示例 |
|---|---|---|
| `*` | 匹配路径组件中的零个或多个字符。 | `*.java` 匹配当前目录中的所有 Java 文件。 |
| `**` | 匹配零个或多个字符，可跨越目录边界。 | `**.java` 匹配任何子目录中的所有 Java 文件。 |
| `?` | 匹配一个字符。 | `????.java` 匹配所有四个字符（不包括扩展名）的 Java 文件。 |
| `[...]` | 匹配一组字符。可以使用连字符（`[0-9]`）和取反（`[!0-9]`）。 | `Test[0-9].java` 匹配 Test0.java，其中 x 是一个十六进制数字。 |
| `{...}` | 匹配以逗号分隔的替代项。 | `*.{java,class}` 匹配所有 Java 和 class 文件。 |
| `\` | 转义上述任何字符以及 `\` 本身。 | `**\*` 匹配所有名称中包含 `*` 的文件。 |

> **警告：** 如果你在 Windows 上使用 glob 语法，则必须对反斜杠进行*两次*转义：一次是针对 glob 语法，一次是针对 Java 字符串语法：`Files.newDirectoryStream(dir, "C:\\\*")`。

如果要访问目录的所有后代，请调用 `walkFileTree` 方法，并提供一个 `FileVisitor` 类型的对象。该对象会在以下情况得到通知：

- 遇到文件时：`FileVisitResult visitFile(T path, BasicFileAttributes attrs)`
- 处理目录之前：`FileVisitResult preVisitDirectory(T dir, IOException ex)`
- 处理目录之后：`FileVisitResult postVisitDirectory(T dir, IOException ex)`
- 尝试访问文件或目录时发生错误（例如尝试打开没有必要权限的目录）：`FileVisitResult visitFileFailed(T path, IOException ex)`

在每种情况下，你都可以指定是否：

- 继续访问下一个文件：`FileVisitResult.CONTINUE`
- 继续遍历，但不访问此目录中的条目：`FileVisitResult.SKIP_SUBTREE`
- 继续遍历，但不访问此文件的兄弟节点：`FileVisitResult.SKIP_SIBLINGS`
- 终止遍历：`FileVisitResult.TERMINATE`

如果任何方法抛出异常，遍历也会终止，并且该异常会从 `walkFileTree` 方法中抛出。

> **注意：** `FileVisitor` 接口是一个泛型类型，但你不太可能需要除 `FileVisitor<Path>` 之外的任何类型。`walkFileTree` 方法愿意接受 `FileVisitor<? super Path>`，但 `Path` 并没有很多超类型。

便捷类 `SimpleFileVisitor` 实现了 `FileVisitor` 接口。除 `visitFileFailed` 之外的所有方法都不执行任何操作并继续。`visitFileFailed` 方法会抛出导致失败的异常，从而终止访问。

例如，以下代码展示如何打印出给定目录的所有子目录：

```java
Files.walkFileTree(Paths.get("/"), new SimpleFileVisitor<Path>()
{
    public FileVisitResult preVisitDirectory(Path path, BasicFileAttributes attrs)
        throws IOException
    {
        System.out.println(path);
        return FileVisitResult.CONTINUE;
    }

    public FileVisitResult postVisitDirectory(Path dir, IOException exc)
    {
        return FileVisitResult.CONTINUE;
    }

    public FileVisitResult visitFileFailed(Path path, IOException exc)
        throws IOException
    {
        return FileVisitResult.SKIP_SUBTREE;
    }
});
```

请注意，我们需要重写 `postVisitDirectory` 和 `visitFileFailed`。否则，一旦遇到不允许打开的目录或不允许访问的文件，访问就会失败。

还要注意，路径的属性会作为参数传递给 `preVisitDirectory` 和 `visitFile` 方法。访问器已经进行了 OS 调用来获取属性，因为它需要区分文件和目录。这样，你就不需要再进行一次调用。

`FileVisitor` 接口的其他方法在进入或离开目录时需要执行某些工作时非常有用。例如，当你删除目录树时，需要在删除目录中的所有文件后，再删除当前目录。这是删除目录树的完整代码：

```java
// Delete the directory tree starting at root
Files.walkFileTree(root, new SimpleFileVisitor<Path>()
{
    public FileVisitResult visitFile(Path file, BasicFileAttributes attrs)
        throws IOException
    {
        Files.delete(file);
        return FileVisitResult.CONTINUE;
    }
});
```




```java
public FileVisitResult postVisitDirectory(Path dir, IOException e) throws IOException
{
    if (e != null) throw e;
    Files.delete(dir);
    return FileVisitResult.CONTINUE;
}
```

| 类/接口 | 版本 | 说明 |
| --- | --- | --- |
| `java.nio.file.Files` | 7 | • `static DirectoryStream<Path> newDirectoryStream(Path path)`<br>• `static DirectoryStream<Path> newDirectoryStream(Path path, String glob)`<br>获取给定目录中文件和目录的迭代器。第二个方法只接受与给定 glob 模式匹配的条目。<br>• `static Path walkFileTree(Path start, FileVisitor<? super Path> visitor)`<br>遍历给定路径的所有后代，并将 visitor 应用于所有后代。 |

| 类/接口 | 版本 | 说明 |
| --- | --- | --- |
| `java.nio.file.SimpleFileVisitor<T>` | 7 | • `static FileVisitResult visitFile(T path, BasicFileAttributes attrs)`<br>在访问文件或目录时调用；返回 CONTINUE、SKIP_SUBTREE、SKIP_SIBLINGS 或 TERMINATE 之一。默认实现不执行任何操作并继续。<br>• `static FileVisitResult preVisitDirectory(T dir, BasicFileAttributes attrs)`<br>• `static FileVisitResult postVisitDirectory(T dir, IOException exc)`<br>在访问目录之前和之后调用。默认实现不执行任何操作并继续。<br>• `static FileVisitResult visitFileFailed(T path, IOException exc)`<br>如果在尝试获取给定文件的信息时抛出异常，则调用此方法。默认实现会重新抛出该异常，这会导致访问以该异常终止。如果希望继续，请重写该方法。 |

### 2.4.8 ZIP 文件系统

Paths 类在默认文件系统中查找路径——即用户本地磁盘上的文件。你也可以拥有其他文件系统。其中一种更有用的文件系统是 ZIP 文件系统。如果 zipname 是一个 ZIP 文件的名称，那么调用

```java
FileSystem fs = FileSystems.newFileSystem(Paths.get(zipname), null);
```

将建立一个包含该 ZIP 归档中所有文件的文件系统。如果你知道文件名，从该归档中复制文件是很容易的：

```
    Files.copy(fs.getPath(sourceName), targetPath);
```

这里，`fs.getPath` 类似于任意文件系统中的 `Paths.get`。

要列出 ZIP 归档中的所有文件，可以遍历文件树：

```
    FileSystem fs = FileSystems.newFileSystem(Paths.get(zipname), null);
    Files.walkFileTree(fs.getPath("/"), new SimpleFileVisitor<Path>()
       {
          public FileVisitResult visitFile(Path file, BasicFileAttributes attrs)
             throws IOException
          {
             System.out.println(file);
             return FileVisitResult.CONTINUE;
          }
       });
```

这比第 85 页 2.2.3 节“ZIP 归档”中描述的 API 更好，那个 API 需要一组新类来处理 ZIP 归档。

| 类/接口 | 版本 | 说明 |
| --- | --- | --- |
| `java.nio.file.FileSystems` | 7 | • `static FileSystem newFileSystem(Path path, ClassLoader loader)`<br>遍历已安装的文件系统提供程序，并且如果 loader 不为 null，还遍历给定类加载器能够加载的文件系统。返回第一个接受给定路径的文件系统提供程序创建的文件系统。默认情况下，有一个 ZIP 文件系统的提供程序，它接受名称以 `.zip` 或 `.jar` 结尾的文件。 |

| 类/接口 | 版本 | 说明 |
| --- | --- | --- |
| `java.nio.file.FileSystem` | 7 | • `static Path getPath(String first, String... more)`<br>通过连接给定的字符串来创建路径。 |

## 2.5 内存映射文件

大多数操作系统可以利用虚拟内存实现将文件或文件的一部分“映射”到内存中。然后就可以像访问内存数组一样访问该文件，这比传统的文件操作要快得多。

### 2.5.1 内存映射文件的性能

在本节末尾，你会找到一个程序，该程序使用传统文件输入和内存映射文件计算文件的 CRC32 校验和。在一台机器上，我们计算 JDK 的 jre/lib 目录中 37MB 的 rt.jar 文件的校验和时，得到了表 2.5 所示的计时数据。

**表 2.5 文件操作的计时数据**

| 方法 | 时间 |
| --- | --- |
| 普通输入流 | 110 秒 |
| 缓冲输入流 | 9.9 秒 |
| 随机访问文件 | 162 秒 |
| 内存映射文件 | 7.2 秒 |

如你所见，在这台特定机器上，内存映射比使用缓冲的顺序输入稍快，并且比使用 RandomAccessFile 快得多。

当然，具体数值会因机器不同而有很大差异，但很明显，与随机访问相比，性能提升是显著的。另一方面，对于中等大小文件的顺序读取，没有理由使用内存映射。

`java.nio` 包让内存映射变得非常简单。下面是具体做法。

首先，为文件获取一个*通道*。通道是磁盘文件的一种抽象，允许你访问操作系统特性，如内存映射、文件锁以及文件之间的快速数据传输。

```
    FileChannel channel = FileChannel.open(path, options);
```

然后，通过调用 `FileChannel` 类的 `map` 方法从通道获取一个 `ByteBuffer`。指定要映射的文件区域和*映射模式*。支持三种模式：

- `FileChannel.MapMode.READ_ONLY`：生成的缓冲区是只读的。任何对缓冲区进行写入的尝试都会导致 `ReadOnlyBufferException`。
- `FileChannel.MapMode.READ_WRITE`：生成的缓冲区是可写的，并且更改将在某个时候写回文件。请注意，映射了同一文件的其他程序可能不会立即看到这些更改。多个程序同时映射文件的确切行为取决于操作系统。
- `FileChannel.MapMode.PRIVATE`：生成的缓冲区是可写的，但任何更改都对此缓冲区私有，不会传播到文件。

一旦你有了缓冲区，就可以使用 ByteBuffer 类及其父类 Buffer 的方法读写数据。

缓冲区支持顺序和随机数据访问。缓冲区有一个*位置*，它通过 get 和 put 操作推进。例如，你可以按顺序遍历缓冲区中的所有字节，如下所示：

```
while (buffer.hasRemaining())
{
    byte b = buffer.get();
    . . .
}
```

或者，你可以使用随机访问：

```
for (int i = 0; i < buffer.limit(); i++)
{
    byte b = buffer.get(i);
    . . .
}
```

你还可以使用以下方法读写字节数组：

```
get(byte[] bytes)
get(byte[] bytes, int offset, int length)
```

最后，还有以下方法：

```
getInt          getChar
getLong         getFloat
getShort        getDouble
```

用于读取以*二进制*值存储在文件中的基本类型值。正如我们已经提到的，Java 对二进制数据使用大端序。然而，如果你需要处理包含小端序二进制数的文件，只需调用

```
buffer.order(ByteOrder.LITTLE_ENDIAN);
```

要确定缓冲区当前的字节顺序，请调用

```
ByteOrder b = buffer.order();
```

> **警告：** 这一对方法不使用 set/get 命名约定。

要向缓冲区写入数字，请使用以下方法之一：

```
putInt        putChar
putLong       putFloat
putShort      putDouble
```

在某个时刻，当然是在通道关闭时，这些更改会被写回文件。

清单 2.5 计算文件的 32 位循环冗余校验和（CRC32）。该校验和通常用于确定文件是否已损坏。文件损坏很可能导致校验和发生变化。java.util.zip 包中包含一个 CRC32 类，它使用以下循环计算字节序列的校验和：

```
var crc = new CRC32();
while (more bytes)
    crc.update(next byte);
long checksum = crc.getValue();
```

CRC 计算的细节并不重要。我们只是将其作为有用文件操作的一个示例。（在实践中，你会以更大的块读取和更新数据，而不是一次一个字节。这样速度差异就不会那么明显。）

按以下方式运行程序：

```
java memoryMap.MemoryMapTest filename
```

### 清单 2.5 memoryMap/MemoryMapTest.java

```java
package memoryMap;

import java.io.*;
import java.nio.*;
import java.nio.channels.*;
import java.nio.file.*;
import java.util.zip.*;

/**
 * This program computes the CRC checksum of a file in four ways. <br>
 * Usage: java memoryMap.MemoryMapTest filename
 * @version 1.02 2018-03-01
 * @author Cay Horstmann
 */
```

*（续）*

### 代码清单 2.5（续）

```java
public class MemoryMapTest
{
    public static long checksumInputStream(Path filename) throws IOException
    {
        try (InputStream in = Files.newInputStream(filename))
        {
            var crc = new CRC32();

            int c;
            while ((c = in.read()) != -1)
                crc.update(c);
            return crc.getValue();
        }
    }

    public static long checksumBufferedInputStream(Path filename) throws IOException
    {
        try (var in = new BufferedInputStream(Files.newInputStream(filename)))
        {
            var crc = new CRC32();

            int c;
            while ((c = in.read()) != -1)
                crc.update(c);
            return crc.getValue();
        }
    }

    public static long checksumRandomAccessFile(Path filename) throws IOException
    {
        try (var file = new RandomAccessFile(filename.toFile(), "r"))
        {
            long length = file.length();
            var crc = new CRC32();

            for (long p = 0; p < length; p++)
            {
                file.seek(p);
                int c = file.readByte();
                crc.update(c);
            }
            return crc.getValue();
        }
    }

    public static long checksumMappedFile(Path filename) throws IOException
    {
        try (FileChannel channel = FileChannel.open(filename))
        {
            var crc = new CRC32();
            int length = (int) channel.size();
            MappedByteBuffer buffer = channel.map(FileChannel.MapMode.READ_ONLY, 0, length);

            for (int p = 0; p < length; p++)
            {
                int c = buffer.get(p);
                crc.update(c);
            }
            return crc.getValue();
        }
    }

    public static void main(String[] args) throws IOException
    {
        System.out.println("Input Stream:");
        long start = System.currentTimeMillis();
        Path filename = Paths.get(args[0]);
        long crcValue = checksumInputStream(filename);
        long end = System.currentTimeMillis();
        System.out.println(Long.toHexString(crcValue));
        System.out.println((end - start) + " milliseconds");

        System.out.println("Buffered Input Stream:");
        start = System.currentTimeMillis();
        crcValue = checksumBufferedInputStream(filename);
        end = System.currentTimeMillis();
        System.out.println(Long.toHexString(crcValue));
        System.out.println((end - start) + " milliseconds");

        System.out.println("Random Access File:");
        start = System.currentTimeMillis();
        crcValue = checksumRandomAccessFile(filename);
        end = System.currentTimeMillis();
        System.out.println(Long.toHexString(crcValue));
        System.out.println((end - start) + " milliseconds");

        System.out.println("Mapped File:");
        start = System.currentTimeMillis();
        crcValue = checksumMappedFile(filename);
        end = System.currentTimeMillis();
        System.out.println(Long.toHexString(crcValue));
        System.out.println((end - start) + " milliseconds");
    }
}
```

### java.nio.ByteBuffer 1.4

- `byte get()`  
  从当前位置获取一个字节，并将当前位置推进到下一个字节。
- `byte get(int index)`  
  从指定索引处获取一个字节。
- `ByteBuffer put(byte b)`  
  在当前���置放入一个字节，并将当前位置推进到下一个字节。返回对该缓冲区的引用。
- `ByteBuffer put(int index, byte b)`  
  在指定索引处放入一个字节。返回对该缓冲区的引用。
- `ByteBuffer get(byte[] destination)`  
- `ByteBuffer get(byte[] destination, int offset, int length)`  
  用缓冲区中的字节填充一个字节数组或字节数组的某个区域，并将当前位置前进读取的字节数。如果缓冲区中剩余字节不足，则不读取任何字节，并抛出 `BufferUnderflowException`。返回对该缓冲区的引用。
- `ByteBuffer put(byte[] source)`  
- `ByteBuffer put(byte[] source, int offset, int length)`  
  将字节数组中的所有字节，或字节数组某个区域中的字节，放入缓冲区，并将当前位置前进读取的字节数。如果缓冲区中剩余字节不足，则不写入任何字节，并抛出 `BufferOverflowException`。返回对该缓冲区的引用。
- `Xxx getXxx()`  
- `Xxx getXxx(int index)`  
- `ByteBuffer putXxx(Xxx value)`  
- `ByteBuffer putXxx(int index, Xxx value)`  
  获取或放入一个二进制数。`Xxx` 是 `Int`、`Long`、`Short`、`Char`、`Float` 或 `Double` 之一。
- `ByteBuffer order(ByteOrder order)`  
- `ByteOrder order()`  
  设置或获取字节顺序。order 的值为 `ByteOrder` 类的常量 `BIG_ENDIAN` 或 `LITTLE_ENDIAN` 之一。
- `static ByteBuffer allocate(int capacity)`  
  构造一个具有给定容量的缓冲区。

### java.nio.ByteBuffer 1.4 *（续）*

| 方法 | 描述 |
|---|---|
| `static ByteBuffer wrap(byte[] values)` | 构造一个由给定数组支持的缓冲区。 |
| `CharBuffer asCharBuffer()` | 构造一个由此缓冲区支持的字符缓冲区。对字符缓冲区的更改会反映到此缓冲区中，但字符缓冲区有自己的位置、限制和标记。 |

### java.nio.CharBuffer 1.4

| 方法 | 描述 |
|---|---|
| `char get()`<br>`CharBuffer get(char[] destination)`<br>`CharBuffer get(char[] destination, int offset, int length)` | 从缓冲区的位置开始获取一个 char 值或一段 char 值，并将位置移过已读取的字符。最后两个方法返回 this。 |
| `CharBuffer put(char c)`<br>`CharBuffer put(char[] source)`<br>`CharBuffer put(char[] source, int offset, int length)`<br>`CharBuffer put(String source)`<br>`CharBuffer put(CharBuffer source)` | 从缓冲区的位置开始放入一个 char 值或一段 char 值，并将位置推进到已写入字符之后。从 CharBuffer 读取时，会读取所有剩余字符。所有方法均返回 this。 |

### 2.5.2 缓冲区数据结构

使用内存映射时，你会创建一个跨越整个文件或你所关心的文件区域的单一缓冲区。你也可以使用缓冲区来读写更小块的信息。

本节简要描述 Buffer 对象的基本操作。缓冲区是一个由相同类型的值组成的数组。Buffer 类是一个抽象类，具体子类包括 ByteBuffer、CharBuffer、DoubleBuffer、FloatBuffer、IntBuffer、LongBuffer 和 ShortBuffer。

> 注意：StringBuffer 类与这些缓冲区无关。

在实践中，你最常使用的是 `ByteBuffer` 和 `CharBuffer`。如图 2.9 所示，缓冲区具有

- *容量*，永不改变
- *位置*，即读取或写入下一个值的位置
- *限制*，超过该限制后读写便没有意义
- 可选地，*标记*，用于重复读或写操作

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_155_0.png)

**图 2.9** 缓冲区

这些值满足条件

$0 \leq mark \leq position \leq limit \leq capacity$

缓冲区的主要用途是“先写入，再读取”的循环。一开始，缓冲区的位置为 0，限制为容量。持续调用 put 向缓冲区添加值。当数据用完或达到容量时，就该切换到读取。

调用 flip 将限制设置为当前位置，并将位置设置为 0。现在，只要 remaining 方法（返回 *limit − position*）为正，就持续调用 get。读完缓冲区中的所有值后，调用 clear 为下一个写入循环做好准备。clear 方法将位置重置为 0，并将限制重置为容量。

如果要重新读取缓冲区，请使用 rewind 或 mark/reset（详情见 API 注释）。

要获得缓冲区，请调用静态方法，例如 `ByteBuffer.allocate` 或 `ByteBuffer.wrap`。然后，你可以从通道填充缓冲区，或将其内容写入通道。例如，


```java
ByteBuffer buffer = ByteBuffer.allocate(RECORD_SIZE);
channel.read(buffer);
channel.position(newpos);
buffer.flip();
channel.write(buffer);
```

这可以成为随机访问文件的一种有用替代方案。

**java.nio.Buffer 1.4**

- `Buffer clear()`
  - 通过将位置设置为 0、限制设置为容量来准备写入此缓冲区；返回此缓冲区。
- `Buffer flip()`
  - 通过将限制设置为当前位置、位置设置为 0，准备在写入后读取此缓冲区；返回此缓冲区。
- `Buffer rewind()`
  - 通过将位置设置为 0 并保持限制不变，准备重新读取相同值；返回此缓冲区。
- `Buffer mark()`
  - 将此缓冲区的标记设置为当前位置；返回此缓冲区。
- `Buffer reset()`
  - 将此缓冲区的位置设置为标记，从而允许再次读取或写入已标记部分；返回此缓冲区。
- `int remaining()`
  - 返回剩余可读或可写值的数量——即限制与位置之差。
- `int position()`
- `void position(int newValue)`
  - 获取和设置此缓冲区的位置。
- `int capacity()`
  - 返回此缓冲区的容量。

## 2.6 文件锁定

当多个同时执行的程序需要修改同一个文件时，它们需要以某种方式通信，否则文件很容易损坏。文件锁可以解决这个问题。文件锁控制对文件或文件中某个字节范围的访问。

假设你的应用程序保存一个包含用户首选项的配置文件。如果用户调用了应用程序的两个实例，可能会出现两者都想同时写入配置文件的情况。在这种情况下，第一个实例应锁定该文件。当第二个实例发现文件已锁定时，它可以决定等到文件解锁，或者直接跳过写入过程。

要锁定文件，请调用 `FileChannel` 类的 `lock` 或 `tryLock` 方法。

```
FileChannel channel = FileChannel.open(path);
FileLock lock = channel.lock();
```

或

```
FileLock lock = channel.tryLock();
```

第一次调用会阻塞，直到锁可用。第二次调用立即返回：如果锁可用则返回该锁，否则返回 null。文件会保持锁定，直到通道关闭或对锁调用 `release` 方法。

也可以使用以下调用锁定文件的一部分

```
FileLock lock(long start, long size, boolean shared)
```

或

```
FileLock tryLock(long start, long size, boolean shared)
```

`shared` 标志为 false 时，会锁定文件以进行读取和写入。为 true 时表示共享锁，它允许多个进程读取该文件，同时阻止任何进程获取独占锁。并非所有操作系统都支持共享锁。即使你只是请求共享锁，也可能得到独占锁。调用 `FileLock` 类的 `isShared` 方法可以查明你拥有的是哪种锁。

> **注意：** 如果锁定文件的尾部，而文件随后增长到超出锁定部分，则新增区域不会被锁定。要锁定所有字节，请使用 `Long.MAX_VALUE` 作为大小。

完成后务必解锁。一如既往，最好使用 try-with-resources 语句来完成：

```
try (FileLock lock = channel.lock())
{
    access the locked file or segment
}
```

## 2.7 正则表达式

正则表达式用于指定字符串模式。每当需要定位匹配特定模式的字符串时，都可以使用正则表达式。例如，我们的一个示例程序通过查找模式为 `<a href=". . .">` 的字符串，来定位 HTML 文件中的所有超链接。

当然，在指定模式时，`. . .` 这种表示法不够精确。你需要使用一种描述模式的特殊语法，准确指定什么样的字符序列才是合法匹配。

在以下各节中，我们将介绍 Java API 使用的正则表达式语法，并讨论如何让正则表达式发挥作用。

### 2.7.1 正则表达式语法

让我们从一个简单示例开始。正则表达式

```
[Jj]ava.+
```

匹配以下形式的任意字符串：

- 第一个字母是 J 或 j。
- 接下来的三个字母是 `ava`。
- 字符串的其余部分由一个或多个任意字符组成。

例如，字符串 "Javaese" 匹配这个特定的正则表达式，而字符串 "core Java" 不匹配。

如你所见，需要了解一点语法才能理解正则表达式的含义。幸运的是，对于大多数用途，几个简单的结构就足够了。

- 一个*字符类*是一组字符备选项，括在方括号中，例如 `[Jj]`、`[0-9]`、`[A-Za-z]` 或 `[^0-9]`。这里 `-` 表示范围（Unicode 值落在两个边界之间的所有字符），`^` 表示补集（除指定字符之外的所有字符）。
- 要在字符类中包含 `-`，请将其放在第一项或最后一项。要包含 `]`，请将其放在第一项。要包含 `^`，请将其放在除开头之外的任何位置。只需要转义 `[` 和 `\`。
- 有许多预定义字符类，例如 `\d`（数字）或 `\p{Sc}`（Unicode 货币符号）。参见表 2.6 和表 2.7。

**表 2.6 正则表达式语法**

| 表达式 | 描述 | 示例 |
|---|---|---|
| **字符** |  |  |
| `c`, not one of `. * + ?`<br>`{ \| ( ) [ \ ^ $` | 字符 `c` | `c` |
| `.` | 除行终止符之外的任意字符；如果设置了 DOTALL 标志，则为任意字符 |  |
| `\x{p}` | 十六进制代码为 `p` 的 Unicode 码点 | `\x{10546}` |
| `\uhhhh, \xhh, \0o, \00, \0000` | 具有给定十六进制或八进制值的 UTF-16 代码单元 | `\uFEFF` |
| `\a, \e, \f, \n, \r, \t` | 警报符（`\x{7}`）、转义符（`\x{1B}`）、换页符（`\x{C}`）、换行符（`\x{A}`）、回车符（`\x{D}`）、制表符（`\x{9}`） | `\n` |
| `\cC`, where `c` is in `[A-Z]` or one of `@ [ \ ] ^ _` | 与字符 `c` 对应的控制字符 | `\cH` 是退格符（`\x{8}`） |
| `\c_` where `c` is not in `[A-Za-z0-9]` | 字符 `c` | `\` |
| `\Q...\E` | 引号开始和结束之间的所有内容 | `\Q( . . . )\E` 匹配字符串 `( . . . )` |
| **字符类** |  |  |
| `[C₁C₂...Cₙ]`, where `Cᵢ` are characters, ranges `c-d`, or character classes | 由 `C₁, C₂, ...` 表示的任意字符 | `[0-9.+]` |
| `[^...]` | 字符类的补集 | `[^\d\s]` |
| `[..., && ...]` | 字符类的交集 | `[\p{L}&&[^A-Za-z]]` |
| `\p{...}, \P{...}` | 预定义字符类（见表 2.7）；其补集 | `\p{L}` 匹配一个 Unicode 字母，`\pL` 也一样——可以省略单个字母周围的花括号 |
| `\d`, `\D` | 数字（`[0-9]`，或设置 UNICODE CHARACTER CLASS 标志时为 `\p{Digit}`）；其补集 | `\d+` 是一个数字序列 |
| `\w`, `\W` | 单词字符（`[a-zA-Z0-9_]`，或设置 UNICODE CHARACTER CLASS 标志时为 Unicode 单词字符）；其补集 |  |
| `\s`, `\S` | 空白（`\n\r\t\f\x{B}`，或设置 UNICODE CHARACTER CLASS 标志时为 `\p{IsWhite_Space}`）；其补集 | `\s*,\s*` 是由可选空白包围的逗号 |
| `\h`, `\v`, `\H`, `\V` | 水平空白、垂直空白及其补集 |  |
| **序列与选择** |  |  |
| `XY` | 来自 X 的任意字符串后跟来自 Y 的任意字符串 | `[1-9][0-9]*` 是不带前导零的正数 |
| `X\|Y` | 来自 X 或 Y 的任意字符串 | `http\|ftp` |
| **分组** |  |  |
| `(X)` | 捕获 X 的匹配 | `'('.*')'` 捕获带引号的文本 |
| `\n` | 第 n 个组 | `('('.*')').\1` 匹配 'Fred' 或 "Fred"，但不匹配 'Fred' |
| `(?<name>X)` | 用给定名称捕获 X 的匹配 | `'(?<id>[a-zA-Z0-9]+)'` 捕获名称为 id 的匹配 |
| `\k<name>` | 具有给定名称的组 | `\k<id>` 匹配名称为 id 的组 |
| `(?:X)` | 使用括号但不捕获 X | 在 `(?:http://)?(.*)` 中，`://` 之后的匹配为 `\1` |




#### 表2.6 *（续）*

| 表达式 | 描述 | 示例 |
|---|---|---|
| `(?idmsux-idmsux:X), (?idmsux-idmsux)`，标志位于 `idmsux` 中 | 匹配但不捕获 X，同时开启或关闭（`-` 后）给定标志 | `(?i:jpeg)` 是不区分大小写的匹配 |
| 其他 `(?... )` | 参见 Pattern API 文档 | |
| **量词** |  |  |
| `X?` | 可选的 X | `\+?` 是可选的正号 |
| `X*`, `X+` | 0 个或多个 X，1 个或多个 X | `[1-9][0-9]+` 是 ≥10 的整数 |
| `X{n}`, `X{n,}`, `X{m,n}` | *n* 次 X，至少 *n* 次 X，*m* 到 *n* 次 X | `[0-7]{1,3}` 是一到三位八进制数字 |
| `Q?`，其中 Q 是量化的表达式 | 勉强量词，在尝试更长匹配之前，先尝试最短匹配 | `<.*?>` 捕获尖括号内最短的序列 |
| `Q+`，其中 Q 是量化的表达式 | 占有量词，取最长匹配而不回溯 | `'[^']*+'` 匹配单引号括起的字符串，并在没有结束引号的字符串上快速失败 |
| **边界匹配** |  |  |
| `^`, `$` | 输入的开头、结尾（或多行模式中行的开头、结尾） | `^Java$` 匹配输入或 `Java` 行 |
| `\A`, `\Z`, `\z` | 输入的开头、输入的结尾、输入的绝对结尾（在多行模式下不变） |  |
| `\b`, `\B` | 单词边界，非单词边界 | `\bJava\b` 匹配单词 `Java` |
| `\R` | Unicode 换行符 |  |
| `\G` | 上一次匹配的结束位置 |  |

#### 表2.7 与 \p 一起使用的预定义字符类名称

| 字符类名称 | 说明 |
| --- | --- |
| posixClass | posixClass 是 Lower、Upper、Alpha、Digit、Alnum、Punct、Graph、Print、Cntrl、XDigit、Space、Blank、ASCII 之一，根据 UNICODE_CHARACTER_CLASS 标志解释为 POSIX 或 Unicode 类 |
| IsScript, sc=Script, script=Script | 由 Character.UnicodeScript.forName 接受的脚本 |
| InBlock, blk=Block, block=Block | 由 Character.UnicodeBlock.forName 接受的块 |
| Category, InCategory, gc=Category, general_category=Category | Unicode 通用类别的一字母或两字母名称 |
| IsProperty | Property 是 Alphabetic、Ideographic、Letter、Lowercase、Uppercase、Titlecase、Punctuation、Control、White Space、Digit、Hex_Digit、Join_Control、Noncharacter_Code_Point、Assigned 之一 |
| javaMethod | 调用 Character.isMethod 方法（必须不是已弃用的方法） |

- 大多数字符匹配自身，例如前面示例中的 `ava` 字符。
- `.` 符号匹配任何字符（取决于标志设置，可能不包括行终止符）。
- 使用 `\` 作为转义字符。例如，`\.` 匹配句点，`\\` 匹配反斜杠。
- `^` 和 `$` 分别匹配行的开头和结尾。
- 如果 `X` 和 `Y` 是正则表达式，那么 `XY` 表示“`X` 的任何匹配后跟 `Y` 的匹配”。`X | Y` 表示“`X` 或 `Y` 的任何匹配”。
- 你可以对表达式 `X` 应用量词 `X+`（1 个或多个）、`X*`（0 个或多个）和 `X?`（0 个或 1 个）。
- 默认情况下，量词匹配能使整体匹配成功的最多重复次数。你可以通过后缀 `?`（勉强或吝啬匹配：匹配最少的重复次数）和 `+`（占有或贪婪匹配：匹配最多的次数，即使这会导致整体匹配失败）来修改该行为。

例如，字符串 `cab` 匹配 `[a-z]*ab`，但不匹配 `[a-z]*+ab`。在第一种情况下，表达式 `[a-z]*` 只匹配字符 `c`，因此字符 `ab` 匹配模式中的其余部分。但贪婪版本 `[a-z]*+` 匹配字符 `cab`，导致模式中剩余部分无法匹配。

- 你可以使用组来定义子表达式。将组放在 `( )` 中，例如 `([+-]?)([0-9]+)`。然后你可以让模式匹配器返回每个组的匹配，或者使用 `\n` 对组进行反向引用，其中 n 是组号，从 `\1` 开始。

例如，下面是一个稍微复杂但可能有用的正则表达式，用于描述十进制或十六进制整数：

```text
[+-]?[0-9]+|0[xX][0-9A-Fa-f]+
```

遗憾的是，正则表达式语法在各种程序和库之间并未完全标准化；对于基本结构存在共识，但在细节上有许多令人恼火的差异。Java 正则表达式类使用的语法与 Perl 语言中使用的语法相似，但不完全一样。表2.6 展示了 Java 语法的所有结构。有关正则表达式语法的更多信息，请参阅 Pattern 类的 API 文档或 Jeffrey E. F. Friedl 所著的《精通正则表达式》（O’Reilly and Associates, 2006）。

### 2.7.2 匹配字符串

正则表达式最简单的用途是测试特定字符串是否匹配它。以下是在 Java 中编写该测试的方法。首先，从包含正则表达式的字符串构造一个 Pattern 对象。然后，从该模式获取一个 Matcher 对象并调用其 matches 方法：

```java
Pattern pattern = Pattern.compile(patternString);
Matcher matcher = pattern.matcher(input);
if (matcher.matches()) . . .
```

匹配器的输入是实现了 CharSequence 接口的任何类的对象，例如 String、StringBuilder 或 CharBuffer。

编译模式时，你可以设置一个或多个标志，例如：

```java
Pattern pattern = Pattern.compile(expression,
    Pattern.CASE_INSENSITIVE + Pattern.UNICODE_CASE);
```

你也可以在模式内部指定它们：

```java
String regex = "(?i)an expression";
```

以下是这些标志：

- **Pattern.CASE_INSENSITIVE** 或 **i**：匹配字符时不区分字母大小写。默认情况下，此标志仅考虑 US ASCII 字符。

嵌套组按左括号的顺序排序。例如，给定模式

```text
(([1-9]|[0-2]):([0-5][0-9]))[ap]m
```

和输入

```text
11:59am
```

匹配器报告以下组

| 组索引 | 开始 | 结束 | 字符串 |
|---:|---:|---:|---|
| 0 | 0 | 7 | 11:59am |
| 1 | 0 | 5 | 11:59 |
| 2 | 0 | 2 | 11 |
| 3 | 3 | 5 | 59 |

清单2.6 会提示输入一个模式，然后提示输入要匹配的字符串。它将输出输入是否匹配该模式。如果输入匹配且模式包含组，程序将以括号形式打印组边界，例如：

```text
((11):(59))am
```

#### **清单2.6** `regex/RegexTest.java`

```java
package regex;

import java.util.*;
import java.util.regex.*;

/**
 * This program tests regular expression matching. Enter a pattern and strings to match,
 * or hit Cancel to exit. If the pattern contains groups, the group boundaries are displayed
 * in the match.
 * @version 1.03 2018-05-01
 * @author Cay Horstmann
 */
public class RegexTest
{
   public static void main(String[] args) throws PatternSyntaxException
   {
      var in = new Scanner(System.in);
      System.out.println("Enter pattern: ");
      String patternString = in.nextLine();
      Pattern pattern = Pattern.compile(patternString);

      while (true)
      {
         System.out.println("Enter string to match: ");
         String input = in.nextLine();
         if (input == null || input.equals("")) return;
         Matcher matcher = pattern.matcher(input);
         if (matcher.matches())
         {
            System.out.println("Match");
            int g = matcher.groupCount();
            if (g > 0)
            {
               for (int i = 0; i < input.length(); i++)
               {
                  // Print any empty groups
                  for (int j = 1; j <= g; j++)
                     if (i == matcher.start(j) && i == matcher.end(j))
                        System.out.print("()");
                  // Print ( for non-empty groups starting here
                  for (int j = 1; j <= g; j++)
                     if (i == matcher.start(j) && i != matcher.end(j))
                        System.out.print('(');
                  System.out.print(input.charAt(i));
                  // Print ) for non-empty groups ending here
                  for (int j = 1; j <= g; j++)
                     if (i + 1 != matcher.start(j) && i + 1 == matcher.end(j))
                        System.out.print(')');
               }
               System.out.println();
            }
         }
         else
            System.out.println("No match");
      }
   }
}
```

### 2.7.3 查找多个匹配

通常，你不想将整个输入与正则表达式匹配，而是在输入中查找一个或多个匹配的子字符串。使用 `Matcher` 类的 *find* 方法查找下一个匹配。如果它返回 true，使用 `start` 和 `end` 方法查找匹配的范围，或使用不带参数的 `group` 方法获取匹配的字符串。




```java
while (matcher.find())
{
    int start = matcher.start();
    int end = matcher.end();
    String match = matcher.group();
    . . .
}
```

通过这种方式，你可以依次处理每个匹配项。如代码片段所示，你可以获取匹配的字符串及其在输入字符串中的位置。

更优雅的方式是，你可以调用 results 方法获取一个 `Stream<MatchResult>`。`MatchResult` 接口具有 `group`、`start` 和 `end` 方法，就像 `Matcher` 一样。（事实上，`Matcher` 类实现了该接口。）以下是如何获取所有匹配项的列表：

```java
List<String> matches = pattern.matcher(input)
    .results()
    .map(MatchResult::group)
    .collect(Collectors.toList());
```

如果数据在文件中，你可以使用 `Scanner.findAll` 方法获取一个 `Stream<MatchResult>`，而无需先将内容读入字符串。你可以传入一个 `Pattern` 或模式字符串：

```java
var in = new Scanner(path, StandardCharsets.UTF_8);
Stream<String> words = in.findAll("\\p{L}+")
    .map(MatchResult::group);
```

程序清单 2.7 使用了这一机制。它定位网页中的所有超文本引用并打印它们。要运行该程序，请在命令行中提供一个 URL，例如

```bash
java match.HrefMatch http://horstmann.com
```

#### 程序清单 2.7 `match/HrefMatch.java`

```java
package match;

import java.io.*;
import java.net.*;
import java.nio.charset.*;
import java.util.regex.*;

/**
 * This program displays all URLs in a web page by matching a regular expression that
 * describes the <a href=...> HTML tag. Start the program as <br>
 * java match.HrefMatch URL
12  * @version 1.03 2018-03-19
13  * @author Cay Horstmann
14  */
15 public class HrefMatch
16 {
17    public static void main(String[] args)
18    {
19       try
20       {
21          // get URL string from command line or use default
22          String urlString;
23          if (args.length > 0) urlString = args[0];
24          else urlString = "http://openjdk.java.net/";
25
26          // read contents of URL
27          InputStream in = new URL(urlString).openStream();
28          var input = new String(in.readAllBytes(), StandardCharsets.UTF_8);
29
30          // search for all occurrences of pattern
31          var patternString = "\\bhttps?://[\\w\\d\\./?#\\[\\]@!$&'()*+,;=]*\\b";
32          Pattern pattern = Pattern.compile(patternString, Pattern.CASE_INSENSITIVE);
33          pattern.matcher(input)
34             .results()
35             .map(MatchResult::group)
36             .forEach(System.out::println);
37       }
38       catch (IOException | PatternSyntaxException e)
39       {
40          e.printStackTrace();
41       }
42    }
43 }
```

### 2.7.4 沿分隔符拆分

有时，你希望沿匹配的分隔符拆分输入，并保留其他所有内容。`Pattern.split` 方法可自动完成此任务。你会获得一个字符串数组，其中分隔符已被移除：

```java
String input = . . .
Pattern commas = Pattern.compile("\\s*,\\s*");
String[] tokens = commas.split(input);
// "1, 2, 3" turns into ["1", "2", "3"]
```

如果有很多标记，你可以惰性地获取它们：

```java
Stream<String> tokens = commas.splitAsStream(input);
```

如果你不在意预编译模式或惰性获取，可以直接使用 `String.split` 方法：

```java
String[] tokens = input.split("\\s*,\\s*");
```

如果输入在文件中，请使用扫描器：

```java
var in = new Scanner(path, StandardCharsets.UTF_8);
in.useDelimiter("\\s*,\\s*");
Stream<String> tokens = in.tokens();
```

### 2.7.5 替换匹配项

`Matcher` 类的 `replaceAll` 方法将正则表达式的所有出现替换为替换字符串。例如，以下指令将所有数字序列替换为 `#` 字符：

```java
Pattern pattern = Pattern.compile("[0-9]+");
Matcher matcher = pattern.matcher(input);
String output = matcher.replaceAll("#");
```

替换字符串可以包含对模式中组的引用：`$n` 替换为第 n 个组，`${name}` 替换为具有给定名称的组。使用 `\$` 在替换文本中包含 `$` 字符。

如果你有一个可能包含 `$` 的字符串，并且不希望它们被解释为组替换，请调用 `matcher.replaceAll(Matcher.quoteReplacement(str))`。

如果你希望执行比拼接组匹配更复杂的操作，可以提供替换函数而不是替换字符串。该函数接受一个 `MatchResult` 并生成一个字符串。例如，这里我们将所有至少包含四个字母的单词替换为其大写版本：

```java
String result = Pattern.compile("\\p{L}{4,}")
    .matcher("Mary had a little lamb")
    .replaceAll(m -> m.group().toUpperCase());
// Yields "MARY HAD A LITTLE LAMB"
```

`replaceFirst` 方法仅替换模式的第一次出现。

**`java.util.regex.Pattern` 1.4**

| 方法 | 描述 |
|---|---|
| `static Pattern compile(String expression)`<br>`static Pattern compile(String expression, int flags)` | 将正则表达式字符串编译为模式对象，以便快速处理匹配。flags 参数设置以下一个或多个位：`CASE_INSENSITIVE`、`UNICODE_CASE`、`MULTILINE`、`UNIX_LINES`、`DOTALL` 和 `CANON_EQ`。 |
| `Matcher matcher(CharSequence input)` | 返回一个匹配器对象，你可以使用它来定位输入中模式的匹配项。 |
| `String[] split(CharSequence input)`<br>`String[] split(CharSequence input, int limit)`<br>`Stream<String> splitAsStream(CharSequence input)` 8 | 将输入字符串拆分为标记，模式指定分隔符的形式。返回标记的数组或流。分隔符不属于标记。第二种形式有一个参数 limit，表示要生成的最大字符串数。如果已找到 limit - 1 个匹配的分隔符，则返回数组的最后一项包含剩余的未拆分输入。如果 limit ≤ 0，则拆分整个输入。如果 limit 为 0，则尾随的空字符串不会放入返回的数组中。 |

**`java.util.regex.Matcher` 1.4**

| 方法 | 描述 |
|---|---|
| `boolean matches()` | 如果输入匹配模式，则返回 true。 |
| `boolean lookingAt()` | 如果输入的开头匹配模式，则返回 true。 |
| `boolean find()`<br>`boolean find(int start)` | 尝试查找下一个匹配项，如果找到另一个匹配项则返回 true。 |
| `int start()`<br>`int end()` | 返回当前匹配项的起始位置或结束位置之后的位置。 |
| `String group()` | 返回当前匹配项。 |
| `int groupCount()` | 返回输入模式中的组数。 |
| `int start(int groupIndex)`<br>`int start(String name)` 8<br>`int end(int groupIndex)`<br>`int end(String name)` 8 | 返回当前匹配项中某个组的起始位置或结束位置之后的位置。组由从 1 开始的索引指定，或由 0 表示整个匹配项，或由标识命名组的字符串指定。 |
| `String group(int groupIndex)`<br>`String group(String name)` 7 | 返回与给定组匹配的字符串，该组由从 1 开始的索引表示，或由 0 表示整个匹配项，或由标识命名组的字符串表示。 |
| `String replaceAll(String replacement)`<br>`String replaceFirst(String replacement)` | 返回通过将全部匹配项或第一个匹配项替换为替换字符串而从匹配器输入获得的字符串。替换字符串可以包含对模式组的引用，如 $n。使用 \$ 包含 $ 符号。 |
| `static String quoteReplacement(String str)` 5.0 | 引用 `str` 中的所有 `\` 和 `$`。 |
| `String replaceAll(Function<MatchResult, String> replacer)` 9 | 将每个匹配项替换为应用于 MatchResult 的 replacer 函数的结果。 |
| `Stream<MatchResult> results()` 9 | 生成所有匹配结果的流。 |

**`java.util.regex.MatchResult` 5**

| 方法 | 描述 |
|---|---|
| `String group()`<br>`String group(int group)` | 生成匹配的字符串或给定组匹配的字符串。 |
| `int start()`<br>`int end()`<br>`int start(int group)`<br>`int end(int group)` | 生成匹配字符串或给定组匹配字符串的起始和结束偏移量。 |




| java.util.Scanner 5.0 |
| --- |
| - `Stream<MatchResult> findAll(Pattern pattern)` 9<br>生成一个流，包含该扫描器产生的输入中给定模式的所有匹配项。 |

现在你已经了解了如何在 Java 中执行输入和输出操作，并概览了作为“新 I/O”规范一部分的正则表达式包。下一章，我们将转向 XML 数据的处理。

*本页有意留白*

本章介绍 XML，并涵盖 Java 库的 XML 特性。一如既往，我们会在此过程中指出何时使用 XML 是合理的——以及何时你必须有所保留，并尝试用老办法解决问题：通过良好的设计和代码。

## 3.1 XML 简介

在第一卷第 13 章中，你已经看到了使用*属性文件*来描述程序配置的方法。属性文件包含一组名称/值对，例如

```
fontname=Times Roman
fontsize=12
windowsize=400 200
color=# 50 100
```

你可以使用 `Properties` 类通过一次方法调用读取这样的文件。这是一个不错的功能，但它还远远不够。在许多情况下，你想要描述的信息比属性文件格式能够轻松处理的结构更复杂。考虑示例中的 *字体名称*/*字体大小* 条目。更面向对象的做法是使用单个条目：

```
font=Times Roman 12
```

但这样一来，解析字体描述就变得很麻烦，因为你必须弄清楚字体名称在哪里结束、字体大小从哪里开始。

属性文件只有单一的扁平层级结构。你经常能看到程序员通过如下键名来绕过这一限制：

```
title.fontname=Helvetica
title.fontsize=36
body.fontname=Times Roman
body.fontsize=12
```

属性文件格式的另一个缺点是键必须唯一。要存储一系列值，你需要另一种变通方法，例如

```
menu.item.1=Times Roman
menu.item.2=Helvetica
menu.item.3=Goudy Old Style
```

XML 格式解决了这些问题。它可以表达层次结构，因此比属性文件的扁平表结构更灵活。

用于描述程序配置的 XML 文件可能如下所示：

```xml
<config>
    <entry id="title">
        <font>
            <name>Helvetica</name>
            <size>36</size>
        </font>
    </entry>
    <entry id="body">
        <font>
            <name>Times Roman</name>
            <size>12</size>
        </font>
    </entry>
    <entry id="background">
        <color>
            <red>0</red>
            <green>50</green>
            <blue>100</blue>
        </color>
    </entry>
</config>
```

XML 格式允许你表达层次结构并记录重复元素，而无需扭曲形式。

XML 文件的格式很直观。它看起来类似于 HTML 文件。这是有充分理由的——XML 和 HTML 都是古老的标准通用标记语言（SGML）的后代。

SGML 自 20 世纪 70 年代以来一直用于描述复杂文档的结构。它在一些需要持续维护大量文档的行业中得到了成功应用——尤其是飞机制造业。然而，SGML 相当复杂，因此从未大规模流行起来。这种复杂性很大程度上源于 SGML 有两个相互冲突的目标。SGML 希望确保文档按照其文档类型的规则形成，但它也希望通过允许减少输入量的快捷方式来使数据录入变得容易。XML 被设计为 SGML 的简化版本，以便在互联网上使用。正如通常情况那样，越简单越好，XML 立即受到了热烈欢迎，而这是 SGML 长期以来未能获得的。

> **注意：** 你可以在 www.xml.com/axml/axml.html 找到一个非常好的 XML 标准版本，其中带有 Tim Bray 的注释。

尽管 XML 和 HTML 有共同的根源，但两者之间存在重要差异。

- 与 HTML 不同，XML 区分大小写。例如，`<H1>` 和 `<h1>` 是不同的 XML 标签。
- 在 HTML 中，如果从上下文中可以清楚看出段落或列表项在哪里结束，你可以省略结束标签，例如 `</p>` 或 `</li>`。在 XML 中，你绝不能省略结束标签。
- 在 XML 中，只有单个标签而没有匹配结束标签的元素必须以 `/` 结尾，例如 `<img src="coffeecup.png"/>`。这样，解析器就知道不必寻找 `</img>` 标签。
- 在 XML 中，属性值必须用引号括起来。在 HTML 中，引号是可选的。例如，`<applet code="MyApplet.class" width=300 height=300>` 是合法的 HTML，但不是合法的 XML。在 XML 中，必须使用引号：`width="300"`。
- 在 HTML 中，属性可以没有值，例如 `<input type="radio" name="language" value="Java" checked>`。在 XML 中，所有属性都必须有值，例如 `checked="true"` 或（唉）`checked="checked"`。
- 对于 HTML 版本 4 和 5，存在称为 XHTML 的 XML 表述。

## 3.2 XML 文档的结构

XML 文档应以如下头部开始

```xml
<?xml version="1.0"?>
```

或

```xml
<?xml version="1.0" encoding="UTF-8"?>
```

严格来说，头部是可选的，但强烈建议使用。

> **注意：** 由于 SGML 是为处理真实文档而创建的，因此 XML 文件被称为文档，尽管其中许多描述的是通常不会被称为文档的数据集。

头部之后可以跟一个*文档类型定义*（DTD），例如

```
<!DOCTYPE web-app PUBLIC
  "-//Sun Microsystems, Inc.//DTD Web Application 2.2//EN"
  "http://java.sun.com/j2ee/dtds/web-app_2_2.dtd">
```

DTD 是确保文档正确性的重要机制，但并非必需。我们将在本章后面讨论它们。

最后，XML 文档的正文包含*根元素*，它可以包含其他元素。例如，

```xml
<?xml version="1.0"?>
<!DOCTYPE config ...>
<config>
    <entry id="title">
        <font>
            <name>Helvetica</name>
            <size>36</size>
        </font>
    </entry>
    ...
</config>
```

一个元素可以包含*子元素*、文本，或两者兼有。在前面的示例中，font 元素有两个子元素：name 和 size。name 元素包含文本 "Helvetica"。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_179_0.png)

> **提示：** 最好将 XML 文档结构化为一个元素要么包含子元素，要么包含文本。以下是你应避免的示例：

```xml
<font>
    Helvetica
    <size>36</size>
</font>
```

这在 XML 规范中称为*混合内容*。正如你将在本章后面看到的，如果避免混合内容，可以简化解析。

XML 元素可以包含属性，例如

```xml
<size unit="pt">36</size>
```

XML 设计者对于何时使用元素、何时使用属性存在一些分歧。例如，将字体描述为

```xml
<font name="Helvetica" size="36"/>
```

似乎比

```xml
<font>
    <name>Helvetica</name>
    <size>36</size>
</font>
```

更容易。然而，属性的灵活性要差得多。假设你想为大小值添加单位。如果使用属性，就必须将单位添加到属性值中：

```xml
<font name="Helvetica" size="36 pt"/>
```

唉！现在你必须解析字符串 "36 pt"，这正是 XML 旨在避免的那种麻烦。向 size 元素添加属性要干净得多：

```xml
<font>
  <name>Helvetica</name>
  <size units="pt">36</size>
</font>
```

一个常用的经验法则是，属性只应用于修改值的解释，而不是用于指定值。如果你发现自己陷入一场形而上学式的讨论：某个特定设置是否是对值解释的修改，那就直接对属性说“不”，全程使用元素。许多有用的 XML 文档根本不使用属性。

> **注意：** 在 HTML 中，属性使用规则很简单：如果它不显示在网页上，它就是属性。例如，考虑超链接
>
>     <a href="http://java.sun.com">Java Technology</a>
>
> 字符串 Java Technology 会显示在网页上，但链接的 URL 不是显示页面的一部分。然而，这条规则对大多数 XML 文件并没有那么有帮助，因为 XML 文件中的数据通常不是供人查看的。

元素和文本是 XML 文档的“面包和黄油”。以下是你可能遇到的其他一些标记指令：

- *字符引用*的形式为 `&#decimalValue;` 或 `&#xhexValue;`。例如，é 字符可以用以下任一形式表示：

  ```
  &#233; &#xE9;
  ```

- *实体引用*的形式为 `&name;`。实体引用

  ```
  &lt; &gt; &amp; &quot; &apos;
  ```

  具有预定义含义：小于号、大于号、与号、引号和撇号字符。你可以在 DTD 中定义其他实体引用。




- *CDATA 节*由 `<![CDATA[` 和 `]]>` 分隔。它们是字符数据的一种特殊形式。你可以使用它们来包含含有 `<`、`&` 和 `>` 等非字符数据的字符串，而不必让这些数据被解释为标记，例如：

```
<![CDATA[< & > are my favorite delimiters]]>
```

CDATA 节不能包含字符串 `]]>`。请谨慎使用此功能！它常常被用作将遗留数据偷偷带入 XML 文档的后门。

- *处理指令*是给处理 XML 文档的应用程序的指令。它们由 `<?` 和 `?>` 分隔，例如

```
<?xml-stylesheet href="mystyle.css" type="text/css"?>
```

每个 XML 文档都以一条处理指令开始

```
<?xml version="1.0"?>
```

- *注释*由 `<!--` 和 `-->` 分隔，例如

```
<!-- This is a comment. -->
```

注释不应包含字符串 `--`。注释应只是供人类读者阅读的信息。它们绝不应包含隐藏命令；命令应使用处理指令。

## 3.3 解析 XML 文档

要处理 XML 文档，你需要解析它。解析器是一种程序，它读取文件、确认文件格式正确、将其分解为组成元素，并让程序员能够访问这些元素。Java 库提供了两种 XML 解析器：

- 树解析器，例如文档对象模型（DOM）解析器，它将 XML 文档读入树结构。
- 流式解析器，例如用于 XML 的简单 API（SAX）解析器，它在读取 XML 文档时生成事件。

对大多数用途而言，DOM 解析器更易于使用，因此我们先介绍它们。如果你处理的文档非常长，其树结构会占用大量内存，或者你只对少数几个元素感兴趣而不关心它们的上下文，那么你可以考虑流式解析器。更多信息请参见第 3.7 节“流式解析器”（第 196 页）。

DOM 解析器接口由万维网联盟（W3C）标准化。org.w3c.dom 包包含 Document 和 Element 等接口类型的定义。不同的供应商（例如 Apache 组织和 IBM）编写了 DOM 解析器，其类实现了这些接口。用于 XML 处理的 Java API（JAXP）库实际上使得插入这些解析器中的任意一个成为可能。但 JDK 也自带一个派生自 Apache 解析器的 DOM 解析器。

要读取 XML 文档，你需要一个 DocumentBuilder 对象，可以像这样从 DocumentBuilderFactory 获取：

```java
DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
DocumentBuilder builder = factory.newDocumentBuilder();
```

现在你可以从文件读取文档：

```java
File f = . . .;
Document doc = builder.parse(f);
```

或者，你可以使用 URL：

```java
URL u = . . .;
Document doc = builder.parse(u.toString());
```

你甚至可以指定任意输入流：

```java
InputStream in = . . .;
Document doc = builder.parse(in);
```

> 注意：如果你使用输入流作为输入源，解析器将无法定位相对于文档位置引用的其他文件，例如同一目录中的 DTD。你可以安装“实体解析器”来克服该问题。更多信息请参阅 www.xml.com/pub/a/2004/03/03/catalogs.html 或 www.ibm.com/developers/xml/library/x-mxd3.html。

Document 对象是 XML 文档树结构在内存中的表示。它由一些对象组成，这些对象的类实现了 Node 接口及其各种子接口。图 3.1 展示了这些子接口的继承层次结构。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_183_0.png)

**图 3.1** Node 接口及其子接口

通过调用 getDocumentElement 方法开始分析文档内容。它返回根元素。

```java
Element root = doc.getDocumentElement();
```

例如，如果你正在处理一个文档

```xml
<?xml version="1.0"?>
<font>
    ...
</font>
```

那么调用 `getDocumentElement` 会返回 `font` 元素。

`getTagName` 方法返回元素的标签名。在前面的示例中，`root.getTagName()` 返回字符串 "font"。

要获取元素的子节点（可能是子元素、文本、注释或其他节点），请使用 `getChildNodes` 方法。该方法返回一个 `NodeList` 类型的集合。该类型在标准 Java 集合之前就已标准化，因此它具有不同的访问协议。`item` 方法获取指定索引处的项，`getLength` 方法给出项的总数。你可以像这样枚举所有子节点：

```java
NodeList children = root.getChildNodes();
for (int i = 0; i < children.getLength(); i++)
{
    Node child = children.item(i);
    ...
}
```

分析子节点时要小心。例如，假设你正在处理以下文档

```xml
<font>
    <name>Helvetica</name>
    <size>36</size>
</font>
```

你可能期望 font 元素有两个子节点，但解析器报告了五个：

- `<font>` 与 `<name>` 之间的空白
- `name` 元素
- `</name>` 与 `<size>` 之间的空白
- `size` 元素
- `</size>` 与 `</font>` 之间的空白

图 3.2 展示了 DOM 树。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_184_0.png)

**图 3.2** 一个简单的 DOM 树

如果你只期望子元素，可以忽略空白：

```java
for (int i = 0; i < children.getLength(); i++)
{
    Node child = children.item(i);
    if (child instanceof Element)
    {
        var childElement = (Element) child;
        . . .
    }
}
```

现在你只查看两个元素，标签名分别为 name 和 size。

正如你将在下一节看到的，如果你的文档有 DTD，你可以做得更好。这样解析器就知道哪些元素没有文本节点作为子节点，并且可以为你抑制空白。

在分析 name 和 size 元素时，你想获取它们包含的文本字符串。这些文本字符串本身包含在 Text 类型的子节点中。你知道这些 Text 节点是仅有的子节点，因此可以使用 getFirstChild 方法，而不必遍历另一个 NodeList。然后，使用 getData 方法获取存储在 Text 节点中的字符串：

```java
for (int i = 0; i < children.getLength(); i++)
{
    Node child = children.item(i);
    if (child instanceof Element)
    {
        var childElement = (Element) child;
        var textNode = (Text) childElement.getFirstChild();
        String text = textNode.getData().trim();
        if (childElement.getTagName().equals("name"))
            name = text;
        else if (childElement.getTagName().equals("size"))
            size = Integer.parseInt(text);
    }
}
```

> **提示：** 对 getData 方法的返回值调用 trim 是个好主意。如果 XML 文件的作者将开始标签和结束标签放在不同行，例如
>
> ```xml
> <size>
>     36
> </size>
> ```
>
> 那么解析器会将所有换行符和空格包含在文本节点数据中。调用 trim 方法会移除实际数据周围的空白。

你还可以使用 getLastChild 方法获取最后一个子节点，并使用 getNextSibling 获取节点的下一个同级节点。因此，遍历节点子节点的另一种方式是

```java
for (Node childNode = element.getFirstChild();
    childNode != null;
    childNode = childNode.getNextSibling())
{
    . . .
}
```

要枚举节点的属性，请调用 getAttributes 方法。它返回一个 NamedNodeMap 对象，其中包含描述这些属性的 Node 对象。你可以像在 NodeList 中那样遍历 NamedNodeMap 中的节点。然后，调用 getNodeName 和 getNodeValue 方法获取属性名和值。

```java
NamedNodeMap attributes = element.getAttributes();
for (int i = 0; i < attributes.getLength(); i++)
{
    Node attribute = attributes.item(i);
    String name = attribute.getNodeName();
    String value = attribute.getNodeValue();
    . . .
}
```

或者，如果你知道属性的名称，可以直接获取对应的值：

```java
String unit = element.getAttribute("unit");
```

现在你已经了解了如何分析 DOM 树。代码清单 3.1 中的程序运用这些技术，将 XML 文档转换为 JSON 格式。

树形显示清楚地展示了子元素如何被包含空白和注释的文本所包围。你可以清楚地看到换行符和回车符显示为 `\n`。

你不必熟悉 JSON 就能理解该程序如何操作 DOM 树。只需注意以下几点：

- 我们使用 DocumentBuilder 从文件读取 Document。
- 对于每个元素，我们打印标签名、属性以及元素。
- 对于字符数据，我们根据数据生成一个字符串。如果数据来自注释，我们会添加 "Comment: " 前缀。




### 代码清单 3.1 dom/JSONConverter.java

```java
package dom;

import java.io.*;
import java.util.*;

import javax.xml.parsers.*;

import org.w3c.dom.*;
import org.w3c.dom.CharacterData;
import org.xml.sax.*;

/**
 * This program displays an XML document as a tree in JSON format.
 * @version 1.2 2018-04-02
 * @author Cay Horstmann
 */
public class JSONConverter
{
    public static void main(String[] args)
        throws SAXException, IOException, ParserConfigurationException
    {
        String filename;
        if (args.length == 0)
        {
            try (var in = new Scanner(System.in))
            {
                System.out.print("Input file: ");
                filename = in.nextLine();
            }
        }
        else
            filename = args[0];
        DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
        DocumentBuilder builder = factory.newDocumentBuilder();

        Document doc = builder.parse(filename);
        Element root = doc.getDocumentElement();
        System.out.println(convert(root, 0));
    }

    public static StringBuilder convert(Node node, int level)
    {
        if (node instanceof Element)
        {
            return elementObject((Element) node, level);
        }
        else if (node instanceof CharacterData)
        {
            return characterString((CharacterData) node, level);
        }
        else
        {
            return pad(new StringBuilder(), level).append(
                jsonEscape(node.getClass().getName()));
        }
    }

    private static Map<Character, String> replacements = Map.of('\b', "\\b", '\f',
        "\\f", '\n', "\\n", '\r', "\\r", '\t', "\\t", '"', "\\\"", '\\', "\\\\");

    private static StringBuilder jsonEscape(String str)
    {
        var result = new StringBuilder("\"");
        for (int i = 0; i < str.length(); i++)
        {
            char ch = str.charAt(i);
            String replacement = replacements.get(ch);
            if (replacement == null) result.append(ch);
            else result.append(replacement);
        }
        result.append("\"");
        return result;
    }

    private static StringBuilder characterString(CharacterData node, int level)
    {
        var result = new StringBuilder();
        StringBuilder data = jsonEscape(node.getData());
        if (node instanceof Comment) data.insert(1, " Comment: ");
        pad(result, level).append(data);
        return result;
    }

    private static StringBuilder elementObject(Element elem, int level)
    {
        var result = new StringBuilder();
        pad(result, level).append("{\n");
        pad(result, level + 1).append("\"name\": ");
        result.append(jsonEscape(elem.getTagName()));
        NamedNodeMap attrs = elem.getAttributes();
        if (attrs.getLength() > 0)
        {
            pad(result.append(",\n"), level + 1).append("\"attributes\": ");
            result.append(attributeObject(attrs));
        }
        NodeList children = elem.getChildNodes();
        if (children.getLength() > 0)
        {
            pad(result.append(",\n"), level + 1).append("\"children\": [\n");
            for (int i = 0; i < children.getLength(); i++)
            {
                if (i > 0) result.append(",\n");
                result.append(convert(children.item(i), level + 2));
            }
            result.append("\n");
            pad(result, level + 1).append("]\n");
        }
        pad(result, level).append("}");
        return result;
    }

    private static StringBuilder pad(StringBuilder builder, int level)
    {
        for (int i = 0; i < level; i++) builder.append("  ");
        return builder;
    }

    private static StringBuilder attributeObject(NamedNodeMap attrs)
    {
        var result = new StringBuilder("{");
        for (int i = 0; i < attrs.getLength(); i++)
        {
            if (i > 0) result.append(", ");
            result.append(jsonEscape(attrs.item(i).getNodeName()));
            result.append(": ");
            result.append(jsonEscape(attrs.item(i).getNodeValue()));
        }
        result.append("}");
        return result;
    }
}
```

### javax.xml.parsers.DocumentBuilderFactory 1.4

| API | 版本 |
|---|---|
| `javax.xml.parsers.DocumentBuilderFactory` | `1.4` |

- `static DocumentBuilderFactory newInstance()`  
  返回 `DocumentBuilderFactory` 类的一个实例。
- `DocumentBuilder newDocumentBuilder()`  
  返回 `DocumentBuilder` 类的一个实例。

### javax.xml.parsers.DocumentBuilder 1.4

| 方法 | 描述 |
|---|---|
| `Document parse(File f)` | |
| `Document parse(String url)` | |
| `Document parse(InputStream in)` | 从给定的文件、URL 或输入流中解析 XML 文档，并返回解析后的文档。 |

### org.w3c.dom.Document 1.4

| 方法 | 描述 |
|---|---|
| `Element getDocumentElement()` | 返回文档的根元素。 |

### org.w3c.dom.Element 1.4

| 方法 | 描述 |
|---|---|
| `String getTagName()` | 返回元素的名称。 |
| `String getAttribute(String name)` | 返回具有给定名称的属性的值；如果不存在该属性，则返回空字符串。 |

### org.w3c.dom.Node 1.4

| 方法 | 描述 |
|---|---|
| `NodeList getChildNodes()` | 返回一个节点列表，其中包含此节点的所有子节点。 |
| `Node getFirstChild()` | |
| `Node getLastChild()` | 获取此节点的第一个或最后一个子节点；如果此节点没有子节点，则返回 null。 |
| `Node getNextSibling()` | |
| `Node getPreviousSibling()` | 获取此节点的下一个或上一个同级节点；如果此节点没有同级节点，则返回 null。 |
| `Node getParentNode()` | 获取此节点的父节点；如果此节点是文档节点，则返回 null。 |
| `NamedNodeMap getAttributes()` | 返回一个节点映射，其中包含描述此节点所有属性的 Attr 节点。 |

### org.w3c.dom.Node 1.4（续）

| 方法 | 描述 |
|---|---|
| `String getNodeName()` | 返回此节点的名称。如果该节点是 Attr 节点，则名称是属性名。 |
| `String getNodeValue()` | 返回此节点的值。如果该节点是 Attr 节点，则该值是属性值。 |

### org.w3c.dom.CharacterData 1.4

| 方法 | 描述 |
|---|---|
| `String getData()` | 返回存储在此节点中的文本。 |

### org.w3c.dom.NodeList 1.4

| 方法 | 描述 |
|---|---|
| `int getLength()` | 返回此列表中的节点数。 |
| `Node item(int index)` | 返回具有给定索引的节点。索引介于 0 和 getLength() - 1 之间。 |

### org.w3c.dom.NamedNodeMap 1.4

| 方法 | 描述 |
|---|---|
| `int getLength()` | 返回此映射中的节点数。 |
| `Node item(int index)` | 返回具有给定索引的节点。索引介于 0 和 getLength() - 1 之间。 |

## 3.4 验证 XML 文档

在上一节中，你了解了如何遍历 DOM 文档的树结构。然而，使用这种方法，你将不得不进行相当多繁琐的编程和错误检查。这不仅涉及处理元素之间的空白；你还需要检查文档是否包含你预期的节点。例如，假设你正在读取以下元素：

```xml
<font>
  <name>Helvetica</name>
  <size>36</size>
</font>
```

你获取第一个子节点。哎呀……它是一个包含空白 "\n" 的文本节点。你跳过文本节点并找到第一个元素节点。然后，你需要检查其标签名是否为 "name"，并且它是否有一个文本类型的子节点。你继续处理下一个非空白子节点，并进行同样的检查。如果文档作者调换了子节点的顺序，或者添加了另一个子元素，该怎么办？编写所有这些错误检查代码很繁琐——但跳过检查则是鲁莽的。

幸运的是，XML 解析器的主要优点之一是它可以自动验证文档是否具有正确的结构。这使解析变得简单得多。例如，如果你知道 font 片段已经通过验证，你可以直接获取两个孙节点，将它们强制转换为文本节点，并获取文本数据，而无需任何进一步检查。

为了指定文档结构，你可以提供 DTD 或 XML Schema 定义。DTD 或 schema 包含规则，这些规则通过为每个元素指定合法的子元素和属性，说明文档应如何构成。例如，DTD 可能包含如下规则：

```dtd
<ELEMENT font (name,size)>
```

这条规则表示 font 元素必须始终有两个子元素，即 name 和 size 元素。XML Schema 语言将相同的约束表达为

```xml
<xsd:element name="font">
  <xsd:sequence>
    <xsd:element name="name" type="xsd:string"/>
    <xsd:element name="size" type="xsd:int"/>
  </xsd:sequence>
</xsd:element>
```

与 DTD 相比，XML Schema 可以表达更复杂的验证条件（例如 size 元素必须包含一个整数）。与 DTD 语法不同，XML Schema 语法本身使用 XML，如果你需要处理 schema 文件，这会是一个优点。

在下一节中，我们将详细讨论 DTD，然后简要介绍 XML Schema 支持的基础知识。最后，我们将展示一个完整的应用程序，演示验证如何简化 XML 编程。



### 3.4.1 文档类型定义

有几种提供 DTD 的方法。可以像这样在 XML 文档中包含一个 DTD：

```xml
<?xml version="1.0"?>
<!DOCTYPE config [
  <!ELEMENT config . . .>
  more rules
  . . .
]>
<config>
  . . .
</config>
```

如你所见，规则包含在 DOCTYPE 声明中，位于由 [ . . . ] 分隔的块内。文档类型必须与根元素的名称匹配，例如我们示例中的 config。

在 XML 文档内部提供 DTD 有些少见，因为 DTD 可能会变得很长。将 DTD 存储在外部更合理。SYSTEM 声明可用于此目的。指定包含该 DTD 的 URL，例如：

```xml
<!DOCTYPE config SYSTEM "config.dtd">
```

或

```xml
<!DOCTYPE config SYSTEM "http://myserver.com/config.dtd">
```

> **注意：** 如果为 DTD 使用相对 URL（例如 "config.dtd"），请向解析器提供 File 或 URL 对象，而不是 InputStream。如果必须从输入流进行解析，请提供实体解析器（见下面的注释）。

识别众所周知的 DTD 的机制起源于 SGML。下面是一个示例：

```xml
<!DOCTYPE web-app
  PUBLIC "-//Sun Microsystems, Inc.//DTD Web Application 2.2//EN"
  "http://java.sun.com/j2ee/dtds/web-app_2_2.dtd">
```

如果 XML 处理器知道如何通过公共标识符定位 DTD，就无需访问该 URL。

注意：DTD 的系统标识符 URL 可能实际上不可用，或被有意放慢。后者的一个例子是 XHTML 1.0 Strict DTD 的系统标识符 http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd。如果解析 XHTML 文件，提供该 DTD 可能需要一两分钟。

补救方法是使用一个实体解析器，将公共标识符映射到本地文件。在 Java 9 之前，必须提供一个类的对象，该类实现 EntityResolver 接口并提供 resolveEntity 方法。

如今，可以使用 XML 目录来管理这种映射。提供一个或多个如下形式的目录文件

```xml
<?xml version="1.0"?>
<!DOCTYPE catalog PUBLIC  "-//OASIS//DTD XML Catalogs V1.0//EN"
    "http://www.oasis-open.org/committees/entity/release/1.0/catalog.dtd">
<catalog xmlns="urn:oasis:names:tc:entity:xmlns:xml:catalog" prefer="public">
    <public publicId="..." uri="..."/>
    ...
</catalog>
```

然后像这样构造并安装一个解析器：

```java
builder.setEntityResolver(CatalogManager.catalogResolver(
    CatalogFeatures.defaults(),
    Paths.get("catalog.xml").toAbsolutePath().toUri()));
```

完整示例见代码清单 3.6。

除了在程序中设置目录文件位置，还可以使用 javax.xml.catalog.files 系统属性在命令行中指定它们。提供以分号分隔的绝对文件 URL。

既然已经了解了解析器如何定位 DTD，现在让我们考虑各种规则。

ELEMENT 规则指定一个元素可以拥有哪些子元素。使用由表 3.1 所示组件构成的正则表达式。

下面是几个简单但典型的示例。以下规则表明 menu 元素包含 0 个或多个 item 元素：

```xml
<!ELEMENT menu (item)*>
```

这组规则表明 font 由一个 name 后跟一个 size 来描述，其中每个都包含文本：

```xml
<!ELEMENT font (name,size)>
<!ELEMENT name (#PCDATA)>
<!ELEMENT size (#PCDATA)>
```

必须重写这样的规则，要么引入另一个 caption 元素，要么允许 image 元素和文本的任意组合。

这一限制简化了 XML 解析器在解析*混合内容*（标签和文本的混合）时的工作。由于允许混合内容会失去一些控制，最好设计 DTD 时使所有元素要么包含其他元素，要么只包含文本。

> **注意：** 实际上，在 DTD 规则中可以指定元素的任意正则表达式，这种说法并不完全正确。XML 解析器可能会拒绝某些导致非确定性解析的复杂规则集。例如，正则表达式 `((x,y)|(x,z))` 就是非确定性的。当解析器看到 x 时，它不知道应选择两个备选分支中的哪一个。该表达式可以改写为确定性形式 `(x,(y|z))`。然而，有些表达式无法重新表述，例如 `((x,y)*|x?)`。Java XML 库中的解析器在遇到有歧义的 DTD 时不会发出警告；它只是在解析时选择第一个匹配的备选分支，这会导致它拒绝一些正确的输入。解析器完全有权这样做，因为 XML 标准允许解析器假定 DTD 是无歧义的。

还可以指定规则来描述元素的合法属性。一般语法为

```
<!ATTLIST element attribute type default>
```

**表 3.2** 属性类型

| 类型 | 含义 |
|---|---|
| CDATA | 任意字符串 |
| (A₁\|A₂\|…\|Aₙ) | 字符串属性 A₁、A₂、…、Aₙ 之一 |
| NMTOKEN, NMTOKENS | 一个或多个名称记号 |
| ID | 唯一 ID |
| IDREF, IDREFS | 对一个唯一 ID 的一个或多个引用 |
| ENTITY, ENTITIES | 一个或多个未解析实体 |

**表 3.3** 属性默认值

| 默认值 | 含义 |
|---|---|
| `#REQUIRED` | 属性是必需的。 |
| `#IMPLIED` | 属性是可选的。 |
| A | 属性是可选的；如果未指定，解析器报告其为 `A`。 |
| #FIXED A | 该属性必须未指定或为 `A`；无论哪种情况，解析器都报告其为 `A`。 |

下面是两个典型的属性规范：

```
<ATTLIST font style (plain|bold|italic|bold-italic) "plain">
<ATTLIST size unit CDATA #IMPLIED>
```

第一个规范描述 font 元素的 style 属性。有四个合法属性值，默认值是 plain。第二个规范表示 size 元素的 unit 属性可以包含任意字符数据序列。

> **注意。** 我们通常建议使用元素而不是属性来描述数据。因此，字体样式应作为单独的元素，例如 `<font><style>plain</style>...</font>`。不过，对于枚举类型，属性具有不可否认的优势，因为解析器可以验证值是否合法。例如，如果字体样式是属性，解析器会检查它是否为四个允许值之一，并在未提供值时提供默认值。

CDATA 属性值的处理与之前见过的 #PCDATA 处理有细微不同，而且与 `<![CDATA[...]]>` 节完全无关。属性值首先会被规范化——也就是说，解析器会处理字符引用和实体引用（例如 `&#233;` 或 `&lt;`），并将空白替换为空格。

NMTOKEN（或名称记号）类似于 CDATA，但大多数非字母数字字符和内部空白是不允许的，并且解析器会移除前导和尾随空白。NMTOKENS 是以空白分隔的名称记号列表。

ID 构造非常有用。ID 是一个名称记号，在文档中必须唯一——解析器会检查唯一性。你将在下一个示例程序中看到一个应用。IDREF 是对同一文档中存在的 ID 的引用，解析器也会检查它。IDREFS 是以空白分隔的 ID 引用列表。

ENTITY 属性值引用一个“未解析的外部实体”。这是来自 SGML 的占位结构，实践中很少使用。位于 www.xml.com/axml/axml.html 的带注释 XML 规范中有一个示例。

DTD 还可以定义实体，即在解析期间被替换的缩写。你可以在 Firefox 浏览器的用户界面描述中找到使用实体的好例子。这些描述以 XML 格式编写，并包含诸如以下的实体定义

```xml
<!ENTITY back.label "Back">
```

在其他地方，文本可以包含实体引用，例如：

```xml
<menuitem label="&back.label;"/>
```

解析器会用替换字符串替换实体引用。要使应用程序国际化，只需更改实体定义中的字符串。实体的其他用法更复杂，也更少见；详情请参阅 XML 规范。

DTD 的介绍到此结束。既然已经了解了如何使用 DTD，现在可以配置解析器来利用它们。

首先，告诉文档构建器工厂开启验证：

```java
factory.setValidating(true);
```

该工厂生成的所有构建器都会根据 DTD 验证其输入。验证最有用的好处是忽略元素内容中的空白。例如，考虑以下 XML 片段

```xml
<font>
    <name>Helvetica</name>
    <size>36</size>
</font>
```

非验证解析器会报告 font、name 和 size 元素之间的空白，因为它无法知道 font 的子元素是

```dtd
(name, size)
(#PCDATA, name, size)*
```

或者也许是

```dtd
ANY
```

一旦 DTD 指定子元素为 (name, size)，解析器就知道它们之间的空白不是文本。调用


```
factory.setIgnoringElementContentWhitespace(true);
```

这样，构建器将不再报告文本节点中的空白。这意味着你现在可以依赖这样一个事实：字体节点有两个子节点。你不再需要编写冗长的循环：

```
for (int i = 0; i < children.getLength(); i++)
{
    Node child = children.item(i);
    if (child instanceof Element)
    {
        var childElement = (Element) child;
        if (childElement.getTagName().equals("name")) ...;
        else if (childElement.getTagName().equals("size")) ...;
    }
}
```

相反，你可以直接访问第一个和第二个子节点：

```
var nameElement = (Element) children.item(0);
var sizeElement = (Element) children.item(1);
```

这就是 DTD 如此有用的原因。你不必用规则检查代码给程序增加负担——当你获得文档时，解析器已经完成了这项工作。

当解析器报告错误时，你的应用程序需要对此进行处理——记录它、向用户显示它，或者抛出异常以放弃解析。因此，每当你使用验证时，都应该安装错误处理器。提供一个实现了 ErrorHandler 接口的对象。该接口有三个方法：

```
void warning(SAXParseException exception)
void error(SAXParseException exception)
void fatalError(SAXParseException exception)
```

使用 DocumentBuilder 类的 setErrorHandler 方法安装错误处理器：

```
builder.setErrorHandler(handler);
```

| javax.xml.parsers.DocumentBuilder | 1.4 |
| --- | --- |
| • `void setEntityResolver(EntityResolver resolver)` | 设置解析器以定位正在解析的 XML 文档中引用的实体。 |
| • `void setErrorHandler(ErrorHandler handler)` | 设置处理器以报告解析过程中出现的错误和警告。 |

#### org.xml.sax.EntityResolver 1.4

- `public InputSource resolveEntity(String publicID, String systemID)`

返回一个输入源，其中包含由给定 ID 引用的数据；如果该解析器不知道如何解析特定名称，则返回 null。如果未提供公共 ID，则 publicID 参数可以为 null。

#### org.xml.sax.InputSource 1.4

- `InputSource(InputStream in)`
- `InputSource(Reader in)`
- `InputSource(String systemID)`

根据流、读取器或系统 ID（通常是相对或绝对 URL）构造输入源。

#### org.xml.sax.ErrorHandler 1.4

- `void fatalError(SAXParseException exception)`
- `void error(SAXParseException exception)`
- `void warning(SAXParseException exception)`

重写这些方法，以提供针对致命错误、非致命错误和警告的处理器。

#### org.xml.sax.SAXParseException 1.4

- `int getLineNumber()`
- `int getColumnNumber()`

返回导致异常的已处理输入末尾的行号和列号。

#### javax.xml.catalog.CatalogManager 9

- `static CatalogResolver catalogResolver(CatalogFeatures features, URI... uris)`

生成一个使用所提供的 URI 处的目录文件的解析器。此类实现了 EntityResolver，以及 StAX、模式验证和 XSL 转换所使用的解析器类。

#### javax.xml.catalog.CatalogFeatures 9

- `static CatalogFeatures defaults()`

生成一个具有默认设置的实例。

#### javax.xml.parsers.DocumentBuilderFactory 1.4

- `boolean isValidating()`
- `void setValidating(boolean value)`  
  获取或设置工厂的 validating 属性。如果设置为 true，则此工厂生成的解析器会验证其输入。
- `boolean isIgnoringElementContentWhitespace()`
- `void setIgnoringElementContentWhitespace(boolean value)`  
  获取或设置工厂的 ignoringElementContentWhitespace 属性。如果设置为 true，则此工厂生成的解析器会忽略没有混合内容（即元素和 #PCDATA 的混合）的元素节点之间的空白。

### 3.4.2 XML Schema

XML Schema 比 DTD 语法复杂得多，因此我们只介绍基础知识。如需更多信息，我们推荐 www.w3.org/TR/xmlschema-0 上的教程。

要在文档中引用模式文件，请向根元素添加属性，例如：

```
    <?xml version="1.0"?>
    <config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:noNamespaceSchemaLocation="config.xsd">
       ...
    </config>
```

此声明表示应使用模式文件 config.xsd 来验证文档。如果你的文档使用了命名空间，语法会稍微复杂一些——详情请参阅 XML Schema 教程。（前缀 xsi 是命名空间别名；更多信息请参阅第 193 页的 3.6 节“使用命名空间”。）

模式为每个元素和属性定义一个类型。简单类型是字符串，也许对其内容有限制。其他一切都是复杂类型。具有简单类型的元素可以没有属性和子元素。否则，它必须具有复杂类型。相反，属性总是具有简单类型。

FontType 是 name、size 和 style 元素的序列。在此类型定义中，我们使用 ref 属性来引用模式中其他位置的定义。你也可以像这样嵌套定义：

```xml
<xsd:complexType name="FontType">
    <xsd:sequence>
        <xsd:element name="name" type="xsd:string"/>
        <xsd:element name="size" type="xsd:int"/>
        <xsd:element name="style">
            <xsd:simpleType>
                <xsd:restriction base="xsd:string">
                    <xsd:enumeration value="PLAIN" />
                    <xsd:enumeration value="BOLD" />
                    <xsd:enumeration value="ITALIC" />
                    <xsd:enumeration value="BOLD ITALIC" />
                </xsd:restriction>
            </xsd:simpleType>
        </xsd:element>
    </xsd:sequence>
</xsd:complexType>
```

请注意 style 元素的*匿名类型定义*。

xsd:sequence 构造等价于 DTD 中的连接表示法。xsd:choice 构造等价于 | 运算符。例如，

```xml
<xsd:complexType name="contactInfo">
    <xsd:choice>
        <xsd:element ref="email"/>
        <xsd:element ref="phone"/>
    </xsd:choice>
</xsd:complexType>
```

这等价于 DTD 类型 `email|phone`。

要允许元素重复，请使用 minOccurs 和 maxOccurs 属性。例如，DTD 类型 item* 的等价形式是

```xml
<xsd:element name="item" type="..." minOccurs="0" maxOccurs="unbounded"/>
```

要指定属性，请将 xsd:attribute 元素添加到 complexType 定义中：

```xml
<xsd:element name="size">
    <xsd:complexType>
        . . .
        <xsd:attribute name="unit" type="xsd:string" use="optional" default="cm"/>
    </xsd:complexType>
</xsd:element>
```

这等价于 DTD 语句

```dtd
<!ATTLIST size unit CDATA #IMPLIED "cm">
```

将模式的元素和类型定义放在 xsd:schema 元素内：

```
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema">
    ...
    </xsd:schema>
```

使用模式解析 XML 文件与使用 DTD 解析文件类似，但有两个区别：

1. 你需要开启对命名空间的支持，即使你的 XML 文件中没有使用命名空间。

   ```
   factory.setNamespaceAware(true);
   ```

2. 你需要使用以下魔法咒语让工厂为处理模式做好准备：

   ```
   final String JAXP_SCHEMA_LANGUAGE =
       "http://java.sun.com/xml/jaxp/properties/schemaLanguage";
   final String W3C_XML_SCHEMA = "http://www.w3.org/2001/XMLSchema";
   factory.setAttribute(JAXP_SCHEMA_LANGUAGE, W3C_XML_SCHEMA);
   ```

### 3.4.3 一个实际示例

在本节中，我们将通过一个实际示例来展示 XML 在真实场景中的使用。

假设一个应用程序需要配置数据来指定任意对象，而不仅仅是文本字符串。我们提供了两种实例化对象的机制：使用构造器，以及使用工厂方法。下面演示如何使用构造器创建颜色对象：

```
    <construct class="java.awt.Color">
        <int>255</int>
        <int>200</int>
        <int>100</int>
    </construct>
```

下面是一个使用工厂方法的示例：

```
    <factory class="java.util.logging.Logger" method="getLogger">
        <string>com.horstmann.corejava</string>
    </factory>
```

如果省略工厂方法名，则默认为 getInstance。

如你所见，这里有用于描述字符串和整数的元素。我们还支持布尔类型，并且可以以同样的方式添加其他基本类型。




只是为了展示语法，还有第二种用于基本类型的机制：

```xml
<value type="int">30</value>
```

配置是一系列条目。每个条目都有一个 ID 和一个对象：

```xml
<config>
    <entry id="background">
        <construct class="java.awt.Color">
            <value type="int">55</value>
            <value type="int">200</value>
            <value type="int">100</value>
        </construct>
    </entry>
    ...
</config>
```

解析器会检查 ID 是否唯一。

清单 3.4 中所示的 DTD 很直接。

清单 3.5 包含等效的 schema。在 schema 中，我们可以提供额外的检查：int 或 boolean 元素只能包含整数或布尔内容。请注意使用 xs:group 构造来定义重复使用的复杂类型部分。

清单 3.2 中的程序展示了如何解析配置文件。清单 3.3 中定义了一个示例配置。

如果你选择的文件包含字符串 -schema，程序将使用 schema 而不是 DTD。

这个例子是 XML 的典型用法。XML 格式足够健壮，可以表达复杂关系。XML 解析器通过接管有效性检查和提供默认值这类常规工作来增加价值。

#### 清单 3.2 read/XMLReadTest.java

```java
package read;

import java.io.*;
import java.lang.reflect.*;
import java.util.*;

import javax.xml.parsers.*;

import org.w3c.dom.*;
import org.xml.sax.*;

12 /**
13  * This program shows how to use an XML file to describe Java objects
14  * @version 1.0 2018-04-03
15  * @author Cay Horstmann
16  */
17 public class XMLReadTest
18 {
19    public static void main(String[] args) throws ParserConfigurationException,
20          SAXException, IOException, ReflectiveOperationException
21    {
22       String filename;
23       if (args.length == 0)
24       {
25          try (var in = new Scanner(System.in))
26          {
27             System.out.print("Input file: ");
28             filename = in.nextLine();
29          }
30       }
31       else
32          filename = args[0];
33
34       DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
35       factory.setValidating(true);
36
37       if (filename.contains("-schema"))
38       {
39          factory.setNamespaceAware(true);
40          final String JAXP_SCHEMA_LANGUAGE =
41                "http://java.sun.com/xml/jaxp/properties/schemaLanguage";
42          final String W3C_XML_SCHEMA = "http://www.w3.org/2001/XMLSchema";
43          factory.setAttribute(JAXP_SCHEMA_LANGUAGE, W3C_XML_SCHEMA);
44       }
45
46       factory.setIgnoringElementContentWhitespace(true);
47
48       DocumentBuilder builder = factory.newDocumentBuilder();
49
50       builder.setErrorHandler(new ErrorHandler()
51       {
52          public void warning(SAXParseException e) throws SAXException
53          {
54             System.err.println("Warning: " + e.getMessage());
55          }
56
57          public void error(SAXParseException e) throws SAXException
58          {
System.err.println("Error: " + e.getMessage());
System.exit(0);
}

public void fatalError(SAXParseException e) throws SAXException
{
    System.err.println("Fatal error: " + e.getMessage());
    System.exit(0);
}
});

Document doc = builder.parse(filename);
Map<String, Object> config = parseConfig(doc.getDocumentElement());
System.out.println(config);
}

private static Map<String, Object> parseConfig(Element e)
    throws ReflectiveOperationException
{
    var result = new HashMap<String, Object>();
    NodeList children = e.getChildNodes();
    for (int i = 0; i < children.getLength(); i++)
    {
        var child = (Element) children.item(i);
        String name = child.getAttribute("id");
        Object value = parseObject((Element) child.getFirstChild());
        result.put(name, value);
    }
    return result;
}

private static Object parseObject(Element e)
    throws ReflectiveOperationException
{
    String tagName = e.getTagName();
    if (tagName.equals("factory")) return parseFactory(e);
    else if (tagName.equals("construct")) return parseConstruct(e);
    else
    {
        String childData = ((CharacterData) e.getFirstChild()).getData();
        if (tagName.equals("int"))
            return Integer.valueOf(childData);
        else if (tagName.equals("boolean"))
            return Boolean.valueOf(childData);
        else
            return childData;
    }
}
```

#### 清单 3.3 read/config.xml

```xml
<?xml version="1.0"?>
<!DOCTYPE config SYSTEM "config.dtd">
<config>
  <entry id="background">
    <construct class="java.awt.Color">
      <int>55</int>
      <int>200</int>
      <int>100</int>
    </construct>
  </entry>
  <entry id="currency">
    <factory class="java.util.Currency">
      <string>USD</string>
    </factory>
  </entry>
</config>
```

#### 清单 3.4 read/config.dtd

```dtd
<!ELEMENT config (entry)*>

<!ELEMENT entry (string|int|boolean|construct|factory)*>
<!ATTLIST entry id ID #IMPLIED>

<!ELEMENT construct (string|int|boolean|construct|factory)*>
<!ATTLIST construct class CDATA #IMPLIED>

<!ELEMENT factory (string|int|boolean|construct|factory)*>
<!ATTLIST factory class CDATA #IMPLIED>
<!ATTLIST factory method CDATA "getInstance">

<!ELEMENT string (#PCDATA)>
<!ELEMENT int (#PCDATA)>
<!ELEMENT boolean (#PCDATA)>
```

#### 清单 3.5 read/config.xsd

```xml
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema">
  <xsd:element name="config">
    <xsd:complexType>
      <xsd:sequence>
        <xsd:element name="entry" minOccurs="0" maxOccurs="unbounded">
          <xsd:complexType>
            <xsd:group ref="Object"/>
            <xsd:attribute name="id" type="xsd:ID"/>
          </xsd:complexType>
</xsd:complexType>
</xsd:element>
</xsd:sequence>
</xsd:complexType>
</xsd:element>

<xsd:element name="construct">
    <xsd:complexType>
        <xsd:group ref="Arguments"/>
        <xsd:attribute name="class" type="xsd:string"/>
    </xsd:complexType>
</xsd:element>

<xsd:element name="factory">
    <xsd:complexType>
        <xsd:group ref="Arguments"/>
        <xsd:attribute name="class" type="xsd:string"/>
        <xsd:attribute name="method" type="xsd:string" default="getInstance"/>
    </xsd:complexType>
</xsd:element>

<xsd:group name="Object">
    <xsd:choice>
        <xsd:element ref="construct"/>
        <xsd:element ref="factory"/>
        <xsd:element name="string" type="xsd:string"/>
        <xsd:element name="int" type="xsd:int"/>
        <xsd:element name="boolean" type="xsd:boolean"/>
    </xsd:choice>
</xsd:group>

<xsd:group name="Arguments">
    <xsd:sequence>
        <xsd:group ref="Object" minOccurs="0" maxOccurs="unbounded"/>
    </xsd:sequence>
</xsd:group>
</xsd:schema>
```

## 3.5 使用 XPath 定位信息

如果你想在 XML 文档中定位特定的信息，遍历 DOM 树的节点可能会有些麻烦。XPath 语言使访问树节点变得简单。例如，假设你有这个 XHTML 文档：

```html
<html>
    <head>
        . . .
        <title>... </title>
        . . .
    </head>
</html>
```

你可以通过求值 XPath 表达式来获取标题文本

```
/html/head/title/text()
```

这比普通的 DOM 方法简单得多：

- 1. 获取文档根节点。
- 2. 获取第一个子节点并将其转换为 Element。
- 3. 在其子节点中定位 title 元素。
- 4. 获取它的第一个子节点并将其转换为 CharacterData 节点。
- 5. 获取其数据。

一个 XPath 可以描述 XML 文档中的*一组节点*。例如，XPath

```
/html/body/form
```

描述 XHTML 文件中所有作为 body 元素子节点的 form 元素集合。你可以使用 [] 运算符选择特定元素：

```
/html/body/form[1]
```

是第一个 form。（索引值从 1 开始。）

使用 @ 运算符获取属性值。XPath 表达式

```
/html/body/form[1]/@action
```

描述第一个 form 的 action 属性。XPath 表达式

```
/html/body/form/@action
```

描述 body 元素的所有子 form 元素的所有 action 属性节点。

有许多有用的 XPath 函数。例如，

```
count(/html/body/form)
```

返回 body 元素的 form 子元素数量。还有更多更复杂的 XPath 表达式；请参阅 www.w3.org/TR/xpath 上的规范或 www.zvon.org/xxl/XPathTutorial/General/examples.html 上的在线教程。



要计算 XPath 表达式，首先从 XPathFactory 创建一个 XPath 对象：

```java
XPathFactory xpathFactory = XPathFactory.newInstance();
XPath path = xpathFactory.newXPath();
```

然后，调用 evaluate 方法计算 XPath 表达式：

```java
String username = path.evaluate("/html/head/title/text()", doc);
```

可以使用同一个 XPath 对象计算多个表达式。

这种形式的 evaluate 方法返回字符串结果。它适用于检索文本，例如前一个示例中 title 元素的文本子节点。

如果 XPath 表达式产生多个节点，请进行如下调用：

```java
XPathNodes result = path.evaluateExpression("/html/body/form", doc, XPathNodes.class);
```

XPathNodes 类类似于 NodeList，但它扩展了 Iterable 接口，允许使用增强 for 循环。

此方法在 Java 9 中添加。在较早版本中，请改用以下调用：

```java
var nodes = (NodeList) path.evaluate("/html/body/form", doc, XPathConstants.NODESET);
```

如果结果是单个节点，请使用以下调用之一：

```java
Node node = path.evaluateExpression("/html/body/form[1]", doc, Node.class);
node = (Node) path.evaluate("/html/body/form[1]", doc, XPathConstants.NODE);
```

如果结果是数字，请使用：

```java
int count = path.evaluateExpression("count(/html/body/form)", doc, Integer.class);
count = ((Number) path.evaluate("count(/html/body/form)",
    doc, XPathConstants.NUMBER)).intValue();
```

不必从文档根开始搜索；可以从任意节点或节点列表开始。例如，如果已有来自先前求值的节点，可以调用

```java
String result = path.evaluate(expression, node);
```

如果不知道 XPath 表达式求值的结果（也许因为它来自用户），则调用

```java
XPathEvaluationResult<?> result = path.evaluateExpression(expression, doc);
```

表达式 `result.type()` 是 `XPathEvaluationResult.XPathResultType` 枚举的常量 `STRING`、`NODESET`、`NODE` 之一。调用 `result.value()` 获取值。

程序清单 3.6 中的程序演示了任意 XPath 表达式的求值。加载一个 XML 文件并输入一个表达式。表达式的结果显示出来。

### 程序清单 3.6 xpath/XPathTest.java

```java
package xpath;

import java.io.*;
import java.nio.file.*;
import java.util.*;

import javax.xml.catalog.*;
import javax.xml.parsers.*;
import javax.xml.xpath.*;

import org.w3c.dom.*;
import org.xml.sax.*;

/**
 * This program evaluates XPath expressions.
 * @version 1.1 2018-04-06
 * @author Cay Horstmann
 */
public class XPathTest
{
   public static void main(String[] args) throws Exception
   {
      DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
      DocumentBuilder builder = factory.newDocumentBuilder();

      // Avoid a delay in parsing an XHTML file--see the first note in
      // Section 3.3.1
      builder.setEntityResolver(CatalogManager.catalogResolver(
         CatalogFeatures.defaults(),
         Paths.get("xpath/catalog.xml").toAbsolutePath().toUri()));

      XPathFactory xpathfactory = XPathFactory.newInstance();
      XPath path = xpathfactory.newXPath();
      try (var in = new Scanner(System.in))
      {
         String filename;
         if (args.length == 0)
         {
            System.out.print("Input file: ");
            filename = in.nextLine();
         }
         else
            filename = args[0];

         Document doc = builder.parse(filename);
         var done = false;
         while (!done)
         {
            System.out.print("\nXPath expression (empty line to exit): ");
            String expression = in.nextLine();
            if (expression.trim().isEmpty()) done = true;
            else
            {
               try
               {
                  XPathEvaluationResult<?> result
                     = path.evaluateExpression(expression, doc);
                  if (result.type() == XPathEvaluationResult.XPathResultType.NODESET)
                  {
                     for (Node n : (XPathNodes) result.value())
                        System.out.println(description(n));
                  }
                  else if (result.type() == XPathEvaluationResult.XPathResultType.NODE)
                     System.out.println((Node) result.value());
                  else
                     System.out.println(result.value());
               }
               catch (XPathExpressionException e)
               {
                  System.out.println(e.getMessage());
               }
            }
         }
      }
   }

   public static String description(Node n)
   {
      if (n instanceof Element) return "Element " + n.getNodeName();
      else if (n instanceof Attr) return "Attribute " + n;
      else return n.toString();
   }
}
```

| **java.xml.xpath.XPathFactory 5.0** |
| --- |
| - `static XPathFactory newInstance()`<br>  返回用于创建 XPath 对象的 XPathFactory 实例。<br>- `XPath newXPath()`<br>  构造用于求值 XPath 表达式的 XPath 对象。 |

| **java.xml.xpath.XPath 5.0** |
| --- |
| - `String evaluate(String expression, Object startingPoint)`<br>  从给定起始点开始求值表达式。起始点可以是节点或节点列表。如果结果是节点或节点集，返回的字符串由所有文本节点子级的数据组成。<br>- `Object evaluate(String expression, Object startingPoint, QName resultType)`<br>  从给定起始点开始求值表达式。起始点可以是节点或节点列表。resultType 是 XPathConstants 类中的常量 STRING、NODE、NODESET、NUMBER 或 BOOLEAN 之一。返回值为 String、Node、NodeList、Number 或 Boolean。<br>- `<T> T evaluateExpression(String expression, Object item, Class<T> type)` 9<br>  求值给定表达式，并将结果作为给定类型的值返回。<br>- `XPathEvaluationResult<?> evaluateExpression(String expression, InputSource source)` 9<br>  求值给定表达式。 |

| **java.xml.xpath.XPathEvaluationResult&lt;T&gt; 9** |
| --- |
| - `XPathEvaluationResult.XPathResultType type()`<br>  返回枚举常量 STRING、NODESET、NODE、NUMBER、BOOLEAN 之一。<br>- `T value()`<br>  返回结果值。 |

## 3.6 使用命名空间

Java 语言使用包来避免名称冲突。程序员可以为不同的类使用相同名称，只要它们不在同一个包中。XML 为元素和属性名称提供了类似的*命名空间*机制。

命名空间由统一资源标识符（URI）标识，例如

http://www.w3.org/2001/XMLSchema
uuid:1c759aed-b748-475c-ab68-10679700c4f2
urn:com:books-r-us

HTTP URL 形式最常见。注意 URL 仅用作标识符字符串，而不是文档定位器。例如，命名空间标识符

http://www.horstmann.com/corejava
http://www.horstmann.com/corejava/index.html

表示*不同*的命名空间，尽管 Web 服务器会为两个 URL 提供相同的文档。

命名空间 URL 处不必有任何文档——XML 解析器不会尝试在该位置查找任何内容。不过，为帮助遇到可能不熟悉的命名空间的程序员，通常会在该 URL 位置放置一个说明命名空间用途的文档。例如，如果将浏览器指向 XML Schema 命名空间的命名空间 URL（http://www.w3.org/2001/XMLSchema），就会找到描述 XML Schema 标准的文档。

为什么使用 HTTP URL 作为命名空间标识符？因为很容易确保它们唯一。如果选择一个真实 URL，主机部分的唯一性由域名系统保证。你的组织随后可以安排 URL 其余部分的唯一性。这与 Java 包名中使用反向域名的基本原理相同。

当然，尽管长命名空间标识符有利于唯一性，但你并不想处理不必要长的标识符。在 Java 编程语言中，使用 `import` 机制指定包的长名称，然后只使用简短的类名。在 XML 中，有类似的机制：

```xml
<element xmlns="namespaceURI">
    children
</element>
```

该元素及其子元素现在属于给定命名空间。

子元素可以提供自己的命名空间，例如：

```xml
<element xmlns="namespaceURI1">
    <child xmlns="namespaceURI2">
        grandchildren
    </child>
    more children
</element>
```




然后，第一个子节点及其孙节点属于第二个命名空间。如果你只需要一个命名空间，或者这些命名空间天然嵌套，那么这个简单机制就能很好地工作。否则，你会想使用第二种在 Java 中没有对应机制的机制。你可以为命名空间设置一个前缀——即你为特定文档选择的简短标识符。下面是一个典型示例——XML Schema 文件中的 xsd 前缀：

```xml
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema">
  <xsd:element name="config"/>
  . . .
</xsd:schema>
```

属性

```
xmlns:prefix="namespaceURI"
```

定义了一个命名空间和一个前缀。在我们的示例中，前缀是字符串 xsd。因此，xsd:schema 实际上表示命名空间 http://www.w3.org/2001/XMLSchema 中的 schema。

> **注意：** 只有子元素会继承其父元素的命名空间。没有显式前缀的属性永远不属于任何命名空间。考虑这个刻意构造的示例：
>
> ```xml
> <configuration xmlns="http://www.horstmann.com/corejava"
>     xmlns:si="http://www.bipm.fr/enus/3_SI/si.html">
>   <size value="210" si:unit="mm"/>
>   . . .
> </configuration>
> ```
>
> 在这个示例中，元素 configuration 和 size 属于 URI 为 http://www.horstmann.com/corejava 的命名空间。属性 si:unit 属于 URI 为 http://www.bipm.fr/enus/3_SI/si.html 的命名空间。然而，属性 value 不属于任何命名空间。

你可以控制解析器如何处理命名空间。默认情况下，Java XML 库的 DOM 解析器不支持命名空间感知。

要开启命名空间处理，请调用 DocumentBuilderFactory 的 setNamespaceAware 方法：

```java
factory.setNamespaceAware(true);
```

现在，该工厂创建的所有构建器都支持命名空间。每个节点都有三个属性：

- *限定名*，带前缀，由 `getNodeName`、`getTagName` 等方法返回
- 命名空间 URI，由 `getNamespaceURI` 方法返回
- *本地名*，不带前缀或命名空间，由 `getLocalName` 方法返回

下面是一个示例。假设解析器看到以下元素：

```xml
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema">
```

那么它会报告以下内容：

- 限定名 = xsd:schema
- 命名空间 URI = http://www.w3.org/2001/XMLSchema
- 本地名 = schema

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_218_0.png)

> **注意：** 如果关闭命名空间感知，`getNamespaceURI` 和 `getLocalName` 会返回 null。

**org.w3c.dom.Node 1.4**

| 方法 | 描述 |
|---|---|
| `String getLocalName()` | 返回本地名（不带前缀）；如果解析器不支持命名空间感知，则返回 null。 |
| `String getNamespaceURI()` | 返回命名空间 URI；如果节点不属于任何命名空间，或者解析器不支持命名空间感知，则返回 null。 |

**javax.xml.parsers.DocumentBuilderFactory 1.4**

| 方法 | 描述 |
|---|---|
| `boolean isNamespaceAware()`<br>`void setNamespaceAware(boolean value)` | 获取或设置工厂的 namespaceAware 属性。如果设置为 true，则该工厂生成的解析器支持命名空间感知。 |

## 3.7 流解析器

DOM 解析器会将整个 XML 文档读入树形数据结构。对于大多数实际应用来说，DOM 工作得很好。但是，如果文档很大，而且你的处理算法足够简单，可以在读取过程中分析节点，而不必查看整个树结构，那么 DOM 可能效率不高。在这些情况下，你应该使用流解析器。

在接下来的几节中，我们讨论 Java 库提供的流解析器：古老的 SAX 解析器和 Java 6 中新增的更现代的 StAX 解析器。SAX 解析器使用事件回调，而 StAX 解析器提供遍历解析事件的迭代器。后者通常更方便一些。

### 3.7.1 使用 SAX 解析器

SAX 解析器在解析 XML 输入的各个组成部分时报告事件，但它不以任何方式存储文档——构建数据结构由事件处理器负责。事实上，DOM 解析器就是构建在 SAX 解析器之上的。它在接收解析器事件时构建 DOM 树。

每当你使用 SAX 解析器时，都需要一个处理器来为各种解析事件定义事件动作。ContentHandler 接口定义了几个回调方法，解析器在解析文档时会执行这些方法。以下是最重要的几个：

- 每次遇到起始标签或结束标签时，都会调用 startElement 和 endElement。
- 每当遇到字符数据时，都会调用 characters。
- startDocument 和 endDocument 分别在文档开始和结束时各调用一次。

例如，在解析以下片段时

```
<font>
  <name>Helvetica</name>
  <size units="pt">36</size>
</font>
```

解析器会进行以下回调：

1. startElement，元素名：font
2. startElement，元素名：name
3. characters，内容：Helvetica
4. endElement，元素名：name
5. startElement，元素名：size，属性：units="pt"
6. characters，内容：36
7. endElement，元素名：size
8. endElement，元素名：font

你的处理器需要重写这些方法，并让它们在解析文件时执行你想要执行的操作。本节末尾的程序会打印 HTML 文件中的所有链接 `<a href="...">`。它只是重写了处理器的 startElement 方法，以检查名称为 `a` 且具有名称为 `href` 的属性的链接。这对于实现“网络爬虫”——一种通过跟随链接访问越来越多网页的程序——可能很有用。

> **注意：** HTML 不必是有效的 XML，而且许多网页偏离正确的 XML 太多，以至于示例程序无法解析它们。然而，W3C 编写的大多数页面都使用 XHTML（一种属于正确 XML 的 HTML 方言）。你可以使用这些页面来测试示例程序。例如，如果你运行
>
> ```
> java SAXTest http://www.w3.org/MarkUp
> ```
>
> 你将看到该页面上所有链接的 URL 列表。

这个示例程序很好地展示了 SAX 的用法。我们完全不关心 `a` 元素出现在什么上下文中，也不需要存储树结构。

以下是你获取 SAX 解析器的方式：

```java
SAXParserFactory factory = SAXParserFactory.newInstance();
SAXParser parser = factory.newSAXParser();
```

现在你可以处理文档了：

```java
parser.parse(source, handler);
```

这里，`source` 可以是文件、URL 字符串或输入流。`handler` 属于 `DefaultHandler` 的子类。`DefaultHandler` 类为以下四个接口定义了空实现方法：

- ContentHandler
- DTDHandler
- EntityResolver
- ErrorHandler

示例程序定义了一个处理器，它重写 `ContentHandler` 接口的 `startElement` 方法，以留意带有 href 属性的 a 元素：

```java
var handler = new DefaultHandler()
{
    public void startElement(String namespaceURI, String lname, String qname,
            Attributes attrs) throws SAXException
    {
        if (lname.equalsIgnoreCase("a") && attrs != null)
        {
            for (int i = 0; i < attrs.getLength(); i++)
            {
                String aname = attrs.getLocalName(i);
                if (aname.equalsIgnoreCase("href"))
                    System.out.println(attrs.getValue(i));
            }
        }
    }
};
```

startElement 方法有三个描述元素名的参数。qname 参数报告形如 prefix:localname 的限定名。如果开启命名空间处理，那么 namespaceURI 和 localname 参数会提供命名空间和本地（非限定）名。

与 DOM 解析器一样，命名空间处理默认是关闭的。要激活命名空间处理，请调用工厂类的 setNamespaceAware 方法：

```java
SAXParserFactory factory = SAXParserFactory.newInstance();
factory.setNamespaceAware(true);
SAXParser saxParser = factory.newSAXParser();
```

在这个程序中，我们处理另一个常见问题。XHTML 文件以一个包含 DTD 引用的标签开头，解析器会想要加载它。可以理解，W3C 并不太乐意提供数十亿份诸如 www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd 这样的文件副本。他们一度完全拒绝提供，但在撰写本文时情况仍然如此。在这里，他们以极慢的速度提供 DTD。如果你不需要验证文档，只需调用

```java
factory.setFeature("http://apache.org/xml/features/nonvalidating/load-external-dtd", false);
```

清单 3.7 包含了网络爬虫程序的代码。在本章后面，你将看到 SAX 的另一个有趣用法。将非 XML 数据源转换为 XML 的一种简单方法是报告 XML 解析器会报告的 SAX 事件。详情请参见第 216 页的 3.9 节“XSL 转换”。

```
Listing 3.7  SAX/SAXTest.java

1  package sax;

2  import java.io.*;
3  import java.net.*;
4  import javax.xml.parsers.*;
5  import org.xml.sax.*;
6  import org.xml.sax.helpers.*;
```




#### 清单 3.7（续）

```java
/**
 * This program demonstrates how to use a SAX parser. The program prints all
 * hyperlinks of an XHTML web page. <br>
 * Usage: java SAXTest URL
 * @version 1.01 2018-05-01
 * @author Cay Horstmann
 */
public class SAXTest
{
   public static void main(String[] args) throws Exception
   {
      String url;
      if (args.length == 0)
      {
         url = "http://www.w3.org";
         System.out.println("Using " + url);
      }
      else url = args[0];

      var handler = new DefaultHandler()
      {
         public void startElement(String namespaceURI, String lname,
               String qname, Attributes attrs)
         {
            if (lname.equals("a") && attrs != null)
            {
               for (int i = 0; i < attrs.getLength(); i++)
               {
                  String aname = attrs.getLocalName(i);
                  if (aname.equals("href"))
                     System.out.println(attrs.getValue(i));
               }
            }
         }
      };

      SAXParserFactory factory = SAXParserFactory.newInstance();
      factory.setNamespaceAware(true);
      factory.setFeature(
            "http://apache.org/xml/features/nonvalidating/load-external-dtd",
            false);
      SAXParser saxParser = factory.newSAXParser();
      InputStream in = new URL(url).openStream();
      saxParser.parse(in, handler);
   }
}
```

#### javax.xml.parsers.SAXParserFactory 1.4

- `static SAXParserFactory newInstance()`  
  返回 SAXParserFactory 类的实例。
- `SAXParser newSAXParser()`  
  返回 SAXParser 类的实例。
- `boolean isNamespaceAware()`
- `void setNamespaceAware(boolean value)`  
  获取或设置工厂的 namespaceAware 属性。如果设置为 `true`，则该工厂生成的解析器是命名空间感知的。
- `boolean isValidating()`
- `void setValidating(boolean value)`  
  获取或设置工厂的 validating 属性。如果设置为 `true`，则该工厂生成的解析器会验证其输入。

#### javax.xml.parsers.SAXParser 1.4

- `void parse(File f, DefaultHandler handler)`
- `void parse(String uri, DefaultHandler handler)`
- `void parse(InputStream in, DefaultHandler handler)`  
  从给定文件、URL 或输入流解析 XML 文档，并将解析事件报告给给定的处理器。

#### org.xml.sax.ContentHandler 1.4

- `void startDocument()`
- `void endDocument()`  
  在文档开始或结束时被调用。
- `void startElement(String uri, String lname, String qname, Attributes attr)`
- `void endElement(String uri, String lname, String qname)`  
  在元素开始或结束时被调用。如果解析器是命名空间感知的，它会报告命名空间的 URI、不带前缀的本地名称以及带前缀的限定名称。
- `void characters(char[] data, int start, int length)`  
  当解析器报告字符数据时被调用。

#### org.xml.sax.Attributes 1.4

- `int getLength()`  
  返回此属性集合中存储的属性数量。
- `String getLocalName(int index)`  
  返回给定索引处属性的本地名称（不带前缀）；如果解析器不是命名空间感知的，则返回空字符串。
- `String getURI(int index)`  
  返回给定索引处属性的命名空间 URI；如果节点不属于命名空间，或解析器不是命名空间感知的，则返回空字符串。
- `String getQName(int index)`  
  返回给定索引处属性的限定名称（带前缀）；如果解析器不报告限定名称，则返回空字符串。
- `String getValue(int index)`
- `String getValue(String qname)`
- `String getValue(String uri, String lname)`  
  从给定索引、限定名称或命名空间 URI + 本地名称返回属性值。如果值不存在，则返回 `null`。

### 3.7.2 使用 StAX 解析器

StAX 解析器是一种“拉式解析器”。无需安装事件处理器，只需使用以下基本循环遍历事件：

```
InputStream in = url.openStream();
XMLInputFactory factory = XMLInputFactory.newInstance();
XMLStreamReader parser = factory.createXMLStreamReader(in);
while (parser.hasNext())
{
    int event = parser.next();
    Call parser methods to obtain event details
}
```

例如，解析以下片段时

```xml
<font>
    <name>Helvetica</name>
    <size units="pt">36</size>
</font>
```

解析器会产生以下事件：

1. START_ELEMENT，元素名称：font
2. CHARACTERS，内容：空白
3. START_ELEMENT，元素名称：name
4. CHARACTERS，内容：Helvetica
5. END_ELEMENT，元素名称：name
6. CHARACTERS，内容：空白
7. START_ELEMENT，元素名称：size
8. CHARACTERS，内容：36
9. END_ELEMENT，元素名称：size
10. CHARACTERS，内容：空白
11. END_ELEMENT，元素名称：font

要分析属性值，请调用 `XMLStreamReader` 类的相应方法。例如，

```java
String units = parser.getAttributeValue(null, "units");
```

获取当前元素的 `units` 属性。

默认情况下，命名空间处理是启用的。你可以通过修改工厂来停用它：

```java
XMLInputFactory factory = XMLInputFactory.newInstance();
factory.setProperty(XMLInputFactory.IS_NAMESPACE_AWARE, false);
```

清单 3.8 包含使用 StAX 解析器实现的 Web 爬虫程序代码。如你所见，该代码比等效的 SAX 代码更简单，因为你不必担心事件处理。

#### 清单 3.8 stax/StAXTest.java

```java
package stax;

import java.io.*;
import java.net.*;
import javax.xml.stream.*;

/**
 * This program demonstrates how to use a StAX parser. The program prints all
 * hyperlinks of an HTML web page. <br>
 * Usage: java stax.StAXTest URL
 * @author Cay Horstmann
 * @version 1.1 2018-05-01
 */
public class StAXTest
{
  public static void main(String[] args) throws Exception
  {
    String urlString;
    if (args.length == 0)
    {
      urlString = "http://www.w3.org";
      System.out.println("Using " + urlString);
    }
    else urlString = args[0];
    var url = new URL(urlString);
    InputStream in = url.openStream();
    XMLInputFactory factory = XMLInputFactory.newInstance();
    XMLStreamReader parser = factory.createXMLStreamReader(in);
    while (parser.hasNext())
    {
      int event = parser.next();
      if (event == XMLStreamConstants.START_ELEMENT)
      {
        if (parser.getLocalName().equals("a"))
        {
          String href = parser.getAttributeValue(null, "href");
          if (href != null)
            System.out.println(href);
        }
      }
    }
  }
}
```

#### javax.xml.stream.XMLInputFactory 6

- `static XMLInputFactory newInstance()`  
  返回 XMLInputFactory 类的实例。
- `void setProperty(String name, Object value)`  
  为此工厂设置属性；如果该属性不受支持或无法设置为给定值，则抛出 `IllegalArgumentException`。JDK 实现支持以下布尔值属性：

| 属性 | 描述 |
| --- | --- |
| `"javax.xml.stream.isValidating"` | 当为 `false`（默认值）时，不验证文档。规范未要求。 |
| `"javax.xml.stream.isNamespaceAware"` | 当为 `true`（默认值）时，处理命名空间。规范未要求。 |
| `"javax.xml.stream.isCoalescing"` | 当为 `false`（默认值）时，相邻字符数据不合并。 |
| `"javax.xml.stream.isReplacingEntityReferences"` | 当为 `true`（默认值）时，实体引用被替换并作为字符数据报告。 |
| `"javax.xml.stream.isSupportingExternalEntities"` | 当为 `true`（默认值）时，解析外部实体。规范未为此属性提供默认值。 |
| `"javax.xml.stream.supportDTD"` | 当为 `true`（默认值）时，DTD 作为事件报告。 |

- `XMLStreamReader createXMLStreamReader(InputStream in)`
- `XMLStreamReader createXMLStreamReader(InputStream in, String characterEncoding)`
- `XMLStreamReader createXMLStreamReader(Reader in)`
- `XMLStreamReader createXMLStreamReader(Source in)`  
  创建一个从给定流、读取器或 JAXP 源读取的解析器。

#### javax.xml.stream.XMLStreamReader 6

- `boolean hasNext()`  
  如果还有另一个解析事件，则返回 `true`。
- `int next()`  
  将解析器状态设置为下一个解析事件，并返回以下常量之一：START_ELEMENT、END_ELEMENT、CHARACTERS、START_DOCUMENT、END_DOCUMENT、CDATA、COMMENT、SPACE（可忽略的空白）、PROCESSING_INSTRUCTION、ENTITY_REFERENCE、DTD。
- `boolean isStartElement()`
- `boolean isEndElement()`
- `boolean isCharacters()`
- `boolean isWhiteSpace()`  
  如果当前事件是开始元素、结束元素、字符数据或空白，则返回 `true`。




```text
Element rootElement = doc.createElement(rootName);
Element childElement = doc.createElement(childName);
```

使用 `createTextNode` 方法构造文本节点：

```text
Text textNode = doc.createTextNode(textContents);
```

将根元素添加到文档中，并将子节点添加到各自的父节点中：

```text
doc.appendChild(rootElement);
rootElement.appendChild(childElement);
childElement.appendChild(textNode);
```

在构建 DOM 树时，你可能还需要设置元素属性。只需调用 Element 类的 `setAttribute` 方法：

```text
rootElement.setAttribute(name, value);
```

### 3.8.2 使用命名空间的文档

如果使用命名空间，创建文档的过程会略有不同。

首先，将构建器工厂设置为可感知命名空间，然后创建构建器：

```text
DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
factory.setNamespaceAware(true);
builder = factory.newDocumentBuilder();
```

然后使用 `createElementNS` 而不是 `createElement` 来创建任何节点：

```text
String namespace = "http://www.w3.org/2000/svg";
Element rootElement = doc.createElementNS(namespace, "svg");
```

如果你的节点具有带命名空间前缀的限定名，那么任何必要的、以 `xmlns` 为前缀的属性都会自动创建。例如，如果你需要在 XHTML 中使用 SVG，可以像这样构造元素：

```text
Element svgElement = doc.createElementNS(namespace, "svg:svg");
```

当写出该元素时，它会变成

```xml
<svg:svg xmlns:svg="http://www.w3.org/2000/svg">
```

如果需要设置名称位于命名空间中的元素属性，请使用 Element 类的 `setAttributeNS` 方法：

```text
rootElement.setAttributeNS(namespace, qualifiedName, value);
```

### 3.8.3 写出文档

说来有些奇怪，将 DOM 树写入输出流并不那么容易。最简单的方法是使用可扩展样式表语言转换（XSLT）API。有关 XSLT 的更多信息，请参阅第 216 页的 3.9 节“XSLT 转换”。现在，可以把下面的代码看作生成 XML 输出的神奇咒语。

我们对文档应用不做任何操作的转换，并捕获其输出。为了在输出中包含 DOCTYPE 节点，我们还需要将 SYSTEM 和 PUBLIC 标识符设置为输出属性。

```java
// construct the do-nothing transformation
Transformer t = TransformerFactory.newInstance().newTransformer();
// set output properties to get a DOCTYPE node
t.setOutputProperty(OutputKeys.DOCTYPE_SYSTEM, systemIdIdentifier);
t.setOutputProperty(OutputKeys.DOCTYPE_PUBLIC, publicIdentifier);
// set indentation
t.setOutputProperty(OutputKeys.INDENT, "yes");
t.setOutputProperty(OutputKeys.METHOD, "xml");
t.setOutputProperty("{http://xml.apache.org/xslt}indent-amount", "2");
// apply the do-nothing transformation and send the output to a file
t.transform(new DOMSource(doc), new StreamResult(new FileOutputStream(file)));
```

另一种方法是使用 LSSerializer 接口。要获取实例，必须使用以下神奇咒语：

```java
DOMImplementation impl = doc.getImplementation();
var implLS = (DOMImplementationLS) impl.getFeature("LS", "3.0");
LSSerializer ser = implLS.createLSSerializer();
```

如果需要空格和换行，请设置此标志：

```java
ser.getDomConfig().setParameter("format-pretty-print", true);
```

然后，将文档转换为字符串就足够简单了：

```java
String str = ser.writeToString(doc);
```

如果希望直接将输出写入文件，则需要一个 LSOutput：

```java
LSOutput out = implLS.createLSOutput();
out.setEncoding("UTF-8");
out.setByteStream(new FileOutputStream(path));
ser.write(doc, out);
```

| **javax.xml.parsers.DocumentBuilder** | **1.4** |
|---|---|
| • `Document newDocument()` | 返回一个空文档。 |

| **org.w3c.dom.Document** | **1.4** |
|---|---|
| • `Element createElement(String name)` | 使用给定名称创建一个元素。 |
| • `Element createElementNS(String uri, String qname)` | 使用给定名称创建一个元素。 |
| • `Text createTextNode(String data)` | 使用给定数据创建一个文本节点。 |

| **org.w3c.dom.Node** | **1.4** |
|---|---|
| • `Node appendChild(Node child)` | 将一个节点追加到此节点的子节点列表中。返回被追加的节点。 |

| **org.w3c.dom.Element** | **1.4** |
|---|---|
| • `void setAttribute(String name, String value)` |  |
| • `void setAttributeNS(String uri, String qname, String value)` | 将具有给定名称的属性设置为给定值。如果限定名有别名前缀，则 uri 不能为 null。 |

| **javax.xml.transform.TransformerFactory** | **1.4** |
|---|---|
| • `static TransformerFactory newInstance()` | 返回 TransformerFactory 类的一个实例。 |
| • `Transformer newTransformer()` | 返回执行恒等（不做任何操作）转换的 Transformer 类的一个实例。 |

| **javax.xml.transform.Transformer** | **1.4** |
|---|---|
| • `void setOutputProperty(String name, String value)` | 设置输出属性。请参阅 `www.w3.org/TR/xsl#output` 了解标准输出属性列表。最有用的属性如下所示：<br><br>`doctype-public` — 在 DOCTYPE 声明中使用的公共 ID<br>`doctype-system` — 在 DOCTYPE 声明中使用的系统 ID<br>`indent` — “yes”或“no”<br>`method` — “xml”、“html”、“text”或自定义字符串 |
| • `void transform(Source from, Result to)` | 转换一个 XML 文档。 |

要写出没有子元素的元素（例如 `<img .../>`），请使用以下调用

```java
writer.writeEmptyElement(name);
```

最后，在文档末尾调用

```java
writer.writeEndDocument();
```

此调用会关闭所有打开的元素。

你仍然需要关闭 XMLStreamWriter，而且必须手动完成，因为 XMLStreamWriter 接口没有扩展 AutoCloseable 接口。

与 DOM/XSLT 方法一样，你不必担心属性值和字符数据中的字符转义。但是，可能会生成格式不正确的 XML，例如包含多个根节点的文档。此外，当前版本的 StAX 不支持生成缩进输出。

清单 3.9 中的程序展示了两种写出 XML 的方法。

#### 清单 3.9 `write/XMLWriteTest.java`

```java
package write;

import java.io.*;
import java.nio.file.*;
import java.util.*;
import javax.xml.parsers.*;
import javax.xml.stream.*;
import javax.xml.transform.*;
import javax.xml.transform.dom.*;
import javax.xml.transform.stream.*;

import org.w3c.dom.*;
/**
 * This program shows how to write an XML file. It produces modern art in SVG
 * format.
 * @version 1.12 2016-04-27
 * @author Cay Horstmann
 */
public class XMLWriteTest
{
   public static void main(String[] args) throws Exception
   {
      Document doc = newDrawing(600, 400);
      writeDocument(doc, "drawing1.svg");
      writeNewDrawing(600, 400, "drawing2.svg");
   }

   private static Random generator = new Random();
29  /**
30   * Creates a new random drawing.
31   * @param drawingWidth the width of the drawing in pixels
32   * @param drawingHeight the width of the drawing in pixels
33   * @return the DOM tree of the SVG document
34   */
35  public static Document newDrawing(int drawingWidth, int drawingHeight)
36      throws ParserConfigurationException
37  {
38      DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
39      factory.setNamespaceAware(true);
40      DocumentBuilder builder = factory.newDocumentBuilder();
41      var namespace = "http://www.w3.org/2000/svg";
42      Document doc = builder.newDocument();
43      Element svgElement = doc.createElementNS(namespace, "svg");
44      doc.appendChild(svgElement);
45      svgElement.setAttribute("width", "" + drawingWidth);
46      svgElement.setAttribute("height", "" + drawingHeight);
47      int n = 10 + generator.nextInt(20);
48      for (int i = 1; i <= n; i++)
49      {
50          int x = generator.nextInt(drawingWidth);
51          int y = generator.nextInt(drawingHeight);
52          int width = generator.nextInt(drawingWidth - x);
53          int height = generator.nextInt(drawingHeight - y);
54          int r = generator.nextInt(256);
55          int g = generator.nextInt(256);
56          int b = generator.nextInt(256);
57
58          Element rectElement = doc.createElementNS(namespace, "rect");
59          rectElement.setAttribute("x", "" + x);
60          rectElement.setAttribute("y", "" + y);
61          rectElement.setAttribute("width", "" + width);
62          rectElement.setAttribute("height", "" + height);
63          rectElement.setAttribute("fill", String.format("#%02x%02x%02x", r, g, b));
64          svgElement.appendChild(rectElement);
65      }
66      return doc;
67  }
68
69  /**
70   * Saves a document using DOM/XSLT
71   * @param doc the document to be written
72   * @param filename the name of the destination file
73   */
74  public static void writeDocument(Document doc, String filename)
75      throws TransformerException, IOException
76  {
```



```java
Transformer t = TransformerFactory.newInstance().newTransformer();
t.setOutputProperty(OutputKeys.DOCTYPE_SYSTEM,
    "http://www.w3.org/TR/2000/CR-SVG-20000802/DTD/svg-20000802.dtd");
t.setOutputProperty(OutputKeys.DOCTYPE_PUBLIC,
    "-//W3C//DTD SVG 20000802//EN");
t.setOutputProperty(OutputKeys.INDENT, "yes");
t.setOutputProperty(OutputKeys.METHOD, "xml");
t.setOutputProperty("{http://xml.apache.org/xslt}indent-amount", "2");
t.transform(new DOMSource(doc), new StreamResult(
    Files.newOutputStream(Paths.get(filename))));
}

/**
 * Uses StAX to write an SVG document with a random drawing.
 * @param drawingWidth the width of the drawing in pixels
 * @param drawingHeight the height of the drawing in pixels
 * @param filename the name of the destination file
 */
public static void writeNewDrawing(int drawingWidth, int drawingHeight,
    String filename) throws XMLStreamException, IOException
{
    XMLOutputFactory factory = XMLOutputFactory.newInstance();
    XMLStreamWriter writer = factory.createXMLStreamWriter(
        Files.newOutputStream(Paths.get(filename)));
    writer.writeStartDocument();
    writer.writeDTD("<!DOCTYPE svg PUBLIC \"-//W3C//DTD SVG 20000802//EN\" "
        + "\"http://www.w3.org/TR/2000/CR-SVG-20000802/DTD/svg-20000802.dtd\">");
    writer.writeStartElement("svg");
    writer.writeDefaultNamespace("http://www.w3.org/2000/svg");
    writer.writeAttribute("width", "" + drawingWidth);
    writer.writeAttribute("height", "" + drawingHeight);
    int n = 10 + generator.nextInt(20);
    for (int i = 1; i <= n; i++)
    {
        int x = generator.nextInt(drawingWidth);
        int y = generator.nextInt(drawingHeight);
        int width = generator.nextInt(drawingWidth - x);
        int height = generator.nextInt(drawingHeight - y);
        int r = generator.nextInt(256);
        int g = generator.nextInt(256);
        int b = generator.nextInt(256);
        writer.writeEmptyElement("rect");
        writer.writeAttribute("x", "" + x);
        writer.writeAttribute("y", "" + y);
        writer.writeAttribute("width", "" + width);
        writer.writeAttribute("height", "" + height);
        writer.writeAttribute("fill", String.format("#%02x%02x%02x", r, g, b));
    }
    writer.writeEndDocument(); // closes svg element
}
```

#### java.xml.stream.XMLOutputFactory 6

- `static XMLOutputFactory newInstance()`
  返回 XMLOutputFactory 类的一个实例。
- `XMLStreamWriter createXMLStreamWriter(OutputStream stream)`
- `XMLStreamWriter createXMLStreamWriter(OutputStream stream, String encoding)`
- `XMLStreamWriter createXMLStreamWriter(Writer writer)`
- `XMLStreamWriter createXMLStreamWriter(Result result)`
  创建一个将内容写入给定流、写入器或 JAXP 结果的写入器。

#### java.xml.stream.XMLStreamWriter 6

- `void writeStartDocument()`
- `void writeStartDocument(String version)`
- `void writeStartDocument(String encoding, String xmlVersion)`
  在文档顶部写入 XML 处理指令。注意，encoding 参数仅用于写入该属性。它不会设置输出的字符编码。
- `void setDefaultNamespace(String namespaceURI)`
- `void setPrefix(String prefix, String namespaceURI)`
  设置默认命名空间或与某个前缀关联的命名空间。该声明的作用域为当前元素；如果尚未写入任何元素，则作用域为文档根。
- `void writeStartElement(String localName)`
- `void writeStartElement(String namespaceURI, String localName)`
  写入开始标签，并将 namespaceURI 替换为关联的前缀。
- `void writeEndElement()`
  关闭当前元素。
- `void writeEndDocument()`
  关闭所有打开的元素。
- `void writeEmptyElement(String localName)`
- `void writeEmptyElement(String namespaceURI, String localName)`
  写入自闭合标签，并将 namespaceURI 替换为关联的前缀。
- `void writeAttribute(String localName, String value)`
- `void writeAttribute(String namespaceURI, String localName, String value)`
  为当前元素写入属性，并将 namespaceURI 替换为关联的前缀。

我们不需要深入讨论 SVG 的细节；就我们的目的而言，只需知道如何表示一组彩色矩形即可。下面是一个示例：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 20000802//EN"
  "http://www.w3.org/TR/2000/CR-SVG-20000802/DTD/svg-20000802.dtd">
<svg xmlns="http://www.w3.org/2000/svg" width="150" height="150">
  <rect x="231" y="61" width="9" height="12" fill="#6e4a13"/>
  <rect x="107" y="106" width="5" height="5" fill="#c406eb"/>
  ...
</svg>
```

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_238_0.png)

> **注意：** SVG 大量使用属性。事实上，有些属性相当复杂。例如，下面是一个 path 元素：
>
> ```xml
> <path d="M 100 100 L 300 100 L 200 300 Z"/>
> ```
>
> 其中 M 表示“moveto”命令，L 表示“lineto”，而 z 表示“closepath”（!）。显然，这种数据格式的设计者对于使用 XML 表示结构化数据并没有太大信心。在你自己的 XML 格式中，可能更愿意使用元素而不是复杂属性。

## 3.9 XSL 转换

XSL 转换（XSLT）机制允许你指定将 XML 文档转换为其他格式的规则，例如纯文本、XHTML 或任何其他 XML 格式。XSLT 通常用于从一种机器可读的 XML 格式转换为另一种，或者将 XML 转换为供人阅读的呈现格式。

你需要提供一个 XSLT 样式表，描述如何将 XML 文档转换为某种其他格式。XSLT 处理器读取 XML 文档和样式表，并生成所需的输出（参见图 3.4）。

XSLT 规范相当复杂，关于这个主题已经有整本书的著作。我们不可能讨论 XSLT 的所有特性，因此只通过一个代表性示例来讲解。你可以在 Don Box 等人的 *Essential XML* 一书中找到更多信息。XSLT 规范可在 www.w3.org/TR/xslt 获取。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_239_0.png)

**图 3.4** 应用 XSL 转换

假设我们想把包含员工记录的 XML 文件转换为 HTML 文档。考虑下面这个输入文件：

```xml
<staff>
    <employee>
        <name>Carl Cracker</name>
        <salary>75000.0</salary>
        <hiredate year="1987" month="12" day="15"/>
    </employee>
    <employee>
        <name>Harry Hacker</name>
        <salary>50000.0</salary>
        <hiredate year="1989" month="10" day="1"/>
    </employee>
    <employee>
        <name>Tony Tester</name>
        <salary>40000.0</salary>
        <hiredate year="1990" month="3" day="15"/>
    </employee>
</staff>
```

期望的输出是一个 HTML 表格：

```html
<table border="1">
<tr>
<td>Carl Cracker</td><td>$75000.0</td><td>1987-12-15</td>
</tr>
<tr>
<td>Harry Hacker</td><td>$50000.0</td><td>1989-10-1</td>
</tr>
<tr>
<td>Tony Tester</td><td>$40000.0</td><td>1990-3-15</td>
</tr>
</table>
```

带有转换模板的样式表具有如下形式：

```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<xsl:stylesheet
    xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
    version="1.0">
  <xsl:output method="html"/>

template1

template2
. . .
</xsl:stylesheet>
```

在我们的示例中，xsl:output 元素将 method 指定为 HTML。其他有效的 method 设置是 xml 和 text。

下面是一个典型模板：

```xml
<xsl:template match="/staff/employee">
    <tr><xsl:apply-templates/></tr>
</xsl:template>
```

match 属性的值是一个 XPath 表达式。该模板表示：每当遇到 XPath 集合 /staff/employee 中的节点时，执行以下操作：

1. 输出字符串 `<tr>`。
2. 在处理其子节点时继续应用模板。
3. 处理完所有子节点后输出字符串 `</tr>`。

换句话说，这个模板围绕每条员工记录生成 HTML 表格行标记。

XSLT 处理器从检查根元素开始处理。每当一个节点匹配某个模板时，它就应用该模板。（如果有多个模板匹配，则使用最佳匹配的模板；详细而繁琐的细节请参阅 www.w3.org/TR/xslt 上的规范。）如果没有模板匹配，处理器会执行默认操作。对于文本节点，默认操作是将内容包含在输出中。对于元素，默认操作是不产生输出，但继续处理其子节点。

下面是一个用于转换员工文件中 name 节点的模板：

```xml
<xsl:template match="/staff/employee/name">
    <td><xsl:apply-templates/></td>
</xsl:template>
```



如你所见，该模板会生成 `<td>...</td>` 分隔符，并要求处理器递归访问 name 元素的子节点。这里只有一个子节点——文本节点。当处理器访问该节点时，它会输出文本内容（当然，前提是没有其他匹配的模板）。

如果想将属性值复制到输出中，你就得稍微多费点功夫。下面是一个示例：

```xml
<xsl:template match="/staff/employee/hiredate">
    <td><xsl:value-of select="@year"/>-<xsl:value-of
    select="@month"/>-<xsl:value-of select="@day"/></td>
</xsl:template>
```

处理 hiredate 节点时，该模板会输出

1. 字符串 `<td>`
2. year 属性的值
3. 一个连字符
4. month 属性的值
5. 一个连字符
6. day 属性的值
7. 字符串 `</td>`

`xsl:value-of` 语句会计算节点集的字符串值。节点集由 select 属性的 XPath 值指定。在本例中，路径相对于当前处理的节点。节点集通过拼接所有节点的字符串值转换为字符串。属性节点的字符串值就是其值。文本节点的字符串值就是其内容。元素节点的字符串值是其子节点字符串值的拼接（但不包括其属性）。

代码清单 3.10 包含将带有员工记录的 XML 文件转换为 HTML 表格的样式表。

代码清单 3.11 展示了一组不同的转换。输入是同一个 XML 文件，输出是熟悉的属性文件格式的纯文本：

```text
employee.1.name=Carl Cracker
employee.1.salary=75000.0
employee.1.hiredate=1987-12-15
employee.2.name=Harry Hacker
employee.2.salary=50000.0
employee.2.hiredate=1989-10-1
employee.3.name=Tony Tester
employee.3.salary=40000.0
employee.3.hiredate=1990-3-15
```

该示例使用了 `position()` 函数，它返回当前节点从其父节点视角看到的位置。因此，只需切换样式表，我们就能得到完全不同的输出。这意味着你可以放心地使用 XML 来描述数据；如果某些应用程序需要使用另一种格式，只需使用 XSLT 生成替代格式即可。

在 Java 平台上生成 XSL 转换很简单。为每个样式表设置一个转换器工厂。然后获取一个转换器对象，并让它将源转换为结果：

```
var styleSheet = new File(filename);
var styleSource = new StreamSource(styleSheet);
Transformer t = TransformerFactory.newInstance().newTransformer(styleSource);
t.transform(source, result);
```

transform 方法的参数是实现 Source 和 Result 接口的类的对象。有几个类实现了 Source 接口：

- `DOMSource`
- `SAXSource`
- `StAXSource`
- `StreamSource`

你可以从文件、流、读取器或 URL 构造 StreamSource，也可以从 DOM 树的节点构造 DOMSource。例如，在上一节中，我们这样调用恒等转换：

```
t.transform(new DOMSource(doc), result);
```

在我们的示例程序中，我们做了稍微更有趣的事情。我们不是从现有的 XML 文件开始，而是生成一个 SAX XML 读取器，它通过发出适当的 SAX 事件来造成正在解析 XML 文件的假象。实际上，我们的 XML 读取器读取的是第 1 章所述的平面文件。输入文件如下所示：

```
Carl Cracker|75000.0|1987|12|15
Harry Hacker|50000.0|1989|10|1
Tony Tester|40000.0|1990|3|15
```

我们的 XML 读取器在处理输入时会生成 SAX 事件。下面是实现了 `XMLReader` 接口的 `EmployeeReader` 类的 parse 方法的一部分：

```
var attributes = new AttributesImpl();
handler.startDocument();
handler.startElement("", "staff", "staff", attributes);
while ((line = in.readLine()) != null)
{
    handler.startElement("", "employee", "employee", attributes);
    var tokenizer = new StringTokenizer(line, "|");
    handler.startElement("", "name", "name", attributes);
    String s = tokenizer.nextToken();
    handler.characters(s.toCharArray(), 0, s.length());
    handler.endElement("", "name", "name");
    . . . handler.endElement("", "employee", "employee");
}
handler.endElement("", rootElement, rootElement);
handler.endDocument();
```

转换器的 SAXSource 由该 XML 读取器构造：

```
t.transform(new SAXSource(new EmployeeReader(),
    new InputSource(new FileInputStream(filename))), result);
```

这是一种将非 XML 遗留数据转换为 XML 的巧妙技巧。当然，大多数 XSLT 应用程序已经拥有 XML 输入数据，你可以直接在 StreamSource 上调用 transform 方法：

```
t.transform(new StreamSource(file), result);
```

转换结果是一个实现 Result 接口的类的对象。Java 库提供了三个类：

- DOMResult
- SAXResult
- StreamResult

要将结果存储在 DOM 树中，请使用 DocumentBuilder 生成新的文档节点，并将其包装到 DOMResult 中：

```
Document doc = builder.newDocument();
t.transform(source, new DOMResult(doc));
```

要将输出保存到文件中，请使用 StreamResult：

```
t.transform(source, new StreamResult(file));
```

代码清单 3.12 包含完整的源代码。

### 代码清单 3.10 `transform/makehtml.xsl`

```xml
<?xml version="1.0" encoding="ISO-8859-1"?>

<xsl:stylesheet
    xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
    version="1.0">

<xsl:output method="html"/>

<xsl:template match="/staff">
    <table border="1"><xsl:apply-templates/></table>
</xsl:template>

<xsl:template match="/staff/employee">
    <tr><xsl:apply-templates/></tr>
</xsl:template>

<xsl:template match="/staff/employee/name">
    <td><xsl:apply-templates/></td>
</xsl:template>

<xsl:template match="/staff/employee/salary">
    <td><xsl:apply-templates/></td>
</xsl:template>

<xsl:template match="/staff/employee/hiredate">
    <td><xsl:value-of select="@year"/><xsl:value-of
    select="@month"/><xsl:value-of select="@day"/></td>
</xsl:template>

</xsl:stylesheet>
```

### 代码清单 3.11 `transform/makeprop.xsl`

```xml
<?xml version="1.0"?>

<xsl:stylesheet
    xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
    version="1.0">

<xsl:output method="text" omit-xml-declaration="yes"/>

<xsl:template match="/staff/employee">
employee:<xsl:value-of select="position()"
/>/name=<xsl:value-of select="name/text()"/>
/employee:<xsl:value-of select="position()"
/>/salary=<xsl:value-of select="salary/text()"/>
employee:<xsl:value-of select="position()"
/>/hiredate=<xsl:value-of select="hiredate/@year"
/>:<xsl:value-of select="hiredate/@month"
/>:<xsl:value-of select="hiredate/@day"/>
</xsl:template>

</xsl:stylesheet>
```

### 代码清单 3.12 transform/TransformTest.java

```java
package transform;

import java.io.*;
import java.nio.file.*;
import java.util.*;
import javax.xml.transform.*;
import javax.xml.transform.sax.*;
import javax.xml.transform.stream.*;
import org.xml.sax.*;
import org.xml.sax.helpers.*;

/**
 * This program demonstrates XSL transformations. It applies a transformation to a set of
 * employee records. The records are stored in the file employee.dat and turned into XML
 * format. Specify the stylesheet on the command line, e.g.<br>
 * java transform.TransformTest transform/makeprop.xsl
 * @version 1.04 2018-04-10
 * @author Cay Horstmann
 */
public class TransformTest
{
   public static void main(String[] args) throws Exception
   {
      Path path;
      if (args.length > 0) path = Paths.get(args[0]);
      else path = Paths.get("transform", "makeprop.xsl");
      try (InputStream styleIn = Files.newInputStream(path))
      {
         var styleSource = new StreamSource(styleIn);

         Transformer t = TransformerFactory.newInstance().newTransformer(styleSource);
         t.setOutputProperty(OutputKeys.INDENT, "yes");
         t.setOutputProperty(OutputKeys.METHOD, "xml");
         t.setOutputProperty("{http://xml.apache.org/xslt}indent-amount", "2");

         try (InputStream docIn = Files.newInputStream(Paths.get("transform", "employee.dat")))
         {
            t.transform(new SAXSource(new EmployeeReader(), new InputSource(docIn)),
               new StreamResult(System.out));
         }
      }
   }
}

/**
 * This class reads the flat file employee.dat and reports SAX parser events to act as if it
 * was parsing an XML file.
```



### 清单 3.12（续）

```java
 */
class EmployeeReader implements XMLReader
{
    private ContentHandler handler;

    public void parse(InputSource source) throws IOException, SAXException
    {
        InputStream stream = source.getByteStream();
        var in = new BufferedReader(new InputStreamReader(stream));
        String rootElement = "staff";
        var atts = new AttributesImpl();

        if (handler == null) throw new SAXException("No content handler");

        handler.startDocument();
        handler.startElement("", rootElement, rootElement, atts);
        String line;
        while ((line = in.readLine()) != null)
        {
            handler.startElement("", "employee", "employee", atts);
            var t = new StringTokenizer(line, "|");

            handler.startElement("", "name", "name", atts);
            String s = t.nextToken();
            handler.characters(s.toCharArray(), 0, s.length());
            handler.endElement("", "name", "name");

            handler.startElement("", "salary", "salary", atts);
            s = t.nextToken();
            handler.characters(s.toCharArray(), 0, s.length());
            handler.endElement("", "salary", "salary");

            atts.addAttribute("", "year", "year", "CDATA", t.nextToken());
            atts.addAttribute("", "month", "month", "CDATA", t.nextToken());
            atts.addAttribute("", "day", "day", "CDATA", t.nextToken());
            handler.startElement("", "hiredate", "hiredate", atts);
            handler.endElement("", "hiredate", "hiredate");
            atts.clear();

            handler.endElement("", "employee", "employee");
        }

        handler.endElement("", rootElement, rootElement);
        handler.endDocument();
    }

}
```

```java
public void setContentHandler(ContentHandler newValue)
{
    handler = newValue;
}

public ContentHandler getContentHandler()
{
    return handler;
}

// the following methods are just do-nothing implementations
public void parse(String systemId) throws IOException, SAXException {}
public void setErrorHandler(ErrorHandler handler) {}
public ErrorHandler getErrorHandler() { return null; }
public void setDTDHandler(DTDHandler handler) {}
public DTDHandler getDTDHandler() { return null; }
public void setEntityResolver(EntityResolver resolver) {}
public EntityResolver getEntityResolver() { return null; }
public void setProperty(String name, Object value) {}
public Object getProperty(String name) { return null; }
public void setFeature(String name, boolean value) {}
public boolean getFeature(String name) { return false; }
```

### javax.xml.transform.TransformerFactory 1.4

- `Transformer newTransformer(Source stylesheet)`

  返回 Transformer 类的一个实例，该类从给定源读取样式表。

### javax.xml.transform.stream.StreamSource 1.4

- `StreamSource(File f)`
- `StreamSource(InputStream in)`
- `StreamSource(Reader in)`
- `StreamSource(String systemID)`

  从文件、流、读取器或系统 ID（通常是相对或绝对 URL）构造一个流源。

### javax.xml.transform.sax.SAXSource 1.4

- `SAXSource(XMLReader reader, InputSource source)`

  构造一个 SAX 源，它从给定输入源获取数据，并使用给定读取器解析输入。

### org.xml.sax.XMLReader 1.4

- `void setContentHandler(ContentHandler handler)`

  设置处理器，在解析输入时向其通知解析事件。

- `void parse(InputSource source)`

  解析来自给定输入源的输入，并将解析事件发送给内容处理器。

### javax.xml.transform.dom.DOMResult 1.4

- `DOMResult(Node n)`

  从给定节点构造一个源。通常，n 是一个新的文档节点。

### org.xml.sax.helpers.AttributesImpl 1.4

- `void addAttribute(String uri, String lname, String qname, String type, String value)`

  向此属性集合添加一个属性。lname 参数是不带前缀的本地名称，qname 是带前缀的限定名称。type 参数是 "CDATA"、"ID"、"IDREF"、"IDREFS"、"NMTOKEN"、"NMTOKENS"、"ENTITY"、"ENTITIES" 或 "NOTATION" 之一。

- `void clear()`

  从此属性集合中移除所有属性。

本示例结束了我们对 Java 库中 XML 支持的讨论。现在，你应该对 XML 的主要优势有了良好的认识——特别是其自动解析和验证，以及强大的转换机制。当然，只有当你设计好 XML 格式时，所有这些技术才会为你所用。你需要确保这些格式足够丰富，能够表达你所有的业务需求，确保它们长期稳定，并确保你的业务伙伴愿意接受你的 XML 文档。这些问题可能比处理解析器、DTD 或转换更具挑战性。

在下一章中，我们将讨论 Java 平台上的网络编程，从网络套接字的基础知识开始，然后转向电子邮件和万维网的高级协议。

# 网络

## 本章内容

- 4.1 连接到服务器，第 227 页
- 4.2 实现服务器，第 236 页
- 4.3 获取 Web 数据，第 251 页
- 4.4 HTTP 客户端，第 271 页
- 4.5 发送电子邮件，第 278 页

本章开头，我们先回顾基本的网络概念，然后转向编写连接网络服务的 Java 程序。我们将向你展示网络客户端和服务器是如何实现的。最后，你将了解如何从 Java 程序发送电子邮件，以及如何从 Web 服务器收集信息。

## 4.1 连接到服务器

在接下来的几节中，你将连接到服务器，首先手动并使用 telnet 连接，然后使用 Java 程序连接。

### 4.1.1 使用 Telnet

telnet 程序是网络编程的绝佳调试工具。你应该能够通过在命令 shell 中输入 `telnet` 来启动它。

**注意：** 在 Windows 中，你需要激活 telnet。转到控制面板，选择“程序”，单击“启用或关闭 Windows 功能”，然后选中“Telnet 客户端”复选框。Windows 防火墙还会阻止本章使用的不少网络端口；你可能需要管理员账户才能解除阻止。

你可能使用过 telnet 连接到远程计算机，但也可以用它来与 Internet 主机提供的其他服务通信。下面是一个可以做什么的示例。输入

```
telnet time-a.nist.gov 13
```

如图 4.1 所示，你应该会收到类似下面的一行：

```
57488 16-04-10 04:23:00 50 0 610.5 UTC(NIST) *
```

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_250_0.png)

**图 4.1** “time of day”服务的输出

发生了什么？你连接到了大多数 UNIX 机器持续运行的“time of day”服务。你连接到的特定服务器由美国国家标准与技术研究院运营，提供铯原子钟的测量结果。（当然，由于网络延迟，报告的时间并不完全准确。）

按照惯例，“time of day”服务始终附加到“端口”号 13。

```
GET / HTTP/1.1
Host: horstmann.com
blank line
```

也就是说，在末尾按两次 Enter 键。

图 4.3 显示了响应。它应该看起来出奇地熟悉——你得到了一页 HTML 格式的文本，即 Cay Horstmann 的主页。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_252_0.png)

**图 4.3** 使用 telnet 访问 HTTP 端口

这与你的 Web 浏览器获取网页所经历的流程完全相同。它使用 HTTP 从服务器请求网页。当然，浏览器会更好地显示 HTML 代码。

> **注意：** 当你连接到在同一 IP 地址上托管多个域的 Web 服务器时，Host 键/值对是必需的。如果服务器只托管单个域，则可以省略它。

### 4.1.2 使用 Java 连接到服务器

清单 4.1 中的第一个网络程序将完成我们使用 telnet 所做的相同事情——连接到一个端口并打印出它发现的内容。

这个简单程序的关键语句如下：

```
var s = new Socket("time-a.nist.gov", 13);
InputStream inStream = s.getInputStream();
```



#### 清单 4.1 `socket/SocketTest.java`

```java
package socket;

import java.io.*;
import java.net.*;
import java.nio.charset.*;
import java.util.*;

/**
 * This program makes a socket connection to the atomic clock in Boulder, Colorado, and prints
 * the time that the server sends.
 * @version 1.22 2018-03-17
 * @author Cay Horstmann
 */
public class SocketTest
{
   public static void main(String[] args) throws IOException
   {
      try (var s = new Socket("time-a.nist.gov", 13);
            var in = new Scanner(s.getInputStream(), StandardCharsets.UTF_8))
      {
         while (in.hasNextLine())
         {
            String line = in.nextLine();
            System.out.println(line);
         }
      }
   }
}
```

第一行打开一个 `socket`，它是一种网络软件抽象，使数据能够进出此程序。我们将远程地址和端口号传递给套接字构造函数。如果连接失败，会抛出 `UnknownHostException`。如果还有其他问题，则发生 `IOException`。由于 `UnknownHostException` 是 `IOException` 的子类，并且这是一个示例程序，我们只捕获超类。

一旦套接字打开，`java.net.Socket` 中的 `getInputStream` 方法会返回一个 `InputStream` 对象，你可以像使用任何其他流一样使用它。获取流之后，此程序只是将每一行输入打印到标准输出。此过程会持续到流结束且服务器断开连接。

此程序仅适用于非常简单的服务器，例如“一天中的时间”服务。在更复杂的网络程序中，客户端向服务器发送请求数据，而服务器可能不会在响应结束时立即断开连接。你将在本章的多个示例中看到如何实现该行为。

Socket 类令人愉快且易于使用，因为 Java 库隐藏了建立网络连接以及通过连接发送数据的复杂性。`java.net` 包本质上提供了与处理文件时相同的编程接口。

> **注意：** 在本书中，我们仅涵盖传输控制协议（TCP）。Java 平台还支持用户数据报协议（UDP），它可用于发送数据包（也称为*数据报*），其开销远小于 TCP。缺点是数据包不必按顺序传递给接收应用程序，甚至可以完全丢弃。接收方需要将数据包按顺序排列，并请求重传丢失的数据包。UDP 非常适合可以容忍数据包丢失的应用程序——例如，音频或视频流或连续测量。

| `java.net.Socket` | 1.0 |
| --- | --- |
| `Socket(String host, int port)` | 构造一个套接字以连接到给定的主机和端口。 |
| `InputStream getInputStream()` |  |
| `OutputStream getOutputStream()` | 获取用于从套接字读取数据或向套接字写入数据的流。 |

### 4.1.3 套接字超时

从套接字读取会阻塞，直到数据可用。如果主机不可达，你的应用程序会等待很长时间，最终是否超时取决于底层操作系统。

你可以决定哪种超时值适合你的特定应用程序。然后，调用 `setSoTimeout` 方法设置超时值（以毫秒为单位）。

```java
var s = new Socket(...);
s.setSoTimeout(10000); // time out after 10 seconds
```

如果已为套接字设置超时值，那么所有后续读取操作在操作完成其工作之前达到超时时间时，都会抛出 `SocketTimeoutException`。你可以捕获该异常并对超时作出反应。

```java
    try
    {
        InputStream in = s.getInputStream(); // read from in
        . . .
    }
    catch (SocketTimeoutException e)
    {
        react to timeout
    }
```

写操作没有超时。

还有一个额外的超时问题需要解决。构造函数 `Socket(String host, int port)` 可能会无限期阻塞，直到与主机建立初始连接。你可以先构造一个未连接的套接字，然后带超时地连接它，从而克服此问题：

```java
    var s = new Socket();
    s.connect(new InetSocketAddress(host, port), timeout);
```

有关如何允许用户随时中断套接字连接，请参见第 244 页的 4.2.4 节“可中断套接字”。

#### `java.net.Socket` 1.0

- `Socket()` 1.0：创建一个尚未连接的套接字。
- `void connect(SocketAddress address)` 1.4：将此套接字连接到给定地址。
- `void connect(SocketAddress address, int timeoutInMilliseconds)` 1.4：将此套接字连接到给定地址，或在时间间隔到期时返回。
- `void setSoTimeout(int timeoutInMilliseconds)` 1.1：设置此套接字上读请求的阻塞时间。如果达到超时，则抛出 `SocketTimeoutException`。
- `boolean isConnected()` 1.4：如果套接字已连接，则返回 true。
- `boolean isClosed()` 1.4：如果套接字已关闭，则返回 true。

### 4.1.4 Internet 地址

通常，你不必太担心 Internet 地址——由 4 个字节（对于 IPv6，则为 16 个字节）组成的数字主机地址，例如 129.6.15.28。但是，如果需要在主机名和 Internet 地址之间转换，可以使用 InetAddress 类。

java.net 包支持 IPv6 Internet 地址，前提是主机操作系统支持。

静态 getByName 方法返回主机的 InetAddress 对象。例如，

```java
InetAddress address = InetAddress.getByName("time-a.nist.gov");
```

返回一个 InetAddress 对象，该对象封装了四个字节 129.6.15.28 的序列。可以使用 getAddress 方法访问这些字节。

```java
byte[] addressBytes = address.getAddress();
```

一些流量很大的主机名对应多个 Internet 地址，以便于负载均衡。例如，在撰写本文时，主机名 google.com 对应十二个不同的 Internet 地址。访问主机时会随机选择其中一个。可以使用 getAllByName 方法获取所有主机。

```java
InetAddress[] addresses = InetAddress.getAllByName(host);
```

最后，有时你需要本地主机的地址。如果只是请求 localhost 的地址，你总是会得到本地回环地址 127.0.0.1，其他人无法使用它连接到你的计算机。相反，使用静态 getLocalHost 方法获取本地主机的地址。

```java
InetAddress address = InetAddress.getLocalHost();
```

清单 4.2 是一个简单的程序：如果你不指定任何命令行参数，它会打印本地主机的 Internet 地址；如果你在命令行上指定主机名，它会打印另一台主机的所有 Internet 地址，例如

```java
java inetAddress.InetAddressTest www.horstmann.com
```

#### 清单 4.2 `inetAddress/InetAddressTest.java`

```java
package inetAddress;

import java.io.*;
import java.net.*;

/**
 * This program demonstrates the InetAddress class. Supply a host name as command-line
 * argument, or run without command-line arguments to see the address of the local host.
 * @version 1.02 2012-06-05
 * @author Cay Horstmann
 */
public class InetAddressTest
{
   public static void main(String[] args) throws IOException
   {
      if (args.length > 0)
      {
         String host = args[0];
         InetAddress[] addresses = InetAddress.getAllByName(host);
         for (InetAddress a : addresses)
            System.out.println(a);
      }
      else
      {
         InetAddress localHostAddress = InetAddress.getLocalHost();
         System.out.println(localHostAddress);
      }
   }
}
```

| `java.net.InetAddress` | 1.0 |
| --- | --- |
| `static InetAddress getByName(String host)` |  |
| `static InetAddress[] getAllByName(String host)` | 为给定主机名构造一个 InetAddress，或所有 Internet 地址的数组。 |
| `static InetAddress getLocalHost()` | 为本地主机构造一个 InetAddress。 |
| `byte[] getAddress()` | 返回包含数字地址的字节数组。 |
| `String getHostAddress()` | 返回由句点分隔的十进制数字组成的字符串，例如 "129.6.15.28"。 |
| `String getHostName()` | 返回主机名。 |





## 4.2 实现服务器

既然我们已经实现了一个从互联网接收数据的基本网络客户端，那么让我们来编写一个可以向客户端发送信息的简单服务器。

### 4.2.1 服务器套接字

服务器程序在启动时会等待客户端连接到其端口。对于我们的示例程序，我们选择了端口号 8189，该端口未被任何标准服务使用。`ServerSocket` 类建立套接字。在我们的例子中，命令

```java
var s = new ServerSocket(8189);
```

建立了一个监听 8189 端口的服务器。命令

```java
Socket incoming = s.accept();
```

告诉程序无限期等待，直到有客户端连接到该端口。一旦有人通过网络发送正确的请求连接到该端口，此方法就会返回一个表示已建立连接的 `Socket` 对象。你可以使用该对象来获取输入和输出流，如下面的代码所示：

```java
InputStream inStream = incoming.getInputStream();
OutputStream outStream = incoming.getOutputStream();
```

服务器发送到服务器输出流的所有内容都会成为客户端程序的输入，而客户端程序的所有输出最终都会进入服务器输入流。

本章的所有示例中，我们都是通过套接字传输文本。因此，我们将流转换为扫描器和写入器。

```java
var in = new Scanner(inStream, StandardCharsets.UTF_8);
var out = new PrintWriter(new OutputStreamWriter(outStream, StandardCharsets.UTF_8),
    true /* autoFlush */);
```

让我们向客户端发送一条问候语：

```java
out.println("Hello! Enter BYE to exit.");
```

当你使用 telnet 连接到端口 8189 上的这个服务器程序时，你会看到终端屏幕上出现这条问候语。

在这个简单服务器中，我们只是逐行读取客户端输入，并将其回显。这证明了程序能够接收输入。实际的服务器显然会根据输入进行计算并返回答案。

```java
String line = in.nextLine();
out.println("Echo: " + line);
if (line.trim().equals("BYE")) done = true;
```

最后，我们关闭传入的套接字。

```java
incoming.close();
```

仅此而已。每个服务器程序，例如 HTTP Web 服务器，都会持续执行这个循环：

- 1. 它通过传入的数据流接收来自客户端的命令（“获取这些信息”）。
- 2. 它解码客户端命令。
- 3. 它收集客户端请求的信息。
- 4. 它通过传出的数据流将信息发送给客户端。

清单 4.3 是完整的程序。

#### 清单 4.3 `server/EchoServer.java`

```java
package server;

import java.io.*;
import java.net.*;
import java.nio.charset.*;
import java.util.*;

/**
 * This program implements a simple server that listens to port 8189 and echoes back all
 * client input.
 * @version 1.22 2018-03-17
 * @author Cay Horstmann
 */
public class EchoServer
{
    public static void main(String[] args) throws IOException
    {
18  // establish server socket
19  try (var s = new ServerSocket(8189))
20  {
21      // wait for client connection
22      try (Socket incoming = s.accept())
23      {
24          InputStream inStream = incoming.getInputStream();
25          OutputStream outStream = incoming.getOutputStream();
26
27          try (var in = new Scanner(inStream, StandardCharsets.UTF_8))
28          {
29              var out = new PrintWriter(
30                  new OutputStreamWriter(outStream, StandardCharsets.UTF_8),
31                  true /* autoFlush */);
32
33              out.println("Hello! Enter BYE to exit.");
34
35              // echo client input
36              var done = false;
37              while (!done && in.hasNextLine())
38              {
39                  String line = in.nextLine();
40                  out.println("Echo: " + line);
41                  if (line.trim().equals("BYE")) done = true;
42              }
43          }
44      }
45  }
46
47 }
```

要试用它，请编译并运行该程序。然后使用 telnet 连接到服务器 localhost（或 IP 地址 127.0.0.1）和端口 8189。

如果你直接连接到互联网，那么世界上任何知道你 IP 地址和这个神奇端口号的人都可以访问你的回显服务器。

当你连接到该端口时，你会看到如图 4.4 所示的消息：

Hello! Enter BYE to exit.

输入任意内容，并观察输入在屏幕上回显。输入 BYE（全部大写字母）即可断开连接。服务器程序也会随之终止。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_261_0.png)

图 4.4 访问回显服务器

| java.net.ServerSocket 1.0 | |
| --- | --- |
| ServerSocket(int port) | 创建一个监听某个端口的服务器套接字。 |
| Socket accept() | 等待连接。此方法会阻塞（即闲置）当前线程，直到连接建立。该方法返回一个 `Socket` 对象，程序可以通过它与连接的客户端进行通信。 |
| void close() | 关闭服务器套接字。 |

### 4.2.2 服务多个客户端

前面的示例中的简单服务器有一个问题。假设我们想允许多个客户端同时连接到我们的服务器。通常，服务器在服务器计算机上持续运行，来自世界各地互联网的客户端可能想同时使用它。如果不支持多连接，任何一个客户端都可以通过长时间连接来独占该服务。通过线程的魔力，我们可以做得更好。

每当程序建立新的套接字连接——也就是说，每次调用 `accept()` 返回一个套接字——我们就会启动一个新线程来处理服务器与*那个*客户端之间的连接。主程序只需返回并等待下一个连接。为了实现这一点，服务器的主循环应该如下所示：

```java
while (true)
{
    Socket incoming = s.accept();
    var r = new ThreadedEchoHandler(incoming);

    var t = new Thread(r);
    t.start();
}
```

`ThreadedEchoHandler` 类实现了 `Runnable`，并在其 `run` 方法中包含与客户端通信的循环。

```java
class ThreadedEchoHandler implements Runnable
{
    . . .
    public void run()
    {
        try (InputStream inStream = incoming.getInputStream();
             OutputStream outStream = incoming.getOutputStream())
        {
            *Process input and send response*
        }
        catch(IOException e)
        {
            *Handle exception*
        }
    }
}
```

当每个连接都启动一个新线程时，多个客户端可以同时连接到服务器。你可以很容易地验证这一点。

- 1. 编译并运行服务器程序（清单 4.4）。
- 2. 打开多个 telnet 窗口，如图 4.5 所示。
- 3. 在窗口之间切换并输入命令。注意，你可以同时通过所有窗口进行通信。
- 4. 完成后，切换到启动服务器程序的窗口，并按 Ctrl+C 终止它。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_263_0.png)

**图 4.5** 多个 telnet 窗口同时通信

> **注意：** 在此程序中，我们为每个连接生成一个单独的线程。这种方法对于高性能服务器来说并不理想。你可以通过使用 `java.nio` 包的功能来实现更高的服务器吞吐量。有关更多信息，请参阅 [www.ibm.com/developerworks/java/library/j-javaio](http://www.ibm.com/developerworks/java/library/j-javaio)。

#### 清单 4.4 `threaded/ThreadedEchoServer.java`

```java
package threaded;

import java.io.*;
import java.net.*;
import java.nio.charset.*;
import java.util.*;

/**
 * This program implements a multithreaded server that listens to port 8189 and echoes back
 * all client input.
 * @author Cay Horstmann
 * @version 1.23 2018-03-17
 */
public class ThreadedEchoServer
{
    public static void main(String[] args)
    {
        try (var s = new ServerSocket(8189))
        {
            int i = 1;

            while (true)
            {
                Socket incoming = s.accept();
                System.out.println("Spawning " + i);
                Runnable r = new ThreadedEchoHandler(incoming);
                var t = new Thread(r);
                t.start();
                i++;
            }
        }
        catch (IOException e)
        {
            e.printStackTrace();
        }
    }
}

/**
 * This class handles the client input for one server socket connection.
 */
class ThreadedEchoHandler implements Runnable
{
    private Socket incoming;

    /**
     * Constructs a handler.
     * @param incomingSocket the incoming socket
     */
    public ThreadedEchoHandler(Socket incomingSocket)
    {
        incoming = incomingSocket;
    }
```


```java
public void run()
{
    try (InputStream inStream = incoming.getInputStream();
         OutputStream outStream = incoming.getOutputStream();
         var in = new Scanner(inStream, StandardCharsets.UTF_8);
         var out = new PrintWriter(
             new OutputStreamWriter(outStream, StandardCharsets.UTF_8),
             true /* autoflush */))
    {
        out.println("Hello! Enter BYE to exit.");

        // echo client input
        var done = false;
        while (!done && in.hasNextLine())
        {
            String line = in.nextLine();
            out.println("Echo: " + line);
            if (line.trim().equals("BYE"))
                done = true;
        }
    }
    catch (IOException e)
    {
        e.printStackTrace();
    }
}
```

### 4.2.3 半关闭

*半关闭*允许套接字连接的一端终止其输出，同时仍从另一端接收数据。

这是一个典型场景。假设你向服务器传输数据，但一开始并不知道数据有多少。对于文件，你只需在数据末尾关闭文件。然而，如果关闭套接字，就会立即与服务器断开连接，无法读取响应。

半关闭解决了这个问题。你可以关闭套接字的输出流，从而向服务器表明请求数据已结束，但保持输入流打开。

客户端代码如下所示：

```java
try (var socket = new Socket(host, port))
{
    var in = new Scanner(socket.getInputStream(), StandardCharsets.UTF_8);
    var writer = new PrintWriter(socket.getOutputStream());
    // send request data
    writer.print(...);
    writer.flush();
    socket.shutdownOutput();
    // now socket is half-closed
    // read response data
    while (in.hasNextLine())
    {
        String line = in.nextLine();
        ...
    }
}
```

服务器端只是读取输入，直到到达输入流的末尾。然后发送响应。

当然，此协议仅适用于一次性服务，例如 HTTP：客户端连接、发出请求、获取响应，然后断开连接。

| java.net.Socket | 1.0 |
|---|---|
| `void shutdownOutput()` | 1.3 |
| 将输出流设置为“流结束”。 | |
| `void shutdownInput()` | 1.3 |
| 将输入流设置为“流结束”。 | |
| `boolean isOutputShutdown()` | 1.4 |
| 如果输出已关闭，则返回 true。 | |
| `boolean isInputShutdown()` | 1.4 |
| 如果输入已关闭，则返回 true。 | |

### 4.2.4 可中断套接字

当连接到套接字时，当前线程会阻塞，直到连接建立或超时。类似地，当通过套接字读取数据时，当前线程会阻塞，直到操作成功或超时。（写入数据没有超时。）

在交互式应用中，你可能希望给用户一个选项，直接取消一个看起来不会产生结果的套接字连接。然而，如果线程阻塞在一个无响应的套接字上，你无法通过调用 interrupt 来解除阻塞。

要中断套接字操作，请使用 SocketChannel，这是 java.nio 包的一项特性。如下打开 SocketChannel：

```java
SocketChannel channel = SocketChannel.open(new InetSocketAddress(host, port));
```

通道没有关联的流。相反，它具有使用 Buffer 对象的读取和写入方法。（有关 NIO 缓冲区的更多信息，请参见第 1 章。）这些方法声明在 ReadableByteChannel 和 WritableByteChannel 接口中。

如果你不想处理缓冲区，可以使用 Scanner 类从 SocketChannel 读取，因为 Scanner 有一个接受 ReadableByteChannel 参数的构造器：

```java
var in = new Scanner(channel, StandardCharsets.UTF_8);
```

要将通道转换为输出流，请使用静态方法 Channels.newOutputStream。

```java
OutputStream outStream = Channels.newOutputStream(channel);
```

这就是你需要做的全部。每当线程在打开、读取或写入操作期间被中断时，该操作不会阻塞，而是以异常终止。

代码清单 4.5 中的程序对比了可中断套接字和阻塞套接字。服务器发送数字，并在第十个数字之后假装卡住。单击任一按钮，就会启动一个连接到服务器并打印输出的线程。第一个线程使用可中断套接字；第二个线程使用阻塞套接字。如果在前十个数字内单击 Cancel 按钮，则可以中断任一线程。

然而，在前十个数字之后，你只能中断第一个线程。第二个线程会一直阻塞，直到服务器最终关闭连接（参见图 4.6）。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_267_0.png)

#### 代码清单 4.5 InterruptibleSocketTest.java

```java
package interruptible;

import java.awt.*;
import java.awt.event.*;
import java.util.*;
import java.net.*;
import java.io.*;
import java.nio.charset.*;
import java.nio.channels.*;
import javax.swing.*;

/**
 * This program shows how to interrupt a socket channel.
 * @author Cay Horstmann
 * @version 1.05 2018-03-17
 */
public class InterruptibleSocketTest
{
   public static void main(String[] args)
   {
      EventQueue.invokeLater(() ->
         {
            var frame = new InterruptibleSocketFrame();
            frame.setTitle("InterruptibleSocketTest");
            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            frame.setVisible(true);
         });
   }
}

class InterruptibleSocketFrame extends JFrame
{
   private Scanner in;
   private JButton interruptibleButton;
   private JButton blockingButton;
   private JButton cancelButton;
   private JTextArea messages;
   private TestServer server;
   private Thread connectThread;

   public InterruptibleSocketFrame()
   {
      var northPanel = new JPanel();
      add(northPanel, BorderLayout.NORTH);

      final int TEXT_ROWS = 20;
      final int TEXT_COLUMNS = 60;
      messages = new JTextArea(TEXT_ROWS, TEXT_COLUMNS);
      add(new JScrollPane(messages));

      interruptibleButton = new JButton("Interruptible");
      blockingButton = new JButton("Blocking");

      northPanel.add(interruptibleButton);
      northPanel.add(blockingButton);

      interruptibleButton.addActionListener(event ->
      {
         interruptibleButton.setEnabled(false);
         blockingButton.setEnabled(false);
         cancelButton.setEnabled(true);
         connectThread = new Thread(() ->
         {
            try
            {
               connectInterruptibly();
            }
            catch (IOException e)
            {
               messages.append("\nInterruptibleSocketTest.connectInterruptibly: " + e);
            }
         });
         connectThread.start();
      });

      blockingButton.addActionListener(event ->
      {
         interruptibleButton.setEnabled(false);
         blockingButton.setEnabled(false);
         cancelButton.setEnabled(true);
         connectThread = new Thread(() ->
         {
            try
            {
               connectBlocking();
            }
            catch (IOException e)
            {
               messages.append("\nInterruptibleSocketTest.connectBlocking: " + e);
            }
         });
         connectThread.start();
      });

      cancelButton = new JButton("Cancel");
      cancelButton.setEnabled(false);
      northPanel.add(cancelButton);
```

#### 代码清单 4.5（续）

```java
      cancelButton.addActionListener(event ->
      {
         connectThread.interrupt();
         cancelButton.setEnabled(false);
      });

      server = new TestServer();
      new Thread(server).start();
      pack();
   }

   /**
    * Connects to the test server, using interruptible I/O
    */
   public void connectInterruptibly() throws IOException
   {
      messages.append("Interruptible:\n");
      try (SocketChannel channel
            = SocketChannel.open(new InetSocketAddress("localhost", 8189)))
      {
         in = new Scanner(channel, StandardCharsets.UTF_8);
         while (!Thread.currentThread().isInterrupted())
         {
            messages.append("Reading ");
            if (in.hasNextLine())
            {
               String line = in.nextLine();
               messages.append(line);
               messages.append("\n");
            }
         }
      }
      finally
      {
         EventQueue.invokeLater(() ->
         {
            messages.append("Channel closed\n");
            interruptibleButton.setEnabled(true);
            blockingButton.setEnabled(true);
         });
      }
   }

   /**
    * Connects to the test server, using blocking I/O
    */
   public void connectBlocking() throws IOException
   {
```




```java
messages.append("Blocking:\n");
try (var sock = new Socket("localhost", 8189))
{
    in = new Scanner(sock.getInputStream(), StandardCharsets.UTF_8);
    while (!Thread.currentThread().isInterrupted())
    {
        messages.append("Reading ");
        if (in.hasNextLine())
        {
            String line = in.nextLine();
            messages.append(line);
            messages.append("\n");
        }
    }
}
finally
{
    EventQueue.invokeLater(() ->
    {
        messages.append("Socket closed\n");
        interruptButton.setEnabled(true);
        blockingButton.setEnabled(true);
    });
}
}

/**
 * A multithreaded server that listens to port 8189 and sends numbers to the client,
 * simulating a hanging server after 10 numbers.
 */
class TestServer implements Runnable
{
    public void run()
    {
        try (var s = new ServerSocket(8189))
        {
            while (true)
            {
                Socket incoming = s.accept();
                Runnable r = new TestServerHandler(incoming);
                new Thread(r).start();
            }
        }
        catch (IOException e)
        {
            messages.append("\nTestServer.run: " + e);
        }
    }
}
```

#### 代码清单 4.5（续）

```java
/**
 * This class handles the client input for one server socket connection.
 */
class TestServerHandler implements Runnable
{
    private Socket incoming;
    private int counter;

    /**
     * Constructs a handler.
     * @param i the incoming socket
     */
    public TestServerHandler(Socket i)
    {
        incoming = i;
    }

    public void run()
    {
        try
        {
            try
            {
                OutputStream outStream = incoming.getOutputStream();
                var out = new PrintWriter(
                    new OutputStreamWriter(outStream, StandardCharsets.UTF_8),
                    true /* autoFlush */);
                while (counter < 100)
                {
                    counter++;
                    if (counter <= 10) out.println(counter);
                    Thread.sleep(100);
                }
            }
            finally
            {
                incoming.close();
                messages.append("Closing server\n");
            }
        }
        catch (Exception e)
        {
            messages.append("\nTestServerHandler.run: " + e);
        }
    }
}
```

**java.net.InetSocketAddress** 1.4

- `InetSocketAddress(String hostname, int port)` 使用给定的主机和端口构造地址对象，并在构造期间解析主机名。如果主机名无法解析，则地址对象的 unresolved 属性被设置为 true。
- `boolean isUnresolved()` 如果此地址对象无法解析，则返回 true。

**java.nio.channels.SocketChannel** 1.4

- `static SocketChannel open(SocketAddress address)` 打开一个套接字通道并将其连接到远程地址。

**java.nio.channels.Channels** 1.4

- `static InputStream newInputStream(ReadableByteChannel channel)` 构造一个从给定通道读取的输入流。
- `static OutputStream newOutputStream(WritableByteChannel channel)` 构造一个写入给定通道的输出流。

## 4.3 获取 Web 数据

要在 Java 程序中访问 Web 服务器，你会希望在比套接字连接和 HTTP 请求更高的层次上工作。在以下各节中，我们讨论 Java 库为此目的提供的类。

### 4.3.1 URL 和 URI

URL 和 URLConnection 类封装了从远程站点检索信息的大部分复杂性。你可以从字符串构造 URL 对象：

```java
var url = new URL(urlString);
```

如果你只想获取资源的内容，请使用 URL 类的 openStream 方法。此方法产生一个 InputStream 对象。按通常方式使用它——例如，构造一个 Scanner：

```java
InputStream inStream = url.openStream();
var in = new Scanner(inStream, StandardCharsets.UTF_8);
```

*java.net* 包对 URL（统一资源定位符）和 URI（统一资源标识符）作了有用的区分。

URI 是一种纯语法构造，包含指定 Web 资源的字符串的各个部分。URL 是一种特殊的 URI，即具有足够信息来定位资源。其他 URI，例如

```java
mailto:cay@horstmann.com
```

不是定位符——从这个标识符中没有数据可定位。这样的 URI 称为 URN（统一资源名）。

在 Java 库中，URI 类没有用于访问标识符所指定资源的方法——其唯一目的是解析。相比之下，URL 类可以打开到该资源的流。因此，URL 类仅适用于 Java 库知道如何处理的方案，例如 `http:`、`https:`、`ftp:`、本地文件系统（`file:`）和 JAR 文件（`jar:`）。

要理解为什么解析并非易事，请考虑 URI 可能有多复杂。例如，

```java
http://google.com?q=Beach+Chalet
ftp://username:password@ftp.yourserver.com/pub/file.txt
```

URI 规范给出了这些标识符构成的规则。URI 的语法为

```java
[scheme:]schemeSpecificPart[#fragment]
```

这里，`[ . . . ]` 表示可选部分，而 `:` 和 `#` 按字面包含在标识符中。

如果存在 *scheme:* 部分，则该 URI 称为*绝对* URI。否则，称为*相对* URI。

如果 *schemeSpecificPart* 不以 `/` 开头，则绝对 URI 是*不透明*的，例如

```java
mailto:cay@horstmann.com
```

所有绝对非不透明 URI 和所有相对 URI 都是*分层*的。例如

```java
http://horstmann.com/index.html
../../java/net/Socket.html#Socket()
```

分层 URI 的 *schemeSpecificPart* 具有以下结构

```java
[//authority][path][?query]
```

其中，同样，`[ . . . ]` 表示可选部分。

对于基于服务器的 URI，*authority* 部分的形式为

```java
[user-info@]host[:port]
```

*port* 必须是整数。

标准化 URI 的 RFC 2396 还支持基于注册表的机制，其中 *authority* 具有不同的格式，但这并不常用。

`URI` 类的目的之一是解析标识符并将其分解为各个组成部分。你可以使用以下方法检索它们

```java
getScheme
getSchemeSpecificPart
getAuthority
getUserInfo
getHost
getPort
getPath
getQuery
getFragment
```

`URI` 类的另一个目的是处理绝对和相对标识符。如果你有一个绝对 URI，例如

```java
http://docs.mycompany.com/api/java/net/ServerSocket.html
```

以及一个相对 URI，例如

```java
../java/net/Socket.html#Socket()
```

那么你可以将两者组合成一个绝对 URI。

```java
http://docs.mycompany.com/api/java/net/Socket.html#Socket()
```

此过程称为*解析*相对 URI。

相反的过程称为*相对化*。例如，假设你有一个*基* URI

```java
http://docs.mycompany.com/api
```

以及一个 URI

```java
http://docs.mycompany.com/api/java/lang/String.html
```

那么相对化后的 URI 是

```java
java/lang/String.html
```

`URI` 类支持这两种操作：

```java
relative = base.relativize(combined);
combined = base.resolve(relative);
```

### 4.3.2 使用 URLConnection 检索信息

如果你想要关于 Web 资源的附加信息，应该使用 URLConnection 类，它比基本的 URL 类提供更多控制。

使用 URLConnection 对象时，必须仔细安排步骤。

- 1. 调用 URL 类的 `openConnection` 方法以获得 URLConnection 对象：

  ```java
  URLConnection connection = url.openConnection();
  ```

- 2. 使用以下方法设置任意请求属性

  ```java
  setDoInput
  setDoOutput
  setIfModifiedSince
  setUseCaches
  setAllowUserInteraction
  setRequestProperty
  setConnectTimeout
  setReadTimeout
  ```

  我们将在本节后面和 API 注释中讨论这些方法。

- 3. 通过调用 connect 方法连接到远程资源：

  ```java
  connection.connect();
  ```

  除了建立到服务器的套接字连接外，此方法还向服务器查询*头信息*。

- 4. 连接到服务器后，可以查询头信息。`getHeaderFieldKey` 和 `getHeaderField` 两个方法枚举头部的所有字段。`getHeaderFields` 方法获取包含头部字段的标准 Map 对象。为方便起见，以下方法查询标准字段：

  ```java
  getContentType
  getContentLength
  getContentEncoding
  getDate
  getExpiration
  getLastModified
  ```

- 5. 最后，可以访问资源数据。使用 `getInputStream` 方法获得用于读取信息的输入流。（这与 URL 类的 `openStream` 方法返回的输入流相同。）另一个方法 `getContent` 在实践中不太有用。由 `text/plain` 和 `image/gif` 等标准内容类型返回的对象需要


`com.sun` 层次结构中的类来处理。你可以注册自己的内容处理器，但我们在本书中不讨论这种技术。

> **警告：** 然而，有些程序员在使用 `URLConnection` 类时会形成错误的心智模型。因此，务必遵循该连接的设置步骤。

现在让我们详细看看 `URLConnection` 的一些方法。有几个方法会在连接到服务器之前设置连接的属性。最重要的是 `setDoInput` 和 `setDoOutput`。默认情况下，该连接提供一个用于从服务器读取的输入流，但不提供用于写入的输出流。如果你想要一个输出流（例如，用于向 Web 服务器发送数据），需要调用

```
connection.setDoOutput(true);
```

接下来，你可能想设置一些请求头。请求头会与请求命令一起发送到服务器。下面是一个示例：

```
GET www.server.com/index.html HTTP/1.0
Referer: http://www.somewhere.com/links.html
Proxy-Connection: Keep-Alive
User-Agent: Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.8.1.4)
Host: www.server.com
Accept: text/html, image/gif, image/jpeg, image/png, */*
Accept-Language: en
Accept-Charset: iso-8859-1,utf-8
Cookie: orangemilano=19218887281987
```

`setIfModifiedSince` 方法告诉该连接，你只对某个日期之后修改过的数据感兴趣。

最后，你可以使用万能的 `setRequestProperty` 方法来设置任何对特定协议有意义的名称/值对。关于 HTTP 请求头的格式，请参阅 RFC 2616。其中一些参数没有很好的文档记录，而是由程序员们口口相传。例如，如果你想访问受密码保护的网页，必须执行以下操作：

1. 将用户名、一个冒号和密码连接起来。

```
String input = username + ":" + password;
```

2. 计算所得字符串的 Base64 编码。（Base64 编码将字节序列编码为可打印 ASCII 字符序列。）

```
Base64.Encoder encoder = Base64.getEncoder();
String encoding = encoder.encodeToString(input.getBytes(StandardCharsets.UTF_8));
```

3. 调用 setRequestProperty 方法，名称使用 "Authorization"，值使用 "Basic " + encoding。

```
connection.setRequestProperty("Authorization", "Basic " + encoding);
```

> **提示：** 你刚刚看到了如何访问受密码保护的网页。要通过 FTP 访问受密码保护的文件，需使用一种完全不同的方法：构造如下形式的 URL
>
> ftp://username:password@ftp.yourserver.com/pub/file.txt

一旦调用 connect 方法，就可以查询响应头信息。首先，让我们看看如何枚举所有响应头字段。这个类的实现者觉得有必要通过引入另一种迭代协议来表达他们的个性。调用

```
String key = connection.getHeaderFieldKey(n);
```

会从响应头中获取第 n 个键，其中 n 从 1 开始！如果 n 为 0 或大于头字段总数，则返回 null。没有方法返回字段数量；你只需不断调用 getHeaderFieldKey，直到得到 null。类似地，调用

```
String value = connection.getHeaderField(n);
```

会返回第 n 个值。

getHeaderFields 方法返回响应头字段的 Map。

```
Map<String,List<String>> headerFields = connection.getHeaderFields();
```

下面是一个典型 HTTP 请求的一组响应头字段：

```
Date: Wed, 27 Aug 2008 00:15:48 GMT
Server: Apache/2.2.2 (Unix)
Last-Modified: Sun, 22 Jun 2008 20:53:38 GMT
Accept-Ranges: bytes
Content-Length: 4613
Connection: close
Content-Type: text/html
```

> **注意：** 你可以通过 `connection.getHeaderField(0)` 或 `headerFields.get(null)` 获取响应状态行（例如 "HTTP/1.1 200 OK"）。

为方便起见，有六个方法用于查询最常见头类型的值，并在适当时将其转换为数值类型。表 4.1 展示了这些便捷方法。返回类型为 long 的方法返回自 1970 年 1 月 1 日 GMT 以来的秒数。

#### 表 4.1 响应头值的便捷方法

| 键名 | 方法名 | 返回类型 |
| --- | --- | --- |
| Date | `getDate` | `long` |
| Expires | `getExpiration` | `long` |
| Last-Modified | `getLastModified` | `long` |
| Content-Length | `getContentLength` | `int` |
| Content-Type | `getContentType` | `String` |
| Content-Encoding | `getContentEncoding` | `String` |

代码清单 4.6 中的程序让你可以试验 URL 连接。运行程序时，在命令行中提供一个 URL 以及可选的用户名和密码，例如：

```
java urlConnection.URLConnectionTest http://www.yourserver.com user password
```

该程序会打印

- 头部的所有键和值
- 表 4.1 中六个便捷方法的返回值
- 所请求资源的前十行

#### 代码清单 4.6 `urlConnection/URLConnectionTest.java`

```java
package urlConnection;

import java.io.*;
import java.net.*;
import java.nio.charset.*;
import java.util.*;

/**
 * This program connects to an URL and displays the response header data and the first
 * 10 lines of the requested data.
 *
 * Supply the URL and an optional username and password (for HTTP basic authentication) on the
 * command line.
 * @version 1.2 2018-03-17
 * @author Cay Horstmann
 */
public class URLConnectionTest
{
   public static void main(String[] args)
   {
      try
      {
         String urlName;
         if (args.length > 0) urlName = args[0];
         else urlName = "http://horstmann.com";

         var url = new URL(urlName);
         URLConnection connection = url.openConnection();

         // set username, password if specified on command line

         if (args.length > 2)
         {
            String username = args[1];
            String password = args[2];
            String input = username + ":" + password;
            Base64.Encoder encoder = Base64.getEncoder();
            String encoding = encoder.encodeToString(input.getBytes(StandardCharsets.UTF_8));
            connection.setRequestProperty("Authorization", "Basic " + encoding);
         }

         connection.connect();

         // print header fields

         Map<String, List<String>> headers = connection.getHeaderFields();
         for (Map.Entry<String, List<String>> entry : headers.entrySet())
         {
            String key = entry.getKey();
            for (String value : entry.getValue())
               System.out.println(key + ": " + value);
         }

         // print convenience functions

System.out.println("----------");
System.out.println("getContentType: " + connection.getContentType());
System.out.println("getContentLength: " + connection.getContentLength());
System.out.println("getContentEncoding: " + connection.getContentEncoding());
System.out.println("getDate: " + connection.getDate());
System.out.println("getExpiration: " + connection.getExpiration());
System.out.println("getLastModified: " + connection.getLastModified());
System.out.println("----------");

String encoding = connection.getContentEncoding();
if (encoding == null) encoding = "UTF-8";
try (var in = new Scanner(connection.getInputStream(), encoding))
{
    // print first ten lines of contents

    for (int n = 1; in.hasNextLine() && n <= 10; n++)
        System.out.println(in.nextLine());
    if (in.hasNextLine()) System.out.println(". . .");
}
catch (IOException e)
{
    e.printStackTrace();
}
      }
   }
}
```

| API | 描述 |
| --- | --- |
| `java.net.URL` (1.0) | |
| `InputStream openStream()` | 打开一个输入流，用于读取资源数据。 |
| `URLConnection openConnection()` | 返回一个 URLConnection 对象，该对象管理与资源的连接。 |

| API | 描述 |
| --- | --- |
| `java.net.URLConnection` (1.0) | |
| `void setDoInput(boolean doInput)` | 如果 doInput 为 true，用户可以从这个 URLConnection 接收输入。 |
| `boolean getDoInput()` | 如果 doInput 为 true，用户可以从这个 URLConnection 接收输入。 |
| `void setDoOutput(boolean doOutput)` | 如果 doOutput 为 true，用户可以向这个 URLConnection 发送输出。 |
| `boolean getDoOutput()` | 如果 doOutput 为 true，用户可以向这个 URLConnection 发送输出。 |



#### java.net.URLConnection 1.0 *（续）*

- `void setIfModifiedSince(long time)`
- `long getIfModifiedSince()`

  `ifModifiedSince` 属性配置此 `URLConnection` 仅获取自给定时间以来修改的数据。时间以自 1970 年 1 月 1 日 GMT 午夜以来的秒数给出。

- `void setConnectTimeout(int timeout)` 5.0
- `int getConnectTimeout()` 5.0

  设置或获取连接超时时间（以毫秒为单位）。如果在建立连接之前超时时间已过，关联输入流的 connect 方法将抛出 `SocketTimeoutException`。

- `void setReadTimeout(int timeout)` 5.0
- `int getReadTimeout()` 5.0

  设置或获取读取数据超时时间（以毫秒为单位）。如果在读取操作成功之前超时时间已过，read 方法将抛出 `SocketTimeoutException`。

- `void setRequestProperty(String key, String value)`

  设置请求头字段。

- `Map<String,List<String>> getRequestProperties()` 1.4

  返回请求属性的映射。同一键的所有值都放在一个列表中。

- `void connect()`

  连接到远程资源并获取响应头信息。

- `Map<String,List<String>> getHeaderFields()` 1.4

  返回响应头的映射。同一键的所有值都放在一个列表中。

- `String getHeaderFieldKey(int n)`

  获取第 n 个响应头字段的键；如果 n ≤ 0 或大于响应头字段数，则返回 null。

- `String getHeaderField(int n)`

  获取第 n 个响应头字段的值；如果 n ≤ 0 或大于响应头字段数，则返回 null。

- `int getContentLength()`

  获取内容长度（如果可用），否则返回 -1。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_284_0.png)

**图 4.7** 一个 HTML 表单

服务器端程序处理表单数据，并生成另一个 HTML 页面，由 Web 服务器发送回浏览器。该过程如图 4.8 所示。响应页面可以包含新信息（例如，在信息搜索程序中），或仅包含确认信息。然后 Web 浏览器显示响应页面。

本书不讨论服务器端程序的实现。我们只关注编写与现有服务器端程序交互的客户端程序。

当表单数据发送到 Web 服务器时，无论数据是由 servlet、CGI 脚本还是其他服务器端技术解释，都没有关系。客户端以标准格式将数据发送到 Web 服务器，Web 服务器负责将其传递给生成响应的程序。

常用的向 Web 服务器发送信息的两种命令称为 GET 和 POST。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_285_0.png)

**图 4.8** 服务器端程序执行期间的数据流

在 GET 命令中，只需将查询参数附加到 URL 的末尾。URL 的形式为

```
http://host/path?query
```

每个参数的形式为 *name=value*。参数用 & 字符分隔。参数值使用 *URL 编码* 方案进行编码，规则如下：

- 保留 A 到 Z、a 到 z、0 到 9 以及 . - _ 字符不变。
- 将所有空格替换为 + 字符。
- 将所有其他字符编码为 UTF-8，并将每个字节编码为 % 后跟两位十六进制数。

例如，要传输 *San Francisco, CA*，应使用 San+Francisco%2cCA，因为十六进制数 2c 是逗号字符（','）的 UTF-8 编码。

这种编码方式可以防止任何中间程序干扰空格和其他特殊字符。

在撰写本文时，Google Maps 网站 (www.google.com/maps) 接受名称分别为 q 和 hl 的查询参数，其值是位置查询

> **注意：** 如果在重定向中需要将 Cookie 从一个站点发送到另一个站点，可以这样配置全局 Cookie 处理器：
>
> `CookieHandler.setDefault(new CookieManager(null, CookiePolicy.ACCEPT_ALL));`
>
> 然后 Cookie 将正确地包含在重定向中。

尽管重定向通常会自动处理，但在某些情况下你需要自己手动处理。出于安全原因，不支持 HTTP 和 HTTPS 之间的自动重定向。重定向也可能因更微妙的原因而失败。例如，早期版本的邮政编码服务使用过重定向。回想一下，我们设置了 User-Agent 请求参数，以便邮局不会认为我们是通过 Java API 发出请求。虽然可以在初始请求中将用户代理设置为其他字符串，但该设置不会用于自动重定向。相反，自动重定向总是发送一个包含单词 Java 的通用用户代理字符串。

在这种情况下，你可以手动执行重定向。在连接服务器之前，关闭自动重定向：

```
connection.setInstanceFollowRedirects(false);
```

发出请求后，获取响应代码：

```
int responseCode = connection.getResponseCode();
```

检查是否为以下之一：

- `HttpURLConnection.HTTP_MOVED_PERM`
- `HttpURLConnection.HTTP_MOVED_TEMP`
- `HttpURLConnection.HTTP_SEE_OTHER`

在这种情况下，获取 Location 响应头以得到重定向的 URL。然后断开连接，并建立到新 URL 的新连接：

```
String location = connection.getHeaderField("Location");
if (location != null)
{
   URL base = connection.getURL();
   connection.disconnect();
   connection = (HttpURLConnection) new URL(base, location).openConnection();
   . . .
}
```

该程序展示的技术在需要从现有网站查询信息时非常有用。只需找出需要发送的参数，然后从回复中剥离 HTML 标签和其他不必要的信息。

#### **清单 4.7** post/PostTest.java

```java
package post;

import java.io.*;
import java.net.*;
import java.nio.charset.*;
import java.nio.file.*;
import java.util.*;

/**
 * This program demonstrates how to use the URLConnection class for a POST request.
 * @version 1.42 2018-03-17
 * @author Cay Horstmann
 */
public class PostTest
{
   public static void main(String[] args) throws IOException
   {
      String propsFilename = args.length > 0 ? args[0] : "post/post.properties";
      var props = new Properties();
      try (InputStream in = Files.newInputStream(Paths.get(propsFilename)))
      {
         props.load(in);
      }
      String urlString = props.remove("url").toString();
      Object userAgent = props.remove("User-Agent");
      Object redirects = props.remove("redirects");
      CookieHandler.setDefault(new CookieManager(null, CookiePolicy.ACCEPT_ALL));
      String result = doPost(new URL(urlString), props,
         userAgent == null ? null : userAgent.toString(),
         redirects == null ? -1 : Integer.parseInt(redirects.toString()));
      System.out.println(result);
   }

   /**
    * Do an HTTP POST.
    * @param url the URL to post to
    * @param nameValuePairs the query parameters
    * @param userAgent the user agent to use, or null for the default user agent
    * @param redirects the number of redirects to follow manually, or -1 for automatic
    * redirects
    * @return the data returned from the server
    */
   public static String doPost(URL url, Map<Object, Object> nameValuePairs, String userAgent,
         int redirects) throws IOException
   {
      var connection = (HttpURLConnection) url.openConnection();
      if (userAgent != null)
         connection.setRequestProperty("User-Agent", userAgent);
```




#### **清单 4.7** *（续）*

```java
97    while (in.hasNextLine())
98    {
99        response.append(in.nextLine());
100       response.append("\n");
101   }
102   }
103   catch (IOException e)
104   {
105       InputStream err = connection.getErrorStream();
106       if (err == null) throw e;
107       try (var in = new Scanner(err))
108       {
109           response.append(in.nextLine());
110           response.append("\n");
111       }
112   }
113
114       return response.toString();
115   }
116 }
```

| **java.net.HttpURLConnection 1.0** |
| --- |
| • `InputStream getErrorStream()`<br>返回一个流，你可以从中读取 Web 服务器错误消息。 |

| **java.net.URLEncoder 1.0** |
| --- |
| • `static String encode(String s, String encoding)` 1.4<br>返回字符串 s 的 URL 编码形式，使用给定的字符编码方案。（推荐的方案是 "UTF-8"。）在 URL 编码中，字符 A-Z、a-z、0-9、'.'、'-'、'*' 保持不变。空格被编码为 +，所有其他字符被编码为形式为 %XY 的编码字节序列，其中 0xXY 是该字节的十六进制值。 |

| **java.net.URLDecoder 1.2** |
| --- |
| • `static String decode(String s, String encoding)` 1.4<br>返回在给定字符编码方案下对 URL 编码字符串 s 的解码结果。 |

## 4.4 HTTP 客户端

`URLConnection` 类设计时，HTTP 尚未成为 Web 的通用协议。它支持多种协议，但其 HTTP 支持有些繁琐。当决定支持 HTTP/2 时，显然最好提供一个现代客户端接口，而不是改造现有 API。`HttpClient` 提供了更方便的 API 和对 HTTP/2 的支持。在 Java 9 和 10 中，API 类位于 `jdk.incubator.http` 包中，以便让 API 有机会根据用户反馈演进。从 Java 11 起，`HttpClient` 位于 `java.net.http` 包中。

> **注意：** 在 Java 9 和 10 中，你需要使用以下命令行选项运行程序
>
> `--add-modules jdk.incubator.httpclient`

HTTP 客户端 API 提供了比 `URLConnection` 类更简单的连接 Web 服务器的机制，后者有一套相当繁琐的步骤。

一个 `HttpClient` 可以发出请求并接收响应。通过调用以下代码获取客户端：

```java
HttpClient client = HttpClient.newHttpClient();
```

或者，如果需要配置客户端，可以使用构建器 API，如下所示：

```java
HttpClient client = HttpClient.newBuilder()
    .followRedirects(HttpClient.Redirect.ALWAYS)
    .build();
```

也就是说，先获取一个构建器，调用方法来定制将要构建的对象，然后调用 build 方法完成构建过程。这是构造不可变对象的一种常见模式。

在构造请求时，你也遵循构建器模式。下面是一个 GET 请求：

```java
HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("http://hostname.com"))
    .GET()
    .build();
```

URI 是“统一资源标识符”，在使用 HTTP 时，它与 URL 相同。然而，在 Java 中，URL 类提供了实际打开到 URL 的连接的方法，而 URI 类只关心语法（方案、主机、端口、路径、查询、片段等）。

对于 POST 请求，你需要一个“主体发布器”，它将请求数据转换为要发布的数据。字符串、字节数组和文件都有对应的主体发布器。例如，如果你的请求采用 JSON，只需将 JSON 字符串提供给字符串主体发布器即可。

```java
HttpRequest request = HttpRequest.newBuilder()
    .uri(new URI(url))
    .header("Content-Type", "application/json")
    .POST(HttpRequest.BodyPublishers.ofString(jsonString))
    .build();
```

遗憾的是，该 API 不支持常见内容类型所需的格式。清单 4.8 中的示例程序提供了用于表单数据和文件上传的主体发布器。

发送请求时，必须告诉客户端如何处理响应。如果只想要字符串形式的响应体，可以像这样使用 HttpResponse.BodyHandlers.ofString() 发送请求：

```java
HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
```

`HttpResponse` 类是一个泛型类型，其类型参数表示响应体的类型。可以像下面这样简单地获取响应体字符串：

```java
String bodyString = response.body();
```

还有其他响应体处理器，可以将响应作为字节数组或输入流获取。BodyHandlers.ofFile(filePath) 生成一个处理器，将响应保存到给定文件；BodyHandlers.ofFileDownload(directoryPath) 将响应保存到给定目录，并使用 Content-Disposition 头中的文件名。最后，从 BodyHandlers.discarding() 获得的处理器只是丢弃响应。

处理响应内容并不被视为该 API 的一部分。例如，如果收到 JSON 数据，你需要一个 JSON 库来解析内容。

`HttpResponse` 对象还会提供状态码和响应头。

```java
int status = response.statusCode();
HttpHeaders responseHeaders = response.headers();
```

你可以将 `HttpHeaders` 对象转换为映射：

```java
Map<String, List<String>> headerMap = responseHeaders.map();
```

映射的值是列表，因为在 HTTP 中，每个键可以有多个值。

### 清单 4.8  *（续）*

```java
import java.net.http.HttpRequest.*;

class MoreBodyPublishers
{
    public static BodyPublisher ofFormData(Map<Object, Object> data)
    {
        var first = true;
        var builder = new StringBuilder();
        for (Map.Entry<Object, Object> entry : data.entrySet())
        {
            if (first) first = false;
            else builder.append("&");
            builder.append(URLEncoder.encode(entry.getKey().toString(),
                StandardCharsets.UTF_8));
            builder.append("=");
            builder.append(URLEncoder.encode(entry.getValue().toString(),
                StandardCharsets.UTF_8));
        }
        return BodyPublishers.ofString(builder.toString());
    }

    private static byte[] bytes(String s) { return s.getBytes(StandardCharsets.UTF_8); }

    public static BodyPublisher ofMimeMultipartData(Map<Object, Object> data, String boundary)
        throws IOException
    {
        var byteArrays = new ArrayList<byte[]>();
        byte[] separator = bytes("--" + boundary + "\r\nContent-Disposition: form-data; name=");
        for (Map.Entry<Object, Object> entry : data.entrySet())
        {
            byteArrays.add(separator);

            if (entry.getValue() instanceof Path)
            {
                var path = (Path) entry.getValue();
                String mimeType = Files.probeContentType(path);
                byteArrays.add(bytes("\"" + entry.getKey() + "\"; filename=\"" + path.getFileName()
                    + "\"\r\nContent-Type: " + mimeType + "\r\n"));
                byteArrays.add(Files.readAllBytes(path));
            }
            else
                byteArrays.add(bytes("\"" + entry.getKey() + "\"\r\n\r\n" + entry.getValue() + "\r\n"));
        }
        byteArrays.add(bytes("--" + boundary + "--"));
        return BodyPublishers.ofByteArrays(byteArrays);
    }

58 public static BodyPublisher ofSimpleJSON(Map<Object, Object> data)
59 {
60     var builder = new StringBuilder();
61     builder.append("{");
62     var first = true;
63     for (Map.Entry<Object, Object> entry : data.entrySet())
64     {
65         if (first) first = false;
66         else
67             builder.append(", ");
68         builder.append(jsonEscape(entry.getKey().toString())).append(": ")
69             .append(jsonEscape(entry.getValue().toString()));
70     }
71     builder.append("}");
72     return BodyPublishers.ofString(builder.toString());
73 }

75 private static Map<Character, String> replacements = Map.of('\b', "\\b", '\f', "\\f",
76     '\n', "\\n", '\r', "\\r", '\t', "\\t", '\"', "\\\"", '\\', "\\\\");

78 private static String jsonEscape(String str)
79 {
80     var result = new StringBuilder("\"");
81     for (int i = 0; i < str.length(); i++)
82     {
83         char ch = str.charAt(i);
84         String replacement = replacements.get(ch);
85         if (replacement == null) result.append(ch);
86         else result.append(replacement);
87     }
88     result.append("\"");
89     return result;
90 }
91 }

93 public class HttpClientTest
94 {
95     public static void main(String[] args)
96         throws IOException, URISyntaxException, InterruptedException
97     {
98         System.setProperty("jdk.httpclient.HttpClient.log", "headers,errors");
99         String propsFilename = args.length > 0 ? args[0] : "client/post.properties";
100         Path propsPath = Paths.get(propsFilename);
101         var props = new Properties();
102         try (InputStream in = Files.newInputStream(propsPath))
103         {
104             props.load(in);
105         }
```



### 清单 4.8（续）

```java
106    String urlString = "" + props.remove("url");
107    String contentType = "" + props.remove("Content-Type");
108    if (contentType.equals("multipart/form-data")) {
110        var generator = new Random();
111        String boundary = new BigInteger(256, generator).toString();
112        contentType += ";boundary=" + boundary;
113        props.replaceAll((k, v) ->
114            v.toString().startsWith("file:")
115                ? propsPath.getParent().resolve(Paths.get(v.toString().substring(7)))
116                : v);
117    }
118    String result = doPost(urlString, contentType, props);
119    System.out.println(result);
120    }
121
122    public static String doPost(String url, String contentType, Map<Object, Object> data)
123        throws IOException, URISyntaxException, InterruptedException
124    {
125        HttpClient client = HttpClient.newBuilder()
126            .followRedirects(HttpClient.Redirect.ALWAYS).build();
127
128        BodyPublisher publisher = null;
129        if (contentType.startsWith("multipart/form-data")) {
131            String boundary = contentType.substring(contentType.lastIndexOf('=') + 1);
132            publisher = MoreBodyPublishers.ofMimeMultipartData(data, boundary);
133        }
134        else if (contentType.equals("application/x-www-form-urlencoded")) {
135            publisher = MoreBodyPublishers.ofFormData(data);
136        } else
137        {
138            contentType = "application/json";
139            publisher = MoreBodyPublishers.ofSimpleJSON(data);
140        }
141
142        HttpRequest request = HttpRequest.newBuilder()
143            .uri(new URI(url))
144            .header("Content-Type", contentType)
145            .POST(publisher)
146            .build();
147        HttpResponse<String> response
148            = client.send(request, HttpResponse.BodyHandlers.ofString());
149        return response.body();
150    }
151 }
```

### java.net.HttpClient 11

- `static HttpClient newHttpClient()`  
  生成一个具有默认配置的 HttpClient。
- `static HttpClient.Builder newBuilder()`  
  生成用于构建 HttpClient 的构建器。
- `<T> HttpResponse<T> send(HttpRequest request, HttpResponse.BodyHandler<T> responseBodyHandler)`
- `<T> CompletableFuture<HttpResponse<T>> sendAsync(HttpRequest request, HttpResponse.BodyHandler<T> responseBodyHandler)`  
  发起同步或异步请求，并使用给定的处理器处理响应正文。

### java.net.HttpClient.Builder 11

- `HttpClient build()`  
  生成一个具有此构建器所配置属性的 HttpClient。
- `HttpClient.Builder followRedirects(HttpClient.Redirect policy)`  
  将重定向策略设置为 HttpClient.Redirect 枚举的 ALWAYS、NEVER 或 NORMAL（仅拒绝从 HTTPS 到 HTTP 的重定向）之一。
- `HttpClient.Builder executor(Executor executor)`  
  设置用于异步请求的执行器。

### java.net.HttpRequest 11

- `static HttpRequest.Builder newBuilder()`  
  生成用于构建 HttpRequest 的构建器。

### java.net.HttpRequest.Builder 11

- `HttpRequest build()`  
  生成一个具有此构建器所配置属性的 HttpRequest。
- `HttpRequest.Builder uri(URI uri)`  
  设置此请求的 URI。
- `HttpRequest.Builder header(String name, String value)`  
  设置此请求的请求头。

### java.net.HttpRequest.Builder 11（续）

| 方法 | 说明 |
| --- | --- |
| `HttpRequest.Builder GET()`<br>`HttpRequest.Builder DELETE()`<br>`HttpRequest.Builder POST(HttpRequest.BodyPublisher bodyPublisher)`<br>`HttpRequest.Builder PUT(HttpRequest.BodyPublisher bodyPublisher)` | 设置此请求的请求方法和正文。 |

### java.net.HttpResponse<T> 11

| 方法 | 说明 |
| --- | --- |
| `T body()` | 返回此响应的正文。 |
| `int statusCode()` | 返回此响应的状态码。 |
| `HttpHeaders headers()` | 返回响应头。 |

### java.net.HttpHeaders 11

| 方法 | 说明 |
| --- | --- |
| `Map<String,List<String>> map()` | 返回这些标头的 Map。 |
| `Optional<String> firstValue(String name)` | 这些标头中具有给定名称的第一个值（如果存在）。 |

## 4.5 发送电子邮件

过去，编写一个通过套接字连接到邮件服务器的 25 号端口（SMTP 端口）来发送电子邮件的程序很简单。Simple Mail Transport Protocol（SMTP）描述了电子邮件消息的格式。一旦连接到服务器，就发送邮件头（采用 SMTP 格式，很容易生成），随后发送邮件正文。

具体步骤如下：

1. 打开一个连接到你的主机的套接字。

   ```java
   var s = new Socket("mail.yourserver.com", 25); // 25 is SMTP
   var out = new PrintWriter(s.getOutputStream(), StandardCharsets.UTF_8);
   ```

2. 向打印流发送以下信息：

   ```text
   HELO sending host
   MAIL FROM: sender e-mail address
   RCPT TO: recipient e-mail address
   DATA
   Subject: subject
   (blank line)
   mail message (any number of lines)
   .
   QUIT
   ```

SMTP 规范（RFC 821）规定，各行必须以 `\r` 后跟 `\n` 结尾。

过去，SMTP 服务器通常愿意转发来自任何人的电子邮件。然而，在如今垃圾邮件泛滥的时代，大多数服务器都内置了检查，只接受来自其信任的用户或 IP 地址范围的请求。身份验证通常通过安全套接字连接进行。

手动实现这些身份验证方案会非常繁琐。相反，我们将向你展示如何使用 JavaMail API 从 Java 程序发送电子邮件。

从 www.oracle.com/technetwork/java/javamail 下载 JavaMail，并将其解压到硬盘上的某个位置。

要使用 JavaMail，需要设置一些取决于邮件服务器的属性。例如，使用 GMail 时，使用

```properties
mail.transport.protocol=smtps
mail.smtps.auth=true
mail.smtps.host=smtp.gmail.com
mail.smtps.user=accountname@gmail.com
```

我们的示例程序从属性文件中读取这些内容。

出于安全原因，我们不把密码放入属性文件，而是提示输入密码。

读取属性文件，然后像这样获取邮件会话：

```java
Session mailSession = Session.getDefaultInstance(props);
```

创建一条包含所需发件人、收件人、主题和邮件正文的消息：

```java
var message = new MimeMessage(mailSession);
message.setFrom(new InternetAddress(from));
message.addRecipient(RecipientType.TO, new InternetAddress(to));
message.setSubject(subject);
message.setText(builder.toString());
```

然后将其发送出去：

```java
Transport tr = mailSession.getTransport();
tr.connect(null, password);
tr.sendMessage(message, message.getAllRecipients());
tr.close();
```

清单 4.9 中的程序从以下格式的文本文件中读取消息

- 发件人
- 收件人
- 主题
- 邮件正文（任意行数）

要运行该程序，请从 https://javaee.github.io/javamail 下载 JavaMail 实现。你还需要 Java Activation Framework 的 JAR 文件——可从 http://www.oracle.com/technetwork/java/javase/jaf-135115.html 获取，或在 Maven Central 上搜索。然后运行

```bash
java -classpath .:javax.mail.jar:activation-1.1.1.jar path/to/message.txt
```

在撰写本文时，GMail 不检查信息的真实性——你可以提供任意发件人。（下次你收到来自 president@whitehouse.gov 的电子邮件，邀请你参加前草坪上的正式晚宴时，请记住这一点。）

> **提示：** 如果你无法弄清楚邮件连接为什么不起作用，请调用
>
> ```java
> mailSession.setDebug(true);
> ```
>
> 并检查消息。此外，JavaMail API FAQ 中有一些有用的调试提示。

### 清单 4.9 `mail/MailTest.java`

```java
1  package mail;

3  import java.io.*;
4  import java.nio.charset.*;
5  import java.nio.file.*;
6  import java.util.*;
7  import javax.mail.*;
8  import javax.mail.internet.*;
9  import javax.mail.internet.MimeMessage.RecipientType;

11 /**
12  * This program shows how to use JavaMail to send mail messages.
13  * @author Cay Horstmann
14  * @version 1.01 2018-03-17
```




```java
*/
public class MailTest
{
    public static void main(String[] args) throws MessagingException, IOException
    {
        var props = new Properties();
        try (InputStream in = Files.newInputStream(Paths.get("mail", "mail.properties")))
        {
            props.load(in);
        }
        List<String> lines = Files.readAllLines(Paths.get(args[0]), StandardCharsets.UTF_8);

        String from = lines.get(0);
        String to = lines.get(1);
        String subject = lines.get(2);

        var builder = new StringBuilder();
        for (int i = 3; i < lines.size(); i++)
        {
            builder.append(lines.get(i));
            builder.append("\n");
        }

        Console console = System.console();
        var password = new String(console.readPassword("Password: "));

        Session mailSession = Session.getDefaultInstance(props);
        // mailSession.setDebug(true);
        var message = new MimeMessage(mailSession);
        message.setFrom(new InternetAddress(from));
        message.addRecipient(RecipientType.TO, new InternetAddress(to));
        message.setSubject(subject);
        message.setText(builder.toString());
        Transport tr = mailSession.getTransport();
        try
        {
            tr.connect(null, password);
            tr.sendMessage(message, message.getAllRecipients());
        }
        finally
        {
            tr.close();
        }
    }
}
```

在本章中，你已经看到了如何用 Java 编写网络客户端和服务器，以及如何从 Web 服务器获取信息。下一章将介绍数据库连接。你将学习如何使用 JDBC API 在 Java 中处理关系数据库。

*此页有意留空*

# 第 5 章

# 数据库编程

## 本章内容

- 5.1 JDBC 的设计，第 284 页
- 5.2 结构化查询语言，第 287 页
- 5.3 JDBC 配置，第 293 页
- 5.4 使用 JDBC 语句，第 299 页
- 5.5 查询执行，第 310 页
- 5.6 可滚动和可更新的结果集，第 322 页
- 5.7 行集，第 329 页
- 5.8 元数据，第 334 页
- 5.9 事务，第 344 页
- 5.10 Web 和企业应用程序中的连接管理，第 349 页

1996 年，Sun 公司发布了第一个版本的 JDBC API。该 API 允许程序员连接到数据库，并使用结构化查询语言（SQL）进行查询或更新。（SQL，通常读作“sequel”，是关系数据库访问的行业标准。）自那时起，JDBC 已成为 Java 库中最常用的 API 之一。

JDBC 已经多次更新。在本书出版时，JDBC 4.3（Java 9 附带的版本）是最新的版本。

在本章中，我们将解释 JDBC 背后的关键思想。我们将向您介绍（或帮助您回顾）SQL——用于关系数据库的行业标准结构化查询语言。然后，我们将提供足够的细节和示例，让您能够开始在常见编程场景中使用 JDBC。

> **注意：** 根据 Oracle 的说法，JDBC 是一个商标术语，而不是 Java 数据库连接（Java Database Connectivity）的首字母缩写。它的命名是为了让人联想到 ODBC——一个由微软首创、后来被纳入 SQL 标准的标准数据库 API。

## 5.1 JDBC 的设计

从一开始，Java 技术的开发者就意识到 Java 在处理数据库方面所展现的潜力。1995 年，他们开始扩展标准 Java 库，以处理对数据库的 SQL 访问。他们最初希望做的是扩展 Java，使程序能够仅用“纯” Java 与任意数据库通信。但他们很快就意识到这是一项不可能完成的任务：数据库种类太多，协议也太多。此外，虽然数据库厂商都赞成 Java 提供一种标准的网络协议用于数据库访问，但他们只有在 Java 使用*他们自己的*网络协议时才会支持。

所有数据库厂商和工具厂商*确实*达成一致的是：Java 提供一个纯 Java API 用于 SQL 访问，并配有一个驱动程序管理器，允许第三方驱动程序连接到特定数据库。这样，数据库厂商可以提供自己的驱动程序插入到驱动程序管理器中。于是，就会有一个简单的机制将第三方驱动程序注册到驱动程序管理器中。

这种组织方式遵循了微软 ODBC 非常成功的模式，ODBC 为数据库访问提供了一种 C 语言接口。JDBC 和 ODBC 都基于相同的理念：按照 API 编写的程序与驱动程序管理器通信，而驱动程序管理器再使用驱动程序与实际数据库通信。

这意味着 JDBC API 是大多数程序员唯一需要处理的东西。

### 5.1.1 JDBC 驱动程序类型

JDBC 规范将驱动程序分为以下*类型*：

- *类型 1 驱动程序*将 JDBC 转换为 ODBC，并依赖 ODBC 驱动程序与数据库通信。早期版本的 Java 包含一个这样的驱动程序，即 *JDBC/ODBC 桥*。然而，该桥需要部署并进行适当配置的 ODBC 驱动程序。当 JDBC 首次发布时，这个桥接器对于测试很方便，但从未打算用于生产环境。目前，许多更好的驱动程序已经可用，JDK 不再提供 JDBC/ODBC 桥。
- *类型 2 驱动程序*部分用 Java 编写，部分用本地代码编写；它与数据库的客户端 API 通信。要使用这种驱动程序，除了 Java 库之外，还需要在客户端上安装一些特定于平台的代码。
- *类型 3 驱动程序*是一种纯 Java 客户端库，它使用与数据库无关的协议将数据库请求发送到服务器组件，然后服务器组件将这些请求转换为特定于数据库的协议。这简化了部署，因为特定于平台的代码只位于服务器上。
- *类型 4 驱动程序*是一种纯 Java 库，它将 JDBC 请求直接转换为特定于数据库的协议。

> **注意：** JDBC 规范可在 https://jcp.org/aboutJava/communityprocess/mrel/jsr221/index3.html 获取。

大多数数据库厂商会随其数据库提供类型 3 或类型 4 驱动程序。此外，许多第三方公司专门生产比数据库厂商提供的驱动程序具有更好的标准符合性、支持更多平台、性能更好，或者在某些情况下仅仅是更可靠的驱动程序。

总之，JDBC 的最终目标是实现以下可能性：

- 程序员可以用 Java 编程语言编写应用程序，使用标准 SQL 语句（甚至 SQL 的专业扩展）访问任何数据库，同时遵循 Java 语言的惯例。
- 数据库厂商和数据库工具厂商可以提供低级驱动程序。因此，他们可以针对自己的特定产品优化驱动程序。

**注：** 如果你好奇为什么 Java 不直接采用 ODBC 模型，根据 1996 年 JavaOne 大会上的解释，原因是：

- ODBC 很难学。
- ODBC 的少数命令带有大量复杂选项。Java 编程语言的首选风格是拥有简单直观的方法，但数量众多。
- ODBC 依赖于 `void*` 指针和其他在 Java 编程语言中不自然的 C 特性。
- 基于 ODBC 的解决方案本质上不如纯 Java 解决方案安全，也更难部署。

### 5.1.2 JDBC 的典型用途

传统的客户端/服务器模型在客户端有丰富的 GUI，在服务器端有数据库（参见图 5.1）。在这种模型中，JDBC 驱动程序部署在客户端。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_308_0.png)

**图 5.1** 传统的客户端/服务器应用程序

然而，如今更常见的是三层模型，其中客户端应用程序不直接调用数据库。相反，它调用服务器上的中间件层，然后由该中间件层进行数据库查询。三层模型有几个优点。它将*视觉呈现*（客户端）与*业务逻辑*（中间层）以及原始数据（数据库）分离开来。因此，就可以访问相同的数据并



来自多个客户端的相同业务规则，例如 Java 桌面应用、Web 浏览器或移动应用。

客户端与中间层之间的通信通常通过 HTTP 进行。JDBC 管理中间层与后端数据库之间的通信。图 5.2 展示了基本架构。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_309_0.png)

**图 5.2** 三层应用程序

## 5.2 结构化查询语言

JDBC 允许你使用 SQL 与数据库通信，SQL 是几乎所有现代关系数据库的命令语言。桌面数据库通常提供 GUI 让用户直接操作数据，但基于服务器的数据库完全通过 SQL 访问。

JDBC 包可以看作一个将 SQL 语句传递给数据库的 API。本节将简要介绍 SQL。如果你之前从未接触过 SQL，可能会觉得这些材料不够充分。如果是这样，请查阅该主题的众多学习资源之一；我们推荐 Alan Beaulieu 的 *学习 SQL*（O’Reilly, 2009）或在线书籍 *以硬核方式学习 SQL*，网址为 http://sql.learncodethehardway.org。

你可以将数据库看作一组带行和列的命名表。每列有一个 *列名*。每行包含一组相关数据。

作为本书的示例数据库，我们使用一组描述经典计算机科学书籍集合的数据库表（参见表 5.1 至表 5.4）。

**表 5.1 作者表**

| Author_ID | Name | Fname |
| --- | --- | --- |
| ALEX | Alexander | Christopher |
| BROO | Brooks | Frederick P. |
| . . . | . . . | . . . |

**表 5.2 书籍表**

| Title | ISBN | Publisher_ID | Price |
| --- | --- | --- | --- |
| 《SQL 标准指南》 | 0-201-96426-0 | 0201 | 47.95 |
| 《模式语言：城镇、建筑、施工》 | 0-19-501919-9 | 019 | 65.00 |
| . . . | . . . | . . . | . . . |

**表 5.3 书籍作者表**

| ISBN | Author_ID | Seq_No |
| --- | --- | --- |
| 0-201-96426-0 | DATE | 1 |
| 0-201-96426-0 | DARW | 2 |
| 0-19-501919-9 | ALEX | 1 |
| . . . | . . . | . . . |

**表 5.4 出版社表**

| Publisher_ID | Name | URL |
| --- | --- | --- |
| 0201 | Addison-Wesley | www.aw-bc.com |
| 0407 | John Wiley & Sons | www.wiley.com |
| . . . | . . . | . . . |

图 5.3 显示了 *Books* 表的视图。图 5.4 显示了将此表与 *Publishers* 表*联接*的结果。*Books* 表和 *Publishers* 表都包含一个出版社标识符。当我们按出版社代码联接这两个表时，会得到一个由联接表的值组成的*查询结果*。结果中的每一行包含一本书的信息，连同出版社名称和网页 URL。请注意，出版社名称和 URL 在几行中重复出现，因为我们有多本书来自同一出版社。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_311_0.png)

**图 5.3** 包含书籍的示例表

联接表的好处是避免数据库表中不必要的数据重复。例如，一个简单的数据库设计可能会将出版社名称和 URL 直接放在 *Books* 表的列中。但这样一来，数据库本身（而不仅仅是查询结果）就会有大量重复条目。如果出版社的网址发生变化，所有条目都需要更新。显然，这容易出错。在关系模型中，我们将数据分布到多个表中，以便没有信息被不必要地重复。例如，每个出版社的 URL 在出版社表中只出现一次。如果需要组合信息，则将表联接起来。

在图中，你可以看到一个用于检查和关联表的图形工具。许多供应商都有工具，通过连接列名和填写表单来以简单形式表达查询。此类工具通常称为 *按示例查询（QBE）* 工具。相比之下，使用 SQL 的查询是用文本写出的，使用 SQL 语法，例如：

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_312_0.png)

**图 5.4** 两张表联接在一起

```sql
SELECT Books.Title, Books.Publisher_ID, Books.Price, Publishers.Name, Publishers.URL
FROM Books, Publishers
WHERE Books.Publisher_ID = Publishers.Publisher_ID
```

在本节的剩余部分，你将学习如何编写此类查询。如果你已经熟悉 SQL，请跳过本节。

按照惯例，SQL 关键字用大写字母书写，虽然这不是必须的。

SELECT 语句相当灵活。你可以使用以下查询简单地选择 Books 表中的所有行：

```sql
SELECT * FROM Books
```

每个 SQL SELECT 语句都必须有 FROM 子句。它告诉数据库要查看哪些表以查找数据。

你可以选择你想要的列：

```sql
SELECT ISBN, Price, Title
FROM Books
```

你可以使用 WHERE 子句限制答案中的行：

```sql
SELECT ISBN, Price, Title
FROM Books
WHERE Price <= 29.95
```

注意“等于”比较。SQL 使用 = 和 <> 进行相等性测试，而不是 Java 编程语言中的 == 或 !=。

> **注意：** 有些数据库供应商支持使用 != 进行不等式测试。这不是标准 SQL，因此我们建议不要这样使用。

`WHERE` 子句还可以通过 `LIKE` 运算符进行模式匹配。但通配符不是通常的 `*` 和 `?`。使用 `%` 表示零个或多个字符，使用下划线表示单个字符。例如，

```sql
SELECT ISBN, Price, Title
FROM Books
WHERE Title NOT LIKE '%n_x%'
```

排除标题中包含诸如 Unix 或 Linux 等单词的书籍。

请注意，字符串用单引号括起来，而不是双引号。字符串内的单引号由一对单引号表示。例如，

```sql
SELECT Title
FROM Books
WHERE Title LIKE '%''%'
```

报告所有包含单引号的标题。

你可以从多个表中选择数据：

```sql
SELECT * FROM Books, Publishers
```

如果没有 WHERE 子句，这个查询并不是很有趣。它列出了两个表中所有行的组合。在我们的案例中，Books 有 20 行，Publishers 有 8 行，结果是一组包含 20 × 8 个条目且大量重复的行。我们确实希望约束查询，即我们只对 *匹配* 书籍与其出版社感兴趣：

```sql
SELECT * FROM Books, Publishers
WHERE Books.Publisher_ID = Publishers.Publisher_ID
```

该查询结果有 20 行，每本书一行，因为每本书在 Publisher 表中都有一个出版社。

当查询中有多个表时，同一列名可能出现在两个不同的位置。我们的例子中就发生了这种情况。Books 和 Publishers 表中都有一个名为 Publisher_ID 的列。如果可能产生歧义，则必须在每个列名前面加上其所属表的名称，例如 Books.Publisher_ID。

你也可以使用 SQL 更改数据库中的数据。例如，假设你想将所有标题中包含“C++”的书籍的当前价格降低 5.00 美元：

```sql
UPDATE Books
SET Price = Price - 5.00
WHERE Title LIKE '%C++%'
```

类似地，要删除所有 C++ 书籍，请使用 DELETE 查询：

```sql
DELETE FROM Books
WHERE Title LIKE '%C++%'
```

SQL 附带内置函数，用于计算平均值、查找列中的最大值和最小值等，我们在此不讨论。

通常，要向表中插入值，可以使用 INSERT 语句：

```sql
INSERT INTO Books
VALUES ('A Guide to the SQL Standard', '0-201-96426-0', '0201', 47.95)
```

对于插入表中的每一行，都需要单独的 INSERT 语句。

当然，在你可以查询、修改和插入数据之前，必须有地方存储数据。使用 CREATE TABLE 语句创建新表。为每一列指定名称和数据类型。例如，

```sql
CREATE TABLE Books
(
    Title CHAR(60),
    ISBN CHAR(13),
    Publisher_ID CHAR(6),
    Price DECIMAL(10,2)
)
```

表 5.5 显示了最常见的 SQL 数据类型。

在本书中，我们不讨论可以与 CREATE TABLE 语句一起使用的其他子句，例如键和约束。





**表 5.5** 常见 SQL 数据类型

| 数据类型 | 描述 |
| --- | --- |
| INTEGER 或 INT | 通常为 32 位整数 |
| SMALLINT | 通常为 16 位整数 |
| NUMERIC(*m*,*n*)、DECIMAL(*m*,*n*) 或 DEC(*m*,*n*) | 定点十进制数，共 *m* 位数字，小数点后 *n* 位数字 |
| FLOAT(*n*) | 具有 *n* 位二进制精度的浮点数 |
| REAL | 通常为 32 位浮点数 |
| DOUBLE | 通常为 64 位浮点数 |
| CHARACTER(*n*) 或 CHAR(*n*) | 长度为 *n* 的定长字符串 |
| VARCHAR(*n*) | 最大长度为 *n* 的变长字符串 |
| BOOLEAN | 布尔值 |
| DATE | 日历日期，取决于具体实现 |
| TIME | 一天中的时间，取决于具体实现 |
| TIMESTAMP | 日期和一天中的时间，取决于具体实现 |
| BLOB | 二进制大对象 |
| CLOB | 字符大对象 |

## 5.3 JDBC 配置

当然，你需要一个可获取 JDBC 驱动程序的数据库程序。有许多优秀的选择，例如 IBM DB2、Microsoft SQL Server、MySQL、Oracle 和 PostgreSQL。

你还必须创建一个供实验使用的数据库。我们假设将其命名为 `COREJAVA`。请创建一个新数据库，或者让数据库管理员创建一个具有相应权限的数据库。你需要能够在数据库中创建、更新和删除表。

如果你以前从未安装过客户端/服务器数据库，可能会发现设置数据库有些复杂——诊断失败原因可能很困难。如果你的设置无法正常工作，最好寻求专家帮助。

如果这是你第一次使用数据库，我们建议你使用 Apache Derby 数据库，可从 [http://db.apache.org/derby](http://db.apache.org/derby) 获取。

如果你的驱动程序的 JAR 文件不支持自动注册，你需要查明供应商使用的 JDBC 驱动程序类的名称。典型的驱动程序名称为

```
org.apache.derby.jdbc.ClientDriver
org.postgresql.Driver
```

有两种方法可以向 DriverManager 注册驱动程序。一种方法是在 Java 程序中加载驱动程序类。例如，

```java
Class.forName("org.postgresql.Driver"); // force loading of driver class
```

该语句会加载驱动程序类，从而执行注册驱动程序的静态初始化器。

或者，你可以设置 jdbc.drivers 属性。你可以通过命令行参数指定该属性，例如

```
java -Djdbc.drivers=org.postgresql.Driver ProgramName
```

或者，你的应用程序可以通过如下调用设置系统属性

```java
System.setProperty("jdbc.drivers", "org.postgresql.Driver");
```

你也可以提供多个驱动程序；用冒号分隔它们，例如：

```
org.postgresql.Driver:org.apache.derby.jdbc.ClientDriver
```

### 5.3.5 连接数据库

在 Java 程序中，像这样打开数据库连接：

```java
String url = "jdbc:postgresql:COREJAVA";
String username = "dbuser";
String password = "secret";
Connection conn = DriverManager.getConnection(url, username, password);
```

驱动程序管理器会遍历已注册的驱动程序，以找到一个能够使用数据库 URL 中指定子协议的驱动程序。

getConnection 方法返回一个 Connection 对象。在接下来的几节中，你将看到如何使用 Connection 对象执行 SQL 语句。

要连接数据库，你需要数据库的用户名和密码。

> **注意：** 默认情况下，Derby 允许使用任意用户名连接，并且不检查密码。会为每个用户生成一组单独的表。默认用户名为 app。

清单 5.1 中的测试程序运用了这些步骤。它从名为 `database.properties` 的文件中加载连接参数，并连接到数据库。示例代码随附的 `database.properties` 文件包含 Derby 数据库的连接信息。如果你使用不同的数据库，请将特定于你的数据库的连接信息放入该文件。以下是连接 PostgreSQL 数据库的示例：

```
jdbc.drivers=org.postgresql.Driver
jdbc.url=jdbc:postgresql:COREJAVA
jdbc.username=dbuser
jdbc.password=secret
```

连接到数据库后，测试程序会执行以下 SQL 语句：

```
CREATE TABLE Greetings (message CHAR(20))
INSERT INTO Greetings VALUES ('Hello, World!')
SELECT * FROM Greetings
```

SELECT 语句的结果会被打印出来，你应该会看到如下输出

```
Hello, World!
```

然后通过执行以下语句删除该表

```
DROP TABLE Greetings
```

要运行此测试，请如前所述启动数据库，并按如下方式启动程序

```
java -classpath .;driverJAR test.TestDb
```

（一如既往，Windows 用户需要使用 ; 而不是 : 来分隔路径元素。）

> **提示：** 调试 JDBC 相关问题的一种方法是启用 JDBC 跟踪。调用 `DriverManager.setLogWriter` 方法将跟踪消息发送到 `PrintWriter`。跟踪输出包含 JDBC 活动的详细列表。大多数 JDBC 驱动程序实现都提供了额外的跟踪机制。例如，使用 Derby 时，你可以向 JDBC URL 添加 `traceFile` 选项：`jdbc:derby://localhost:1527/COREJAVA;create=true;traceFile=trace.out`。

| API | 版本 |
|---|---|
| `java.sql.DriverManager` | 1.1 |

- `static Connection getConnection(String url, String user, String password)` 建立到给定数据库的连接，并返回一个 `Connection` 对象。

#### 清单 5.1  `test/TestDB.java`

```java
package test;

import java.nio.file.*;
import java.sql.*;
import java.io.*;
import java.util.*;

/**
 * This program tests that the database and the JDBC driver are correctly configured.
 * @version 1.03 2018-05-01
 * @author Cay Horstmann
 */
public class TestDB
{
   public static void main(String args[]) throws IOException
   {
      try
      {
         runTest();
      }
      catch (SQLException ex)
      {
         for (Throwable t : ex)
            t.printStackTrace();
      }
   }

   /**
    * Runs a test by creating a table, adding a value, showing the table contents, and
    * removing the table.
    */
   public static void runTest() throws SQLException, IOException
   {
      try (Connection conn = getConnection();
         Statement stat = conn.createStatement())
      {
         stat.executeUpdate("CREATE TABLE Greetings (Message CHAR(20))");
         stat.executeUpdate("INSERT INTO Greetings VALUES ('Hello, World!')");

         try (ResultSet result = stat.executeQuery("SELECT * FROM Greetings"))
         {
            if (result.next())
               System.out.println(result.getString(1));
         }
         stat.executeUpdate("DROP TABLE Greetings");
      }
   }

    /**
     * Gets a connection from the properties specified in the file database.properties.
     * @return the database connection
     */
    public static Connection getConnection() throws SQLException, IOException
    {
        var props = new Properties();
        try (InputStream in = Files.newInputStream(Paths.get("database.properties")))
        {
            props.load(in);
        }
        String drivers = props.getProperty("jdbc.drivers");
        if (drivers != null) System.setProperty("jdbc.drivers", drivers);
        String url = props.getProperty("jdbc.url");
        String username = props.getProperty("jdbc.username");
        String password = props.getProperty("jdbc.password");

        return DriverManager.getConnection(url, username, password);
    }
}
```

## 5.4 使用 JDBC 语句

在接下来的几节中，你将看到如何使用 JDBC Statement 执行 SQL 语句、获取结果并处理错误。然后我们会向你展示一个用于填充数据库的简单程序。

### 5.4.1 执行 SQL 语句

要执行 SQL 语句，首先创建一个 Statement 对象。要创建语句对象，请使用通过调用 DriverManager.getConnection 获得的 Connection 对象。

```
    Statement stat = conn.createStatement();
```

接下来，将要执行的语句放入一个字符串中，例如：

```
    String command = "UPDATE Books"
        + " SET Price = Price - 5.00"
        + " WHERE Title NOT LIKE \"%Introduction%\"";
```

然后，调用 Statement 接口的 executeUpdate 方法：

```
    stat.executeUpdate(command);
```

executeUpdate 方法返回受 SQL 语句影响的行数；对于不返回行数的语句，则返回零。对于


例如，前一个示例中对 `executeUpdate` 的调用返回价格下调了 $5.00 的行数。

`executeUpdate` 方法可以执行诸如 `INSERT`、`UPDATE` 和 `DELETE` 之类的操作，也可以执行诸如 `CREATE TABLE` 和 `DROP TABLE` 之类的数据定义语句。但是，需要改用 `executeQuery` 方法来执行 `SELECT` 查询。此外还有一个通用的 `execute` 语句，可用于执行任意 SQL 语句。它通常仅用于用户交互提供的查询。

执行查询时，你关心的是结果。`executeQuery` 方法返回一个 `ResultSet` 类型的对象，你可以用它逐行遍历结果。

```
ResultSet rs = stat.executeQuery("SELECT * FROM Books");
```

分析结果集的基本循环如下所示：

```
while (rs.next())
{
    *look at a row of the result set*
}
```

> **注意：** `ResultSet` 接口的迭代协议与 `java.util.Iterator` 接口的迭代协议有细微差别。在这里，迭代器被初始化为指向第一行之前的位置。必须调用一次 `next` 方法将迭代器移动到第一行。此外，没有 `hasNext` 方法；应持续调用 `next`，直到它返回 false。

结果集中行的顺序完全是任意的。除非使用 `ORDER BY` 子句专门对结果排序，否则不应赋予行顺序任何意义。

检查单独一行时，你会想了解各字段的内容。大量访问器方法可为你提供这些信息。

```
String isbn = rs.getString(1);
double price = rs.getDouble("Price");
```

有适用于各种类型的访问器，例如 `getString` 和 `getDouble`。每个访问器都有两种形式：一种接受数值参数，另一种接受字符串参数。提供数值参数时，你引用的是具有该编号的列。例如，`rs.getString(1)` 返回当前行中第一列的值。

> **注意：** 与数组索引不同，数据库列号从 1 开始。

提供字符串参数时，你引用的是结果集中具有该名称的列。例如，`rs.getDouble("Price")` 返回标签为 Price 的列的值。使用数值参数效率稍高，但字符串参数使代码更易于阅读和维护。

当方法类型与列类型不匹配时，每个 get 方法都会进行合理的类型转换。例如，调用 `rs.getString("Price")` 会将 Price 列的浮点值转换为字符串。

| java.sql.Connection 1.1 | |
|---|---|
| `Statement createStatement()` | 创建一个 Statement 对象，可用于执行不带参数的 SQL 查询和更新。 |
| `void close()` | 立即关闭当前连接及其创建的 JDBC 资源。 |

| java.sql.Statement 1.1 | |
|---|---|
| `ResultSet executeQuery(String sqlQuery)` | 执行字符串中给定的 SQL 语句，并返回一个 ResultSet 对象以查看查询结果。 |
| `int executeUpdate(String sqlStatement)`<br>`long executeLargeUpdate(String sqlStatement)` 8 | 执行字符串指定的 SQL INSERT、UPDATE 或 DELETE 语句。还执行数据定义语言（DDL）语句，例如 CREATE TABLE。返回受影响的行数；对于没有更新计数的语句，返回 0。 |
| `boolean execute(String sqlStatement)` | 执行字符串指定的 SQL 语句。可能会产生多个结果集和更新计数。如果第一个结果是结果集，则返回 true，否则返回 false。调用 getResultSet 或 getUpdateCount 获取第一个结果。有关处理多个结果的详细信息，请参见第 321 页的 5.5.4 节“多个结果”。 |

#### java.sql.Statement 1.1（续）

- `ResultSet getResultSet()`  
  返回前一条查询语句的结果集；如果前一条语句没有结果集，则返回 null。每条已执行的语句只调用此方法一次。
- `int getUpdateCount()`
- `long getLargeUpdateCount()` 8  
  返回前一条更新语句影响的行数；如果前一条语句是没有更新计数的语句，则返回 -1。每条已执行的语句只调用此方法一次。
- `void close()`  
  关闭此语句对象及其关联的结果集。
- `boolean isClosed()` 6  
  如果此语句已关闭，则返回 true。
- `void closeOnCompletion()` 7  
  使此语句在其所有结果集都关闭后自动关闭。

#### java.sql.ResultSet 1.1

- `boolean next()`  
  使结果集中的当前行向前移动一行。最后一行之后返回 false。注意，必须调用此方法才能前进到第一行。
- `Xxx getXxx(int columnNumber)`
- `Xxx getXxx(String columnLabel)`  
  （Xxx 是诸如 int、double、String、Date 等类型。）
- `<T> T getObject(int columnIndex, Class<T> type)` 7
- `<T> T getObject(String columnLabel, Class<T> type)` 7
- `void updateObject(int columnIndex, Object x, SQLType targetSqlType)` 8
- `void updateObject(String columnLabel, Object x, SQLType targetSqlType)` 8  
  返回或更新具有给定列索引或标签的列的值，并将其转换为指定类型。列标签是 SQL AS 子句中指定的标签；如果未使用 AS，则为列名。
- `int findColumn(String columnName)`  
  给出与列名关联的列索引。

| java.sql.ResultSet 1.1（续） | |
|---|---|
| `void close()` | 立即关闭当前结果集。 |
| `boolean isClosed()` 6 | 如果此结果集已关闭，则返回 true。 |

### 5.4.2 管理连接、语句和结果集

每个 `Connection` 对象可以创建一个或多个 `Statement` 对象。你可以将同一个 `Statement` 对象用于多个不相关的命令和查询。但是，一个 `Statement` *至多有一个*打开的结果集。如果发出多个查询并同时分析其结果，则需要多个 `Statement` 对象。

但请注意，每个连接的语句数量是有限制的。使用 `DatabaseMetaData` 接口的 `getMaxStatements` 方法查明 JDBC 驱动程序支持的并发打开语句数。

在实践中，可能不必为多个并发结果集费心。如果这些结果集相关，应能发出一个组合查询并分析单个结果。让数据库合并查询比让 Java 程序遍历多个结果集高效得多。

在发出新查询或对 `Statement` 对象执行更新之前，务必完成对任何结果集的处理。先前查询的结果集会自动关闭。

使用完 `ResultSet`、`Statement` 或 `Connection` 后，最好立即调用 `close` 方法。这些对象使用大型数据结构，会占用数据库服务器的有限资源。

`Statement` 对象的 `close` 方法会关闭任何关联的结果集。同样，`Connection` 类的 `close` 方法会关闭该连接的所有语句。

反之，可以在 `Statement` 上调用 `closeOnCompletion` 方法，这样一旦其所有结果集都已关闭，它就会自动关闭。

如果连接是短生命周期的，则不必担心关闭语句和结果集。为确保连接对象不可能保持打开状态，请使用 try-with-resources 语句：

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_327_0.png)

**图 5.5** SQL 异常类型

当从数据库读取的数据被意外截断时，会使用 SQLWarning 的 DataTruncation 子类。如果数据截断发生在更新语句中，则会抛出 DataTruncation 异常。

#### java.sql.SQLException 1.1

- `SQLException getNextException()`  
  获取链接到此异常的下一个 SQL 异常；在链末尾返回 `null`。
- `Iterator<Throwable> iterator()` 6  
  获取一个迭代器，用于生成链式 SQL 异常及其原因。
- `String getSQLState()`  
  获取“SQL 状态”——一种标准化错误代码。
- `int getErrorCode()`  
  获取供应商特定的错误代码。



| API | 版本 |
|---|---|
| `java.sql.SQLWarning` | 1.1 |

- `SQLWarning getNextWarning()`  
  返回链接到当前警告的下一个警告；如果已到警告链末尾，则返回 null。

| API | 版本 |
|---|---|
| `java.sql.Connection` | 1.1 |
| `java.sql.Statement` | 1.1 |
| `java.sql.ResultSet` | 1.1 |

- `SQLWarning getWarnings()`  
  返回待处理警告中的第一个；如果没有待处理的警告，则返回 null。

| API | 版本 |
|---|---|
| `java.sql.DataTruncation` | 1.1 |

- `boolean getParameter()`  
  如果数据截断适用于参数，则返回 true；如果适用于列，则返回 false。
- `int getIndex()`  
  返回被截断的参数或列的索引。
- `int getDataSize()`  
  返回本应传输的字节数；如果该值未知，则返回 -1。
- `int getTransferSize()`  
  返回实际传输的字节数；如果该值未知，则返回 -1。

### 5.4.4 填充数据库

我们现在准备编写第一个真正的 JDBC 程序。当然，尝试前面讨论过的一些复杂查询会很好，但我们有一个问题：目前数据库中没有数据。我们需要填充数据库，而一种简单的方法是使用一组 SQL 指令来创建表并向其中插入数据。大多数数据库程序可以处理来自文本文件的一组 SQL 指令，但在语句终止符和其他语法问题方面存在一些令人烦恼的差异。

因此，我们将在一个简单的程序中使用 JDBC，该程序读取包含 SQL 指令的文件（每行一条指令）并执行它们。

具体来说，该程序从文本文件中读取如下格式的数据

```sql
CREATE TABLE Publishers (Publisher_Id CHAR(6), Name CHAR(30), URL CHAR(80));
INSERT INTO Publishers VALUES ('Q201', 'Addison-Wesley', 'www.aw-bc.com');
INSERT INTO Publishers VALUES ('Q471', 'John Wiley & Sons', 'www.wiley.com');
. . . .
```

代码清单 5.2 包含该程序的代码，该程序读取包含 SQL 语句的文件并执行它们。你不必通读代码；只需使用该程序来填充数据库，并运行本章其余部分的示例。

确保数据库服务器正在运行，然后按如下方式运行程序：

```bash
java -classpath driverPath:. exec.ExecSQL Books.sql
java -classpath driverPath:. exec.ExecSQL Authors.sql
java -classpath driverPath:. exec.ExecSQL Publishers.sql
java -classpath driverPath:. exec.ExecSQL BooksAuthors.sql
```

在运行程序之前，请检查文件 database.properties 是否已针对你的环境正确设置（参见第 296 页的 5.3.5 节“连接到数据库”）。

> **注意：** 你的数据库可能还提供了一个直接读取 SQL 文件的工具。例如，使用 Derby 时，可以运行
>
> `java -jar derby/lib/derbyrun.jar ij -p ij.properties Books.sql`
>
> （ij.properties 文件在第 294 页的 5.3.3 节“启动数据库”中进行了说明。）
>
> 在 ExecSQL 命令的数据格式中，我们允许在每行末尾使用可选的分号，因为大多数数据库工具都期望这种格式。

以下步骤简要描述了 ExecSQL 程序：

- 1. 连接到数据库。getConnection 方法读取文件 database.properties 中的属性，并将 jdbc.drivers 属性添加到系统属性中。驱动程序管理器使用 jdbc.drivers 属性来加载相应的数据库驱动程序。getConnection 方法使用 jdbc.url、jdbc.username 和 jdbc.password 属性来打开数据库连接。
- 2. 打开包含 SQL 语句的文件。如果未提供文件名，则提示用户在控制台上输入语句。
- 3. 使用通用的 execute 方法执行每条语句。如果它返回 true，则该语句有一个结果集。我们为本书数据库提供的四个 SQL 文件都以 `SELECT *` 语句结尾，以便你可以看到数据已成功插入。
- 4. 如果有结果集，则打印出结果。由于这是一个通用结果集，我们需要使用元数据来查明结果有多少列。有关更多信息，请参见第 334 页的 5.8 节“元数据”。
- 5. 如果出现任何 SQL 异常，则打印该异常以及其中可能包含的任何链式异常。
- 6. 关闭与数据库的连接。

代码清单 5.2 显示了该程序的代码。

#### **代码清单 5.2** `exec/ExecSQL.java`

```java
package exec;

import java.io.*;
import java.nio.charset.*;
import java.nio.file.*;
import java.util.*;
import java.sql.*;

/**
 * Executes all SQL statements in a file. Call this program as <br>
 * java -classpath driverPath:. ExecSQL commandFile
 *
 * @version 1.33 2018-05-01
 * @author Cay Horstmann
 */
class ExecSQL
{
   public static void main(String args[]) throws IOException
   {
      try (Scanner in = args.length == 0 ? new Scanner(System.in)
            : new Scanner(Paths.get(args[0]), StandardCharsets.UTF_8))
      {
         try (Connection conn = getConnection();
               Statement stat = conn.createStatement())
         {
            while (true)
            {
               if (args.length == 0) System.out.println("Enter command or EXIT to exit:");

               if (!in.hasNextLine()) return;

               String line = in.nextLine().trim();
               if (line.equalsIgnoreCase("EXIT")) return;
               if (line.endsWith(";")) // remove trailing semicolon
                  line = line.substring(0, line.length() - 1);
               try
               {
                  boolean isResult = stat.execute(line);
                  if (isResult)
                  {
                     try (ResultSet rs = stat.getResultSet())
                     {
                        showResultSet(rs);
                     }
                  }
                  else
                  {
                     int updateCount = stat.getUpdateCount();
                     System.out.println(updateCount + " rows updated");
                  }
               }
               catch (SQLException e)
               {
                  for (Throwable t : e)
                     t.printStackTrace();
               }
            }
         }
         catch (SQLException e)
         {
            for (Throwable t : e)
               t.printStackTrace();
         }
      }
   }

   /**
    * Gets a connection from the properties specified in the file database.properties
    * @return the database connection
    */
   public static Connection getConnection() throws SQLException, IOException
   {
      var props = new Properties();
      try (InputStream in = Files.newInputStream(Paths.get("database.properties")))
      {
         props.load(in);
      }
      String drivers = props.getProperty("jdbc.drivers");
      if (drivers != null) System.setProperty("jdbc.drivers", drivers);

      String url = props.getProperty("jdbc.url");
      String username = props.getProperty("jdbc.username");
      String password = props.getProperty("jdbc.password");

      return DriverManager.getConnection(url, username, password);
   }

   /**
    * Prints a result set.
    * @param result the result set to be printed
    */
   public static void showResultSet(ResultSet result) throws SQLException
   {
      ResultSetMetaData metaData = result.getMetaData();
      int columnCount = metaData.getColumnCount();

      for (int i = 1; i <= columnCount; i++)
      {
         if (i > 1) System.out.print(", ");
         System.out.print(metaData.getColumnLabel(i));
      }
      System.out.println();

      while (result.next())
      {
         for (int i = 1; i <= columnCount; i++)
         {
            if (i > 1) System.out.print(", ");
            System.out.print(result.getString(i));
         }
         System.out.println();
      }
   }
}
```

## 5.5 查询执行

在本节中，我们编写一个针对 COREJAVA 数据库执行查询的程序。要使该程序正常工作，你必须拥有一个已按上一节所述填充了表的 COREJAVA 数据库。

查询数据库时，你可以选择作者和出版商，或者将其中任意一个保留为 Any。

你还可以更改数据库中的数据。选择一个出版商并输入一个金额。该出版商的所有价格都会按你输入的金额进行调整，并且程序会显示更改了多少行。更改价格后，你可能想运行一个查询来验证新价格。




### 5.5.1 预编译语句

本程序中，我们使用一个新特性——*预编译语句*。考虑下面这条 SQL 查询，它查找某个特定出版商出版的所有图书，而不考虑作者：

```sql
SELECT Books.Price, Books.Title
FROM Books, Publishers
WHERE Books.Publisher_Id = Publishers.Publisher_Id
AND Publishers.Name = the name from the list box
```

每次用户发起这样的查询时，不必都构建一条单独的查询语句；我们可以准备一条带宿主变量的查询，并多次使用它，每次为该变量填入不同的字符串。这种技术能提升性能。每当数据库执行查询时，它首先会计算如何高效执行的策略。通过预编译并复用查询，可以确保规划步骤只执行一次。

预编译查询中的每个宿主变量都用 ? 表示。如果有多个变量，在设置值时必须记录各个 ? 的位置。例如，我们的预编译查询变成

```java
String publisherQuery
    = "SELECT Books.Price, Books.Title"
    + " FROM Books, Publishers"
    + " WHERE Books.Publisher_Id = Publishers.Publisher_Id AND Publishers.Name = ?";
PreparedStatement stat = conn.prepareStatement(publisherQuery);
```

在执行预编译语句之前，必须用 set 方法将宿主变量绑定到实际值。与 ResultSet 接口的 get 方法一样，针对各种类型也有不同的 set 方法。这里，我们要把一个字符串设置为出版商名称：

```java
stat.setString(1, publisher);
```

第一个参数是要设置的宿主变量的位置编号。位置 1 表示第一个 ?。第二个参数是要赋给该宿主变量的值。

如果复用已经执行过的预编译查询，所有宿主变量都会保持绑定状态，除非用 set 方法更改它们或调用 clearParameters 方法。这意味着只需对从一次查询到下一次查询会发生变化的那些宿主变量调用 setXxx 方法。

所有变量都绑定值之后，就可以执行预编译语句：

```java
ResultSet rs = stat.executeQuery();
```

> **提示：** 通过拼接字符串手动构建查询既繁琐又可能危险。你必须担心引号之类的特殊字符——而且，如果你的查询涉及用户输入，还必须防范注入攻击。因此，只要查询涉及变量，就应使用预编译语句。

价格更新功能通过一条 UPDATE 语句实现。注意我们调用的是 executeUpdate，而不是 executeQuery，因为 UPDATE 语句不返回结果集。executeUpdate 的返回值是更改的行数。

```java
int r = stat.executeUpdate();
System.out.println(r + " rows updated");
```

> **注意：** 关联的 Connection 对象关闭后，PreparedStatement 对象就会失效。不过，许多数据库会自动缓存预编译语句。如果同一条查询被预编译两次，数据库只会复用查询策略。因此，不必担心调用 prepareStatement 的开销。

下面的列表简要说明示例程序的结构：

- 作者和出版商数组列表通过运行两个查询来填充，这两个查询返回数据库中所有作者名和出版商名。

- 涉及作者的查询比较复杂。一本书可以有多个作者，因此 BooksAuthors 表存储作者与图书之间的对应关系。例如，ISBN 为 0-201-96426-0 的图书有两个作者，代码分别为 DATE 和 DARW。

  ```
  0-201-96426-0, DATE, 1
  0-201-96426-0, DARW, 2
  ```

  以此表明这一事实。第三列列出作者的顺序。（我们不能只使用表中行的位置。关系表中没有固定的行顺序。）因此，查询必须连接 Books、BooksAuthors 和 Authors 表，以便将作者名与用户选择的作者名进行比较。

  ```sql
  SELECT Books.Price, Books.Title FROM Books, BooksAuthors, Authors, Publishers
  WHERE Authors.Author_Id = BooksAuthors.Author_Id AND BooksAuthors.ISBN = Books.ISBN
  AND Books.Publisher_Id = Publishers.Publisher_Id AND Authors.Name = ?
  AND Publishers.Name = ?
  ```

> **提示：** 有些 Java 程序员会避免使用这样复杂的 SQL 语句。一种出奇常见但效率很低的变通办法是编写大量 Java 代码来遍历多个结果集。但是，数据库在执行查询代码方面比 Java 程序强得多——这是数据库的核心能力。一条经验法则：如果能在 SQL 中完成，就不要用 Java 来做。

- `changePrices` 方法执行一条 `UPDATE` 语句。注意，`UPDATE` 语句的 `WHERE` 子句需要出版商的*代码*，而我们只知道出版商的*名称*。这个问题用嵌套子查询解决：

  ```sql
  UPDATE Books
  SET Price = Price + ?
  WHERE Books.Publisher_Id = (SELECT Publisher_Id FROM Publishers WHERE Name = ?)
  ```

清单 5.3 是完整的程序代码。

#### **清单 5.3** query/QueryTest.java

```java
 1 package query;
 2
 3 import java.io.*;
 4 import java.nio.file.*;
 5 import java.sql.*;
 6 import java.util.*;
 7
 8 /**
 9  * This program demonstrates several complex database queries.
10  * @version 1.31 2018-05-01
11  * @author Cay Horstmann
12  */
13 public class QueryTest
14 {
15    private static final String allQuery = "SELECT Books.Price, Books.Title FROM Books";
16
17    private static final String authorPublisherQuery = "SELECT Books.Price, Books.Title"
18       + " FROM Books, BooksAuthors, Authors, Publishers"
19       + " WHERE Authors.Author_Id = BooksAuthors.Author_Id AND BooksAuthors.ISBN = Books.ISBN"
20       + " AND Books.Publisher_Id = Publishers.Publisher_Id AND Authors.Name = ?"
21       + " AND Publishers.Name = ?";
22
23    private static final String authorQuery
24       = "SELECT Books.Price, Books.Title FROM Books, BooksAuthors, Authors"
25       + " WHERE Authors.Author_Id = BooksAuthors.Author_Id"
26       + " AND BooksAuthors.ISBN = Books.ISBN"
27       + " AND Authors.Name = ?";

    private static final String publisherQuery
        = "SELECT Books.Price, Books.Title FROM Books, Publishers"
        + " WHERE Books.Publisher_Id = Publishers.Publisher_Id AND Publishers.Name = ?";

    private static final String priceUpdate = "UPDATE Books SET Price = Price + ?"
        + " WHERE Books.Publisher_Id = (SELECT Publisher_Id FROM Publishers WHERE Name = ?)";

    private static Scanner in;
    private static ArrayList<String> authors = new ArrayList<>();
    private static ArrayList<String> publishers = new ArrayList<>();

    public static void main(String[] args) throws IOException
    {
        try (Connection conn = getConnection())
        {
            in = new Scanner(System.in);
            authors.add("Any");
            publishers.add("Any");
            try (Statement stat = conn.createStatement())
            {
                // Fill the authors array list
                var query = "SELECT Name FROM Authors";
                try (ResultSet rs = stat.executeQuery(query))
                {
                    while (rs.next())
                        authors.add(rs.getString(1));
                }

                // Fill the publishers array list
                query = "SELECT Name FROM Publishers";
                try (ResultSet rs = stat.executeQuery(query))
                {
                    while (rs.next())
                        publishers.add(rs.getString(1));
                }
            }
            var done = false;
            while (!done)
            {
                System.out.print("?Query C)hange prices E)xit: ");
                String input = in.next().toUpperCase();
                if (input.equals("Q"))
                    executeQuery(conn);
                else if (input.equals("C"))
                    changePrices(conn);
                else
                    done = true;
77    }
78    catch (SQLException e)
79    {
80        for (Throwable t : e)
81            System.out.println(t.getMessage());
82    }
83 }
84
85 /**
86  * Executes the selected query.
87  * @param conn the database connection
88  */
89 private static void executeQuery(Connection conn) throws SQLException
90 {
91     String author = select("Authors:", authors);
92     String publisher = select("Publishers:", publishers);
93     PreparedStatement stat;
94     if (!author.equals("Any") && !publisher.equals("Any"))
95     {
96         stat = conn.prepareStatement(authorPublisherQuery);
97         stat.setString(1, author);
98         stat.setString(2, publisher);
99     }
100    else if (!author.equals("Any") && publisher.equals("Any"))
101    {
102        stat = conn.prepareStatement(authorQuery);
103        stat.setString(1, author);
104    }
105    else if (author.equals("Any") && !publisher.equals("Any"))
106    {
107        stat = conn.prepareStatement(publisherQuery);
108        stat.setString(1, publisher);
109    }
110    else
111        stat = conn.prepareStatement(allQuery);
112
113    try (ResultSet rs = stat.executeQuery())
114    {
115        while (rs.next())
116            System.out.println(rs.getString(1) + ", " + rs.getString(2));
117    }
118 }
119
120 /**
121  * Executes an update statement to change prices.
122  * @param conn the database connection
 */
```



#### 清单 5.3 *（续）*

```java
public static void changePrices(Connection conn) throws SQLException
{
   String publisher = select("Publishers: ", publishers.subList(1, publishers.size()));
   System.out.print("Change prices by: ");
   double priceChange = in.nextDouble();
   PreparedStatement stat = conn.prepareStatement(priceUpdate);
   stat.setDouble(1, priceChange);
   stat.setString(2, publisher);
   int r = stat.executeUpdate();
   System.out.println(r + " records updated.");
}

/**
 * Asks the user to select a string.
 * @param prompt the prompt to display
 * @param options the options from which the user can choose
 * @return the option that the user chose
 */
public static String select(String prompt, List<String> options)
{
   while (true)
   {
      System.out.println(prompt);
      for (int i = 0; i < options.size(); i++)
         System.out.printf("%2d) %s%n", i + 1, options.get(i));
      int sel = in.nextInt();
      if (sel > 0 && sel <= options.size())
         return options.get(sel - 1);
   }
}

/**
 * Gets a connection from the properties specified in the file database.properties.
 * @return the database connection
 */
public static Connection getConnection() throws SQLException, IOException
{
   var props = new Properties();
   try (InputStream in = Files.newInputStream(Paths.get("database.properties")))
   {
      props.load(in);
   }

   String drivers = props.getProperty("jdbc.drivers");
   if (drivers != null) System.setProperty("jdbc.drivers", drivers);
```

```java
PreparedStatement stat = conn.prepareStatement("SELECT Cover FROM BookCovers WHERE ISBN=?");
...
stat.setInt(1, isbn);
try (ResultSet result = stat.executeQuery())
{
    if (result.next())
    {
        Blob coverBlob = result.getBlob(1);
        Image coverImage = ImageIO.read(coverBlob.getBinaryStream());
    }
}
```

类似地，如果你检索到一个 Clob 对象，可以通过调用 `getSubString` 或 `getCharacterStream` 方法获取字符数据。

要将 LOB 放入数据库，请在 Connection 对象上调用 `createBlob` 或 `createClob`，获取该 LOB 的输出流或 writer，写入数据，然后将对象存储在数据库中。例如，下面是如何存储图像：

```java
Blob coverBlob = connection.createBlob();
int offset = 0;
OutputStream out = coverBlob.setBinaryStream(offset);
ImageIO.write(coverImage, "PNG", out);
PreparedStatement stat = conn.prepareStatement("INSERT INTO Cover VALUES (?, ?)");
stat.setInt(1, isbn);
stat.setBlob(2, coverBlob);
stat.executeUpdate();
```

| 类/方法 | 版本 |
| --- | --- |
| `java.sql.ResultSet` | 1.1 |
| `Blob getBlob(int columnIndex)` | 1.2 |
| `Blob getBlob(String columnLabel)` | 1.2 |
| `Clob getClob(int columnIndex)` | 1.2 |
| `Clob getClob(String columnLabel)` | 1.2 |

获取给定列上的 BLOB 或 CLOB。

| 类/方法 | 版本 | 描述 |
| --- | --- | --- |
| `java.sql.Blob` | 1.2 | |
| `long length()` | | 获取此 BLOB 的长度。 |
| `byte[] getBytes(long startPosition, long length)` | | 获取此 BLOB 中给定范围内的数据。 |

- 调用存储过程
- 外连接
- LIKE 子句中的转义字符

日期和时间字面量在不同数据库之间差异很大。要嵌入日期或时间字面量，请使用 ISO 8601 格式指定值（www.cl.cam.ac.uk/~nkj25/iso-time.html）。驱动程序随后会将其转换为原生格式。对于 DATE、TIME 或 TIMESTAMP 值，分别使用 d、t、ts：

```text
{d '2008-01-24'}
{t '23:59:59'}
{ts '2008-01-24 23:59:59.999'}
```

标量函数是返回单个值的函数。许多函数在数据库中都被广泛支持，但名称各不相同。JDBC 规范提供了标准名称，并将它们转换为数据库特定的名称。要调用函数，请像这样嵌入标准函数名和参数：

```text
{fn left(?, 20)}
{fn user()}
```

你可以在 JDBC 规范中找到受支持的函数名的完整列表。

存储过程是用数据库专用语言编写的、在数据库中执行的过程。要调用存储过程，请使用 call 转义语法。如果过程没有参数，则无需提供括号。使用 = 捕获返回值：

```text
{call PROC1(?, ?)}
{call PROC2}
{call ? = PROC3(?)}
```

两个表的外连接并不要求每个表中的行按照连接条件相匹配。例如，查询

```sql
SELECT * FROM {oj Books LEFT OUTER JOIN Publishers
ON Books.Publisher_Id = Publishers.Publisher_Id}
```

会返回那些在 Publishers 表中 Publisher_Id 没有匹配项的书籍，并用 NULL 值表示不存在匹配。要包含没有匹配书籍的出版商，你需要使用 RIGHT OUTER JOIN；要同时返回两边，则需要使用 FULL OUTER JOIN。之所以需要转义语法，是因为并非所有数据库都使用这些连接的标准表示法。

最后，在 `LIKE` 子句中，`_` 和 `%` 字符具有特殊含义——分别匹配单个字符或一个字符序列。没有标准方法可以按字面意义使用它们。如果你想匹配所有包含 `_` 的字符串，可以使用以下结构：

```text
. . . WHERE ? LIKE %!_% {escape '!'}
```

这里我们将 `!` 定义为转义字符。组合 `!_` 表示一个字面下划线。

### 5.5.4 多个结果

一个查询有可能返回多个结果。这种情况可能发生在执行存储过程时，或者数据库允许在单个查询中提交多条 SELECT 语句时。下面介绍如何检索所有结果集：

1. 使用 `execute` 方法执行 SQL 语句。
2. 检索第一个结果或更新计数。
3. 重复调用 `getMoreResults` 方法以转到下一个结果集。
4. 当没有更多结果集或更新计数时，结束。

如果链中的下一项是结果集，则 `execute` 和 `getMoreResults` 方法返回 true。如果链中的下一项不是更新计数，则 `getUpdateCount` 方法返回 -1。

以下循环遍历所有结果：

```java
boolean isResult = stat.execute(command);
boolean done = false;
while (!done)
{
    if (isResult)
    {
        ResultSet result = stat.getResultSet();
        do something with result
    }
    else
    {
        int updateCount = stat.getUpdateCount();
        if (updateCount >= 0)
            do something with updateCount
        else
            done = true;
    }
    if (!done) isResult = stat.getMoreResults();
}
```

| 类/方法 | 版本 |
| --- | --- |
| `java.sql.Statement` | 1.1 |
| `boolean getMoreResults()` | |
| `boolean getMoreResults(int current)` | 6 |

获取此语句的下一个结果。current 参数为 `CLOSE_CURRENT_RESULT`（默认）、`KEEP_CURRENT_RESULT` 或 `CLOSE_ALL_RESULTS` 之一。如果下一个结果存在且是结果集，则返回 true。

### 5.5.5 检索自动生成的键

大多数数据库都支持某种自动为数据库中的行编号的机制。遗憾的是，不同供应商的机制差异很大。这些自动编号通常用作主键。虽然 JDBC 没有提供与供应商无关的生成键的解决方案，但它确实提供了一种高效检索这些键的方法。当你向表中插入新行并自动生成键时，可以使用以下代码检索它：

```java
stat.executeUpdate(insertStatement, Statement.RETURN_GENERATED_KEYS);
ResultSet rs = stat.getGeneratedKeys();
if (rs.next())
{
    int key = rs.getInt(1);
    . . .
}
```

| 类/方法 | 版本 |
| --- | --- |
| `java.sql.Statement` | 1.1 |
| `boolean execute(String statement, int autogenerated)` | 1.4 |
| `int executeUpdate(String statement, int autogenerated)` | 1.4 |

执行给定的 SQL 语句，如前所述。如果 autogenerated 设置为 `Statement.RETURN_GENERATED_KEYS`，并且该语句是 INSERT 语句，则第一列包含自动生成的键。

## 5.6 可滚动和可更新的结果集

如你所见，`ResultSet` 接口的 `next` 方法会遍历结果集中的行。对于需要分析数据的程序来说，这当然足够了。然而，考虑一下显示表或查询结果的可视化数据展示（例如图 5.4）。你通常希望用户能够在结果集中前后移动。在可滚动的结果集中，你可以前后移动，甚至可以跳转到任何位置。




此外，一旦用户看到显示的结果集内容，他们可能就会想编辑它。在*可更新的*结果集中，你可以通过编程方式更新条目，以便数据库自动更新。我们将在以下各节讨论这些能力。

### 5.6.1 可滚动结果集

默认情况下，结果集不可滚动也不可更新。要从查询中获得可滚动结果集，必须用以下方法获取一个不同的 `Statement` 对象：

```
Statement stat = conn.createStatement(type, concurrency);
```

对于预编译语句，使用以下调用：

```
PreparedStatement stat = con.prepareStatement(command, type, concurrency);
```

type 和 concurrency 的可能值列在表 5.6 和表 5.7 中。你有以下选择：

- 你希望结果集可滚动吗？如果不需要，请使用 `ResultSet.TYPE_FORWARD_ONLY`。
- 如果结果集可滚动，你希望它反映生成该结果集的查询之后数据库中发生的更改吗？（在我们的讨论中，我们假定可滚动结果集使用 `ResultSet.TYPE_SCROLL_INSENSITIVE` 设置。这假定结果集不会“感知”查询执行后发生的数据库更改。）
- 你希望能够通过编辑结果集来更新数据库吗？（详情见下一节。）

表 5.6 ResultSet 类型值

| 值 | 说明 |
|---|---|
| TYPE_FORWARD_ONLY | 结果集不可滚动（默认）。 |
| TYPE_SCROLL_INSENSITIVE | 结果集可滚动，但对数据库更改不敏感。 |
| TYPE_SCROLL_SENSITIVE | 结果集可滚动，且对数据库更改敏感。 |

表 5.7 ResultSet 并发值

| 值 | 说明 |
|---|---|
| CONCUR_READ_ONLY | 结果集不能用于更新数据库（默认）。 |
| CONCUR_UPDATABLE | 结果集可用于更新数据库。 |

例如，如果你只想能够滚动浏览结果集，但不想编辑其数据，请使用：

```
Statement stat = conn.createStatement(
    ResultSet.TYPE_SCROLL_INSENSITIVE, ResultSet.CONCUR_READ_ONLY);
```

通过调用 `ResultSet rs = stat.executeQuery(query);` 返回的所有结果集现在都是可滚动的。可滚动结果集有一个指示当前位置的游标。

> **注意：** 并非所有数据库驱动程序都支持可滚动或可更新结果集。（`DatabaseMetaData` 接口的 `supportsResultSetType` 和 `supportsResultSetConcurrency` 方法会告诉你，某个特定数据库使用某个特定驱动程序支持哪些类型和并发模式。）即使数据库支持所有结果集模式，某个特定查询也可能无法生成具有你请求的所有属性的结果集。（例如，复杂查询的结果集可能不可更新。）在这种情况下，`executeQuery` 方法会返回一个能力较弱的结果集，并向连接对象添加一个 `SQLWarning`。（第 304 页的 5.4.3 节“分析 SQL 异常”展示了如何获取该警告。）或者，你可以使用 `ResultSet` 接口的 `getType` 和 `getConcurrency` 方法来确定结果集实际具有哪种模式。如果你不检查结果集的能力，并执行不支持的操作，例如在不可滚动结果集上调用 `previous`，该操作将抛出 `SQLException`。

滚动非常简单。使用 `if (rs.previous()) { . . .; }` 向后滚动。如果游标位于实际行上，该方法返回 true；如果现在位于第一行之前，则返回 false。

你可以通过调用 `rs.relative(n);` 将游标向后或向前移动任意行数。如果 n 为正，游标向前移动；如果 n 为负，则向后移动；如果 n 为零，则该调用没有效果。如果你试图将游标移动到当前行集之外，它将根据 n 的符号被设置为指向最后一行之后或第一行之前。然后，该方法返回 false，且游标不移动。如果游标位于实际行上，该方法返回 true。

或者，可以将游标设置到特定行号：

```
rs.absolute(n);
```

要获取当前行号，请调用：

```
int currentRow = rs.getRow();
```

结果集中的第一行编号为 1。如果返回值为 0，则游标当前不在某一行上——它要么位于第一行之前，要么位于最后一行之后。

便捷方法 `first`、`last`、`beforeFirst` 和 `afterLast` 将游标移动到第一行、最后一行、第一行之前或最后一行之后的位置。

最后，方法 `isFirst`、`isLast`、`isBeforeFirst` 和 `isAfterLast` 测试游标是否处于这些特殊位置之一。

使用可滚动结果集非常简单。缓存查询数据的繁重工作由数据库驱动程序在幕后完成。

### 5.6.2 可更新结果集

如果你想编辑结果集中的数据，并让更改自动反映到数据库中，请创建可更新结果集。可更新结果集不必是可滚动的，但如果你将数据呈现给用户进行编辑，通常也希望允许滚动。

要获得可更新结果集，请按如下方式创建语句：

```java
Statement stat = conn.createStatement(
   ResultSet.TYPE_SCROLL_INSENSITIVE, ResultSet.CONCUR_UPDATABLE);
```

这样，通过调用 `executeQuery` 返回的结果集就是可更新的。

> **注意：** 并非所有查询都返回可更新结果集。如果你的查询是涉及多个表的连接，结果可能不可更新。但是，如果你的查询只涉及单个表，或者通过主键连接多个表，则应当预期结果集是可更新的。调用 `ResultSet` 接口的 `getConcurrency` 方法以确认。

例如，假设你想提高某些书的价格，但没有简单的条件来发出 `UPDATE` 语句。然后，可以遍历所有图书，并根据任意条件更新价格。

```java
String query = "SELECT * FROM Books";
ResultSet rs = stat.executeQuery(query);
```

```java
while (rs.next())
{
    if (...) 
    {
        double increase = ...;
        double price = rs.getDouble("Price");
        rs.updateDouble("Price", price + increase);
        rs.updateRow(); // make sure to call updateRow after updating fields
    }
}
```

对于与 SQL 类型对应的所有数据类型，都有 updateXxx 方法，例如 updateDouble、updateString 等；指定列的名称或编号（与 getXxx 方法一样），然后指定该字段的新值。

> **注意：** 如果使用第一个参数为列号的 updateXxx 方法，请注意这是*结果集*中的列号。它很可能与数据库中的列号不同。

updateXxx 方法只更改行值，而不更改数据库。完成一行中的字段更新后，必须调用 updateRow 方法。该方法将当前行中的所有更新发送到数据库。如果在未调用 updateRow 的情况下将游标移动到另一行，则该行的更新将从行集中丢弃，并且永远不会传送到数据库。还可以调用 cancelRowUpdates 方法取消对当前行的更新。

前面的示例展示了如何修改现有行。如果要向数据库添加新行，首先使用 moveToInsertRow 方法将游标移动到称为插入行的特殊位置。然后，通过发出 updateXxx 指令在插入行位置构建新行。完成后，调用 insertRow 方法将新行传送到数据库。插入完成后，调用 moveToCurrentRow 将游标移回调用 moveToInsertRow 之前的位置。下面是一个示例：

```java
rs.moveToInsertRow();
rs.updateString("Title", title);
rs.updateString("ISBN", isbn);
rs.updateString("Publisher Id", pubid);
rs.updateDouble("Price", price);
rs.insertRow();
rs.moveToCurrentRow();
```

请注意，你无法影响新数据在结果集或数据库中添加的位置。



如果在插入行中未指定列值，则该值会被设置为 SQL NULL。但是，如果该列具有 NOT NULL 约束，则会抛出异常，并且该行不会被插入。

最后，你可以删除光标所在的行：

```java
rs.deleteRow();
```

`deleteRow` 方法会立即将行从结果集和数据库中移除。

`ResultSet` 接口的 `updateRow`、`insertRow` 和 `deleteRow` 方法为你提供了与执行 `UPDATE`、`INSERT` 和 `DELETE` SQL 语句相同的功能。不过，Java 程序员可能会觉得通过结果集操作数据库内容比构造 SQL 语句更自然。

> **注意：** 如果不小心，你可能会使用可更新的结果集编写出极其低效的代码。执行一条 `UPDATE` 语句的效率远比先查询，然后遍历结果集并沿途修改数据要高得多。可更新的结果集适用于允许用户进行任意修改的交互式程序，但对于大多数程序化修改而言，SQL `UPDATE` 更为合适。

> **注意：** JDBC 2 对结果集做了进一步增强，例如，如果数据已被另一个并发数据库连接修改，可以使用最新数据更新结果集。JDBC 3 又增加了一项改进，规定了事务提交时结果集的行为。然而，这些高级特性超出了本入门章节的讨论范围。我们建议你参阅 Maydene Fisher、Jon Ellis 和 Jonathan Bruce 所著的 *JDBC™ API Tutorial and Reference, Third Edition*（Addison-Wesley，2003 年）以及 JDBC 规范以获取更多信息。

#### java.sql.Connection 1.1

- `Statement createStatement(int type, int concurrency)` 1.2
- `PreparedStatement prepareStatement(String command, int type, int concurrency)` 1.2

  创建一条语句或预处理语句，该语句生成具有给定类型和并发性的结果集。`type` 参数是常量 `TYPE_FORWARD_ONLY`、`TYPE_SCROLL_INSENSITIVE` 或 `TYPE_SCROLL_SENSITIVE` 之一，`concurrency` 是常量 `CONCUR_READ_ONLY` 或 `CONCUR_UPDATABLE` 之一，这些常量均定义在 `ResultSet` 接口中。

#### java.sql.ResultSet 1.1

- `int getType()` 1.2  
  返回此结果集的类型——`TYPE_FORWARD_ONLY`、`TYPE_SCROLL_INSENSITIVE` 或 `TYPE_SCROLL_SENSITIVE` 之一。

- `int getConcurrency()` 1.2  
  返回此结果集的并发设置——`CONCUR_READ_ONLY` 或 `CONCUR_UPDATABLE`。

- `boolean previous()` 1.2  
  将光标移动到前一行。如果光标位于某一行上，则返回 `true`；如果光标位于第一行之前，则返回 `false`。

- `int getRow()` 1.2  
  获取当前行的行号。行号从 1 开始编号。

- `boolean absolute(int r)` 1.2  
  将光标移动到第 r 行。如果光标位于某一行上，则返回 `true`。

- `boolean relative(int d)` 1.2  
  将光标移动 d 行。如果 d 为负数，则光标向后移动。如果光标位于某一行上，则返回 `true`。

- `boolean first()` 1.2
- `boolean last()` 1.2  
  将光标移动到第一行或最后一行。如果光标位于某一行上，则返回 `true`。

- `void beforeFirst()` 1.2
- `void afterLast()` 1.2  
  将光标移动到第一行之前或最后一行之后。

- `boolean isFirst()` 1.2
- `boolean isLast()` 1.2  
  测试光标是否位于第一行或最后一行。

- `boolean isBeforeFirst()` 1.2
- `boolean isAfterLast()` 1.2  
  测试光标是否位于第一行之前或最后一行之后。

- `void moveToInsertRow()` 1.2  
  将光标移动到插入行。插入行是用于通过 `updateXxx` 和 `insertRow` 方法插入新数据的特殊行。

资源。在这种情况下，请使用*行集*。`RowSet` 接口扩展了 `ResultSet` 接口，但行集不必与数据库连接绑定。

如果你需要将查询结果移动到复杂应用程序的另一个层，或移动到其他设备（如手机），行集也很适合。你绝不想移动结果集——它的数据结构可能非常庞大，而且它依赖于数据库连接。

### 5.7.1 构造行集

`javax.sql.rowset` 包提供了以下扩展 `RowSet` 接口的接口：

- `CachedRowSet` 允许断开连接的操作。我们将在下一节讨论缓存行集。
- `WebRowSet` 是可以保存到 XML 文件的缓存行集。该 XML 文件可以移动到 Web 应用程序的另一层，并由另一个 `WebRowSet` 对象在那里打开。
- `FilteredRowSet` 和 `JoinRowSet` 接口支持对行集进行轻量级操作，这些操作相当于 SQL 的 `SELECT` 和 `JOIN` 操作。这些操作在行集存储的数据上执行，无需建立数据库连接。
- `JdbcRowSet` 是 `ResultSet` 的轻量级包装器。它添加了 `RowSet` 接口中的实用方法。

从 Java 7 开始，有一种标准方式获取行集：

```java
RowSetFactory factory = RowSetProvider.newFactory();
CachedRowSet crs = factory.createCachedRowSet();
```

获取其他行集类型也有类似的方法。

### 5.7.2 缓存行集

缓存行集包含来自结果集的所有数据。由于 `CachedRowSet` 是 `ResultSet` 接口的子接口，你可以像使用结果集一样使用缓存行集。缓存行集有一个重要的好处：你可以关闭连接，但仍然使用该行集。正如你将在清单 5.4 的示例程序中看到的，这大大简化了交互式应用程序的实现。每个用户命令只需打开数据库连接，发出查询，将结果放入缓存行集，然后关闭数据库连接。

甚至可以修改缓存行集中的数据。当然，这些修改不会立即反映到数据库中；你需要明确请求接受累积的更改。然后，`CachedRowSet` 会重新连接到数据库，并发出 SQL 语句以写入累积的更改。

你可以从结果集填充 `CachedRowSet`：

```java
ResultSet result = . . .;
RowSetFactory factory = RowSetProvider.newFactory();
CachedRowSet crs = factory.createCachedRowSet();
crs.populate(result);
conn.close(); // 现在可以关闭数据库连接了
```

或者，你可以让 `CachedRowSet` 对象自动建立连接。设置数据库参数：

```java
crs.setURL("jdbc:derby://localhost:1527/COREJAVA");
crs.setUsername("dbuser");
crs.setPassword("secret");
```

然后设置查询语句及其参数：

```java
crs.setCommand("SELECT * FROM Books WHERE Publisher_ID = ?");
crs.setString(1, publisherId);
```

最后，用查询结果填充行集：

```java
crs.execute();
```

此调用会建立数据库连接，发出查询，填充行集，然后断开连接。

如果你的查询结果非常大，你不想将其全部放入行集。毕竟，你的用户可能只看几行。在这种情况下，请指定页面大小：

```java
CachedRowSet crs = . . .;
crs.setCommand(command);
crs.setPageSize(20);
. . .
crs.execute();
```

现在你只会得到 20 行。要获取下一批行，请调用

```java
crs.nextPage();
```

你可以使用与结果集相同的方法来检查和修改行集。如果你修改了行集的内容，必须通过调用

```java
crs.acceptChanges(conn);
```

或

```java
crs.acceptChanges();
```

将其写回数据库。

第二个调用只有在行集配置了连接数据库所需的信息（如 URL、用户名和密码）时才有效。

在第 5.6.2 节“可更新的结果集”（第 325 页）中，你看到并非所有结果集都是可更新的。类似地，包含复杂查询结果的行集可能无法将其更改写回数据库。如果行集包含来自单个表的数据，那么你应该是安全的。

> **注意：** 如果你从结果集填充行集，行集不知道要更新的表的名称。你需要调用 `setTableName` 来设置表名。

另一个复杂性出现在你填充行集之后数据库中的数据发生了变化。这显然是一个可能导致数据不一致的麻烦信号。参考实现会检查原始行集值（即编辑之前的值）是否与数据库中的当前值相同。如果相同，则用编辑后的值替换；否则，抛出 `SyncProviderException`，并且所有更改都不会写入。其他实现可能使用其他同步策略。

#### javax.sql.RowSet 1.4

- `String getURL()`
- `void setURL(String url)`

  获取或设置数据库 URL。

- `String getUsername()`
- `void setUsername(String username)`

  获取或设置用于连接数据库的用户名。

- `String getPassword()`
- `void setPassword(String password)`

  获取或设置用于连接数据库的密码。

- `String getCommand()`
- `void setCommand(String command)`

  获取或设置用于填充此行集而执行的命令。

- `void execute()`

  通过发出用 `setCommand` 设置的语句来填充此行集。为了让驱动程序管理器获得连接，必须设置 URL、用户名和密码。





#### javax.sql.rowset.CachedRowSet 5.0

- `void execute(Connection conn)`  
  通过执行由 `setCommand` 设置的语句来填充此行集。此方法使用给定的连接并*关闭它*。
- `void populate(ResultSet result)`  
  使用来自给定结果集的数据填充此缓存行集。
- `String getTableName()`
- `void setTableName(String tableName)`  
  获取或设置填充此缓存行集所依据的表名。
- `int getPageSize()`
- `void setPageSize(int size)`  
  获取或设置页大小。
- `boolean nextPage()`
- `boolean previousPage()`  
  加载下一页或上一页的行。如果存在下一页或上一页，则返回 true。
- `void acceptChanges()`
- `void acceptChanges(Connection conn)`  
  重新连接数据库并写入因编辑行集而产生的更改。如果因为数据库数据已更改而无法将数据写回，则可能抛出 `SyncProviderException`。

#### javax.sql.rowset.RowSetProvider 7

- `static RowSetFactory newFactory()`  
  创建一个行集工厂。

#### javax.sql.rowset.RowSetFactory 7

- `CachedRowSet createCachedRowSet()`
- `FilteredRowSet createFilteredRowSet()`
- `JdbcRowSet createJdbcRowSet()`
- `JoinRowSet createJoinRowSet()`
- `WebRowSet createWebRowSet()`  
  创建指定类型的行集。

## 5.8 元数据

在前面的章节中，你已经看到了如何填充、查询和更新数据库表。然而，JDBC 还可以提供关于数据库及其表的*结构*的附加信息。例如，你可以获取特定数据库中表的列表，或者某个表的列名和类型。当你实现一个具有预定义数据库的业务应用程序时，这些信息并不有用。毕竟，如果你自己设计表，你就知道它们的结构。然而，对于编写适用于任何数据库的工具的程序员来说，结构信息非常有用。

在 SQL 中，描述数据库或其一部分的数据称为*元数据*（以区别于存储在数据库中的实际数据）。你可以获得三种元数据：关于数据库的、关于结果集的、以及关于预编译语句参数的。

要进一步了解数据库，请从数据库连接请求一个 `DatabaseMetaData` 类型的对象。

```
DatabaseMetaData meta = conn.getMetaData();
```

现在你可以获取一些元数据了。例如，调用

```
ResultSet mrs = meta.getTables(null, null, null, new String[] {"TABLE"});
```

返回一个结果集，其中包含数据库中所有表的信息。（有关此方法的其他参数，请参阅本节末尾的 API 说明。）

结果集中的每一行包含数据库中一个表的信息。第三列是表的名称。（同样，有关其他列的信息，请参阅 API 说明。）以下循环收集所有表名：

```
while (mrs.next())
   tableNames.addItem(mrs.getString(3));
```

数据库元数据还有第二个重要用途。数据库很复杂，SQL 标准为差异性留下了很大的空间。`DatabaseMetaData` 接口中有远超过一百个方法可以查询数据库，其中包括一些名称奇特的调用，例如

```
meta.supportsCatalogsInPrivilegeDefinitions()
```

以及

```
meta.nullPlusNonNullIsNull()
```

显然，这些方法面向有特殊需求的高级用户——尤其是那些需要编写可与多个数据库一起工作的高度可移植代码的用户。

`DatabaseMetaData` 接口提供有关数据库的数据。第二个元数据接口 `ResultSetMetaData` 报告有关结果集的信息。每当你从查询中获得结果集时，都可以查询列数以及每列的名称、类型和字段宽度。下面是一个典型的循环：

```java
ResultSet rs = stmt.executeQuery("SELECT * FROM " + tableName);
ResultSetMetaData meta = rs.getMetaData();
for (int i = 1; i <= meta.getColumnCount(); i++)
{
    String columnName = meta.getColumnLabel(i);
    int columnWidth = meta.getColumnDisplaySize(i);
    . . .
}
```

在本节中，我们将向你展示如何编写这样一个简单的工具。清单 5.4 中的程序使用元数据让你浏览数据库中的所有表。该程序还演示了缓存行集的使用。

顶部的组合框显示数据库中的所有表。选择其中一个，框架中央将填充该表的字段名和第一行的值，如图 5.6 所示。单击 Next 和 Previous 按钮滚动浏览表中的行。你还可以删除一行并编辑行值。单击 Save 按钮将更改保存到数据库。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_357_0.png)

**图 5.6** ViewDB 应用程序

```java
private JButton previousButton;
private JButton nextButton;
private JButton deleteButton;
private JButton saveButton;
private DataPanel dataPanel;
private Component scrollPane;
private JComboBox<String> tableNames;
private Properties props;
private CachedRowSet crs;
private Connection conn;

public ViewDBFrame()
{
    tableNames = new JComboBox<String>();

    try
    {
        readDatabaseProperties();
        conn = getConnection();
        DatabaseMetaData meta = conn.getMetaData();
        try (ResultSet mrs = meta.getTables(null, null, null, new String[] { "TABLE" }))
        {
            while (mrs.next())
                tableNames.addItem(mrs.getString(3));
        }
    }
    catch (SQLException ex)
    {
        for (Throwable t : ex)
            t.printStackTrace();
    }
    catch (IOException ex)
    {
        ex.printStackTrace();
    }

    tableNames.addActionListener(
        event -> showTable((String) tableNames.getSelectedItem(), conn));
    add(tableNames, BorderLayout.NORTH);
    addWindowListener(new WindowAdapter()
    {
        public void windowClosing(WindowEvent event)
        {
            try
            {
                if (conn != null) conn.close();
            }
        }
    });
}
```

### 清单 5.4 *（续）*

```java
/**
 * Deletes current table row.
 */
public void deleteRow()
{
    if (crs == null) return;
    new SwingWorker<Void, Void>()
    {
        public Void doInBackground() throws SQLException
        {
            crs.deleteRow();
            crs.acceptChanges(conn);
            if (crs.isLast())
                if (!crs.last()) crs = null;
            return null;
        }
        public void done()
        {
            dataPanel.showRow(crs);
        }
    }.execute();
}
/**
 * Saves all changes.
 */
public void saveChanges()
{
    if (crs == null) return;
    new SwingWorker<Void, Void>()
    {
        public Void doInBackground() throws SQLException
        {
            dataPanel.setRow(crs);
            crs.acceptChanges(conn);
            return null;
        }
    }.execute();
}
private void readDatabaseProperties() throws IOException
{
    props = new Properties();
    try (InputStream in = Files.newInputStream(Paths.get("database.properties")))
    {
        props.load(in);
    }
}
```

```java
220        String drivers = props.getProperty("jdbc.drivers");
228        if (drivers != null) System.setProperty("jdbc.drivers", drivers);
231     }
232
233     /**
234      * Gets a connection from the properties specified in the file database.properties.
235      * @return the database connection
236      */
237     private Connection getConnection() throws SQLException
238     {
239        String url = props.getProperty("jdbc.url");
240        String username = props.getProperty("jdbc.username");
241        String password = props.getProperty("jdbc.password");
242
243        return DriverManager.getConnection(url, username, password);
244     }
245
246     /**
247      * This panel displays the contents of a result set.
248      */
249     class DataPanel extends JPanel
250     {
251        private java.util.List<JTextField> fields;
252
253        /**
254         * Constructs the data panel.
255         * @param rs the result set whose contents this panel displays
256         */
257        public DataPanel(RowSet rs) throws SQLException
258        {
259           fields = new ArrayList<>();
260           setLayout(new GridBagLayout());
261           var gbc = new GridBagConstraints();
262           gbc.gridwidth = 1;
263           gbc.gridheight = 1;
264
265           ResultSetMetaData rsmd = rs.getMetaData();
266           for (int i = 1; i <= rsmd.getColumnCount(); i++)
267           {
268              gbc.gridy = i - 1;
269
270              String columnName = rsmd.getColumnLabel(i);
271              gbc.gridx = 0;
272              gbc.anchor = GridBagConstraints.EAST;
273              add(new JLabel(columnName), gbc);
274
275              int columnWidth = rsmd.getColumnDisplaySize(i);
276              var tb = new JTextField(columnWidth);
```




### 代码清单 5.4 *(续)*

```java
if (!rsmd.getColumnClassName(i).equals("java.lang.String"))
    tb.setEditable(false);

fields.add(tb);

gbc.gridx = 1;
gbc.anchor = GridBagConstraints.WEST;
add(tb, gbc);
}
}

/**
 * Shows a database row by populating all text fields with the column values.
 */
public void showRow(ResultSet rs)
{
    try
    {
        if (rs == null) return;
        for (int i = 1; i <= fields.size(); i++)
        {
            String field = rs == null ? "" : rs.getString(i);
            JTextField tb = fields.get(i - 1);
            tb.setText(field);
        }
    }
    catch (SQLException ex)
    {
        for (Throwable t : ex)
            t.printStackTrace();
    }
}

/**
 * Updates changed data into the current row of the row set.
 */
public void setRow(RowSet rs) throws SQLException
{
    for (int i = 1; i <= fields.size(); i++)
    {
        String field = rs.getString(i);
        JTextField tb = fields.get(i - 1);
        if (!field.equals(tb.getText()))
            rs.updateString(i, tb.getText());
    }
    rs.updateRow();
}
```

### java.sql.Connection *1.1*

- `DatabaseMetaData getMetaData()`

  返回连接的元数据，形式为 `DatabaseMetaData` 对象。

### java.sql.DatabaseMetaData *1.1*

- `ResultSet getTables(String catalog, String schemaPattern, String tableNamePattern, String types[])`

  返回目录中所有符合模式、表名模式和类型条件的表的描述。*(模式描述一组相关表及访问权限。目录描述一组相关模式。这些概念对于构建大型数据库很重要。)*

  catalog 和 schemaPattern 参数可以为 `""`，以检索没有目录或模式的表，或者为 `null`，以返回不考虑目录或模式的表。

  types 数组包含要包含的表类型的名称。典型类型有 `TABLE`、`VIEW`、`SYSTEM TABLE`、`GLOBAL TEMPORARY`、`LOCAL TEMPORARY`、`ALIAS` 和 `SYNONYM`。如果 types 为 `null`，则返回所有类型的表。

  结果集有五列，所有列均为 String 类型。

  | 列 | 名称 | 说明 |
  |---|---|---|
  | 1 | `TABLE_CAT` | 表目录（可能为 null） |
  | 2 | `TABLE_SCHEM` | 表模式（可能为 null） |
  | 3 | `TABLE_NAME` | 表名 |
  | 4 | `TABLE_TYPE` | 表类型 |
  | 5 | `REMARKS` | 表的注释 |

- `int getJDBCMajorVersion()`  *1.4*
- `int getJDBCMinorVersion()`  *1.4*

  返回建立数据库连接的驱动程序的 JDBC 主版本号或次版本号。例如，JDBC 3.0 驱动程序的主版本号为 3，次版本号为 0。

- `int getMaxConnections()`

  返回允许连接到该数据库的最大并发连接数。

- `int getMaxStatements()`

  返回每个数据库连接允许同时打开的最大语句数，如果数量无限制或未知，则返回 0。

### java.sql.ResultSet 1.1

- `ResultSetMetaData getMetaData()`

  返回与当前 ResultSet 列关联的元数据。

### java.sql.ResultSetMetaData 1.1

- `int getColumnCount()`

  返回当前 ResultSet 对象中的列数。

- `int getColumnDisplaySize(int column)`

  返回由 index 参数指定的列的最大宽度。

- `String getColumnLabel(int column)`

  返回该列的建议标题。

- `String getColumnName(int column)`

  返回与指定列索引关联的列名。

## 5.9 事务

你可以将一组语句组合成一个*事务*。当一切顺利时，事务可以*提交*；或者，如果其中某个语句发生错误，事务可以*回滚*，就好像这些语句从未执行过一样。

将语句分组为事务的主要原因是*数据库完整性*。例如，假设我们要将钱从一个银行账户转到另一个账户。那么，同时借记一个账户并贷记另一个账户很重要。如果系统在借记第一个账户之后、贷记另一个账户之前发生故障，则需要撤销该借记操作。

如果将更新语句分组到一个事务中，事务要么整体成功并可以*提交*，要么在中间某处失败。在这种情况下，你可以执行*回滚*，数据库会自动撤销自上次已提交事务以来发生的所有更新的效果。

### 5.9.1 使用 JDBC 编写事务

默认情况下，数据库连接处于*自动提交模式*，每条 SQL 语句在执行后立即提交到数据库。一旦语句提交，就不能回滚。关闭此默认设置以便使用事务：

```
conn.setAutoCommit(false);
```

以常规方式创建 Statement 对象：

```
    Statement stat = conn.createStatement();
```

多次调用 executeUpdate：

```
    stat.executeUpdate(command1);
    stat.executeUpdate(command2);
    stat.executeUpdate(command3);
```

如果所有语句都执行无误，则调用 commit 方法：

```
    conn.commit();
```

但是，如果发生错误，则调用

```
    conn.rollback();
```

然后，自上次提交以来的所有语句都会被自动撤销。通常，当事务被 SQLException 中断时，你会发出回滚。

### 5.9.2 保存点

对于某些数据库和驱动程序，你可以使用*保存点*对回滚过程进行更细粒度的控制。创建保存点会标记一个点，之后可以返回到该点，而无需放弃整个事务。例如，

```
    Statement stat = conn.createStatement(); // start transaction; rollback() goes here
    stat.executeUpdate(command1);
    Savepoint svpt = conn.setSavepoint(); // set savepoint; rollback(svpt) goes here
    stat.executeUpdate(command2);
```

```
    if (...) conn.rollback(svpt);  // undo effect of command2
    ...
    conn.commit();
```

当不再需要保存点时，应释放它：

```
    conn.releaseSavepoint(svpt);
```

### 5.9.3 批量更新

假设一个程序需要执行许多 INSERT 语句来填充数据库表。你可以通过使用*批量更新*来提高程序的性能。在批量更新中，一系列语句被收集并作为一批提交。

> **注意：** 使用 DatabaseMetaData 接口的 supportsBatchUpdates 方法来确定你的数据库是否支持此功能。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_368_0.png)

批中的语句可以是 INSERT、UPDATE 或 DELETE 等操作，也可以是 CREATE TABLE 或 DROP TABLE 等数据定义语句。如果向批中添加 SELECT 语句，则会抛出异常。（从概念上讲，SELECT 语句在批中没有意义，因为它返回结果集而不更新数据库。）

要执行批处理，首先以常规方式创建 Statement 对象：

```
Statement stat = conn.createStatement();
```

现在，不要调用 executeUpdate，而是调用 addBatch 方法：

```
String command = "CREATE TABLE . . . "
stat.addBatch(command);
```

```
while (true)
{
    command = "INSERT INTO . . . VALUES (" + . . . + ")";
    stat.addBatch(command);
}
```

最后，提交整个批：

```
int[] counts = stat.executeBatch();
```

对 executeBatch 的调用返回一个数组，其中包含所有已提交语句的行数。

为了在批处理模式下进行正确的错误处理，请将批执行视为单个事务。如果批在中间失败，你希望回滚到批开始之前的状态。

首先，关闭自动提交模式，然后收集批、执行它、提交它，最后恢复原来的自动提交模式：

```
boolean autoCommit = conn.getAutoCommit();
conn.setAutoCommit(false);
Statement stat = conn.createStatement();
. . .
// keep calling stat.addBatch(. . .);
. . .
stat.executeBatch();
conn.commit();
conn.setAutoCommit(autoCommit);
```




| java.sql.Connection | 1.1 |
|---|---|
| `boolean getAutoCommit()` | |
| `void setAutoCommit(boolean b)` | 获取或设置此连接的自动提交模式为 b。如果自动提交为 true，所有语句在执行完成后将立即提交。 |
| `void commit()` | 提交自上次提交以来发布的所有语句。 |
| `void rollback()` | 撤销自上次提交以来发布的所有语句的影响。 |
| `Savepoint setSavepoint()` | 1.4 |
| `Savepoint setSavepoint(String name)` | 1.4。设置一个未命名或命名的保存点。 |
| `void rollback(Savepoint svpt)` | 1.4。回滚到给定的保存点。 |
| `void releaseSavepoint(Savepoint svpt)` | 1.4。释放给定的保存点。 |

| java.sql.Savepoint | 1.4 |
|---|---|
| `int getSavepointId()` | 获取此未命名保存点的 ID，如果这是命名保存点，则抛出 `SQLException`。 |
| `String getSavepointName()` | 获取此保存点的名称，如果这是未命名保存点，则抛出 `SQLException`。 |

| java.sql.Statement | 1.1 |
|---|---|
| `void addBatch(String command)` | 1.2。将此命令添加到此语句的当前命令批处理中。 |
| `int[] executeBatch()` | 1.2 |
| `long[] executeLargeBatch()` | 8。执行当前批处理中的所有命令。返回数组中的每个值对应一个批处理语句。如果它是非负值，则它是一个行数。如果它是值 `SUCCESS_NO_INFO`，则语句成功，但没有可用的行数。如果它是 `EXECUTE_FAILED`，则语句失败。 |

- `java.sql.DatabaseMetaData` 1.1
  - `boolean supportsBatchUpdates()` 1.2：如果驱动程序支持批量更新，则返回 true。

### 5.9.4 高级 SQL 类型

表 5.8 列出了 JDBC 支持的 SQL 数据类型及其在 Java 编程语言中的对应类型。

**表 5.8** SQL 数据类型及其对应的 Java 类型

| SQL 数据类型 | Java 数据类型 |
|---|---|
| INTEGER or INT | int |
| SMALLINT | short |
| NUMERIC(m,n), DECIMAL(m,n) or DEC(m,n) | java.math.BigDecimal |
| FLOAT(n) | double |
| REAL | float |
| DOUBLE | double |
| CHARACTER(n) or CHAR(n) | String |
| VARCHAR(n), LONG VARCHAR | String |
| BOOLEAN | boolean |
| DATE | java.sql.Date |
| TIME | java.sql.Time |
| TIMESTAMP | java.sql.Timestamp |
| BLOB | java.sql.Blob |
| CLOB | java.sql.Clob |
| ARRAY | java.sql.Array |
| ROWID | java.sql.RowId |
| NCHAR(n), NVARCHAR(n), LONG NVARCHAR | String |
| NCLOB | java.sql.NClob |
| SQLXML | java.sql.SQLXML |

SQL `ARRAY` 是一个值序列。例如，在 Student 表中，可以有一个 `ARRAY OF INTEGER` 类型的 Scores 列。`getArray` 方法返回一个接口类型为 `java.sql.Array` 的对象。该接口有获取数组值的方法。

当你从数据库获取 LOB 或数组时，只有在你请求单个值时，实际内容才会从数据库中获取。这是一种有用的性能增强，因为数据量可能很大。

某些数据库支持 `ROWID` 值，这些值描述行的位置，以便可以非常快速地检索该行。JDBC 4 引入了接口 `java.sql.RowId`，以及在查询中提供行 ID 并从结果中检索行 ID 的方法。

*国家字符串*（`NCHAR` 及其变体）以本地字符编码存储字符串，并使用本地排序约定来存储它们。JDBC 4 提供了在查询和结果中将 Java String 对象与国家字符串相互转换的方法。

某些数据库可以存储用户定义的结构化类型。JDBC 3 提供了一种将结构化 SQL 类型自动映射到 Java 对象的机制。

某些数据库为 XML 数据提供原生存储。JDBC 4 引入了 `SQLXML` 接口，该接口可以在内部 XML 表示与 DOM、`Source`/`Result` 接口以及二进制流之间进行协调。有关详细信息，请参阅 `SQLXML` 类的 API 文档。

我们不再进一步讨论这些高级 SQL 类型。你可以在 *JDBC API 教程与参考* 和 JDBC 规范中找到有关这些主题的更多信息。

## 5.10 Web 和企业应用程序中的连接管理

前面章节中描述的通过 `database.properties` 文件进行简单化数据库连接设置的方法，适用于小型测试程序，但无法扩展到更大的应用程序。

当 JDBC 应用程序部署在 Web 或企业环境中时，数据库连接的管理与 JNDI 集成。整个企业中数据源的属性可以存储在目录中。使用目录可以集中管理用户名、密码、数据库名称和 JDBC URL。

在这种环境中，你可以使用以下代码建立数据库连接：

```java
var jndiContext = new InitialContext();
var source = (DataSource) jndiContext.lookup("java:comp/env/jdbc/corejava");
Connection conn = source.getConnection();
```

请注意，`DriverManager` 不再参与其中。相反，JNDI 服务会定位一个 *数据源*。数据源是一个接口，它允许简单的 JDBC 连接以及更高级的服务，例如执行涉及多个数据库的分布式事务。`DataSource` 接口定义在 `javax.sql` 标准扩展包中。

> **注意：** 在 Java EE 容器中，你甚至不必编写 JNDI 查找代码。只需在 `DataSource` 字段上使用 `Resource` 注解，数据源引用将在你的应用程序加载时设置：
>
> ```java
> @Resource(name="jdbc/corejava")
> private DataSource source;
> ```

当然，数据源需要在某个地方进行配置。如果你编写在 Apache Tomcat 等 servlet 容器或 GlassFish 等应用服务器中执行的数据库程序，请将数据库配置（包括 JNDI 名称、JDBC URL、用户名和密码）放在配置文件中，或在管理 GUI 中进行设置。

用户名和登录的管理只是需要特别关注的问题之一。另一个问题涉及建立数据库连接的成本。我们的示例数据库程序使用了两种获取数据库连接的策略。清单 5.3 中的 `QueryDB` 程序在程序开始时建立单个数据库连接，并在程序结束时将其关闭。清单 5.4 中的 `ViewDB` 程序在需要时打开新连接。

然而，这两种方法都不令人满意。数据库连接是有限资源。如果用户离开应用程序一段时间，连接不应保持打开状态。相反，为每个查询获取连接并在之后关闭它的成本非常高。

解决方案是*池化*连接。这意味着数据库连接并未物理关闭，而是保留在队列中并重复使用。连接池是一项重要的服务，JDBC 规范为实现者提供了挂钩来提供该服务。然而，JDK 本身不提供任何实现，数据库供应商通常也不会在其 JDBC 驱动程序中包含实现。相反，Web 容器和应用服务器的供应商提供连接池实现。

使用连接池对程序员来说是完全透明的。通过获取数据源并调用 getConnection，从池化连接源获取连接。当你使用完连接后，调用 close。这不会关闭物理连接，而是告诉池你已用完它。连接池通常也会尽力池化预编译语句。

你现在已经了解了 JDBC 的基础知识，并且足以实现简单的数据库应用程序。然而，正如我们在本章开头提到的，数据库很复杂，相当多的高级主题超出了这一入门章节的范围。有关高级 JDBC 功能的概述，请参阅 JDBC API 教程与参考或 JDBC 规范。

在本章中，你学习了如何在 Java 中使用关系数据库。下一章将介绍 Java 8 日期和时间库。




*此页有意留空*

# 第 6 章：日期和时间 API

## 本章内容

- 6.1 时间线，第 354 页
- 6.2 本地日期，第 358 页
- 6.3 日期调整器，第 364 页
- 6.4 本地时间，第 365 页
- 6.5 时区时间，第 367 页
- 6.6 格式化和解析，第 371 页
- 6.7 与遗留代码互操作，第 376 页

光阴似箭，我们可以轻易地设定一个起点，然后以秒为单位向前或向后计数。那么为什么处理时间如此困难呢？问题出在人类身上。如果我们只需告诉彼此：“1523793600 见，别迟到！”一切都会很简单。但我们希望时间与日光和季节相关联。事情就变得复杂了。Java 1.0 有一个 `Date` 类，事后看来，它相当幼稚，当 Java 1.1 引入日历类时，它的大部分方法已被弃用。它的 API 并不出色，它的实例是可变的，而且没有处理闰秒等问题。第三次终于成功了，Java 8 中引入的 `java.time` API 弥补了过去的缺陷，并且应该能在相当长一段时间内为我们服务。在本章中，你将了解是什么让时间计算如此令人头疼，以及日期和时间 API 如何解决这些问题。

静态方法 `Instant.now()` 返回当前瞬时。你可以像通常那样使用 `equals` 和 `compareTo` 方法比较两个瞬时，因此可以将瞬时用作时间戳。

要计算两个瞬时之间的差异，可以使用静态方法 `Duration.between`。例如，下面演示了如何测量算法的运行时间：

```java
Instant start = Instant.now();
runAlgorithm();
Instant end = Instant.now();
Duration timeElapsed = Duration.between(start, end);
long millis = timeElapsed.toMillis();
```

Duration 是两个瞬时之间的时间量。你可以调用 `toNanos`、`toMillis`、`toSeconds`、`toMinutes`、`toHours` 或 `toDays`，以常规单位获取 Duration 的长度。

> **注意：** 在 Java 8 中，你必须调用 `getSeconds` 而不是 `toSeconds`。

如果需要纳秒级精度，请注意溢出。一个 long 值可以容纳将近 300 年的纳秒数。如果你的持续时间短于此，只需将它们转换为纳秒。你可以使用更长的持续时间——`Duration` 对象在 long 中存储秒数，并在额外的 int 中存储纳秒数。Duration API 提供了许多方法，本节末尾展示了这些方法，用于执行算术运算。

例如，如果你想检查一个算法是否至少比另一个快十倍，可以这样计算：

```java
Duration timeElapsed2 = Duration.between(start2, end2);
boolean overTenTimes
    = timeElapsed.multipliedBy(10).minus(timeElapsed2).isNegative();
```

这仅仅是为了展示语法。既然这些算法不会运行数百年，你可以直接使用：

```java
boolean overTenTimesFaster = timeElapsed.toNanos() * 10 < timeElapsed2.toNanos();
```

> **注意：** Instant 和 Duration 类是不可变的，所有方法（如 multipliedBy 或 minus）都会返回一个新实例。

```java
42
43 public static void runAlgorithm2()
44 {
45     int size = 10;
46     List<Integer> list = new Random().ints(1, 100).map(i -> i % 100).limit(size)
47         .boxed().collect(Collectors.toList());
48     while (!IntStream.range(1, list.size())
49         .allMatch(i -> list.get(i - 1).compareTo(list.get(i)) <= 0))
50         Collections.shuffle(list);
51     System.out.println(list);
52 }
53 }
```

| java.time.Instant 8 |
| --- |
| • static Instant now()<br>从可用的最佳系统时钟获取当前瞬时。 |
| • Instant plus(TemporalAmount amountToAdd)<br>• Instant minus(TemporalAmount amountToSubtract)<br>返回一个距离此 Instant 指定时间量的瞬时。Duration 和 Period 类（参见 6.2 节“本地日期”，第 358 页）实现了 TemporalAmount 接口。 |
| • Instant (plus\|minus)(Nanos\|Millis\|Seconds)(long number)<br>返回一个距离此 Instant 指定纳秒、毫秒或秒数的 Instant。 |

| java.time.Duration 8 |
| --- |
| • static Duration of(Nanos\|Millis\|Seconds\|Minutes\|Hours\|Days)(long number)<br>返回给定数量时间单位的持续时间。 |
| • static Duration between(Temporal startInclusive, Temporal endExclusive)<br>返回给定时间点之间的持续时间。Temporal 接口由 Instant 类、LocalDate/LocalDateTime/LocalTime（参见 6.4 节“本地时间”，第 365 页）以及 ZonedDateTime（参见 6.5 节“时区时间”，第 367 页）实现。 |

### 清单 6.2 `localdates/LocalDates.java`

```java
package localdates;

/**
 * @version 1.0 2016-05-10
 * @author Cay Horstmann
 */
import java.time.*;
import java.time.temporal.*;
import java.util.stream.*;

public class LocalDates
{
    public static void main(String[] args)
    {
        LocalDate today = LocalDate.now(); // Today's date
        System.out.println("today: " + today);

        LocalDate alonzosBirthday = LocalDate.of(1903, 6, 14);
        alonzosBirthday = LocalDate.of(1903, Month.JUNE, 14);
        // Uses the Month enumeration
        System.out.println("alonzosBirthday: " + alonzosBirthday);

        LocalDate programmersDay = LocalDate.of(2018, 1, 1).plusDays(255);
        // September 13, but in a leap year it would be September 12
        System.out.println("programmersDay: " + programmersDay);

        LocalDate independenceDay = LocalDate.of(2018, Month.JULY, 4);
        LocalDate christmas = LocalDate.of(2018, Month.DECEMBER, 25);

        System.out.println("Until christmas: " + independenceDay.until(christmas));
        System.out.println("Until christmas: "
                + independenceDay.until(christmas, ChronoUnit.DAYS));

        System.out.println(LocalDate.of(2016, 1, 31).plusMonths(1));
        System.out.println(LocalDate.of(2016, 3, 31).minusMonths(1));

        DayOfWeek startOfLastMillennium = LocalDate.of(1900, 1, 1).getDayOfWeek();
        System.out.println("startOfLastMillennium: " + startOfLastMillennium);
        System.out.println(startOfLastMillennium.getValue());
        System.out.println(DayOfWeek.SATURDAY.plus(3));

        LocalDate start = LocalDate.of(2000, 1, 1);
        LocalDate endExclusive = LocalDate.now();
        Stream<LocalDate> firstDaysInMonth = start.datesUntil(endExclusive, Period.ofMonths(1));
        System.out.println("firstDaysInMonth: "
                + firstDaysInMonth.collect(Collectors.toList()));
    }
}
```

### java.time.LocalDate 8

- `static LocalDate now()`  
  获取当前 LocalDate。
- `static LocalDate of(int year, int month, int dayOfMonth)`
- `static LocalDate of(int year, Month month, int dayOfMonth)`  
  返回具有给定年、月（1 到 12 之间的整数，或 Month 枚举的值）和日（1 到 31 之间）的本地日期。
- `LocalDate (plus|minus)(Days|Weeks|Months|Years)(long number)`  
  返回通过添加或减去给定数量时间单位得到的 LocalDate。
- `LocalDate plus(TemporalAmount amountToAdd)`
- `LocalDate minus(TemporalAmount amountToSubtract)`  
  返回一个与此 LocalDate 相距给定时间量的 LocalDate。Duration 和 Period 类实现了 TemporalAmount 接口。
- `LocalDate withDayOfMonth(int dayOfMonth)`
- `LocalDate withDayOfYear(int dayOfYear)`
- `LocalDate withMonth(int month)`
- `LocalDate withYear(int year)`  
  返回一个新的 LocalDate，其月中的日、年中的日、月或年已更改为给定值。
- `int getDayOfMonth()`  
  获取月中的日（1 到 31 之间）。
- `int getDayOfYear()`  
  获取年中的日（1 到 366 之间）。
- `DayOfWeek getDayOfWeek()`  
  获取周中的日，返回 DayOfWeek 枚举的一个值。
- `Month getMonth()`
- `int getMonthValue()`  
  以 Month 枚举值或 1 到 12 之间的数字形式获取月份。
- `int getYear()`  
  获取年份，范围在 -999,999,999 到 999,999,999 之间。
- `Period until(ChronoLocalDate endDateExclusive)`  
  获取直到给定结束日期的 Period。ChronoLocalDate 接口由 LocalDate 以及非公历日历的日期类实现。



### java.time.LocalDate ⁸（续）

- `boolean isBefore(ChronoLocalDate other)`
- `boolean isAfter(ChronoLocalDate other)`  
  如果此日期在给定日期之前或之后，则返回 true。
- `boolean isLeapYear()`  
  如果该年是闰年，则返回 true——也就是说，如果它能被 4 整除但不能被 100 整除，或者能被 400 整除。该算法适用于所有过去的年份，尽管这在历史上并不准确。（闰年是在年份 −46 发明的，而涉及被 100 和 400 整除的规则是在 1582 年格里高利历改革中引入的。这项改革花了 300 多年才被普遍采用。）
- `Stream<LocalDate> datesUntil(LocalDate endExclusive)` ⁹
- `Stream<LocalDate> datesUntil(LocalDate endExclusive, Period step)` ⁹  
  生成一个从该 `LocalDate` 到结束日期的日期流，步长为 1 或给定周期。

### java.time.Period ⁸

- `static Period of(int years, int months, int days)`
- `Period of(Days|Weeks|Months|Years)(int number)`  
  生成一个具有给定数量时间单位的 `Period`。
- `int get(Days|Months|Years)()`  
  获取此 `Period` 的天数、月数或年数。
- `Period (plus|minus)(Days|Months|Years)(long number)`  
  生成一个通过加上或减去给定数量时间单位而得到的 `Period`。
- `Period plus(TemporalAmount amountToAdd)`
- `Period minus(TemporalAmount amountToSubtract)`  
  生成一个与该 `Period` 相距给定时间量的 `Period`。`Duration` 和 `Period` 类实现 `TemporalAmount` 接口。
- `Period with(Days|Months|Years)(int number)`  
  返回一个新的 `Period`，其天数、月数或年数已更改为给定数字。

## 6.3 日期调整器

对于调度应用程序，你经常需要计算诸如“每月第一个星期二”之类的日期。TemporalAdjusters 类提供了许多用于常见调整的静态方法。将调整方法的结果传递给 with 方法。例如，某月的第一个星期二可以这样计算：

```
LocalDate firstTuesday = LocalDate.of(year, month, 1).with(
    TemporalAdjusters.nextOrSame(DayOfWeek.TUESDAY));
```

一如既往，with 方法返回一个新的 LocalDate 对象，而不修改原对象。本节末尾的 API 注释列出了可用的调整器。

你也可以通过实现 TemporalAdjuster 接口来创建自己的调整器。下面是一个用于计算下一个工作日的调整器：

```
TemporalAdjuster NEXT_WORKDAY = w ->
{
    var result = (LocalDate) w;
    do
    {
        result = result.plusDays(1);
    }
    while (result.getDayOfWeek().getValue() >= 6);
    return result;
};

LocalDate backToWork = today.with(NEXT_WORKDAY);
```

注意，lambda 表达式的参数类型为 Temporal，必须将其强制转换为 LocalDate。可以使用 ofDateAdjuster 方法避免这种强制转换，该方法期望一个类型为 UnaryOperator<LocalDate> 的 lambda。

```
TemporalAdjuster NEXT_WORKDAY = TemporalAdjusters.ofDateAdjuster(w ->
{
    LocalDate result = w; // No cast
    do
    {
        result = result.plusDays(1);
    }
    while (result.getDayOfWeek().getValue() >= 6);
    return result;
});
```

| java.time.LocalDate 9 |
| --- |
| - `LocalDate with(TemporalAdjuster adjuster)`<br>返回使用给定调整器调整此日期后的结果。 |

| java.time.temporal.TemporalAdjusters 9 |
| --- |
| - `static TemporalAdjuster next(DayOfWeek dayOfWeek)`<br>- `static TemporalAdjuster nextOrSame(DayOfWeek dayOfWeek)`<br>- `static TemporalAdjuster previous(DayOfWeek dayOfWeek)`<br>- `static TemporalAdjuster previousOrSame(DayOfWeek dayOfWeek)`<br>返回一个将日期调整到给定星期几的调整器。<br><br>- `static TemporalAdjuster dayOfWeekInMonth(int n, DayOfWeek dayOfWeek)`<br>- `static TemporalAdjuster lastInMonth(DayOfWeek dayOfWeek)`<br>返回一个将该月的日期调整到第 n 个或最后一个给定星期几的调整器。<br><br>- `static TemporalAdjuster firstDayOfMonth()`<br>- `static TemporalAdjuster firstDayOfNextMonth()`<br>- `static TemporalAdjuster firstDayOfYear()`<br>- `static TemporalAdjuster firstDayOfNextYear()`<br>- `static TemporalAdjuster lastDayOfMonth()`<br>- `static TemporalAdjuster lastDayOfYear()`<br>返回一个将日期调整到给定月份或年份中的某一天的调整器。 |

## 6.4 本地时间

`LocalTime` 表示一天中的时间，例如 15:30:00。可以使用 `now` 或 `of` 方法创建实例：

```
LocalTime rightNow = LocalTime.now();
LocalTime bedtime = LocalTime.of(22, 30); // or LocalTime.of(22, 30, 0)
```

API 注释展示了本地时间的常见操作。plus 和 minus 操作会以 24 小时为一天循环回绕。例如，

```
LocalTime wakeup = bedtime.plusHours(8); // wakeup is 6:30:00
```

> **注意：** LocalTime 不关心 AM/PM。这种区分留给格式化器——参见第 6.6 节“格式化和解析”（第 371 页）。

有一个表示日期和时间的 LocalDateTime 类。该类适合在固定时区中存储时间点——例如，用于课程或事件的时间表。但是，如果需要执行跨越夏令时的计算，或者需要处理不同时区的用户，则应使用我们接下来讨论的 ZonedDateTime 类。

| java.time.LocalTime 8 |
| --- |
| - `static LocalTime now()`<br>获取当前 LocalTime。<br><br>- `static LocalTime of(int hour, int minute)`<br>- `static LocalTime of(int hour, int minute, int second)`<br>- `static LocalTime of(int hour, int minute, int second, int nanoOfSecond)`<br>生成一个具有给定小时（介于 0 和 23 之间）、分钟、秒（介于 0 和 59 之间）和纳秒（介于 0 和 999,999,999 之间）的本地时间。<br><br>- `LocalTime (plus\|minus)(Hours\|Minutes\|Seconds\|Nanos)(long number)`<br>生成一个通过加上或减去给定数量时间单位而得到的 LocalTime。<br><br>- `LocalTime plus(TemporalAmount amountToAdd)`<br>- `LocalTime minus(TemporalAmount amountToSubtract)`<br>生成一个与该 LocalTime 相距给定时间量的 LocalTime。<br><br>- `LocalTime with(Hour\|Minute\|Second\|Nano)(int value)`<br>返回一个新的 LocalTime，其小时、分钟、秒或纳秒已更改为给定值。<br><br>- `int getHour()`<br>获取小时（介于 0 和 23 之间）。<br><br>- `int getMinute()`<br>- `int getSecond()`<br>获取分钟或秒（介于 0 和 59 之间）。<br><br>- `int getNano()`<br>获取纳秒（介于 0 和 999,999,999 之间）。<br><br>- `int toSecondOfDay()`<br>- `long toNanoOfDay()`<br>生成自午夜以来的秒数或纳秒数。<br><br>- `boolean isBefore(LocalTime other)`<br>- `boolean isAfter(LocalTime other)`<br>如果此时间在给定时间之前或之后，则返回 true。 |

`ZonedDateTime` 的许多方法与 `LocalDateTime` 的相同（参见本节末尾的 API 注释）。大多数都很直接，但夏令时引入了一些复杂情况。

夏令时开始时，时钟拨快一小时。当构造一个落在被跳过小时内的时刻时，会发生什么？例如，2013 年，中欧在 3 月 31 日 2:00 切换到夏令时。如果尝试构造不存在的时刻 3 月 31 日 2:30，实际会得到 3:30。

```
ZonedDateTime skipped = ZonedDateTime.of(
    LocalDate.of(2013, 3, 31),
    LocalTime.of(2, 30),
    ZoneId.of("Europe/Berlin"));
    // Constructs March 31 3:30
```

相反，当夏令时结束时，时钟拨回一小时，会有两个具有相同本地时间的瞬间！当构造该时间范围内的一个时刻时，会得到两者中较早的那个。

```
ZonedDateTime ambiguous = ZonedDateTime.of(
    LocalDate.of(2013, 10, 27), // End of daylight savings time
    LocalTime.of(2, 30),
    ZoneId.of("Europe/Berlin"));
    // 2013-10-27T02:30+02:00[Europe/Berlin]
ZonedDateTime anHourLater = ambiguous.plusHours(1);
    // 2013-10-27T02:30+01:00[Europe/Berlin]
```

一小时后，时间的时和分相同，但时区偏移量已经改变。

在跨越夏令时边界调整日期时，你也需要注意。例如，如果将会议安排在下周，不要加上七天的持续时间：

```
ZonedDateTime nextMeeting = meeting.plus(Duration.ofDays(7));
    // Caution! Won't work with daylight savings time
```

而应使用 `Period` 类。

```
ZonedDateTime nextMeeting = meeting.plus(Period.ofDays(7)); // OK
```

清单 6.3 中的示例程序演示了 `ZonedDateTime` 类。

> **警告：** 还有一个 `OffsetDateTime` 类，它表示带有 UTC 偏移量但没有时区规则的时间。该类适用于特别要求不存在这些规则的专用应用程序，例如某些网络协议。对于人类时间，请使用 `ZonedDateTime`。





### 清单 6.3 `zonedtimes/ZonedTimes.java`

```java
package zonedtimes;

/**
 * @version 1.0 2016-05-10
 * @author Cay Horstmann
 */

import java.time.*;

public class ZonedTimes
{
   public static void main(String[] args)
   {
      ZonedDateTime apollo11launch = ZonedDateTime.of(1969, 7, 16, 9, 32, 0, 0,
            ZoneId.of("America/New_York")); // 1969-07-16T09:32-04:00[America/New_York]
      System.out.println("apollo11launch: " + apollo11launch);

      Instant instant = apollo11launch.toInstant();
      System.out.println("instant: " + instant);

      ZonedDateTime zonedDateTime = instant.atZone(ZoneId.of("UTC"));
      System.out.println("zonedDateTime: " + zonedDateTime);

      ZonedDateTime skipped = ZonedDateTime.of(LocalDate.of(2013, 3, 31),
            LocalTime.of(2, 30), ZoneId.of("Europe/Berlin")); // Constructs March 31 3:30
      System.out.println("skipped: " + skipped);

      ZonedDateTime ambiguous = ZonedDateTime.of(
            LocalDate.of(2013, 10, 27), // End of daylight savings time
            LocalTime.of(2, 30), ZoneId.of("Europe/Berlin"));
            // 2013-10-27T02:30+02:00[Europe/Berlin]
      ZonedDateTime anHourLater = ambiguous.plusHours(1);
            // 2013-10-27T02:30+01:00[Europe/Berlin]
      System.out.println("ambiguous: " + ambiguous);
      System.out.println("anHourLater: " + anHourLater);

      ZonedDateTime meeting = ZonedDateTime.of(LocalDate.of(2013, 10, 31),
            LocalTime.of(14, 30), ZoneId.of("America/Los_Angeles"));
      System.out.println("meeting: " + meeting);
      ZonedDateTime nextMeeting = meeting.plus(Duration.ofDays(7));
            // Caution! Won't work with daylight savings time
      System.out.println("nextMeeting: " + nextMeeting);
      nextMeeting = meeting.plus(Period.ofDays(7)); // OK
      System.out.println("nextMeeting: " + nextMeeting);
   }
}
```

### `java.time.ZonedDateTime` 8

| 方法 | 说明 |
|---|---|
| `static ZonedDateTime now()` | 获取当前的 ZonedDateTime。 |
| `static ZonedDateTime of(int year, int month, int dayOfMonth, int hour, int minute, int second, int nanoOfSecond, ZoneId zone)` |  |
| `static ZonedDateTime of(LocalDate date, LocalTime time, ZoneId zone)` |  |
| `static ZonedDateTime of(LocalDateTime localDateTime, ZoneId zone)` |  |
| `static ZonedDateTime ofInstant(Instant instant, ZoneId zone)` | 根据给定参数和时区生成一个 ZonedDateTime。 |
| `ZonedDateTime plus(plus\|minus)(Days\|Weeks\|Months\|Years\|Hours\|Minutes\|Seconds\|Nanos)(long number)` | 通过添加或减去给定数量的时间单位得到一个 ZonedDateTime。 |
| `ZonedDateTime plus(TemporalAmount amountToAdd)` |  |
| `ZonedDateTime minus(TemporalAmount amountToSubtract)` | 返回一个与此 ZonedDateTime 相差给定时间量的 ZonedDateTime。 |
| `ZonedDateTime with(DayOfMonth\|DayOfYear\|Month\|Year\|Hour\|Minute\|Second\|Nano)(int value)` | 返回一个新的 ZonedDateTime，其中给定的时间单位被指定值替换。 |
| `ZonedDateTime withZoneSameInstant(ZoneId zone)` |  |
| `ZonedDateTime withZoneSameLocal(ZoneId zone)` | 返回给定时区中的新 ZonedDateTime，可以表示相同的瞬间或相同的本地时间。 |
| `int getDayOfMonth()` | 获取月份中的日期（1 到 31）。 |
| `int getDayOfYear()` | 获取年份中的天数（1 到 366）。 |
| `DayOfWeek getDayOfWeek()` | 获取星期几，返回 DayOfWeek 枚举值。 |
| `Month getMonth()` |  |
| `int getMonthValue()` | 获取月份，返回 Month 枚举值或 1 到 12 的数字。 |
| `int getYear()` | 获取年份，介于 −999,999,999 和 999,999,999 之间。 |
| `int getHour()` | 获取小时（0 到 23）。 |
| `int getMinute()` |  |
| `int getSecond()` | 获取分钟或秒（0 到 59）。 |
| `int getNano()` | 获取纳秒（0 到 999,999,999）。 |
| `public ZoneOffset getOffset()` | 获取相对于 UTC 的偏移量。偏移量可以从 −12:00 到 +14:00。有些时区有非整小时偏移。偏移量会随夏令时改变。 |
| `LocalDate toLocalDate()` |  |
| `LocalTime toLocalTime()` |  |
| `LocalDateTime toLocalDateTime()` |  |
| `Instant toInstant()` | 返回本地日期、时间或日期时间，或对应的瞬间。 |
| `boolean isBefore(ChronoZonedDateTime other)` |  |
| `boolean isAfter(ChronoZonedDateTime other)` | 如果此带时区的日期/时间早于或晚于给定的带时区日期/时间，则返回 true。 |

## 6.6 格式化和解析

DateTimeFormatter 类提供了三种格式化器来打印日期/时间值：

- 预定义的标准格式化器（见表 6.1）
- 特定于语言环境的格式化器
- 具有自定义模式的格式化器

要使用标准格式化器之一，只需调用其 format 方法：

```java
String formatted = DateTimeFormatter.ISO_OFFSET_DATE_TIME.format(apollo11launch);
// 1969-07-16T09:32:00-04:00
```

标准格式化器主要用于机器可读的时间戳。要向人类读者呈现日期和时间，请使用特定于语言环境的格式化器。日期和时间都有四种样式：SHORT、MEDIUM、LONG 和 FULL——参见表 6.2。

### 表 6.1 预定义格式化器

| 格式化器 | 描述 | 示例 |
|---|---|---|
| `BASIC_ISO_DATE` | 不带分隔符的年、月、日和时区偏移 | `19690716-0500` |
| `ISO_LOCAL_DATE`, `ISO_LOCAL_TIME`, `ISO_LOCAL_DATE_TIME` | 分隔符 `-`、`:`、`T` | `1969-07-16`, `09:32:00`, `1969-07-16T09:32:00` |
| `ISO_OFFSET_DATE`, `ISO_OFFSET_TIME`, `ISO_OFFSET_DATE_TIME` | 类似 `ISO_LOCAL_XXX`，但带有时区偏移 | `1969-07-16-05:00`, `09:32:00-05:00`, `1969-07-16T09:32:00-05:00` |
| `ISO_ZONED_DATE_TIME` | 带有时区偏移和时区 ID | `1969-07-16T09:32:00-05:00[America/New_York]` |
| `ISO_INSTANT` | 以 UTC 表示，并由 `Z` 时区 ID 标识 | `1969-07-16T14:32:00Z` |
| `ISO_DATE`, `ISO_TIME`, `ISO_DATE_TIME` | 类似 `ISO_OFFSET_DATE`、`ISO_OFFSET_TIME` 和 `ISO_OFFSET_DATE_TIME`，但时区信息是可选的 | `1969-07-16-05:00`, `09:32:00-05:00`, `1969-07-16T09:32:00-05:00[America/New_York]` |
| `ISO_ORDINAL_DATE` | 年份和年内天序，适用于 `LocalDate` | `1969-197` |
| `ISO_WEEK_DATE` | 年份、周和星期几，适用于 `LocalDate` | `1969-W29-3` |
| `RFC_1123_DATE_TIME` | 电子邮件时间戳的标准，在 RFC 822 中定义，并在 RFC 1123 中更新为四位年份 | `Wed, 16 Jul 1969 09:32:00 -0500` |

静态方法 `ofLocalizedDate`、`ofLocalizedTime` 和 `ofLocalizedDateTime` 会创建这样的格式化器。例如：

```java
DateTimeFormatter formatter = DateTimeFormatter.ofLocalizedDateTime(FormatStyle.LONG);
String formatted = formatter.format(apollo11launch);
    // July 16, 1969 9:32:00 AM EDT
```

这些方法使用默认的语言环境。若要更改为其他语言环境，只需使用 `withLocale` 方法。

### 表 6.2 特定于语言环境的格式化样式

| 样式 | 日期 | 时间 |
|---|---|---|
| SHORT | 7/16/69 | 9:32 AM |
| MEDIUM | Jul 16, 1969 | 9:32:00 AM |
| LONG | July 16, 1969 | 9:32:00 AM EDT |
| FULL | Wednesday, July 16, 1969 | 9:32:00 AM EDT |

```java
formatted = formatter.withLocale(Locale.FRENCH).format(apollo11launch);
// 16 juillet 1969 09:32:00 EDT
```

DayOfWeek 和 Month 枚举具有 getDisplayName 方法，用于提供不同语言环境和格式下的星期和月份名称。

```java
for (DayOfWeek w : DayOfWeek.values())
    System.out.print(w.getDisplayName(TextStyle.SHORT, Locale.ENGLISH) + " ");
// Prints Mon Tue Wed Thu Fri Sat Sun
```

有关语言环境的更多信息，请参见第 7 章。

> **注意：** `java.time.format.DateTimeFormatter` 类旨在替代 `java.util.DateFormat`。如果为了向后兼容需要后者的实例，请调用 `formatter.toFormat()`。

最后，你可以通过指定模式来定制自己的日期格式。例如，

```java
formatter = DateTimeFormatter.ofPattern("E yyyy-MM-dd HH:mm");
```

将一个日期格式化为形如 Wed 1969-07-16 09:32 的形式。每个字母表示一个不同的时间字段，字母重复的次数选择特定的格式，这些规则晦涩难懂，似乎是随着时间有机发展而来的。表 6.3 展示了最有用的模式元素。

要从字符串解析日期/时间值，请使用静态 parse 方法之一。例如，

```java
LocalDate churchsBirthday = LocalDate.parse("1903-06-14");
ZonedDateTime apollo11launch =
    ZonedDateTime.parse("1969-07-16 03:32:00-0400",
        DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ssxx"));
```

第一个调用使用标准的 ISO_LOCAL_DATE 格式化器，第二个调用使用自定义格式化器。




### 表 6.3 日期/时间格式常用的格式符号

| ChronoField 或用途 | 示例 |
|---|---|
| ERA | G: AD, GGGG: Anno Domini, GGGGG: A |
| YEAR_OF_ERA | yy: 69, yyyy: 1969 |
| MONTH_OF_YEAR | M: 7, MM: 07, MMM: Jul, MMMM: July, MMMMM: J |
| DAY_OF_MONTH | d: 6, dd: 06 |
| DAY_OF_WEEK | e: 3, E: Wed, EEEE: Wednesday, EEEEE: W |
| HOUR_OF_DAY | H: 9, HH: 09 |
| CLOCK_HOUR_OF_AM_PM | K: 9, KK: 09 |
| AMPM_OF_DAY | a: AM |
| MINUTE_OF_HOUR | mm: 02 |
| SECOND_OF_MINUTE | ss: 00 |
| NANO_OF_SECOND | nnnnnn: 000000 |
| 时区 ID | VV: America/New_York |
| 时区名称 | z: EDT, zzzz: Eastern Daylight Time, v: ET, vvvv: Eastern Time |
| 时区偏移 | x: -04, xx: -0400, xxx: -04:00, XXX：相同，但零用 Z 表示 |
| 本地化时区偏移 | O: GMT-4, OOOO: GMT-04:00 |
| 修正儒略日 | g: 58243 |

清单 6.4 中的程序展示了如何格式化和解析日期与时间。

**清单 6.4** `formatting/Formatting.java`

```java
package formatting;

/**
 * @version 1.0 2016-05-10
 * @author Cay Horstmann
 */

import java.time.*;
import java.time.format.*;
import java.util.*;

public class Formatting
{
```

| `java.time.format.DateTimeFormatter` 8 | *(续)* |
|---|---|
| • `DateTimeFormatter withLocale(Locale locale)`<br>生成一个与此格式化器相等的格式化器，使用给定的区域设置。<br>• `static DateTimeFormatter ofPattern(String pattern)`<br>• `static DateTimeFormatter ofPattern(String pattern, Locale locale)`<br>生成使用给定模式和区域设置的格式化器。有关模式语法，请参见表 6.3。 | |

| `java.time.LocalDate` 8 |
|---|
| • `static LocalDate parse(CharSequence text)`<br>• `static LocalDate parse(CharSequence text, DateTimeFormatter formatter)`<br>使用默认格式化器或给定格式化器生成一个 LocalDate。 |

| `java.time.ZonedDateTime` 8 |
|---|
| • `static ZonedDateTime parse(CharSequence text)`<br>• `static ZonedDateTime parse(CharSequence text, DateTimeFormatter formatter)`<br>使用默认格式化器或给定格式化器生成一个 ZonedDateTime。 |

## 6.7 与遗留代码互操作

作为一个新创建的 API，Java 日期和时间 API 必须与现有类互操作——尤其是无处不在的 java.util.Date、java.util.GregorianCalendar 和 java.sql.Date/Time/Timestamp。

Instant 类与 java.util.Date 非常相似。在 Java 8 中，该类新增了两个方法：将 Date 转换为 Instant 的 toInstant 方法，以及执行相反转换的静态 from 方法。

类似地，ZonedDateTime 与 java.util.GregorianCalendar 非常相似，并且该类在 Java 8 中新增了转换方法。toZonedDateTime 方法将 GregorianCalendar 转换为 ZonedDateTime，而静态 from 方法执行相反的转换。

java.sql 包中的日期和时间类还提供了另一组转换。还可以将 DateTimeFormatter 传递给使用 java.text.Format 的遗留代码。表 6.4 总结了这些转换。

### 表 6.4 java.time 类与遗留类之间的转换

| 类 | 转换为遗留类 | 从遗留类转换 |
| --- | --- | --- |
| Instant<br>↔ java.util.Date | Date.from(instant) | date.toInstant() |
| ZonedDateTime<br>↔ java.util.GregorianCalendar | GregorianCalendar.from(zonedDateTime) | cal.toZonedDateTime() |
| Instant<br>↔ java.sql.Timestamp | Timestamp.from(instant) | timestamp.toInstant() |
| LocalDateTime<br>↔ java.sql.Timestamp | Timestamp.valueOf(localDateTime) | timestamp.toLocalDateTime() |
| LocalDate<br>↔ java.sql.Date | Date.valueOf(localDate) | date.toLocalDate() |
| LocalTime<br>↔ java.sql.Time | Time.valueOf(localTime) | time.toLocalTime() |
| DateTimeFormatter<br>→ java.text.DateFormat | formatter.toFormat() | 无 |
| java.util.TimeZone<br>↔ ZoneId | TimeZone.getTimeZone(id) | timeZone.toZoneId() |
| java.nio.file.attribute.FileTime<br>↔ Instant | FileTime.from(instant) | fileTime.toInstant() |

现在你已经知道如何使用 Java 8 日期和时间库处理世界各地的日期和时间值。下一章将进一步讨论面向国际受众的编程。你将看到如何以对客户有意义的方式格式化程序消息、数字和货币，无论他们身在何处。

*本页有意留白*

国际化程序所涉及的远不止 Unicode 支持。日期、时间、货币甚至数字在世界各地的格式都不同。你需要一种简单的方法来为不同语言配置菜单和按钮名称、消息字符串和键盘快捷键。

在本章中，我们将展示如何编写国际化的 Java 程序，以及如何本地化日期、时间、数字、文本和 GUI。我们将展示 Java 为编写国际化程序提供的工具。最后，我们将以一个完整示例结束本章——一个带有英语、德语和中文用户界面的退休计算器。

## 7.1 区域设置

当你看到一个适应国际市场的应用程序时，最明显的差异是语言。对于真正的国际化来说，这种观察实际上有些局限，因为国家之间可以共享一种共同语言，但你可能仍然需要做一些工作，才能让两个国家的计算机用户都满意。正如奥斯卡·王尔德的名言所说：“如今我们与美国确实一切共通，当然，语言除外。”

### 7.1.1 为什么需要区域设置？

当你提供程序的国际版本时，所有程序消息都需要翻译成当地语言。然而，仅仅翻译用户界面文本是不够的。还有许多更细微的差异——例如，数字在英语和德语中的格式就大不相同。数字

123,456.78

对德国用户应显示为

123.456,78

也就是说，小数点和小数逗号分隔符的角色被颠倒了。日期的显示也有类似变化。在美国，日期（多少有些不合理地）显示为月/日/年。德国使用更合理的日/月/年顺序，而在中国，用法是年/月/日。因此，日期

3/22/61

对德国用户应显示为

22.03.1961

当然，如果月份名称明确写出来，语言差异就会变得明显。英语的

March 22, 1961

在德语中应显示为

22. März 1961

或在中文中显示为

1961年3月22日

*区域设置* 捕获诸如此类的本地偏好。每当你呈现数字、日期、货币值以及其他格式因语言或地点而异的项目时，都需要使用区域设置感知 API。

### 7.1.2 指定区域设置

一个区域设置最多由五个部分组成：

- 1. 语言，由两到三个小写字母指定，例如 `en`（英语）、`de`（德语）或 `zh`（中文）。表 7.1 显示了常见代码。
- 2. 可选的文字系统，由四个字母指定，首字母大写，例如 `Latin`（拉丁文）、`Cyrl`（西里尔文）或 `Hant`（繁体汉字）。这很有用，因为某些语言（例如塞尔维亚语）使用拉丁字母或西里尔字母书写，而一些中文读者更喜欢繁体字而非简体字。
- 3. 可选的国家或地区，由两个大写字母或三位数字指定，例如 `US`（美国）或 `CH`（瑞士）。表 7.2 显示了常见代码。
- 4. 可选的变体，指定方言或拼写规则等杂项特征。变体如今很少使用。挪威语过去有一个“Nynorsk”变体，但现在用不同的语言代码 `nn` 表示。过去用于日本皇历和泰语数字的变体现在表示为扩展（见下一项）。
- 5. 可选的扩展。扩展描述了对日历（例如日本历法）、数字（泰语数字而非西方数字）等的本地偏好。Unicode 标准规定了其中一些扩展。扩展以 `u-` 开头，后跟一个两字母代码，指定该扩展涉及日历（`ca`）、数字（`nu`）等。例如，扩展 `u-nu-thai` 表示使用泰语数字。其他扩展完全是任意的，以 `x-` 开头，例如 `x-java`。





区域设置的规则由互联网工程任务组（IETF）的“最佳当前实践”备忘录 BCP 47 制定（http://tools.ietf.org/html/bcp47）。你可以在 www.w3.org/International/articles/language-tags 找到更通俗易懂的摘要。

#### 表 7.1 常用 ISO 639-1 语言代码

| 语言 | 代码 | 语言 | 代码 |
|---|---|---|---|
| 中文 | zh | 意大利语 | it |
| 丹麦语 | da | 日语 | ja |
| 荷兰语 | nl | 韩语 | ko |
| 英语 | en | 挪威语 | no |
| 法语 | fr | 葡萄牙语 | pt |
| 芬兰语 | fi | 西班牙语 | es |
| 德语 | de | 瑞典语 | sv |
| 希腊语 | el | 土耳其语 | tr |

#### 表 7.2 常用 ISO 3166-1 国家/地区代码

| 国家/地区 | 代码 | 国家/地区 | 代码 |
|---|---|---|---|
| 奥地利 | AT | 日本 | JP |
| 比利时 | BE | 韩国 | KR |
| 加拿大 | CA | 荷兰 | NL |
| 中国 | CN | 挪威 | NO |
| 丹麦 | DK | 葡萄牙 | PT |
| 芬兰 | FI | 西班牙 | ES |
| 德国 | DE | 瑞典 | SE |
| 英国 | GB | 瑞士 | CH |
| 希腊 | GR | 台湾 | TW |
| 爱尔兰 | IE | 土耳其 | TR |
| 意大利 | IT | 美国 | US |

语言和国家/地区代码看起来有些随意，因为其中一些源自当地语言。德语中的“德语”是 Deutsch，中文中的“中文”是 zhongwen：因此分别是 de 和 zh。而瑞士是 ch，源自拉丁语 *Confoederatio Helvetica*，意为瑞士联邦。

区域设置通过标签来描述——由区域设置元素组成的连字符字符串，例如 en-US。

在德国，你会使用区域设置 de-DE。瑞士有四种官方语言（德语、法语、意大利语和罗曼什语）。在瑞士的德语使用者会希望使用区域设置 de-CH。该区域设置使用德语规则，但货币值以瑞士法郎表示，而不是欧元。

如果只指定语言，比如 de，那么该区域设置不能用于特定国家/地区的问题，例如货币。

你可以像这样从标签字符串构造一个 `Locale` 对象：

```java
Locale usEnglish = Locale.forLanguageTag("en-US");
```

`toLanguageTag` 方法返回给定区域设置的语言标签。例如，`Locale.US.toLanguageTag()` 是字符串 `"en-US"`。

为方便起见，各种国家/地区都有预定义的区域设置对象：

```java
Locale.CANADA
Locale.CANADA_FRENCH
Locale.CHINA
Locale.FRANCE
Locale.GERMANY
Locale.ITALY
Locale.JAPAN
Locale.KOREA
Locale.PRC
Locale.TAIWAN
Locale.UK
Locale.US
```

许多预定义区域设置只指定语言而不指定位置：

```java
Locale.CHINESE
Locale.ENGLISH
Locale.FRENCH
Locale.GERMAN
Locale.ITALIAN
Locale.JAPANESE
Locale.KOREAN
Locale.SIMPLIFIED_CHINESE
Locale.TRADITIONAL_CHINESE
```

最后，静态 `getAvailableLocales` 方法返回虚拟机已知的所有区域设置组成的数组。

> **注意：** 你可以通过 `Locale.getISOLanguages()` 获取所有语言代码，并通过 `Locale.getISOCountries()` 获取所有国家/地区代码。

### 7.1.3 默认区域设置

`Locale` 类的静态 `getDefault` 方法最初获取本地操作系统存储的默认区域设置。你可以通过用不同的区域设置调用 `setDefault` 方法来更改默认的 Java 区域设置。

某些操作系统允许用户为显示消息和格式化指定不同的区域设置。例如，居住在美国的法语使用者可以使用法语菜单，但货币值以美元表示。

要获取这些首选项，请调用

```java
Locale displayLocale = Locale.getDefault(Locale.Category.DISPLAY);
Locale formatLocale = Locale.getDefault(Locale.Category.FORMAT);
```

> **注意：** 在 UNIX 中，你可以通过设置 `LC_NUMERIC`、`LC_MONETARY` 和 `LC_TIME` 环境变量，分别为数字、货币和日期指定不同的区域设置。Java 不会关注这些设置。

> **提示：** 如果你想测试一个只有语言和国家/地区设置的区域设置，可以在启动程序时在命令行中提供它们。例如，这里我们将默认区域设置设为 de-CH：
>
> ```bash
> java -Duser.language=de -Duser.region=CH MyProgram
> ```

### 7.1.4 显示名称

一旦有了区域设置，你能用它做什么？事实证明，起初并没有太多用途。`Locale` 类中唯一有用的方法是用于标识语言和国家/地区代码的方法。最重要的是 `getDisplayName`。它返回描述该区域设置的字符串。这个字符串不包含晦涩的双字母代码，而是采用可以呈现给用户的形式，例如

德语（瑞士）

实际上，这里有一个问题。显示名称是以默认区域设置生成的。这可能不合适。如果你的用户已经选择德语作为首选语言，你可能希望以德语呈现该字符串。你只需将德语区域设置作为参数传入即可。以下代码

```java
var loc = new Locale("de", "CH");
System.out.println(loc.getDisplayName(Locale.GERMAN));
```

打印出

Deutsch (Schweiz)

这个例子说明了为什么需要 Locale 对象。你将它们传给能感知区域设置的方法，这些方法会生成呈现给不同位置用户的文本。你将在后续章节中看到许多这样的例子。

> **警告：** 即使像将字符串转换为小写或大写这样普通的操作，也可能因区域设置而异。例如，在土耳其语区域设置中，字母 I 的小写形式是无点的 ı。那些试图通过将字符串存储为小写来规范化字符串的程序，在土耳其客户那里莫名其妙地失败了，因为在土耳其语中 I 和带点的 İ 没有相同的小写形式。最好始终使用接受 Locale 参数的 toUpperCase 和 toLowerCase 变体。例如，试试：
>
> ```java
> String cmd = "QUIT".toLowerCase(Locale.forLanguageTag("tr"));
> // "quıt" with a dotless ı
> ```
>
> 当然，在土耳其，Locale.getDefault() 得到的正是该区域设置，"QUIT".toLowerCase() 与 "quit" 并不相同。
>
> 如果你想将英语字符串规范化为小写，应该向 toLowerCase 方法传入英语区域设置。

> **注意：** 你可以显式设置输入和输出操作所使用的区域设置。
>
> - 从 `Scanner` 读取数字时，可以使用 `useLocale` 方法设置其区域设置。
> - `String.format` 和 `PrintWriter.printf` 方法可以选择接受一个 `Locale` 参数。

#### `java.util.Locale` 1.1

| 构造器/方法 | 描述 |
| --- | --- |
| `Locale(String language)`<br>`Locale(String language, String country)`<br>`Locale(String language, String country, String variant)` | 使用给定的语言、国家/地区和变体构造一个区域设置。在新代码中不要使用变体——请改用 IETF BCP 47 语言标签。 |
| `static Locale forLanguageTag(String languageTag)` 7 | 构造与给定语言标签对应的区域设置。 |
| `static Locale getDefault()` | 返回默认区域设置。 |
| `static void setDefault(Locale loc)` | 设置默认区域设置。 |
| `String getDisplayName()` | 返回描述该区域设置的名称，使用当前区域设置表示。 |
| `String getDisplayName(Locale loc)` | 返回描述该区域设置的名称，使用给定区域设置表示。 |
| `String getLanguage()` | 返回语言代码——一个小写的双字母 ISO 639 代码。 |
| `String getDisplayLanguage()` | 返回语言的名称，使用当前区域设置表示。 |
| `String getDisplayLanguage(Locale loc)` | 返回语言的名称，使用给定区域设置表示。 |
| `String getCountry()` | 返回国家/地区代码，作为大写的双字母 ISO 3166 代码。 |
| `static String[] getISOCountries()`<br>`static Set<String> getISOCountries(Locale.IsoCountryCode type)` 9 | 获取所有双字母国家/地区代码，或所有 2、3 或 4 个字母的国家/地区代码。类型是枚举常量 PART1_ALPHA2、PART1_ALPHA3 和 PART3 之一。 |
| `String getDisplayCountry()` | 返回国家/地区的名称，使用当前区域设置表示。 |
| `String getDisplayCountry(Locale loc)` | 返回国家/地区的名称，使用给定区域设置表示。 |
| `String toLanguageTag()` 7 | 返回此区域设置的 IETF BCP 47 语言标签，例如 "de-CH"。 |
| `String toString()` | 返回该区域设置的描述，其中语言和国家/地区用下划线分隔（例如 "de_CH"）。仅将此方法用于调试。 |




只需使用 `Number` 类的 `doubleValue` 方法即可获取包装的数值。

> **注意：** `Number` 类型的对象不会自动拆箱——你不能简单地将 `Number` 对象赋给基本类型。而应使用 `doubleValue` 或 `intValue` 方法。

如果数字文本的格式不正确，该方法会抛出 `ParseException`。例如，字符串中的前导空白是*不允许的*。（调用 `trim` 将其移除。）但是，字符串中数字后面的任何字符都会被直接忽略，因此不会抛出异常。

请注意，`getXxxInstance` 工厂方法所需的类实际上并不是 `NumberFormat` 类型。`NumberFormat` 类型是一个抽象类，实际的格式化器属于它的某个子类。工厂方法只是知道如何定位属于特定区域设置的对象。

可以使用静态 `getAvailableLocales` 方法获取当前受支持的区域设置列表。该方法返回一个区域设置数组，对于这些区域设置可以获取数字格式化器对象。

本节示例程序让你试验数字格式化器（参见图 7.1）。图顶部的组合框包含所有带有数字格式化器的区域设置。你可以在数字、货币和百分比格式化器之间进行选择。每次做出其他选择时，文本字段中的数字都会重新格式化。如果你浏览几个区域设置，就能很好地感受到数字或货币值可以被格式化的多种方式。你也可以输入不同的数字，并单击“Parse”按钮来调用 parse 方法，该方法会尝试解析你输入的内容。如果输入解析成功，它会被传递给 format，并显示结果。如果解析失败，文本字段中会显示“Parse error”消息。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_410_0.png)

**图 7.1** NumberFormatTest 程序

清单 7.1 中展示的代码相当直截了当。在构造函数中，我们调用 `NumberFormat.getAvailableLocales`。对于每个区域设置，我们调用 `getDisplayName`，并用 `getDisplayName` 方法返回的字符串填充组合框。（这些字符串未排序；我们将在第 402 页的 7.4 节“排序规则与规范化”中处理此问题。）每当用户选择另一个区域设置或单击某个单选按钮时，我们都会创建一个新的格式化器对象并更新文本字段。当用户单击 Parse 按钮时，我们调用 parse 方法，根据所选区域设置执行实际解析。

> **注意：** 可以使用 `Scanner` 读取本地化的整数和浮点数。调用 `useLocale` 方法设置区域设置。

#### 清单 7.1 `numberFormat/NumberFormatTest.java`

```java
package numberFormat;

import java.awt.*;
import java.awt.event.*;
import java.text.*;
import java.util.*;

import javax.swing.*;

/**
 * This program demonstrates formatting numbers under various locales.
 * @version 1.15 2010-05-01
 * @author Cay Horstmann
 */
public class NumberFormatTest
{
   public static void main(String[] args)
   {
      EventQueue.invokeLater(() ->
         {
            var frame = new NumberFormatFrame();
            frame.setTitle("NumberFormatTest");
            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            frame.setVisible(true);
         });
   }
}

/**
 * This frame contains radio buttons to select a number format, a combo box to pick a locale,
 * a text field to display a formatted number, and a button to parse the text field contents.
 */
```

#### 清单 7.1 *（续）*

```java
class NumberFormatFrame extends JFrame
{
   private Locale[] locales;
   private double currentNumber;
   private JComboBox<String> localeCombo = new JComboBox<>();
   private JButton parseButton = new JButton("Parse");
   private JTextField numberText = new JTextField(30);
   private JRadioButton numberRadioButton = new JRadioButton("Number");
   private JRadioButton currencyRadioButton = new JRadioButton("Currency");
   private JRadioButton percentRadioButton = new JRadioButton("Percent");
   private ButtonGroup rbGroup = new ButtonGroup();
   private NumberFormat currentNumberFormat;

   public NumberFormatFrame()
   {
      setLayout(new GridBagLayout());

      ActionListener listener = event -> updateDisplay();

      var p = new JPanel();
      addRadioButton(p, numberRadioButton, rbGroup, listener);
      addRadioButton(p, currencyRadioButton, rbGroup, listener);
      addRadioButton(p, percentRadioButton, rbGroup, listener);

      add(new JLabel("Locale:"), new GBC(0, 0).setAnchor(GBC.EAST));
      add(localeCombo, new GBC(1, 0).setFill(GBC.HORIZONTAL));
      add(p, new GBC(0, 1, 2, 1));
      add(parseButton, new GBC(0, 2).setInsets(2));
      add(numberText, new GBC(1, 2).setFill(GBC.HORIZONTAL));
      locales = (Locale[]) NumberFormat.getAvailableLocales().clone();
      Arrays.sort(locales, Comparator.comparing(Locale::getDisplayName));
      for (Locale loc : locales)
         localeCombo.addItem(loc.getDisplayName());
      localeCombo.setSelectedItem(Locale.getDefault().getDisplayName());
      currentNumber = 123456.78;
      updateDisplay();

      localeCombo.addActionListener(listener);

      parseButton.addActionListener(event ->
      {
         String s = numberText.getText().trim();
         try
         {
            Number n = currentNumberFormat.parse(s);
            currentNumber = n.doubleValue();
            updateDisplay();
         }
         catch (ParseException e)
         {
            numberText.setText(e.getMessage());
         }
      });
      pack();
   }

   /**
    * Adds a radio button to a container.
    * @param p the container into which to place the button
    * @param b the button
    * @param g the button group
    * @param listener the button listener
    */
   public void addRadioButton(Container p, JRadioButton b, ButtonGroup g,
         ActionListener listener)
   {
      b.setSelected(g.getButtonCount() == 0);
      b.addActionListener(listener);
      g.add(b);
      p.add(b);
   }

   /**
    * Updates the display and formats the number according to the user settings.
    */
   public void updateDisplay()
   {
      Locale currentLocale = locales[localeCombo.getSelectedIndex()];
      currentNumberFormat = null;
      if (numberRadioButton.isSelected())
         currentNumberFormat = NumberFormat.getNumberInstance(currentLocale);
      else if (currencyRadioButton.isSelected())
         currentNumberFormat = NumberFormat.getCurrencyInstance(currentLocale);
      else if (percentRadioButton.isSelected())
         currentNumberFormat = NumberFormat.getPercentInstance(currentLocale);
      String formatted = currentNumberFormat.format(currentNumber);
      numberText.setText(formatted);
   }
}
```

| java.text.NumberFormat | 1.1 |
|---|---|
| • `static Locale[] getAvailableLocales()` | 返回一个 Locale 对象数组，对于这些对象可获取 NumberFormat 格式化器。 |

### 7.2.2 货币

要格式化货币值，可以使用 `NumberFormat.getCurrencyInstance` 方法。然而，该方法不是很灵活——它返回针对单一货币的格式化器。假设你为一位美国客户准备发票，其中一些金额是美元，另一些是欧元。你不能只使用两个格式化器：

```
NumberFormat dollarFormatter = NumberFormat.getCurrencyInstance(Locale.US);
NumberFormat euroFormatter = NumberFormat.getCurrencyInstance(Locale.GERMANY);
```

你的发票会看起来很奇怪，有些值显示为 $100,000，而另一些显示为 10.000 €。（注意，欧元值使用小数点，而不是逗号。）

相反，应使用 Currency 类来控制格式化器使用的货币。你可以通过将货币标识符传递给静态 `Currency.getInstance` 方法来获取 Currency 对象。然后为每个格式化器调用 `setCurrency` 方法。以下是为你的美国客户设置欧元格式化器的方法：

```
NumberFormat euroFormatter = NumberFormat.getCurrencyInstance(Locale.US);
euroFormatter.setCurrency(Currency.getInstance("EUR"));
```

货币标识符由 ISO 4217 定义（参见 https://www.iso.org/iso-4217-currency-codes.html）。表 7.3 提供了部分列表。

**表 7.3** 货币标识符

| 货币值 | 标识符 | 数字代码 |
|---|---|---:|
| 美元 | USD | 840 |
| 欧元 | EUR | 978 |
| 英镑 | GBP | 826 |
| 日元 | JPY | 392 |
| 人民币（元） | CNY | 156 |
| 印度卢比 | INR | 356 |
| 俄罗斯卢布 | RUB | 643 |



#### java.util.Currency

1.4

- `static Currency getInstance(String currencyCode)`
- `static Currency getInstance(Locale locale)`
  - 返回给定 ISO 4217 货币代码或给定区域设置所属国家/地区的 Currency 实例。
- `String toString()`
- `String getCurrencyCode()`
- `int getNumericCode()` 7
- `String getNumericCodeAsString()` 9
  - 获取此货币的 ISO 4217 字母或数字货币代码。
- `String getSymbol()`
- `String getSymbol(Locale locale)`
  - 获取此货币在默认区域设置或给定区域设置下的格式符号。例如，USD 的符号可以是 "$" 或 "US$"，具体取决于区域设置。
- `int getDefaultFractionDigits()`
  - 获取此货币的默认小数位数。
- `static Set<Currency> getAvailableCurrencies()` 7
  - 获取所有可用货币。

## 7.3 日期和时间

格式化日期和时间时，应注意四个与区域设置相关的问题：

- 月份和工作日的名称应使用当地语言表示。
- 年、月、日的顺序存在本地偏好。
- 表达日期时，公历可能不是当地偏好的历法。
- 必须考虑所在地点的时区。

`java.time` 包中的 `DateTimeFormatter` 类可处理这些问题。从表 7.4 所示的格式样式中选择一种。然后获取一个格式化器：

```java
FormatStyle style = ...; // One of FormatStyle.SHORT, FormatStyle.MEDIUM, ...
DateTimeFormatter dateFormatter = DateTimeFormatter.ofLocalizedDate(style);
DateTimeFormatter timeFormatter = DateTimeFormatter.ofLocalizedTime(style);
```

```java
DateTimeFormatter dateTimeFormatter = DateTimeFormatter.ofLocalizedDateTime(style);
    // or DateTimeFormatter.ofLocalizedDateTime(style, style2)
```

这些格式化器使用当前区域设置。要使用其他区域设置，请使用 `withLocale` 方法：

```java
DateTimeFormatter dateTimeFormatter =
    DateTimeFormatter.ofLocalizedDateTime(style).withLocale(locale);
```

现在可以格式化 `LocalDate`、`LocalDateTime`、`LocalTime` 或 `ZonedDateTime`：

```java
ZonedDateTime appointment = . . .;
String formatted = formatter.format(appointment);
```

### 表 7.4 日期和时间格式样式

| 样式 | 日期 | 时间 |
|---|---|---|
| SHORT | 7/16/69 | 9:32 AM |
| MEDIUM | Jul 16, 1969 | 9:32:00 AM |
| LONG | July 16, 1969 | 在 en-US 中为 9:32:00 AM EDT，在 de-DE 中为 9:32:00 MESZ（仅适用于 ZonedDateTime） |
| FULL | Wednesday, July 16, 1969 | 在 en-US 中为 9:32:00 AM EDT，在 de-DE 中为 9:32 Uhr MESZ（仅适用于 ZonedDateTime） |

> **注意：** 这里我们使用 `java.time` 包中的 `DateTimeFormatter` 类。还有一个来自 Java 1.1 的遗留 `java.text.DateFormat` 类，可用于 `Date` 和 `Calendar` 对象。

可以使用 `LocalDate`、`LocalDateTime`、`LocalTime` 或 `ZonedDateTime` 的某个静态 `parse` 方法，解析字符串中的日期或时间：

```java
LocalTime time = LocalTime.parse("9:32 AM", formatter);
```

这些方法不适合解析人工输入，至少在没有预处理的情况下不适合。例如，美国使用的短时间格式化器会解析 "9:32 AM"，但不会解析 "9:32am" 或 "9:32 am"。

> **警告：** 日期格式化器会解析不存在的日期，例如 11 月 31 日，并将其调整为给定月份的最后一天。

有时，你只需要显示工作日和月份的名称，例如在日历应用中。请调用 `DayOfWeek` 和 `Month` 枚举的 `getDisplayName` 方法。

```java
for (Month m : Month.values())
    System.out.println(m.getDisplayName(textStyle, locale) + " ");
```

表 7.5 显示了文本样式。STANDALONE 版本用于在格式化日期之外显示。例如，在芬兰语中，一月在日期内为“tammikuuta”，而单独使用时为“tammikuu”。

### 表 7.5 `java.time.format.TextStyle` 枚举的值

| 样式 | 示例 |
|---|---|
| FULL / FULL_STANDALONE | 一月 |
| SHORT / SHORT_STANDALONE | 1月 |
| NARROW / NARROW_STANDALONE | J |

> **注意：** 一周的第一天可以是星期六、星期日或星期一，具体取决于区域设置。可以这样获取：

```java
DayOfWeek first = WeekFields.of(locale).getFirstDayOfWeek();
```

代码清单 7.2 展示了 `DateFormat` 类的实际应用。你可以选择一个区域设置，查看世界各地如何格式化日期和时间。图 7.2 显示了该程序（在安装中文字体之后）。如你所见，它正确显示了输出。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_418_0.png)

**图 7.2** DateFormatTest 程序

你还可以试验解析。输入日期、时间或日期/时间，然后单击“Parse”按钮。

我们使用一个辅助类 `EnumCombo` 来解决一个技术问题（见代码清单 7.3）。我们希望用 Short、Medium 和 Long 等值填充一个组合框，然后自动将用户的选择转换为 `FormatStyle.SHORT`、`FormatStyle.MEDIUM` 和 `FormatStyle.LONG` 值。我们没有编写重复代码，而是使用反射：将用户的选择转换为大写，将所有空格替换为下划线，然后查找具有该名称的静态字段的值。（有关反射的更多细节，请参见第 I 卷第 5 章。）

### 代码清单 7.2 DateFormat/DateTimeFormatterTest.java

```java
package dateformat;

import java.awt.*;
import java.awt.event.*;
import java.time.*;
import java.time.format.*;
import java.util.*;

import javax.swing.*;

/**
 * This program demonstrates formatting dates under various locales.
 * @version 1.01 2018-05-01
 * @author Cay Horstmann
 */
public class DateTimeFormatterTest
{
   public static void main(String[] args)
   {
      EventQueue.invokeLater(() ->
         {
            var frame = new DateTimeFormatterFrame();
            frame.setTitle("DateFormatTest");
            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            frame.setVisible(true);
         });
   }
}

/**
 * This frame contains combo boxes to pick a locale, date and time formats,
 * text fields to display formatted date and time, and
 * buttons to parse the text field contents.
 */
class DateTimeFormatterFrame extends JFrame
{
   private Locale[] locales;
   private LocalDate currentDate;
   private LocalTime currentTime;
   private ZoneId currentZone;
   private ZonedDateTime currentDateTime;
   private DateTimeFormatter currentDateFormat;
   private DateTimeFormatter currentTimeFormat;
   private DateTimeFormatter currentDateTimeFormat;
   private JComboBox<String> localeCombo = new JComboBox<>();
   private JButton dateParseButton = new JButton("Parse");
   private JButton timeParseButton = new JButton("Parse");
   private JButton dateTimeParseButton = new JButton("Parse");
   private JTextField dateText = new JTextField(30);
   private JTextField timeText = new JTextField(30);
   private JTextField dateTimeText = new JTextField(30);
   private EnumCombo<FormatStyle> dateStyleCombo = new EnumCombo<>(FormatStyle.class,
      "Short", "Medium", "Long", "Full");
   private EnumCombo<FormatStyle> timeStyleCombo = new EnumCombo<>(FormatStyle.class,
      "Short", "Medium");
   private EnumCombo<FormatStyle> dateTimeStyleCombo = new EnumCombo<>(FormatStyle.class,
      "Short", "Medium", "Long", "Full");

   public DateTimeFormatterFrame()
   {
      setLayout(new GridBagLayout());
      add(new JLabel("Locale"), new GBC(0, 0).setAnchor(GBC.EAST));
      add(localeCombo, new GBC(1, 0, 1, 1).setAnchor(GBC.WEST));

      add(new JLabel("Date"), new GBC(0, 1).setAnchor(GBC.EAST));
      add(dateStyleCombo, new GBC(1, 1).setAnchor(GBC.WEST));
      add(dateText, new GBC(2, 1, 1, 1).setFill(GBC.HORIZONTAL));
      add(dateParseButton, new GBC(4, 1).setAnchor(GBC.WEST));

      add(new JLabel("Time"), new GBC(0, 2).setAnchor(GBC.EAST));
      add(timeStyleCombo, new GBC(1, 2).setAnchor(GBC.WEST));
      add(timeText, new GBC(2, 2, 1, 1).setFill(GBC.HORIZONTAL));
      add(timeParseButton, new GBC(4, 2).setAnchor(GBC.WEST));

      add(new JLabel("Date and time"), new GBC(0, 3).setAnchor(GBC.EAST));
      add(dateTimeStyleCombo, new GBC(1, 3).setAnchor(GBC.WEST));
      add(dateTimeText, new GBC(2, 3, 2, 1).setFill(GBC.HORIZONTAL));
      add(dateTimeParseButton, new GBC(4, 3).setAnchor(GBC.WEST));

      locales = (Locale[]) Locale.getAvailableLocales().clone();
      Arrays.sort(locales, Comparator.comparing(Locale::getDisplayName));
      for (Locale loc : locales)
         localeCombo.addItem(loc.getDisplayName());
      localeCombo.setSelectedItem(Locale.getDefault().getDisplayName());
      currentDate = LocalDate.now();
      currentTime = LocalTime.now();
      currentDateTime = ZonedDateTime.now();
      updateDisplay();

      ActionListener listener = event -> updateDisplay();
      localeCombo.addActionListener(listener);
      dateStyleCombo.addActionListener(listener);
      timeStyleCombo.addActionListener(listener);
```

### 清单 7.2（续）

```java
dateTimeStyleCombo.addActionListener(listener);

addAction(dateParseButton, () ->
{
    currentDate = LocalDate.parse(dateText.getText().trim(), currentDateFormat);
});
addAction(timeParseButton, () ->
{
    currentTime = LocalTime.parse(timeText.getText().trim(), currentTimeFormat);
});
addAction(dateTimeParseButton, () ->
{
    currentDateTime = ZonedDateTime.parse(
        dateTimeText.getText().trim(), currentDateTimeFormat);
});

pack();
}

/**
 * Adds the given action to the button and updates the display upon completion.
 * @param button the button to which to add the action
 * @param action the action to carry out when the button is clicked
 */
public void addAction(JButton button, Runnable action)
{
    button.addActionListener(event ->
    {
        try
        {
            action.run();
            updateDisplay();
        }
        catch (Exception e)
        {
            JOptionPane.showMessageDialog(null, e.getMessage());
        }
    });
}

/**
 * Updates the display and formats the date according to the user settings.
 */
public void updateDisplay()
{
    Locale currentLocale = locales[localeCombo.getSelectedIndex()];
    FormatStyle dateStyle = dateStyleCombo.getValue();
    currentDateFormat = DateTimeFormatter.ofLocalizedDate(
        dateStyle).withLocale(currentLocale);
    dateText.setText(currentDateFormat.format(currentDate));
    FormatStyle timeStyle = timeStyleCombo.getValue();
    currentTimeFormat = DateTimeFormatter.ofLocalizedTime(
        timeStyle).withLocale(currentLocale);
    timeText.setText(currentTimeFormat.format(currentTime));
    FormatStyle dateTimeStyle = dateTimeStyleCombo.getValue();
    currentDateTimeFormat = DateTimeFormatter.ofLocalizedDateTime(
        dateTimeStyle).withLocale(currentLocale);
    dateTimeText.setText(currentDateTimeFormat.format(currentDateTime));
}
```

### 清单 7.3 dateFormat/EnumCombo.java

```java
package dateFormat;

import java.util.*;
import javax.swing.*;

/**
 * A combo box that lets users choose from among static field
 * values whose names are given in the constructor.
 * @version 1.15 2016-05-06
 * @author Cay Horstmann
 */
public class EnumCombo<T> extends JComboBox<String>
{
   private Map<String, T> table = new TreeMap<>();

   /**
    * Constructs an EnumCombo yielding values of type T.
    * @param cl a class
    * @param labels an array of strings describing static field names
    * of cl that have type T
    */
   public EnumCombo(Class<?> cl, String... labels)
   {
      for (String label : labels)
      {
         String name = label.toUpperCase().replace(' ', '_');
         try
         {
            java.lang.reflect.Field f = cl.getField(name);
            @SuppressWarnings("unchecked") T value = (T) f.get(cl);
            table.put(label, value);
         }
         catch (Exception e)
         {
            label = "(" + label + ")";
            table.put(label, null);
         }
         addItem(label);
      }
      setSelectedItem(labels[0]);
   }

   /**
    * Returns the value of the field that the user selected.
    * @return the static field value
    */
   public T getValue()
   {
      return table.get(getSelectedItem());
   }
}
```

| java.time.format.DateTimeFormatter 8 |
| --- |
| • `static DateTimeFormatter ofLocalizedDate(FormatStyle dateStyle)`<br>• `static DateTimeFormatter ofLocalizedTime(FormatStyle dateStyle)`<br>• `static DateTimeFormatter ofLocalizedDateTime(FormatStyle dateTimeStyle)`<br>• `static DateTimeFormatter ofLocalizedDateTime(FormatStyle dateStyle, FormatStyle timeStyle)`<br>&nbsp;&nbsp;返回使用指定样式格式化日期、时间或日期和时间的 DateTimeFormatter 实例。<br>• `DateTimeFormatter withLocale(Locale locale)`<br>&nbsp;&nbsp;返回具有给定区域设置的此格式化器的副本。<br>• `String format(TemporalAccessor temporal)`<br>&nbsp;&nbsp;返回格式化给定日期/时间后得到的字符串。 |

| java.time.LocalDate 8<br>java.time.LocalTime 8<br>java.time.LocalDateTime 8<br>java.time.ZonedDateTime 8 |
| --- |
| • `static Xxx parse(CharSequence text, DateTimeFormatter formatter)`<br>&nbsp;&nbsp;解析给定字符串，并返回其中描述的 LocalDate、LocalTime、LocalDateTime 或 ZonedDateTime。如果解析不成功，则抛出 DateTimeParseException。 |

## 7.4 排序规则与规范化

大多数程序员都知道如何使用 String 类的 `compareTo` 方法比较字符串。遗憾的是，在与人类用户交互时，这个方法并不十分有用。`compareTo` 方法使用字符串的 UTF-16 编码值，这会导致荒谬的结果，即使在英语中也是如此。例如，下面五个字符串按照 `compareTo` 方法排序为：

- America
- Zulu
- able
- zebra
- Ångström

对于字典顺序，你会希望将大写和小写视为等价。对于英语使用者来说，示例单词列表将排序为

- able
- America
- Ångström
- zebra
- Zulu

然而，这个顺序对瑞典用户来说是不可接受的。在瑞典语中，字母 Å 与字母 A 不同，并且它排在字母 Z 之后！也就是说，瑞典用户希望这些单词排序为

- able
- America
- zebra
- Zulu
- Ångström

要获得区域设置敏感的比较器，请调用静态 `Collator.getInstance` 方法：

```java
Collator coll = Collator.getInstance(locale);
words.sort(coll); // Collator implements Comparator<Object>
```

由于 Collator 类实现了 Comparator 接口，你可以将 Collator 对象传递给 List.sort(Comparator) 方法，以对字符串列表进行排序。

排序器还有一些高级设置。你可以设置排序器的强度，以选择它应该有多强的区分性。字符差异分为主级、次级或三级。例如，在英语中，“A”和“Z”之间的差异被视为主级，“A”和“Ä”之间的差异被视为次级，“A”和“a”之间的差异被视为三级。

通过将排序器的强度设置为 `Collator.PRIMARY`，你告诉它只关注主级差异。通过将强度设置为 `Collator.SECONDARY`，你指示排序器考虑次级差异。也就是说，当强度设置为“次级”或“三级”时，两个字符串更有可能被视为不同，如表 7.6 所示。

**表 7.6** 不同强度的排序规则（英语区域设置）

| 主级 | 次级 | 三级 |
|---|---|---|
| Angstrom = Ångström | Angstrom ≠ Ångström | Angstrom ≠ Ångström |
| Able = able | Able = able | Able ≠ able |

当强度设置为 `Collator.IDENTICAL` 时，不允许任何差异。这个设置主要与一个相当技术性的排序器设置——*分解模式*——结合使用时有用，我们接下来会讨论它。

有时，一个字符或字符序列在 Unicode 中可以用不止一种方式描述。例如，“Å”可以是 Unicode 字符 U+00C5，也可以表示为一个普通“A”（U+0041）后跟一个 ◦（“组合上环”；U+030A）。也许更令人惊讶的是，字母序列“ffi”可以用单个字符“Latin small ligature ffi”来描述，其代码为 U+FB03。（有人可能会争辩说，这是一个表示问题，不应导致不同的 Unicode 字符，但规则不是我们定的。）

Unicode 标准为字符串定义了四种*规范化形式*（D、KD、C 和 KC）。详情请参见 www.unicode.org/versions/reports/tr15/tr15-23.html。在规范化形式 C 中，带重音字符总是被组合。例如，A 和组合上环 ◦ 的序列会组合成单个字符 Å。在形式 D 中，带重音字符总是被分解为基本字母和组合重音；Å 会变成 A 后跟 ◦。形式 KC 和 KD 还会分解连字或商标符号等字符。

你可以选择希望排序器使用的规范化程度。值 `Collator.NO_DECOMPOSITION` 完全不对字符串进行规范化。这个选项更快，但对于以多种形式表示字符的文本可能不合适。默认值 `Collator.CANONICAL_DECOMPOSITION` 使用规范化形式 D。这对于包含重音但不包含连字的文本很有用。最后，“完全分解”使用规范化形式 KD。示例见表 7.7。





### 表7.7 分解模式之间的差异

| 不分解 | 规范分解 | 完全分解 |
|---|---|---|
| Ä ≠ Å | Ä = Å | Ä = Å |
| ™ ≠ TM | ™ ≠ TM | ™ = TM |

让排序器多次分解一个字符串是非常浪费的。如果一个字符串要与其他字符串进行多次比较，可以将分解结果保存在一个排序键对象中。`getCollationKey` 方法返回一个 `CollationKey` 对象，可用于后续更快速的比较。下面是一个示例：

```java
String a = "...";
CollationKey aKey = coll.getCollationKey(a);
if (aKey.compareTo(coll.getCollationKey(b)) == 0) // fast comparison
    ...
```

最后，即使不进行排序，你可能也希望将字符串转换为其规范化形式——例如，将字符串存储到数据库中，或与另一个程序通信。`java.text.Normalizer` 类可以执行规范化过程。例如，

```java
String name = "Ångström";
String normalized = Normalizer.normalize(name, Normalizer.Form.NFD); // uses normalization
                                                                  // form D
```

规范化后的字符串包含十个字符。“Å”和“ö”被替换为“Å”和“ö”序列。

然而，这通常不是存储和传输的最佳形式。规范化形式 C 首先应用分解，然后以标准化顺序将重音符号重新组合。根据 W3C 的建议，这是通过互联网传输数据的推荐模式。

清单7.4中的程序让你可以试验排序顺序。在文本字段中输入一个单词，并点击“Add”按钮将其添加到单词列表中。每次你添加另一个单词，或者更改区域设置、强度或分解模式，单词列表都会重新排序。= 号表示被视为相同的单词（参见图7.3）。

组合框中的区域设置名称按排序顺序显示，使用默认区域设置的排序器。如果你使用美国英语区域设置运行此程序，你会注意到“Norwegian (Nynorsk)”排在“Norwegian (Norway)”之前，尽管逗号字符的 Unicode 值大于右括号的 Unicode 值。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_427_0.png)

**图7.3** CollationTest 程序

### 清单7.4 `collation/CollationTest.java`

```java
package collation;

import java.awt.*;
import java.awt.event.*;
import java.text.*;
import java.util.*;
import java.util.List;

import javax.swing.*;

/**
 * This program demonstrates collating strings under various locales.
 * @version 1.10 2018-05-01
 * @author Cay Horstmann
 */
public class CollationTest
{
    public static void main(String[] args)
    {
        EventQueue.invokeLater(() ->
        {
            var frame = new CollationFrame();
            frame.setTitle("Collation Test");
            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            frame.setVisible(true);
        });
    }

    /**
     * This frame contains combo boxes to pick a locale, collation strength and decomposition
     * rules, a text field and button to add new strings, and a text area to list the collated
     * strings.
     */
    class CollationFrame extends JFrame
    {
        private Collator collator = Collator.getInstance(Locale.getDefault());
        private List<String> strings = new ArrayList<>();
        private Collator currentCollator;
        private Locale[] locales;
        private JComboBox<String> localeCombo = new JComboBox<>();
        private JTextField newWord = new JTextField(20);
        private JTextArea sortedWords = new JTextArea(20, 20);
        private JButton addButton = new JButton("Add");
        private EnumCombo<Integer> strengthCombo = new EnumCombo<>(Collator.class, "Primary",
                "Secondary", "Tertiary", "Identical");
        private EnumCombo<Integer> decompositionCombo = new EnumCombo<>(Collator.class,
                "Canonical Decomposition", "Full Decomposition", "No Decomposition");

        public CollationFrame()
        {
            setLayout(new GridBagLayout());
            add(new JLabel("Locale"), new GBC(0, 0).setAnchor(GBC.EAST));
            add(new JLabel("Strength"), new GBC(0, 1).setAnchor(GBC.EAST));
            add(new JLabel("Decomposition"), new GBC(0, 2).setAnchor(GBC.EAST));
            add(addButton, new GBC(0, 3).setAnchor(GBC.EAST));
            add(localeCombo, new GBC(1, 0).setAnchor(GBC.WEST));
            add(strengthCombo, new GBC(1, 1).setAnchor(GBC.WEST));
            add(decompositionCombo, new GBC(1, 2).setAnchor(GBC.WEST));
            add(newWord, new GBC(1, 3).setFill(GBC.HORIZONTAL));
            add(new JScrollPane(sortedWords), new GBC(0, 4, 2, 1).setFill(GBC.BOTH));

            locales = (Locale[]) Collator.getAvailableLocales().clone();
            Arrays.sort(locales,
                    (l1, l2) -> collator.compare(l1.getDisplayName(), l2.getDisplayName()));

            for (Locale loc : locales)
                localeCombo.addItem(loc.getDisplayName());
            localeCombo.setSelectedItem(Locale.getDefault().getDisplayName());

            strings.add("America");
            strings.add("able");
            strings.add("Zulu");
            strings.add("zebra");
            strings.add("\u00c5ngstr\u00f6m");
            strings.add("A\u030angstr\u00f6m");
            strings.add("Angstrom");
            strings.add("Able");
            strings.add("office");
            strings.add("o\uFB03ce");
            strings.add("Java\u2122");
            strings.add("Java™");
            updateDisplay();

            addButton.addActionListener(event ->
                {
                    strings.add(newWord.getText());
                    updateDisplay();
                });

            ActionListener listener = event -> updateDisplay();

            localeCombo.addActionListener(listener);
            strengthCombo.addActionListener(listener);
            decompositionCombo.addActionListener(listener);
            pack();
        }

        /**
         * Updates the display and collates the strings according to the user settings.
         */
        public void updateDisplay()
        {
            Locale currentLocale = locales[localeCombo.getSelectedIndex()];
            localeCombo.setLocale(currentLocale);

            currentCollator = Collator.getInstance(currentLocale);
            currentCollator.setStrength(strengthCombo.getValue());
            currentCollator.setDecomposition(decompositionCombo.getValue());

            strings.sort(currentCollator);

            sortedWords.setText("");

            for (int i = 0; i < strings.size(); i++)
            {
                String s = strings.get(i);
                if (i > 0 && s.compareToIgnoreCase(strings.get(i - 1)) == 0)
                    sortedWords.append("=");
                sortedWords.append(s + "\n");
            }
            pack();
        }
    }
}
```

### `java.text.Collator` 1.1

- `static Locale[] getAvailableLocales()`  
  返回一个 Locale 对象数组，这些 Locale 对象具有可用的 Collator 对象。
- `static Collator getInstance()`
- `static Collator getInstance(Locale l)`  
  为默认区域设置或给定区域设置返回一个排序器。
- `int compare(String a, String b)`  
  如果 a 在 b 之前，返回负值；如果它们被视为相同，返回 0；否则返回正值。
- `boolean equals(String a, String b)`  
  如果 a 和 b 被视为相同，返回 true；否则返回 false。
- `void setStrength(int strength)`
- `int getStrength()`  
  设置或获取排序器的强度。更强的排序器能区分更多单词。强度值为 `Collator.PRIMARY`、`Collator.SECONDARY` 和 `Collator.TERTIARY`。
- `void setDecomposition(int decomp)`
- `int getDecomposition()`  
  设置或获取排序器的分解模式。排序器对字符串的分解越充分，在判断两个字符串是否应被视为相同方面就越严格。分解值为 `Collator.NO_DECOMPOSITION`、`Collator.CANONICAL_DECOMPOSITION` 和 `Collator.FULL_DECOMPOSITION`。
- `CollationKey getCollationKey(String a)`  
  返回一个排序键，其中包含字符的分解形式，可以快速地与另一个排序键进行比较。

**注意：** 这个示例表明选择格式的设计者有点糊涂。如果你有三个格式字符串，你需要两个限制来分隔它们。一般来说，需要的限制数量比格式字符串数量少一个。正如你在表7.8中看到的，`MessageFormat` 类会忽略第一个限制。

如果这个类的设计者意识到限制应该位于选项之间，语法就会清晰得多，例如

```text
no houses|1|one house|2{1} houses // not the actual format
```

你可以使用 `<` 符号来表示：如果下界严格小于值，则选择该选项。

你也可以使用 ≤ 符号（表示为 Unicode 字符代码 `\u2264`）作为 `#` 的同义词。如果你愿意，甚至可以为第一个值指定下界为 −∞，写作 `-\u221E`。

例如，

```text
-∞#no houses|0#one house|2<{1} houses
```

或者，使用 Unicode 转义：

```text
-\u221E\u2264no houses|0\u2264one house|2<{1} houses
```

让我们完成自然灾难场景。如果将选择字符串放在原始消息字符串中，我们会得到以下格式指令：

```java
String pattern = "On {2,date,long}, {0} destroyed {1,choice,0#no houses|1#one house|2<{1}
  houses}" + " and caused {3,number,currency} of damage.";
```

或者，用德语：

```java
String pattern
    = "{0} zerstörte am {2,date,long} {1,choice,0#kein Haus|1#ein Haus|2#{1} Häuser}"
      + " und richtete einen Schaden von {3,number,currency} an.";
```

请注意，德语中的单词顺序有所不同，但传递给 format 方法的对象数组是相同的。格式字符串中占位符的顺序处理了单词顺序的变化。

## 7.6 文本输入与输出

如你所知，Java 编程语言本身完全基于 Unicode。然而，Windows 和 Mac OS X 仍然支持传统字符编码，例如西欧国家的 Windows-1252 或 Mac Roman，台湾地区的 Big5。因此，通过文本与用户交流是


并不像它本应的那样简单。以下各节讨论你可能遇到的复杂情况。

### 7.6.1 文本文件

如今，保存和加载文本文件最好使用 UTF-8。但你可能需要处理旧式文件。如果你知道预期的字符编码，可以在写入或读取文本文件时指定它：

```
var out = new PrintWriter(filename, "Windows-1252");
```

要猜测应使用的最佳编码，可以调用以下方法获取“平台编码”：

```
Charset platformEncoding = Charset.defaultCharset();
```

### 7.6.2 行尾

这不是区域设置的问题，而是平台的问题。在 Windows 上，文本文件每行末尾预期使用 \r\n，而基于 UNIX 的系统只需要 \n 字符。如今，大多数 Windows 程序可以只处理 \n。值得注意的例外是记事本。如果用户能够双击你的应用程序生成的文本文件并在记事本中查看它，对你来说很重要，那么请确保该文本文件具有正确的行尾。

用 println 方法写入的任何行都会被正确终止。唯一的问题是你打印的字符串中包含 \n 字符。它们不会自动修改为平台的行尾。

除了在字符串中使用 \n，你还可以使用 printf 和 %n 格式说明符来生成依赖于平台的行尾。例如，

```
out.printf("Hello%nWorld%n");
```

在 Windows 上会生成

```
Hello\r\nWorld\r\n
```

在其他所有地方会生成

```
Hello\nWorld\n
```

### 7.6.3 控制台

如果你编写通过 System.in/System.out 或 System.console() 与用户通信的程序，就必须面对一种可能性：控制台使用的字符编码可能不同于 `Charset.defaultCharset()` 所报告的平台编码。在 Windows 上使用 cmd shell 时，这一点尤其明显。

在美国版 Windows 10 中，命令 shell 仍使用古老的 IBM437 编码，这种编码起源于 1982 年的 IBM 个人计算机。没有官方 API 可以揭示该信息。`Charset.defaultCharset()` 方法将返回 Windows-1252 字符集，这与前者相当不同。例如，欧元符号 € 存在于 Windows-1252 中，但不存在于 IBM437 中。当你调用

```
System.out.println("100 €");
```

时，控制台将显示

```
100 ?
```

你可以建议用户切换控制台的字符编码。在 Windows 中，可以通过 `chcp` 命令实现。例如，

```
chcp 1252
```

将控制台更改为 Windows-1252 代码页。

当然，理想情况下，用户应将控制台切换为 UTF-8。在 Windows 中，命令是

```
chcp 65001
```

不幸的是，这还不足以让 Java 在控制台中使用 UTF-8。还需要使用非官方的 `file.encoding` 系统属性设置平台编码：

```
java -Dfile.encoding=UTF-8 MyProg
```

### 7.6.4 日志文件

当来自 `java.util.logging` 库的日志消息发送到控制台时，它们会以控制台编码写入。你在上一节中看到了如何控制这一点。然而，文件中的日志消息使用 `FileHandler`，它默认使用平台编码。

要将编码更改为 UTF-8，你需要更改日志管理器设置。在日志配置文件中，设置

```
java.util.logging.FileHandler.encoding=UTF-8
```

### 7.6.5 UTF-8 字节顺序标记

如前所述，在可以的时候，对文本文件使用 UTF-8 是个好主意。然而，如果你的应用程序必须读取其他程序创建的 UTF-8 文本文件，你就会遇到另一个潜在问题。将“字节顺序标记”字符 U+FEFF 添加为文件的第一个字符是完全合法的。

在 UTF-16 编码中，每个代码单元是两字节量，字节顺序标记会告诉读取器该文件使用“大端序”还是“小端序”字节顺序。UTF-8 是一种单字节编码，因此不需要指定字节顺序。但如果文件以字节 0xEF 0xBB 0xBF（U+FEFF 的 UTF-8 编码）开头，那就是它使用 UTF-8 的有力指示。因此，Unicode 标准鼓励这种做法。任何读取器都应丢弃开头的字节顺序标记。

美中不足的是，Oracle Java 实现固执地拒绝遵循 Unicode 标准，理由是可能存在兼容性问题。这意味着，作为程序员的你，必须完成平台不愿做的事情。当你读取文本文件并在开头遇到 \uFEFF 时，忽略它。

> **警告：** 不幸的是，JDK 实现者没有遵循这一建议。当你将一份以字节顺序标记开头的有效 UTF-8 源文件传给 javac 编译器时，编译会失败，并显示错误消息“illegal character: \65279”。

### 7.6.6 源文件的字符编码

作为程序员，你需要与 Java 编译器交流——而你是通过本地系统上的工具来完成这件事的。例如，你可以使用中文版记事本来编写 Java 源代码文件。得到的源代码文件*不可移植*，因为它们使用本地字符编码（GB 或 Big5，取决于你使用哪个中文操作系统）。只有编译后的类文件是可移植的——它们会自动对标识符和字符串使用“修改后的 UTF-8”编码。这意味着，当程序编译和运行时，会涉及三种字符编码：

- 源文件：平台编码
- 类文件：修改后的 UTF-8
- 虚拟机：UTF-16

（修改后的 UTF-8 和 UTF-16 格式的定义见第 1 章。）

> **提示：** 你可以使用 `-encoding` 标志指定源文件的字符编码，例如：

```
javac -encoding UTF-8 MyFile.java
```

## 7.7 资源包

在本地化应用程序时，你可能会遇到数量多得令人望而生畏的消息字符串、按钮标签等，它们都需要翻译。为使这项任务可行，你会希望将消息字符串定义在外部位置，通常称为*资源*。这样，执行翻译的人只需编辑资源文件，而不必改动程序的源代码。

在 Java 中，你可以使用属性文件来指定字符串资源，也可以为其他类型的资源实现类。

**注意：** Java 技术资源与 Windows 或 Macintosh 资源不同。Macintosh 或 Windows 可执行程序将菜单、对话框、图标和消息等资源存储在独立于程序代码的区域中。资源编辑器可以检查和更新这些资源，而不会影响程序代码。

**注意：** 第 I 卷，第 5 章描述了 JAR 文件资源的概念，据此可以将数据文件、声音和图像放入 JAR 文件。`Class` 的 `getResource` 方法会找到该文件、打开它，并返回指向该资源的 URL。通过将文件放入 JAR 文件，你把查找文件的工作交给类加载器——它已经知道如何定位 JAR 文件中的项。不过，该机制不支持区域设置。

### 7.7.1 定位资源包

在本地化应用程序时，你会生成一组*资源包*。每个包都是一个属性文件或一个类，用于描述特定于区域设置的项（例如消息、标签等）。对于每个包，你必须为你想要支持的所有区域设置提供版本。

你需要为这些包使用特定的命名约定。例如，特定于德国的资源放入文件 *baseName*`_de_DE` 中；所有德语国家共享的资源放入 *baseName*`_de` 中。一般来说，对所有特定于国家的资源使用

```
baseName_language_country
```

，对所有特定于语言的资源使用

```
baseName_language
```

。最后，作为回退，你可以将默认值放入一个不带任何后缀的文件中。

要加载一个包，请使用以下命令

```java
ResourceBundle currentResources = ResourceBundle.getBundle(baseName, currentLocale);
```

`getBundle` 方法尝试加载按语言和国家/地区与当前区域设置匹配的包。如果不成功，则依次去掉国家/地区和语言。然后对默认区域设置应用相同的搜索，最后查询默认包文件。如果连这次尝试也失败，该方法会抛出 `MissingResourceException`。

也就是说，`getBundle` 方法会尝试加载以下包：

- `baseName_currentLocaleLanguage_currentLocaleCountry`
- `baseName_currentLocaleLanguage`
- `baseName_currentLocaleLanguage_defaultLocaleCountry`
- `baseName_defaultLocaleLanguage`
- `baseName`

一旦 `getBundle` 方法定位到一个包（例如 `baseName_de_DE`），它仍会继续查找 `baseName_de` 和 `baseName`。如果这些包存在，它们会成为资源层次结构中 `baseName_de_DE` 包的父包。之后在查找资源时，如果在当前包中查找不成功，就会搜索父包。也就是说，如果在 `baseName_de_DE` 中未找到某个特定资源，那么还会查询 `baseName_de` 和 `baseName`。

这显然是一项非常有用的服务——而且是一项手工编写会很繁琐的服务。Java 编程语言的资源包机制会自动定位与给定区域设置最匹配的项。向现有程序添加越来越多的本地化很容易——你所要做的就是创建额外的资源包。

> **注意：** 我们简化了对资源包查找的讨论。如果区域设置带有书写系统或变体，查找会复杂得多。详细内情请参阅 `ResourceBundle.Control.getCandidateLocales` 方法的文档。

> **提示：** 你不必把应用程序的所有资源都放入单个包中。你可以为按钮标签准备一个包，为错误消息准备一个包，等等。

### 7.7.2 属性文件

字符串国际化相当直接。你把所有字符串放入一个属性文件，例如 `MyProgramStrings.properties`。这只是一个每行一个键/值对的文本文件。一个典型的文件如下所示：

```text
computeButton=Rechnen
colorName=black
defaultPaperSize=210x297
```

然后按上一节所述为属性文件命名，例如：

```text
MyProgramStrings.properties
MyProgramStrings_en.properties
MyProgramStrings_de_DE.properties
```

可以像下面这样简单地加载资源包：

```java
ResourceBundle bundle = ResourceBundle.getBundle("MyProgramStrings", locale);
```

要查找特定字符串，请调用

```java
String computeButtonLabel = bundle.getString("computeButton");
```

> **注意：** 在 Java 9 之前，用于存储属性的文件必须是 ASCII 文件。如果你使用的是旧版 Java，并且需要在属性文件中放入 Unicode 字符，请使用 `\uxxxx` 编码对其进行编码。例如，要指定 `colorName=Grün`，请使用
> 
> ```text
> colorName=Gr\u00FCn
> ```
> 
> 可以使用 native2ascii 工具生成这些编码。

### 7.7.3 资源包类

要提供非字符串资源，请定义扩展 ResourceBundle 类的类。使用标准命名约定为类命名，例如

```text
MyProgramResources.java
MyProgramResources_en.java
MyProgramResources_de_DE.java
```

使用与加载属性文件相同的 getBundle 方法加载该类：

```java
ResourceBundle bundle = ResourceBundle.getBundle("MyProgramResources", locale);
```

> **注意：** 搜索资源包时，如果类中的资源包和属性文件具有相同的基本名称，则优先使用类中的资源包。

每个资源包类都实现一个查找表。需要为每个想要本地化的设置提供键字符串，并使用该键字符串检索设置。例如，

```java
var backgroundColor = (Color) bundle.getObject("backgroundColor");
double[] paperSize = (double[]) bundle.getObject("defaultPaperSize");
```

实现资源包类的最简单方法是扩展 ListResourceBundle 类。ListResourceBundle 允许你将所有资源放入一个对象数组，然后为你执行查找。遵循以下代码大纲：

```java
public class baseName_language_country extends ListResourceBundle
{
   private static final Object[][] contents =
   {
      { key1, value1 },
      { key2, value2 },
      . . .
   };
   public Object[][] getContents() { return contents; }
}
```

例如，

```java
public class ProgramResources_de extends ListResourceBundle
{
   private static final Object[][] contents =
   {
      { "backgroundColor", Color.black },
      { "defaultPaperSize", new double[] { 210, 297 } }
   };
   public Object[][] getContents() { return contents; }
}
public class ProgramResources_en_US extends ListResourceBundle
{
   private static final Object[][] contents =
   {
      { "backgroundColor", Color.blue },
      { "defaultPaperSize", new double[] { 216, 279 } }
   };
   public Object[][] getContents() { return contents; }
}
```

或者，你的资源包类可以扩展 ResourceBundle 类。然后需要实现两个方法，分别用于枚举所有键和查找给定键的值：

```java
Enumeration<String> getKeys()
Object handleGetObject(String key)
```

ResourceBundle 类的 getObject 方法会调用你提供的 handleGetObject 方法。

- **java.util.ResourceBundle 1.1**
  - `static ResourceBundle getBundle(String baseName, Locale loc)`
  - `static ResourceBundle getBundle(String baseName)`  
    加载具有给定名称的资源包类，用于给定区域设置或默认区域设置，以及其父类。如果资源包类位于某个包中，则基本名称必须包含完整包名，例如 `intl.ProgramResources`。资源包类必须是 public，以便 `getBundle` 方法可以访问它们。
  - `Object getObject(String name)`  
    从资源包或其父资源包中查找对象。
  - `String getString(String name)`  
    从资源包或其父资源包中查找对象，并将其强制转换为字符串。
  - `String[] getStringArray(String name)`  
    从资源包或其父资源包中查找对象，并将其强制转换为字符串数组。
  - `Enumeration<String> getKeys()`  
    返回一个枚举对象，用于枚举此资源包的键。它也会枚举父资源包中的键。
  - `Object handleGetObject(String key)`  
    如果你定义自己的资源查找机制，则应重写此方法，以查找与给定键关联的资源值。

## 7.8 完整示例

在本节中，我们将本章的材料应用于本地化一个退休计算器。该程序计算你为退休储蓄的钱是否足够。你输入自己的年龄、每月储蓄金额等（见图 7.4）。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_444_0.png)

**图 7.4** 英文版退休计算器

文本区域和图表显示退休账户每年的余额。如果在你人生的后期数字变为负数，并且图表中的条形出现在 x 轴下方，你就需要采取一些措施——例如，多存钱、推迟退休、早点去世，或者变得更年轻。

该退休计算器支持三种区域设置（英语、德语和中文）。以下是国际化的一些亮点：

- 标签、按钮和消息被翻译成德语和中文。你可以在 RetireResources_de 和 RetireResources_zh 类中找到它们。英语用作回退——参见 RetireResources 文件。
- 每当区域设置更改时，我们会重置标签并重新格式化文本字段的内容。
- 文本字段按本地格式处理数字、货币金额和百分比。
- 计算字段使用 MessageFormat。格式字符串存储在每个语言的资源包中。
- 为了展示这是可以做到的，我们根据用户选择的语言为条形图使用不同的颜色。

清单 7.5 到 7.8 展示了代码。清单 7.9 到 7.11 是本地化字符串的属性文件。图 7.5 和图 7.6 分别展示了德语和中文的输出。要查看中文字符，请确保已安装中文字体并在 Java 运行时中配置好。否则，中文字符将显示为“缺失字符”图标。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_445_0.png)

**图 7.5** 德文版退休计算器

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_445_1.png)

**图 7.6** 中文版退休计算器

```java
private JLabel inflationPercentLabel = new JLabel();
private JLabel investPercentLabel = new JLabel();
private RetireInfo info = new RetireInfo();
private Locale[] locales = { Locale.US, Locale.CHINA, Locale.GERMANY };
private Locale currentLocale;
private JComboBox<Locale> localeCombo = new LocaleCombo(locales);
private ResourceBundle res;
private ResourceBundle resStrings;
private NumberFormat currencyFmt;
private NumberFormat numberFmt;
private NumberFormat percentFmt;

public RetireFrame()
{
   setLayout(new GridBagLayout());
   add(languageLabel, new GBC(0, 0).setAnchor(GBC.EAST));
   add(savingsLabel, new GBC(0, 1).setAnchor(GBC.EAST));
   add(contribLabel, new GBC(2, 1).setAnchor(GBC.EAST));
   add(incomeLabel, new GBC(4, 1).setAnchor(GBC.EAST));
   add(currentAgeLabel, new GBC(0, 2).setAnchor(GBC.EAST));
   add(retireAgeLabel, new GBC(2, 2).setAnchor(GBC.EAST));
   add(deathAgeLabel, new GBC(4, 2).setAnchor(GBC.EAST));
   add(inflationPercentLabel, new GBC(0, 3).setAnchor(GBC.EAST));
   add(investPercentLabel, new GBC(2, 3).setAnchor(GBC.EAST));
   add(localeCombo, new GBC(1, 0, 3, 1));
   add(savingsField, new GBC(1, 1).setWeight(100, 0).setFill(GBC.HORIZONTAL));
   add(contribField, new GBC(3, 1).setWeight(100, 0).setFill(GBC.HORIZONTAL));
   add(incomeField, new GBC(5, 1).setWeight(100, 0).setFill(GBC.HORIZONTAL));
   add(currentAgeField, new GBC(1, 2).setWeight(100, 0).setFill(GBC.HORIZONTAL));
   add(retireAgeField, new GBC(3, 2).setWeight(100, 0).setFill(GBC.HORIZONTAL));
   add(deathAgeField, new GBC(5, 2).setWeight(100, 0).setFill(GBC.HORIZONTAL));
   add(inflationPercentField, new GBC(1, 3).setWeight(100, 0).setFill(GBC.HORIZONTAL));
   add(investPercentField, new GBC(3, 3).setWeight(100, 0).setFill(GBC.HORIZONTAL));
   add(retireCanvas, new GBC(0, 4, 4, 1).setFill(GBC.BOTH));
   add(new JScrollPane(retireText),
         new GBC(4, 2, 1).setWeight(100, 0).setFill(GBC.BOTH));

   computeButton.setName("computeButton");
   computeButton.addActionListener(event ->
   {
      getInfo();
      updateData();
      updateGraph();
   });
   add(computeButton, new GBC(5, 3));

   retireText.setEditable(false);
   retireText.setFont(new Font("Monospaced", Font.PLAIN, 10));
}
```




### 清单7.5（续）

```java
        info.setSavings(0);
        info.setContrib(9000);
        info.setIncome(60000);
        info.setCurrentAge(35);
        info.setRetireAge(65);
        info.setDeathAge(85);
        info.setInvestPercent(0.1);
        info.setInflationPercent(0.05);

        int localeIndex = 0; // US locale is default selection
        for (int i = 0; i < locales.length; i++)
           // if current locale one of the choices, select it
           if (getLocale().equals(locales[i])) localeIndex = i;
        setCurrentLocale(locales[localeIndex]);

        localeCombo.addActionListener(event ->
           {
              setCurrentLocale((Locale) localeCombo.getSelectedItem());
              validate();
           });
        pack();
    }

    /**
     * Sets the current locale.
     * @param locale the desired locale
     */
    public void setCurrentLocale(Locale locale)
    {
        currentLocale = locale;
        localeCombo.setLocale(currentLocale);
        localeCombo.setSelectedItem(currentLocale);

        res = ResourceBundle.getBundle("retire.RetireResources", currentLocale);
        resStrings = ResourceBundle.getBundle("retire.RetireStrings", currentLocale);
        currencyFmt = NumberFormat.getCurrencyInstance(currentLocale);
        numberFmt = NumberFormat.getNumberInstance(currentLocale);
        percentFmt = NumberFormat.getPercentInstance(currentLocale);

        updateDisplay();
        updateInfo();
        updateData();
        updateGraph();
    }

    /**
     * Updates all labels in the display.
     */
    private int age;
    private double balance;

    /**
     * Gets the available balance for a given year.
     * @param year the year for which to compute the balance
     * @return the amount of money available (or required) in that year
     */
    public double getBalance(int year)
    {
        if (year < currentAge) return 0;
        else if (year == currentAge)
        {
            age = year;
            balance = savings;
            return balance;
        }
        else if (year == age) return balance;
        if (year != age + 1) getBalance(year - 1);
        age = year;
        if (age < retireAge) balance += contrib;
        else balance += income;
        balance = balance * (1 + (investPercent - inflationPercent));
        return balance;
    }

    /**
     * Gets the amount of prior savings.
     * @return the savings amount
     */
    public double getSavings()
    {
        return savings;
    }

    /**
     * Sets the amount of prior savings.
     * @param newValue the savings amount
     */
    public void setSavings(double newValue)
    {
        savings = newValue;
    }

    /**
     * Gets the annual contribution to the retirement account.
     * @return the contribution amount
     */
    public void setCurrentAge(int newValue)
    {
        currentAge = newValue;
    }

    /**
     * Gets the desired retirement age.
     * @return the age
     */
    public int getRetireAge()
    {
        return retireAge;
    }

    /**
     * Sets the desired retirement age.
     * @param newValue the age
     */
    public void setRetireAge(int newValue)
    {
        retireAge = newValue;
    }

    /**
     * Gets the expected age of death.
     * @return the age
     */
    public int getDeathAge()
    {
        return deathAge;
    }

    /**
     * Sets the expected age of death.
     * @param newValue the age
     */
    public void setDeathAge(int newValue)
    {
        deathAge = newValue;
    }

    /**
     * Gets the estimated percentage of inflation.
     * @return the percentage
     */
    public double getInflationPercent()
    {
        return inflationPercent;
    }

    /**
     * Sets the estimated percentage of inflation.
     * @param newValue the percentage
     */
    public void setInflationPercent(double newValue)
    {
        inflationPercent = newValue;
    }

    /**
     * Gets the estimated yield of the investment.
     * @return the percentage
     */
    public double getInvestPercent()
    {
        return investPercent;
    }

    /**
     * Sets the estimated yield of the investment.
     * @param newValue the percentage
     */
    public void setInvestPercent(double newValue)
    {
        investPercent = newValue;
    }
}

/**
 * This component draws a graph of the investment result.
 */
class RetireComponent extends JComponent
{
    private static final int PANEL_WIDTH = 400;
    private static final int PANEL_HEIGHT = 200;
    private static final Dimension PREFERRED_SIZE = new Dimension(800, 600);
    private RetireInfo info = null;
    private Color colorPre;
    private Color colorGain;
    private Color colorLoss;

    public RetireComponent()
    {
        setSize(PANEL_WIDTH, PANEL_HEIGHT);
    }

    /**
     * Sets the retirement information to be plotted.
     * @param newInfo the new retirement info.
     */
    public void setInfo(RetireInfo newInfo)
    {
        info = newInfo;
        repaint();
    }

    public void paintComponent(Graphics g)
    {
        var g2 = (Graphics2D) g;
        if (info == null) return;

        double minValue = 0;
        double maxValue = 0;
        int i;
        for (i = info.getCurrentAge(); i <= info.getDeathAge(); i++)
        {
            double v = info.getBalance(i);
            if (minValue > v) minValue = v;
            if (maxValue < v) maxValue = v;
        }
        if (maxValue == minValue) return;

        int barWidth = getWidth() / (info.getDeathAge() - info.getCurrentAge() + 1);
        double scale = getHeight() / (maxValue - minValue);

        for (i = info.getCurrentAge(); i <= info.getDeathAge(); i++)
        {
            int x1 = (i - info.getCurrentAge()) * barWidth + 1;
            int y1;
            double v = info.getBalance(i);
            int height;
            int yOrigin = (int) (maxValue * scale);

            if (v >= 0)
            {
                y1 = (int) ((maxValue - v) * scale);
                height = yOrigin - y1;
            }
            else
            {
                y1 = yOrigin;
                height = (int) (-v * scale);
            }

            if (i < info.getRetireAge()) g2.setPaint(colorPre);
            else if (v >= 0) g2.setPaint(colorGain);
            else g2.setPaint(colorLoss);
            var bar = new Rectangle2D.Double(x1, y1, barWidth - 2, height);
            g2.fill(bar);
            g2.setPaint(Color.black);
            g2.draw(bar);
        }
    }

    /**
     * Sets the color to be used before retirement.
     * @param color the desired color
     */
    public void setColorPre(Color color)
    {
        colorPre = color;
        repaint();
    }

    /**
     * Sets the color to be used after retirement while the account balance is positive.
     * @param color the desired color
     */
    public void setColorGain(Color color)
    {
        colorGain = color;
        repaint();
    }

    /**
     * Sets the color to be used after retirement when the account balance is negative.
     * @param color the desired color
     */
    public void setColorLoss(Color color)
    {
        colorLoss = color;
        repaint();
    }

    public Dimension getPreferredSize() { return PREFERRED_SIZE; }
}
```

### 清单7.8 retire/RetireResources_zh.java

```java
package retire;

import java.awt.*;

/**
 * These are the Chinese non-string resources for the retirement calculator.
 * @version 1.21 2001-08-27
 * @author Cay Horstmann
 */
public class RetireResources_zh extends java.util.ListResourceBundle
{
   private static final Object[][] contents = {
      // BEGIN LOCALIZE
      { "colorPre", Color.red }, { "colorGain", Color.blue }, { "colorLoss", Color.yellow }
      // END LOCALIZE
   };

   public Object[][] getContents()
   {
      return contents;
   }
}
```

### 清单7.9 retire/RetireStrings.properties

```properties
language=Language
computeButton=Compute
savings=Prior Savings
contrib=Annual Contribution
income=Retirement Income
currentAge=Current Age
retireAge=Retirement Age
deathAge=Life Expectancy
inflationPercent=Inflation
investPercent=Investment Return
retireAge: {0,number} Balance: {1,number,currency}
```

### 清单7.10 retire/RetireStrings_de.properties

```properties
language=Sprache
computeButton=Rechnen
savings=Vorherige Ersparnisse
contrib=Jährliche Einzahlung
income=Einkommen nach Ruhestand
currentAge=Jetziger Alter
retireAge=Ruhestandsalter
```




```properties
deathAge=Lebenserwartung
inflationPercent=Inflation
investPercent=Investitionsgewinn
retire=Alter: {0,number} Guthaben: {1,number,currency}
```

### 清单 7.11 `retire/RetireStrings_zh.properties`

```properties
language=语言
computeButton=计算
savings=储蓄
contrib=每年存款
income=退休收入
currentAge=当前年龄
retireAge=退休年龄
deathAge=预期寿命
inflationPercent=通货膨胀
investPercent=投资回报
retire=年龄：{0,number} 总金额：{1,number,currency}
```

你已经了解了如何使用 Java 语言的国际化特性。现在，你可以使用资源包来提供多种语言的翻译，并使用格式器和排序器进行特定于区域设置的文本处理。

在下一章中，我们将深入探讨脚本、编译和注解处理。

*本页故意留空*

# 第8章 脚本、编译与注解处理

## 本章内容

- 8.1 Java平台的脚本，第440页
- 8.2 编译器API，第452页
- 8.3 使用注解，第463页
- 8.4 注解语法，第471页
- 8.5 标准注解，第478页
- 8.6 源代码级注解处理，第484页
- 8.7 字节码工程，第489页

本章介绍三种处理代码的技术。脚本API允许你调用用脚本语言（如JavaScript或Groovy）编写的代码。当你希望在应用程序内部编译Java代码时，可以使用编译器API。注解处理器对包含注解的Java源文件或类文件进行操作。正如你将看到的，注解处理有许多应用，从简单的诊断到“字节码工程”——将字节码插入类文件，甚至插入正在运行的程序。

## 8.1 Java平台的脚本

脚本语言是一种通过在运行时解释程序文本来避免通常的编辑/编译/链接/运行周期的语言。脚本语言有许多优点：

- 快速周转，鼓励实验
- 改变正在运行的程序的行为
- 允许程序用户进行定制

另一方面，大多数脚本语言缺乏对编写复杂应用程序有益的特性，例如强类型、封装和模块化。

因此，将脚本语言和传统语言的优点结合起来是很有吸引力的。脚本API让你可以在Java平台上做到这一点。它使你能够从Java程序中调用用JavaScript、Groovy、Ruby，甚至Scheme和Haskell等奇特语言编写的脚本。例如，Renjin项目（www.renjin.org）提供了R编程语言（常用于统计编程）的Java实现，以及脚本API的一个“引擎”。

在以下各节中，我们将向你展示如何为特定语言选择引擎、如何执行脚本，以及如何利用某些脚本引擎提供的高级特性。

### 8.1.1 获取脚本引擎

脚本引擎是一个可以执行特定语言脚本的库。当虚拟机启动时，它会发现可用的脚本引擎。要枚举它们，请构造一个`ScriptEngineManager`并调用`getEngineFactories`方法。你可以向每个引擎工厂询问支持的引擎名称、MIME类型和文件扩展名。表8.1显示了典型值。

**表8.1** 脚本引擎工厂的属性

| 引擎 | 名称 | MIME类型 | 扩展名 |
|---|---|---|---|
| Nashorn（包含在JDK中） | nashorn, Nashorn, js, JS, JavaScript, javascript, ECMAScript, ecmascript | application/javascript, application/ecmascript, text/javascript, text/ecmascript | js |
| Groovy | groovy | 无 | groovy |
| Renjin | Renjin | text/x-R | R, r, S, s |

通常，你知道自己需要哪个引擎，只需按名称、MIME类型或扩展名请求它即可。例如：

```java
ScriptEngine engine = manager.getEngineByName("nashorn");
```

Java 8引入了Nashorn，这是Oracle开发的一种JavaScript解释器。你可以通过在类路径上提供必要的JAR文件来添加更多语言。

**`javax.script.ScriptEngineManager`**

| 方法 | 描述 |
|---|---|
| `List<ScriptEngineFactory> getEngineFactories()` | 获取所有已发现的引擎工厂的列表。 |
| `ScriptEngine getEngineByName(String name)` | 获取具有给定名称的脚本引擎。 |
| `ScriptEngine getEngineByExtension(String extension)` | 获取具有给定脚本文件扩展名的脚本引擎。 |
| `ScriptEngine getEngineByMimeType(String mimeType)` | 获取具有给定MIME类型的脚本引擎。 |

**`javax.script.ScriptEngineFactory`**

| 方法 | 描述 |
|---|---|
| `List<String> getNames()` | 获取此工厂已知的名称。 |
| `List<String> getExtensions()` | 获取此工厂已知的脚本文件扩展名。 |
| `List<String> getMimeTypes()` | 获取此工厂已知的MIME类型。 |

### 8.1.2 脚本求值与绑定

一旦有了引擎，你可以简单地通过调用以下代码来调用脚本：

```java
Object result = engine.eval(scriptString);
```

如果脚本存储在文件中，请打开一个Reader并调用

```java
Object result = engine.eval(reader);
```

你可以在同一个引擎上调用多个脚本。如果一个脚本定义了变量、函数或类，大多数脚本引擎会保留这些定义以供后续使用。例如，

```java
engine.eval("n = 1728");
Object result = engine.eval("n + 1");
```

将返回1729。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_464_0.png)

> **注意：** 要确定在多个线程中并发执行脚本是否安全，请调用
>
> `Object param = factory.getParameter("THREADING");`
>
> 返回值为以下之一：
>
> - `null`：并发执行不安全。
> - `"MULTITHREADED"`：并发执行是安全的。一个线程的影响可能对另一个线程可见。
> - `"THREAD-ISOLATED"`：除了`"MULTITHREADED"`之外，还为每个线程维护不同的变量绑定。
> - `"STATELESS"`：除了`"THREAD-ISOLATED"`之外，脚本不会改变变量绑定。

你常常会希望向引擎添加变量绑定。一个绑定由一个名称和一个关联的Java对象组成。例如，考虑以下语句：

```java
engine.put("k", 1728);
Object result = engine.eval("k + 1");
```

脚本代码从“引擎作用域”中的绑定读取k的定义。这一点特别重要，因为大多数脚本语言可以访问Java对象，通常使用的语法比Java语法更简单。例如，

```java
engine.put("b", new JButton());
engine.eval("b.text = 'OK'");
```

反过来，你可以检索由脚本语句绑定的变量：

```java
engine.eval("n = 1728");
Object result = engine.get("n");
```

除了引擎作用域之外，还有一个全局作用域。你添加到`ScriptEngineManager`的任何绑定对所有引擎都可见。

除了将绑定添加到引擎或全局作用域之外，你还可以将它们收集到`Bindings`类型的对象中，并将其传递给`eval`方法：

```java
Bindings scope = engine.createBindings();
scope.put("b", new JButton());
engine.eval(scriptString, scope);
```

如果一组绑定不应在将来调用`eval`方法时持续存在，那么这很有用。

> **注意：** 你可能希望拥有除引擎作用域和全局作用域之外的其他作用域。例如，Web容器可能需要请求作用域和会话作用域。然而，那样的话你就得自己处理了。你需要编写一个实现`ScriptContext`接口的类，管理作用域的集合。每个作用域由一个整数标识，编号较低的作用域应首先被搜索。（标准库提供了一个`SimpleScriptContext`类，但它只包含全局作用域和引擎作用域。）

| API | 版本 |
|---|---|
| `javax.script.ScriptEngine` | 6 |

- `Object eval(String script)`
- `Object eval(Reader reader)`
- `Object eval(String script, Bindings bindings)`
- `Object eval(Reader reader, Bindings bindings)`

求值由字符串或读取器给出的脚本，并受给定绑定的约束。

- `Object get(String key)`
- `void put(String key, Object value)`

获取或放置引擎作用域中的绑定。

- `Bindings createBindings()`

创建一个适合此引擎的空`Bindings`对象。

| API | 版本 |
|---|---|
| `javax.script.ScriptEngineManager` | 6 |

- `Object get(String key)`
- `void put(String key, Object value)`

获取或放置全局作用域中的绑定。

| API | 版本 |
|---|---|
| `javax.script.Bindings` | 6 |

- `Object get(String key)`
- `void put(String key, Object value)`

获取或放置绑定到此`Bindings`对象所表示的作用域中。



### 8.1.3 重定向输入和输出

可以通过调用脚本上下文的 setReader 和 setWriter 方法来重定向脚本的标准输入和输出。例如，

```java
var writer = new StringWriter();
engine.getContext().setWriter(new PrintWriter(writer, true));
```

使用 JavaScript 的 print 或 println 函数写入的任何输出都会发送到 writer。

setReader 和 setWriter 方法只影响脚本引擎的标准输入和输出源。例如，如果执行以下 JavaScript 代码

```javascript
println("Hello");
java.lang.System.out.println("World");
```

只有第一个输出会被重定向。

Nashorn 引擎没有标准输入源的概念。调用 setReader 不会产生任何效果。

**`javax.script.ScriptEngine`**

- `ScriptContext getContext()`

获取此引擎的默认脚本上下文。

**`javax.script.ScriptContext`**

- `Reader getReader()`
- `void setReader(Reader reader)`
- `Writer getWriter()`
- `void setWriter(Writer writer)`
- `Writer getErrorWriter()`
- `void setErrorWriter(Writer writer)`

获取或设置用于输入的读取器，或用于普通输出或错误输出的写入器。

### 8.1.4 调用脚本函数和方法

对于许多脚本引擎，无需实际求值脚本代码，就可以调用脚本语言中的函数。如果允许用户用他们选择的脚本语言实现服务，这会很有用。

提供此功能的脚本引擎实现 Invocable 接口。特别是，Nashorn 引擎实现了 Invocable。

要调用函数，请使用函数名以及后续的函数参数调用 `invokeFunction` 方法：

```javascript
// Define greet function in JavaScript
engine.eval("function greet(how, whom) { return how + ', ' + whom + ' !' }");

// Call the function with arguments "Hello", "World"
result = ((Invocable) engine).invokeFunction("greet", "Hello", "World");
```

如果脚本语言是面向对象的，请调用 `invokeMethod`：

```javascript
// Define Greeter class in JavaScript
engine.eval("function Greeter(how) { this.how = how }");
engine.eval("Greeter.prototype.welcome =\n    function(whom) { return this.how + ', ' + whom + ' !' }");

// Construct an instance
Object yo = engine.eval("new Greeter('Yo')");

// Call the welcome method on the instance
result = ((Invocable) engine).invokeMethod(yo, "welcome", "World");
```

> **注意：** 有关如何在 JavaScript 中定义类的更多信息，请参阅 Douglas Crockford 所著的 *JavaScript——The Good Parts*（O’Reilly，2008）。

> **注意：** 如果脚本引擎未实现 Invocable 接口，你仍然可以用与语言无关的方式调用方法。ScriptEngineFactory 接口的 `getMethodCallSyntax` 方法会生成一个字符串，你可以将其传给 eval 方法。不过，为此所有方法参数都必须绑定到名称，而 `invokeMethod` 可以使用任意值调用。

你还可以更进一步，让脚本引擎实现一个 Java 接口。然后就可以用 Java 方法调用语法调用脚本函数和方法。

具体细节取决于脚本引擎，但通常需要为接口的每个方法提供一个函数。例如，考虑一个 Java 接口

```java
public interface Greeter
{
    String welcome(String whom);
}
```

如果在 Nashorn 中定义了同名全局函数，就可以通过这个接口调用它：

```javascript
// Define welcome function in JavaScript
engine.eval("function welcome(whom) { return 'Hello, ' + whom + '!'; }");

// Get a Java object and call a Java method
Greeter g = ((Invocable) engine).getInterface(Greeter.class);
result = g.welcome("World");
```

在面向对象的脚本语言中，可以通过匹配的 Java 接口访问脚本类。例如，下面展示了如何用 Java 语法调用 JavaScript Greeter 类的对象：

```java
Greeter g = ((Invocable) engine).getInterface(yo, Greeter.class);
result = g.welcome("World");
```

总之，如果希望从 Java 调用脚本代码而不必担心脚本语言语法，Invocable 接口会很有用。

**`javax.script.Invocable`**

| 方法 | 描述 |
|---|---|
| `Object invokeFunction(String name, Object... parameters)`<br>`Object invokeMethod(Object obj, String name, Object... explicitParameters)` | 使用给定名称调用函数或方法，并传入给定参数。 |
| `<T> T getInterface(Class<T> iface)` | 返回给定接口的实现，并用脚本引擎中的函数实现这些方法。 |
| `<T> T getInterface(Object implicitParameter, Class<T> iface)` | 返回给定接口的实现，并用给定对象的方法实现这些方法。 |

### 8.1.5 编译脚本

某些脚本引擎可以将脚本代码编译为中间形式，以便高效执行。这些引擎实现 Compilable 接口。以下示例展示了如何编译并求值脚本文件中包含的代码：

```java
var reader = new FileReader("myscript.js");
CompiledScript script = null;
if (engine instanceof Compilable)
    script = ((Compilable) engine).compile(reader);
```

脚本编译完成后，就可以执行它。以下代码在编译成功时执行已编译的脚本，如果引擎不支持编译，则执行原始脚本：

```java
if (script != null)
    script.eval();
else
    engine.eval(reader);
```

当然，只有在需要重复执行脚本时，编译脚本才有意义。

**`javax.script.Compilable`**

| 方法 | 描述 |
|---|---|
| `CompiledScript compile(String script)`<br>`CompiledScript compile(Reader reader)` | 编译由字符串或读取器给出的脚本。 |

**`javax.script.CompiledScript`**

| 方法 | 描述 |
|---|---|
| `Object eval()`<br>`Object eval(Bindings bindings)` | 求值此脚本。 |

### 8.1.6 示例：脚本化 GUI 事件

为了说明脚本 API，我们将编写一个示例程序，允许用户用他们选择的脚本语言指定事件处理器。

请查看代码清单 8.1 中的程序，它向任意 frame 类添加脚本支持。默认情况下，它读取代码清单 8.2 中的 `ButtonFrame` 类，该类类似于第 I 卷中的事件处理演示，但有两处不同：

- 每个组件都设置了 name 属性。
- 没有事件处理器。

事件处理器定义在属性文件中。每个属性定义的形式为

`componentName.eventName = scriptCode`

例如，如果选择使用 JavaScript，请在一个 `js.properties` 文件中提供事件处理器，如下所示：

```properties
yellowButton.action=panel.background = java.awt.Color.YELLOW
blueButton.action=panel.background = java.awt.Color.BLUE
redButton.action=panel.background = java.awt.Color.RED
```

配套代码还包含用于 Groovy 和 R 的文件。

程序首先为命令行指定的语言加载一个引擎。如果未指定语言，则使用 JavaScript。

然后，如果存在 init_language 脚本，我们就处理它。这对 R 和 Scheme 语言很有用，因为它们需要一些初始化，而我们不希望把这些初始化包含在每个事件处理器脚本中。

接下来，我们递归遍历所有子组件，并将绑定（名称、对象）添加到组件映射中。然后把这些绑定添加到引擎中。

接下来，我们读取 language.properties 文件。对于每个属性，我们合成一个事件处理器代理，使脚本代码得以执行。细节有点技术性。如果想详细了解实现，可以阅读第 I 卷第 6 章中关于代理的章节。不过，关键部分是每个事件处理器都会调用

```java
engine.eval(scriptCode);
```

让我们更详细地看看 yellowButton。当处理下面这一行时

```properties
yellowButton.action=panel.background = java.awt.Color.YELLOW
```

我们会找到名称为 "yellowButton" 的 JButton 组件。然后附加一个 ActionListener，其 actionPerformed 方法执行以下脚本

```javascript
panel.background = java.awt.Color.YELLOW
```

前提是脚本使用 Nashorn 完成。

引擎包含一个绑定，将名称 "panel" 绑定到 JPanel 对象。当事件发生时，会执行 panel 的 setBackground 方法，颜色随之改变。

只需执行以下命令，就可以使用 JavaScript 事件处理器运行此程序

```shell
java ScriptTest
```

对于 Groovy 处理器，请使用

```shell
java -classpath .:groovy/lib/* ScriptTest groovy
```

这里，*groovy* 是安装 Groovy 的目录。



对于 R 的 Renjin 实现，请在类路径中包含 Renjin Studio 和 Renjin 脚本引擎的 JAR 文件。两者均可在 www.renjin.org/downloads.html 获取。

此应用程序演示了如何将脚本用于 Java GUI 编程。还可以更进一步，用 XML 文件描述 GUI，正如你在第 3 章所见。那时我们的程序将成为一个 GUI 解释器，这些 GUI 的视觉呈现由 XML 定义，行为由脚本语言定义。注意这与动态 HTML 页面或动态服务器端脚本环境的相似之处。

#### 清单 8.1 `script/ScriptTest.java`

```java
package script;

import java.awt.*;
import java.beans.*;
import java.io.*;
import java.lang.reflect.*;
import java.util.*;
import javax.script.*;
import javax.swing.*;

/**
 * @version 1.03 2018-05-01
 * @author Cay Horstmann
 */
public class ScriptTest
{
    public static void main(String[] args)
    {
        EventQueue.invokeLater(() ->
        {
            try
            {
                var manager = new ScriptEngineManager();
                String language;
                if (args.length == 0)
                {
                    System.out.println("Available factories: ");
                    for (ScriptEngineFactory factory : manager.getEngineFactories())
                        System.out.println(factory.getEngineName());

                    language = "nashorn";
                }
                else language = args[0];

private static void getComponentBindings(Component c,
        Map<String, Component> namedComponents)
{
    String name = c.getName();
    if (name != null) namedComponents.put(name, c);
    if (c instanceof Container)
    {
        for (Component child : ((Container) c).getComponents())
            getComponentBindings(child, namedComponents);
    }
}

/**
 * Adds a listener to an object whose listener method executes a script.
 * @param beanName the name of the bean to which the listener should be added
 * @param eventName the name of the listener type, such as "action" or "change"
 * @param scriptCode the script code to be executed
 * @param engine the engine that executes the code
 * @param bindings the bindings for the execution
 * @throws IntrospectionException
 */
private static void addListener(String beanName, String eventName, final String scriptCode,
        ScriptEngine engine, Map<String, Component> components)
        throws ReflectiveOperationException, IntrospectionException
{
    Object bean = components.get(beanName);
    EventSetDescriptor descriptor = getEventSetDescriptor(bean, eventName);
    if (descriptor == null) return;
    descriptor.getAddListenerMethod().invoke(bean,
        Proxy.newProxyInstance(null, new Class[] { descriptor.getListenerType() },
            (proxy, method, args) ->
            {
                engine.eval(scriptCode);
                return null;
            }));
}

private static EventSetDescriptor getEventSetDescriptor(Object bean, String eventName)
        throws IntrospectionException
{
    for (EventSetDescriptor descriptor : Introspector.getBeanInfo(bean.getClass())
            .getEventSetDescriptors())
        if (descriptor.getName().equals(eventName)) return descriptor;
    return null;
}
```

#### 清单 8.2 `buttons1/ButtonFrame.java`

```java
package buttons1;

import javax.swing.*;

/**
 * A frame with a button panel.
 * @version 1.00 2007-11-02
 * @author Cay Horstmann
 */
public class ButtonFrame extends JFrame
{
   private static final int DEFAULT_WIDTH = 300;
   private static final int DEFAULT_HEIGHT = 200;

   private JPanel panel;
   private JButton yellowButton;
   private JButton blueButton;
   private JButton redButton;

   public ButtonFrame()
   {
      setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);

      panel = new JPanel();
      panel.setName("panel");
      add(panel);

      yellowButton = new JButton("Yellow");
      yellowButton.setName("yellowButton");
      blueButton = new JButton("Blue");
      blueButton.setName("blueButton");
      redButton = new JButton("Red");
      redButton.setName("redButton");

      panel.add(yellowButton);
      panel.add(blueButton);
      panel.add(redButton);
   }
}
```

## 8.2 编译器 API

有相当多的工具需要编译 Java 代码。显然，开发环境和教授 Java 编程的程序就在其中，测试与构建自动化工具也是如此。另一个例子是 JavaServer Pages 的处理——即嵌入了 Java 语句的网页。

### 8.2.1 调用编译器

调用编译器非常容易。下面是一个示例调用：

```java
JavaCompiler compiler = ToolProvider.getSystemJavaCompiler();
OutputStream outStream = ...;
OutputStream errStream = ...;
int result = compiler.run(null, outStream, errStream,
    "-sourcepath", "src", "Test.java");
```

结果值为 0 表示编译成功。

编译器将其输出和错误消息发送到提供的流。你可以将这些参数设置为 null，此时将使用 System.out 和 System.err。run 方法的第一个参数是输入流。由于编译器不接受控制台输入，你始终可以将其保留为 null。（run 方法继承自通用的 Tool 接口，该接口允许工具读取输入。）

run 方法的其余参数是如果在命令行调用 javac 时会传递给它的参数。这些参数可以是选项或文件名。

### 8.2.2 启动编译任务

使用 CompilationTask 对象可以更好地控制编译过程。如果你想从字符串提供源代码、在内存中捕获类文件，或处理错误和警告消息，这会很有用。

要获得 CompilationTask，请像上一节那样先创建一个编译器对象。然后调用

```java
JavaCompiler.CompilationTask task = compiler.getTask(
    errWriter, // Uses System.err if null
    fileManager, // Uses the standard file manager if null
    diagnostics, // Uses System.err if null
    options, // null if no options
    classes, // For annotation processing; null if none
    sources);
```

最后三个参数是 Iterable 实例。例如，一组选项可以这样指定：

```java
Iterable<String> options = List.of("-d", "bin");
```

sources 参数是 JavaFileObject 实例的 Iterable。如果你想编译磁盘文件，请获取 StandardJavaFileManager 并调用其 getJavaFileObjects 方法：

```java
StandardJavaFileManager fileManager = compiler.getStandardFileManager(null, null, null);
Iterable<JavaFileObject> sources
      = fileManager.getJavaFileObjectsFromStrings(List.of("File1.java", "File2.java"));
JavaCompiler.CompilationTask task = compiler.getTask(
      null, null, null, options, null, sources);
```

**注意：** classes 参数仅用于注解处理。在这种情况下，还需要使用 `Processor` 对象列表调用 `task.processors(annotationProcessors)`。有关注解处理的示例，请参见第 484 页的 8.6 节“源码级注解处理”。

`getTask` 方法返回任务对象，但尚未启动编译过程。`CompilationTask` 类扩展了 `Callable<Boolean>`。你可以将其传递给 `ExecutorService` 以并发执行，或者直接进行同步调用：

```java
Boolean success = task.call();
```

### 8.2.3 捕获诊断信息

要监听错误消息，请安装一个 `DiagnosticListener`。每当编译器报告警告或错误消息时，该监听器都会收到一个 `Diagnostic` 对象。`DiagnosticCollector` 类实现了此接口。它只是收集所有诊断信息，以便你在编译完成后遍历它们。

```java
DiagnosticCollector<JavaFileObject> collector = new DiagnosticCollector<>();
compiler.getTask(null, fileManager, collector, null, null, sources).call();
for (Diagnostic<? extends JavaFileObject> d : collector.getDiagnostics())
{
    System.out.println(d);
}
```

`Diagnostic` 对象包含有关问题位置的信息（包括文件名、行号和列号），以及人类可读的描述。

你也可以为标准文件管理器安装 `DiagnosticListener`，以便捕获关于文件缺失的消息：

```java
StandardJavaFileManager fileManager
      = compiler.getStandardFileManager(diagnostics, null, null);
```

### 8.2.4 从内存读取源文件

如果你动态生成源代码，可以让它从内存中编译，而无需将文件保存到磁盘。使用以下类来保存代码：

```java
public class StringSource extends SimpleJavaFileObject
{
```



```java
var loader = new ByteArrayClassLoader(classFileObjects);
var frame = (JFrame) loader.loadClass("x.Frame").getConstructor().newInstance();
frame.setVisible(true);
```

当您单击按钮时，背景会像往常一样改变颜色。要查看操作是动态编译的，请更改 action.properties 中的一行，例如：

```java
yellowButton.setBackground(java.awt.Color.YELLOW); yellowButton.setEnabled(false);
```

再次运行程序。现在黄色按钮在单击后会被禁用。另外，请查看代码目录。您不会在 x 包中找到这些类的任何源文件或类文件。此示例演示了如何将动态编译与内存中的源文件和类文件结合使用。

### 清单 8.3 `compiler/CompilerTest.java`

```java
package compiler;

import java.awt.*;
import java.io.*;
import java.nio.file.*;
import java.util.*;
import java.util.List;

import javax.swing.*;
import javax.tools.*;
import javax.tools.JavaFileObject.*;

/**
 * @version 1.10 2018-05-01
 * @author Cay Horstmann
 */
public class CompilerTest
{
   public static void main(final String[] args)
         throws IOException, ReflectiveOperationException
   {
      JavaCompiler compiler = ToolProvider.getSystemJavaCompiler();

      var classFileObjects = new ArrayList<ByteArrayClass>();
      var diagnostics = new DiagnosticCollector<JavaFileObject>();

      JavaFileManager fileManager = compiler.getStandardFileManager(diagnostics, null, null);
      fileManager = new ForwardingJavaFileManager<JavaFileManager>(fileManager)
      {
         public JavaFileObject getJavaFileForOutput(Location location,
               String className, Kind kind, FileObject sibling) throws IOException
         {
```

### 清单 8.3（续）

```java
static JavaFileObject buildSource(String superclassName)
   throws IOException, ClassNotFoundException
{
   var builder = new StringBuilder();
   builder.append("package x;\n\n");
   builder.append("public class Frame extends " + superclassName + " {\n");
   builder.append("  protected void addEventHandlers() {\n");
   var props = new Properties();
   props.load(Files.newInputStream(Paths.get(
      superclassName.replace(".", "/")).getParent().resolve("action.properties")));
   for (Map.Entry<Object, Object> e : props.entrySet())
   {
      var beanName = (String) e.getKey();
      var eventCode = (String) e.getValue();
      builder.append("  " + beanName + ".addActionListener(event -> {\n");
      builder.append(eventCode);
      builder.append("\n });\n");
   }
   builder.append("} }\n");
   return new StringSource("x.Frame", builder.toString());
}
}
```

### 清单 8.4 `buttons2/ButtonFrame.java`

```java
package buttons2;

import javax.swing.*;

/**
 * A frame with a button panel.
 * @version 1.00 2007-11-02
 * @author Cay Horstmann
 */
public abstract class ButtonFrame extends JFrame
{
   public static final int DEFAULT_WIDTH = 300;
   public static final int DEFAULT_HEIGHT = 200;

   protected JPanel panel;
   protected JButton yellowButton;
   protected JButton blueButton;
   protected JButton redButton;

   public ButtonFrame()
   {
       setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);

       panel = new JPanel();
       add(panel);

       yellowButton = new JButton("Yellow");
       blueButton = new JButton("Blue");
       redButton = new JButton("Red");

       panel.add(yellowButton);
       panel.add(blueButton);
       panel.add(redButton);

       addEventHandlers();
   }

   protected abstract void addEventHandlers();
}
```

### 清单 8.5 `buttons2/action.properties`

```properties
yellowButton=panel.setBackground(java.awt.Color.YELLOW);
blueButton=panel.setBackground(java.awt.Color.BLUE);
```

### javax.tools.Tool 6

- `int run(InputStream in, OutputStream out, OutputStream err, String... arguments)`  
  使用给定的输入、输出和错误流以及给定的参数运行该工具。成功时返回 0，失败时返回非零值。

### javax.tools.JavaCompiler 6

- `StandardJavaFileManager getStandardFileManager(DiagnosticListener<? super JavaFileObject> diagnosticListener, Locale locale, Charset charset)`  
  获取此编译器的标准文件管理器。您可以按默认错误报告、区域设置和字符集传入 null。
- `JavaCompiler.CompilationTask getTask(Writer out, JavaFileManager fileManager, DiagnosticListener<? super JavaFileObject> diagnosticListener, Iterable<String> options, Iterable<String> classesForAnnotationProcessing, Iterable<? extends JavaFileObject> sourceFiles)`  
  获取一个编译任务，调用该任务时会编译给定的源文件。有关详细信息，请参阅前文的讨论。

| 类 | 版本 | 成员 | 描述 |
|---|---|---|---|
| `javax.tools.StandardJavaFileManager` | 6 | • `Iterable<? extends JavaFileObject> getJavaFileObjectsFromStrings(Iterable<String> filenames)`<br>• `Iterable<? extends JavaFileObject> getJavaFileObjectsFromFiles(Iterable<? extends File> files)` | 将一系列文件名或文件转换为一系列 JavaFileObject 实例。 |

| 类 | 版本 | 成员 | 描述 |
|---|---|---|---|
| `javax.tools.JavaCompiler.CompilationTask` | 6 | • `Boolean call()` | 执行编译任务。 |

| 类 | 版本 | 成员 | 描述 |
|---|---|---|---|
| `javax.tools.DiagnosticCollector<S>` | 6 | • `DiagnosticCollector()` | 构造一个空的收集器。 |
| `javax.tools.DiagnosticCollector<S>` | 6 | • `List<Diagnostic<? extends S>> getDiagnostics()` | 获取收集到的诊断信息。 |

| 类 | 版本 | 成员 | 描述 |
|---|---|---|---|
| `javax.tools.Diagnostic<S>` | 6 | • `S getSource()` | 获取与该诊断关联的源对象。 |
| `javax.tools.Diagnostic<S>` | 6 | • `Diagnostic.Kind getKind()` | 获取此诊断的类型——ERROR、WARNING、MANDATORY_WARNING、NOTE 或 OTHER。 |
| `javax.tools.Diagnostic<S>` | 6 | • `String getMessage(Locale locale)` | 获取描述此诊断所引发问题的消息。传入 null 以使用默认区域设置。 |
| `javax.tools.Diagnostic<S>` | 6 | • `long getLineNumber()`<br>• `long getColumnNumber()` | 获取此诊断所引发问题的位置。 |

| 类 | 成员 | 描述 |
|---|---|---|
| `javax.tools.SimpleJavaFileObject` | • `CharSequence getCharContent(boolean ignoreEncodingErrors)` | 为表示源文件并生成源代码的文件对象重写此方法。 |
| `javax.tools.SimpleJavaFileObject` | • `OutputStream openOutputStream()` | 为表示类文件并生成可写入字节码的流的文件对象重写此方法。 |

| 类 | 成员 | 描述 |
|---|---|---|
| `javax.tools.ForwardingJavaFileManager<M extends JavaFileManager>` | • `protected ForwardingJavaFileManager(M fileManager)` | 构造一个将所有调用委托给给定文件管理器的 JavaFileManager。 |
| `javax.tools.ForwardingJavaFileManager<M extends JavaFileManager>` | • `FileObject getFileForOutput(JavaFileManager.Location location, String className, JavaFileObject.Kind kind, FileObject sibling)` | 如果您想替换文件对象来写入类文件，请拦截此调用；kind 是 SOURCE、CLASS、HTML 或 OTHER。 |

## 8.3 使用注解

注解是插入到源代码中的标签，以便某些工具可以处理它们。这些工具可以在源代码级别操作，也可以处理编译器已将注解放入其中的类文件。

注解不会改变程序的编译方式。无论有没有注解，Java 编译器都会生成相同的虚拟机指令。

要从注解中获益，您需要选择一个处理工具。使用您的处理工具能够理解的注解，然后将处理工具应用到您的代码中。

注解的用途非常广泛，这种通用性一开始可能会令人困惑。以下是注解的一些用途：

- 自动生成辅助文件，例如部署描述符或 bean 信息类
- 自动生成用于测试、日志记录、事务语义等的代码

### 8.3.1 注解简介

我们将从基本概念开始讨论注解，并将其应用到一个具体示例中。在该示例中，我们将方法标记为 AWT 组件的事件监听器，并向您展示一个注解处理器，该处理器分析注解并连接监听器。然后我们将详细讨论语法规则，并以两个注解处理的高级示例结束本章。其中一个处理源代码级注解，另一个使用 Apache 字节码工程库处理类文件，向被注解的方法注入额外的字节码。

下面是一个简单注解的示例：

```java
public class MyClass
{
    ...
    @Test public void checkRandomInsertions()
    {
    }
}
```

注解 @Test 对 checkRandomInsertions 方法进行了注解。

在 Java 中，注解的使用方式类似于*修饰符*，并且放在被注解条目之前，*不带分号*。（修饰符是诸如 public 或 static 之类的关键字。）每个注解的名称前面都有一个 @ 符号，类似于 Javadoc 注释。但是，Javadoc 注释位于 /* ... */ 分隔符内，而注解是代码的一部分。

@Test 注解本身并不做任何事情。它需要一个工具才能发挥作用。例如，JUnit 测试工具（可从 http://junit.org 获取）在测试类时会调用所有标记为 @Test 的方法。另一个工具可能会从类文件中删除所有测试方法，以便在测试完成后它们不会随程序一起发布。

注解可以定义*元素*，例如

```java
@Test(timeout="10000")
```

这些元素可以由读取注解的工具来处理。元素还有其他形式；我们将在本章后面讨论。

除了方法之外，您还可以注解类、字段和局部变量——注解可以放在任何可以放置修饰符（如 public 或 static）的位置。此外，正如您将在第 471 页的 8.4 节“注解语法”中看到的，您还可以注解包、参数变量、类型参数和类型使用。




每个注解都必须由一个*注解接口*定义。接口的方法对应于注解的元素。例如，JUnit Test 注解由以下接口定义：

```java
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
public @interface Test
{
    long timeout() default 0L;
    ...
}
```

@interface 声明会创建一个实际的 Java 接口。处理注解的工具会收到实现该注解接口的对象。工具会调用 timeout 方法，以获取某个特定 Test 注解的 timeout 元素。

Target 和 Retention 注解是*元注解*。它们注解 Test 注解，将其标记为只能应用于方法、并且在类文件加载到虚拟机中时保留的注解。我们将在第 481 页的第 8.5.3 节“元注解”中详细讨论这些内容。

现在你已经了解了程序元数据和注解的基本概念。在下一节中，我们将逐步讲解一个注解处理的具体示例。

> **注意：** 关于注解的一个有说服力的用途，请查看 JCommander（http://jcommander.org）和 picocli（http://picocli.info）。这些库使用注解来处理命令行参数。

### 8.3.2 示例：为事件处理器添加注解

用户界面编程中比较枯燥的任务之一，是将监听器连接到事件源。许多监听器都是这种形式

```java
myButton.addActionListener(() -> doSomething());
```

在本节中，我们将设计一个注解来反转这种连接方式。该注解在清单 8.8 中定义，使用方式如下：

```java
@ActionListenerFor(source="myButton") void doSomething() { . . . }
```

程序员不再需要调用 addActionListener。相反，每个方法都用注解标记。清单 8.7 展示了第 I 卷第 10 章中的 ButtonFrame 类，它使用这些注解重新实现。

#### 清单 8.7 `buttons3/ButtonFrame.java`

```java
package buttons3;

import java.awt.*;
import javax.swing.*;
import runtimeAnnotations.*;

/**
 * A frame with a button panel.
 * @version 1.00 2004-08-17
 * @author Cay Horstmann
 */
public class ButtonFrame extends JFrame
{
   private static final int DEFAULT_WIDTH = 300;
   private static final int DEFAULT_HEIGHT = 200;

   private JPanel panel;
   private JButton yellowButton;
   private JButton blueButton;
   private JButton redButton;

   public ButtonFrame()
   {
      setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);

      panel = new JPanel();
      add(panel);

      yellowButton = new JButton("Yellow");
      blueButton = new JButton("Blue");
      redButton = new JButton("Red");

      panel.add(yellowButton);
      panel.add(blueButton);
      panel.add(redButton);

      ActionListenerInstaller.processAnnotations(this);
   }

   @ActionListenerFor(source = "yellowButton")
   public void yellowBackground()
   {
      panel.setBackground(Color.YELLOW);
   }

   @ActionListenerFor(source = "blueButton")
   public void blueBackground()
   {
      panel.setBackground(Color.BLUE);
   }

   @ActionListenerFor(source = "redButton")
   public void redBackground()
   {
      panel.setBackground(Color.RED);
   }
}
```

#### 清单 8.8 `runtimeAnnotations/ActionListenerFor.java`

```java
package runtimeAnnotations;

import java.lang.annotation.*;

/**
 * @version 1.00 2004-08-17
 * @author Cay Horstmann
 */
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
public @interface ActionListenerFor
{
    String source();
}
```

#### `java.lang.reflect.AnnotatedElement` 5.0

- `boolean isAnnotationPresent(Class<? extends Annotation> annotationType)`  
  如果此项具有给定类型的注解，则返回 true。
- `<T extends Annotation> T getAnnotation(Class<T> annotationType)`  
  获取给定类型的注解；如果此项没有此类注解，则返回 null。
- `<T extends Annotation> T[] getAnnotationsByType(Class<T> annotationType)`  
  获取可重复注解类型的所有注解（见第 481 页的第 8.5.3 节“元注解”），如果没有则返回长度为 0 的数组。
- `Annotation[] getAnnotations()`  
  获取此项存在的所有注解，包括继承的注解。如果不存在任何注解，则返回长度为 0 的数组。
- `Annotation[] getDeclaredAnnotations()`  
  获取此项声明的所有注解，不包括继承的注解。如果不存在任何注解，则返回长度为 0 的数组。

## 8.4 注解语法

在以下各节中，我们将介绍你需要了解的关于注解语法的所有内容。

### 8.4.1 注解接口

注解由注解接口定义：

```java
modifiers @interface AnnotationName
{
    elementDeclaration1
    elementDeclaration2
    . . .
}
```

每个元素声明都具有以下形式

```java
type elementName();
```

或

```java
type elementName() default value;
```

例如，以下注解有两个元素：assignedTo 和 severity：

```java
public @interface BugReport
{
    String assignedTo() default "[none]";
    int severity();
}
```

所有注解接口都隐式扩展 java.lang.annotation.Annotation 接口。该接口是一个普通接口，而不是注解接口。有关此接口提供的方法，请参阅本节末尾的 API 说明。你不能扩展注解接口——换句话说，所有注解接口都直接扩展 java.lang.annotation.Annotation。你永远不需要提供实现注解接口的类。

```java
public @interface ActionListenerFor
{
    String value();
}
```

那么这些注解可以写成

```java
@ActionListenerFor("yellowButton")
```

而不是

```java
@ActionListenerFor(value="yellowButton")
```

一个项可以有多个注解：

```java
@Test
@BugReport(showStopper=true, reportedBy="Joe")
public void checkRandomInsertions()
```

如果某个注解被声明为可重复的，你可以多次重复同一个注解：

```java
@BugReport(showStopper=true, reportedBy="Joe")
@BugReport(reportedBy={"Harry", "Carl"})
public void checkRandomInsertions()
```

> **注意：** 由于注解由编译器求值，所有元素值
> 都必须是编译期常量。例如，
>
> ```java
> @BugReport(showStopper=true, assignedTo="Harry", testCase=MyTestCase.class,
>     status=BugReport.Status.CONFIRMED, . . .)
> ```

> **警告：** 注解元素永远不能设置为 null。甚至不允许默认值为 null。
> 这在实践中可能相当不便。你需要找到其他默认值，例如 "" 或 Void.class。

如果元素值是数组，请将其值括在花括号中：

```java
@BugReport({. . ., reportedBy={"Harry", "Carl"}})
```

如果元素只有一个值，你可以省略花括号：

```java
@BugReport(. . ., reportedBy="Joe") // OK, same as {"Joe"}
```

由于注解元素可以是另一个注解，因此你可以构建任意复杂的注解。例如，

```java
@BugReport(ref=@Reference(id="3352627"), . . .)
```

> **注意：** 在注解中引入循环依赖是错误的。例如，`BugReport` 有一个注解类型为 `Reference` 的元素，因此 `Reference` 不能有一个类型为 `BugReport` 的元素。

### 8.4.3 为声明添加注解

注解可以出现在许多地方。它们分为两类：*声明*和*类型使用*。声明注解可以出现在以下声明处：

- 包
- 类（包括 `enum`）
- 接口（包括注解接口）
- 方法
- 构造器
- 实例字段（包括 `enum` 常量）
- 局部变量
- 参数变量
- 类型参数

对于类和接口，请将注解放置在 class 或 interface 关键字之前：

```java
@Entity public class User { . . . }
```

对于变量，请将它们放在类型之前：

```java
@SuppressWarnings("unchecked") List<User> users = . . .;
public User getUser(@Param("id") String userId)
```

泛型类或方法中的类型参数可以像这样添加注解：

```java
public class Cache<@Immutable V> { . . . }
```

包在文件 `package-info.java` 中添加注解，该文件只包含前面带有注解的 package 语句。

```java
/**
 * Package-level Javadoc
 */
@GPL(version="3")
package com.horstmann.corejava;
import org.gnu.GPL;
```




> **注意：** 局部变量的注解只能在源代码级别处理。类文件不会描述局部变量。因此，当类被编译时，所有局部变量注解都会被丢弃。同样，包的注解在超出源代码级别后不会保留。

### 8.4.4 标注类型使用

声明注解提供有关被声明项的一些信息。例如，在以下声明中

```java
public User getUser(@NonNull String userId)
```

它断言 `userId` 参数不为 null。

> **注意：** `@NonNull` 注解是 Checker Framework（https://checkerframework.org）的一部分。使用该框架，你可以在程序中包含断言——例如，某个参数非空，或某个 String 包含正则表达式。然后，静态分析工具会检查这些断言在给定的源代码体中是否有效。

现在，假设我们有一个类型为 `List<String>` 的参数，并且我们想表达所有字符串都非空。这正是类型使用注解的用武之地。将注解放在类型参数之前：`List<@NonNull String>`。

类型使用注解可以出现在以下位置：

- 与泛型类型参数一起：`List<@NonNull String>`、`Comparator<@NonNull String> reverseOrder()`。
- 在数组的任意位置：`@NonNull String[][] words`（`words[i][i]` 不为 null）、`String @NonNull [] words`（words 不为 null）、`String[] @NonNull [] words`（`words[i]` 不为 null）。
- 与超类和已实现的接口一起：`class Warning extends @Localized Message`。
- 与构造器调用一起：`new @Localized String(...)`。
- 与强制类型转换和 instanceof 检查一起：`(@Localized String) text`、`if (text instanceof @Localized String)`。这些注解仅供外部工具使用。它们对强制类型转换或 instanceof 检查的行为没有影响。
- 与异常规范一起：`public String read() throws @Localized IOException`。
- 与通配符和类型边界一起：`List<@Localized String> extends Message`、`List<? extends @Localized Message>`。
- 与方法引用和构造器引用一起：`@Localized Message::getText`。

```java
public class Point
{
    public boolean equals(@ReadOnly Point this, @ReadOnly Object other) { . . . }
}
```

第一个参数称为*接收者参数*。它必须命名为 `this`。其类型是正在被构造的类。

> **注意：** 只能为方法提供接收者参数，不能为构造器提供。从概念上讲，在构造器完成之前，构造器中的 this 引用并不是给定类型的对象。相反，放在构造器上的注解描述的是被构造对象的属性。

一个不同的隐藏参数会传递给内部类的构造器，即对外围类对象的引用。你也可以将该参数显式化：

```java
public class Sequence
{
    private int from;
    private int to;

    class Iterator implements java.util.Iterator<Integer>
    {
        private int current;
        public Iterator(@ReadOnly Sequence Sequence.this)
        {
            this.current = Sequence.this.from;
        }
        . . .
    }
    . . .
}
```

该参数的命名必须与你引用它时相同，即 `EnclosingClass.this`，其类型是外围类。

## 8.5 标准注解

`java.lang`、`java.lang.annotation` 和 `javax.annotation` 包中定义了许多注解接口。其中四个是描述注解接口行为的元注解。其他是常规注解，可用于标注源代码中的项。表 8.2 展示了这些注解。我们将在接下来的两节中详细讨论它们。

### 8.5.1 用于编译的注解

`@Deprecated` 注解可以附加到任何不再鼓励使用的项上。当你使用已弃用的项时，编译器会警告你。此注解的作用与 `@deprecated` Javadoc 标签相同。但是，该注解会一直保留到运行时。

> **注意：** JDK 自带的 `jar` 工具可以扫描一组 JAR 文件中的已弃用元素。

`@SuppressWarnings` 注解告诉编译器抑制特定类型的警告，例如：

```java
@SuppressWarnings("unchecked")
```

`@Override` 注解仅适用于方法。编译器会检查带有此注解的方法是否确实重写了超类中的方法。例如，如果你声明

```java
public class MyClass
{
    @Override public boolean equals(MyClass other);
    . . .
}
```

那么编译器将报告错误。毕竟，equals 方法*不会*重写 Object 类的 equals 方法，因为该方法的参数类型是 Object，而不是 MyClass。

`@Generated` 注解旨在供代码生成器工具使用。任何生成的源代码都可以被标注，以将其与程序员创建的代码区分开来。例如，代码编辑器可以隐藏生成的代码，或者代码生成器可以移除生成代码的旧版本。每个注解必须包含代码生成器的唯一标识符。日期字符串（采用 ISO 8601 格式）和注释字符串是可选的。例如，

```java
@Generated("com.horstmann.beanproperty", "2008-01-04T12:08:56.235-0700");
```

### 8.5.2 用于管理资源的注解

`@PostConstruct` 和 `@PreDestroy` 注解用于控制对象生命周期的环境，例如 Web 容器和应用服务器。带有这些注解的方法应在对象构造完成后立即调用，或在对象被移除之前立即调用。

`@Resource` 注解旨在用于资源注入。例如，考虑一个访问数据库的 Web 应用。当然，数据库访问信息不应硬编码到 Web 应用中。相反，Web 容器具有某种用户界面，用于设置连接参数和数据源的 JNDI 名称。在 Web 应用中，你可以像这样引用数据源：

```java
@Resource(name="jdbc/mydb")
private DataSource source;
```

当包含此字段的对象被构造时，容器会“注入”对数据源的引用。

### 8.5.3 元注解

`@Target` 元注解应用于注解，限制该注解所适用的项。例如，

```java
@Target({ElementType.TYPE, ElementType.METHOD})
public @interface BugReport
```

表 8.3 展示了所有可能的值。它们属于枚举类型 ElementType。你可以指定任意数量的元素类型，用花括号括起来。

**表 8.3** @Target 注解的元素类型

| 元素类型 | 注解适用于 |
|---|---|
| ANNOTATION_TYPE | 注解类型声明 |
| PACKAGE | 包 |
| TYPE | 类（包括枚举）和接口（包括注解类型） |
| METHOD | 方法 |
| CONSTRUCTOR | 构造器 |
| FIELD | 字段（包括枚举常量） |
| PARAMETER | 方法或构造器参数 |
| LOCAL_VARIABLE | 局部变量 |
| TYPE_PARAMETER | 类型参数 |
| TYPE_USE | 类型的使用 |

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_505_0.png)

图 8.2 文档化注解

`@Inherited` 元注解仅适用于类的注解。当一个类具有继承注解时，它的所有子类都会自动具有相同的注解。这使得创建像标记接口（例如 Serializable）那样工作的注解变得容易。

事实上，注解 `@Serializable` 会比没有方法的 Serializable 标记接口更合适。一个类之所以可序列化，是因为有运行时支持读取和写入其字段，而不是因为任何面向对象设计原则。注解比接口继承更好地描述了这一事实。当然，Serializable 接口是在 JDK 1.1 中创建的，远早于注解的出现。

假设你定义了一个继承注解 `@Persistent`，以表示某个类的对象可以保存在数据库中。那么持久类的子类会自动被标注为持久。

```java
@Inherited @interface Persistent { }
@Persistent class Employee { . . . }
class Manager extends Employee { . . . } // also @Persistent
```

当持久化机制搜索要存储到数据库中的对象时，它会检测到 Employee 和 Manager 对象。





从 Java 8 开始，可以将同一个注解类型多次应用于同一项。为了向后兼容，可重复注解的实现者需要提供一个*容器注解*，用于将重复的注解保存在数组中。

下面演示如何定义 @TestCase 注解及其容器：

```java
@Repeatable(TestCases.class)
@interface TestCase
{
   String params();
   String expected();
}

@interface TestCases
{
   TestCase[] value();
}
```

当用户提供两个或更多 @TestCase 注解时，它们会自动被包装进一个 @TestCases 注解中。

> **注意：** 处理可重复注解时你必须小心。如果调用 `getAnnotation` 来查找某个可重复注解，而该注解实际上是被重复使用的，那么你会得到 `null`。这是因为重复的注解被包装进了容器注解中。
> 
> 在这种情况下，你应该调用 `getAnnotationsByType`。该方法会“穿透”容器，并返回一个包含重复注解的数组。如果只有一个注解，你会得到长度为 1 的数组。使用这个方法，你就不必担心容器注解了。

## 8.6 源代码级注解处理

在前一节中，你了解了如何在运行中的程序里分析注解。注解的另一个用途是自动处理源文件，以生成更多的源代码、配置文件、脚本或任何其他想要生成的内容。

### 8.6.1 注解处理器

注解处理已集成到 Java 编译器中。在编译期间，你可以通过运行以下命令来*调用注解处理器*：

```
javac -processor ProcessorClassName₁,ProcessorClassName₂, . . . sourceFiles
```

编译器会定位源文件中的注解。每个注解处理器依次执行，并被赋予它所感兴趣的注解。如果某个注解处理器创建了新的源文件，该过程会重复进行。一旦某一轮处理没有生成更多源文件，所有源文件就会被编译。

> **注意：** 注解处理器只能生成新的源文件，它不能修改已有的源文件。

注解处理器实现 `Processor` 接口，通常通过扩展 `AbstractProcessor` 类来实现。你需要指定处理器支持哪些注解。在我们的例子中：

```java
@SupportedAnnotationTypes("com.horstmann.annotations.ToString")
@SupportedSourceVersion(SourceVersion.RELEASE_8)
public class ToStringAnnotationProcessor extends AbstractProcessor
{
   public boolean process(Set<? extends TypeElement> annotations,
         RoundEnvironment currentRound)
   {
      . . .
   }
}
```

处理器可以声明特定的注解类型、通配符（如 `"com.horstmann.*"`，表示 `com.horstmann` 包或其任何子包中的所有注解），甚至可以声明 `"*"`（所有注解）。

每一轮处理都会调用一次 `process` 方法，参数包括本轮在所有文件中发现的所有注解集合，以及一个包含当前处理轮次信息的 `RoundEnvironment` 引用。

### 8.6.2 语言模型 API

使用*语言模型* API 来分析源代码级注解。与反射 API（它呈现的是类和方法的虚拟机表示）不同，语言模型 API 让你能够按照 Java 语言的规则来分析 Java 程序。

编译器会生成一棵树，其节点是实现了 `javax.lang.model.element.Element` 接口及其子接口（`TypeElement`、`VariableElement`、`ExecutableElement` 等）的类的实例。这些是反射类 `Class`、`Field/Parameter`、`Method/Constructor` 的编译期对应物。

我不想详细讲解该 API，但以下是处理注解时你需要了解的重点：

- `RoundEnvironment` 会为你提供所有带有特定注解的元素集合。调用以下方法：

      `Set<? extends Element> getElementsAnnotatedWith(Class<? extends Annotation> a)`

- `AnnotatedElement` 接口在源代码级别的等价物是 `AnnotatedConstruct`。使用以下方法：

      `A getAnnotation(Class<?> annotationType)`
      `A[] getAnnotationsByType(Class<?> annotationType)`

  来获取给定注解类的注解或重复注解。

- `TypeElement` 表示一个类或接口。`getEnclosedElements` 方法会返回其字段和方法的列表。

- 在 `Element` 上调用 `getSimpleName`，或在 `TypeElement` 上调用 `getQualifiedName`，会得到一个 `Name` 对象，可以通过 `toString` 将其转换为字符串。

### 8.6.3 使用注解生成源代码

作为示例，我们将使用注解来减少实现 `toString` 方法的繁琐工作。我们不能把这些方法放入原始类中——注解处理器只能生成新类，不能修改已有的类。

因此，我们将所有方法添加到一个工具类 `ToStrings` 中：

```java
public class ToStrings
{
   public static String toString(Point obj)
   {
      生成的代码
   }
   public static String toString(Rectangle obj)
   {
      生成的代码
   }
   . . .

   public static String toString(Object obj)
   {
      return Objects.toString(obj);
   }
}
```

我们不想使用反射，因此我们注解的是访问器方法，而不是字段：

```java
@ToString
public class Rectangle
{
    ...
    @ToString(includeName=false) public Point getTopLeft() { return topLeft; }
    @ToString public int getWidth() { return width; }
    @ToString public int getHeight() { return height; }
}
```

注解处理器随后应生成以下源代码：

```java
public static String toString(Rectangle obj)
{
    var result = new StringBuilder();
    result.append("Rectangle");
    result.append("{");
    result.append(obj.toString(obj).getTopLeft());
    result.append(",");
    result.append("width=");
    result.append(obj.toString(obj).getWidth());
    result.append(",");
    result.append("height=");
    result.append(obj.toString(obj).getHeight());
    result.append("}");
    return result.toString();
}
```

“样板”代码以灰色显示。以下是生成某个类（由给定 `TypeElement` 表示）的 `toString` 方法的方法概要：

```java
private void writeToStringMethod(PrintWriter out, TypeElement te)
{
    String className = te.getQualifiedName().toString();
    打印方法头以及 StringBuilder 的声明
    ToString ann = te.getAnnotation(ToString.class);
    if (ann.includeName())
        打印添加类名的代码
    for (Element c : te.getEnclosedElements())
    {
        ann = c.getAnnotation(ToString.class);
        if (ann != null)
        {
            if (ann.includeName()) 打印添加字段名的代码
            打印追加 toString(obj.methodName()) 的代码
        }
    }
}
打印返回字符串的代码
```

下面是注解处理器中 `process` 方法的概要。它为辅助类创建一个源文件，并写入类头以及每个被注解类的一个方法。

```java
public boolean process(Set<? extends TypeElement> annotations,
        RoundEnvironment currentRound)
{
    if (annotations.size() == 0) return true;
    try
    {
        JavaFileObject sourceFile = processingEnv.getFiler().createSourceFile(
                "com.horstmann.annotations.ToStrings");
        try (var out = new PrintWriter(sourceFile.openWriter()))
        {
            // 打印包和类的代码
            for (Element e : currentRound.getElementsAnnotatedWith(ToString.class))
            {
                if (e instanceof TypeElement)
                {
                    TypeElement te = (TypeElement) e;
                    writeToStringMethod(out, te);
                }
            }
            // 打印 toString(Object) 的代码
        }
        catch (IOException ex)
        {
            processingEnv.getMessager().printMessage(
                    Kind.ERROR, ex.getMessage());
        }
    }
    return true;
}
```

至于那些繁琐的细节，请查看本书的配套代码。

请注意，在后续轮次中，`process` 方法会以一个空的注解列表被调用。此时它会立即返回，以避免重复创建源文件。

首先编译注解处理器，然后按如下方式编译并运行测试程序：

```text
javac sourceAnnotations/ToStringAnnotationProcessor.java
javac -processor sourceAnnotations.ToStringAnnotationProcessor rect/*.java
java rect.SourceLevelAnnotationDemo
```




**提示：** 要查看各轮次，请使用 `-XprintRounds` 标志运行 `javac` 命令：

```text
Round 1:
    input files: {rect.Point, rect.Rectangle,
        rect.SourceLevelAnnotationDemo}
    annotations: [sourceAnnotations.ToString]
    last round: false
Round 2:
    input files: {sourceAnnotations.ToStrings}
    annotations: []
    last round: false
Round 3:
    input files: {}
    annotations: []
    last round: true
```

此示例演示了工具如何收集源文件注解以生成其他文件。生成的文件不必是源文件。注解处理器可以选择生成 XML 描述符、属性文件、shell 脚本、HTML 文档等。

**注意：** 有些人建议使用注解来消除更大的苦差事。如果简单的 getter 和 setter 能够自动生成，那岂不是很好？例如，注解

```java
@Property private String title;
```

可以生成以下方法

```java
public String getTitle() { return title; }
public void setTitle(String title) { this.title = title; }
```

然而，这些方法需要添加到同一个类中。这需要编辑源文件，而不仅仅是生成另一个文件，并且超出了注解处理器的能力。可以为此构建另一个工具，但这样的工具将超出注解的使命。注解旨在作为*关于*代码项的说明，而不是用于添加或更改代码的指令。

## 8.7 字节码工程

你已经看到注解如何在运行时或源代码级别进行处理。还有第三种可能：在字节码级别进行处理。除非在源代码级别移除注解，否则它们会存在于类文件中。类文件格式已有文档记录（见 http://docs.oracle.com/javase/specs/jvms/se10/html）。该格式相当复杂，如果没有专用库，处理类文件将颇具挑战性。其中一个这样的库是 ASM 库，可从 http://asm.ow2.org 获取。

### 8.7.1 修改类文件

在本节中，我们使用 ASM 向带注解的方法添加日志消息。如果一个方法使用

```java
@LogEntry(logger=loggerName)
```

进行注解，那么我们在该方法开头添加以下语句的字节码：

```java
Logger.getLogger(loggerName).entering(className, methodName);
```

例如，如果我们把 Item 类的 hashCode 方法注解为

```java
@LogEntry(logger="global") public int hashCode()
```

那么每当调用该方法时，都会打印类似以下内容的消息：

```text
May 17, 2016 10:57:59 AM Item hashCode
FINER: ENTRY
```

为此，我们执行以下操作：

- 1. 加载类文件中的字节码。
- 2. 定位所有方法。
- 3. 对于每个方法，检查它是否有 LogEntry 注解。
- 4. 如果有，则在方法开头添加以下指令的字节码：

```text
ldc loggerName
invokestatic
    java/util/logging/Logger.getLogger:(Ljava/lang/String;)Ljava/util/logging/Logger;
ldc className
ldc methodName
invokevirtual
    java/util/logging/Logger.entering:(Ljava/lang/String;Ljava/lang/String;)V
```

插入这些字节码听起来很棘手，但 ASM 使其相当简单。我们不会详细描述分析和插入字节码的过程。重点在于，代码清单 8.9 中的程序编辑一个类文件，并在带有 LogEntry 注解的方法开头插入日志调用。

例如，下面展示如何将日志指令添加到代码清单 8.10 中的 Item.java，其中 `asm` 是你安装 ASM 库的目录：

```text
javac set/Item.java
javac -classpath .:asm/lib/* bytecodeAnnotations/EntryLogger.java
java -classpath .:asm/lib/* bytecodeAnnotations.EntryLogger set.Item
```

尝试运行

```text
javap -c set.Item
```

在修改 Item 类文件之前和之后。你可以看到在 hashCode、equals 和 compareTo 方法开头插入的指令。

```text
public int hashCode();
  0: ldc           #85; // String global
  2: invokestatic  #89;
     // Method java/util/logging/Logger.getLogger:(Ljava/lang/String;)Ljava/util/logging/Logger;
  5: ldc           #86; // String Item
  7: ldc           #88; // String hashCode
  9: invokevirtual #84;
     // Method java/util/logging/Logger.entering:(Ljava/lang/String;Ljava/lang/String;)V
 12: bipush        13
 14: aload_0
 15: getfield       #2; // Field description:Ljava/lang/String;
 18: invokevirtual #15; // Method java/lang/String.hashCode:()I
 21: imul
 22: bipush        17
 24: aload_0
 25: getfield       #3; // Field partNumber:I
 28: imul
 29: iadd
 30: ireturn
```

代码清单 8.11 中的 SetTest 程序将 Item 对象插入哈希集。使用修改后的类文件运行它时，你将看到日志消息。

```text
May 17, 2016 10:57:59 AM Item hashCode
FINER: ENTRY
May 17, 2016 10:57:59 AM Item hashCode
FINER: ENTRY
May 17, 2016 10:57:59 AM Item hashCode
FINER: ENTRY
May 17, 2016 10:57:59 AM Item equals
FINER: ENTRY
[[description=Toaster, partNumber=1729], [description=Microwave, partNumber=4104]]
```

注意，当我们两次插入同一个项时，会调用 equals。

此示例展示了字节码工程的强大之处。注解用于向程序添加指令，而字节码编辑工具会读取这些指令并修改虚拟机指令。

**代码清单 8.9** `bytecodeAnnotations/EntryLogger.java`

```java
 1  package bytecodeAnnotations;
 2
 3  import java.io.*;
 4  import java.nio.file.*;
 5
 6  import org.objectweb.asm.*;
 7  import org.objectweb.asm.commons.*;
 8
 9  /**
10   * Adds "entering" logs to all methods of a class that have the LogEntry annotation.
11   * @version 1.21 2018-05-01
12   * @author Cay Horstmann
13   */
14  public class EntryLogger extends ClassVisitor
15  {
16      private String className;
17
18      /**
19       * Constructs an EntryLogger that inserts logging into annotated methods of a given class.
20       * @param cg the class
21       */
22      public EntryLogger(ClassWriter writer, String className)
23      {
24          super(Opcodes.ASM5, writer);
25          this.className = className;
26      }
27
28      public MethodVisitor visitMethod(int access, String methodName, String desc,
29            String signature, String[] exceptions)
30      {
31          MethodVisitor mv = cv.visitMethod(access, methodName, desc, signature, exceptions);
32          return new AdviceAdapter(Opcodes.ASM5, mv, access, methodName, desc)
33          {
34              private String loggerName;
35
36              public AnnotationVisitor visitAnnotation(String desc, boolean visible)
37              {
38                  return new AnnotationVisitor(Opcodes.ASM5)
39                  {
40                      public void visit(String name, Object value)
41                      {
42                          if (desc.equals("LbytecodeAnnotations/LogEntry;")
43                              && name.equals("logger"))
44                              loggerName = value.toString();
45                      }
46                  };
47              }
48
49              public void onMethodEnter()
50              {
51                  if (loggerName != null)
52                  {
53                      visitLdcInsn(loggerName);
54                      visitMethodInsn(INVOKESTATIC, "java/util/logging/Logger", "getLogger",
55                          "(Ljava/lang/String;)Ljava/util/logging/Logger;", false);
56                      visitLdcInsn(className);
57                      visitLdcInsn(methodName);
58                      visitMethodInsn(INVOKEVIRTUAL, "java/util/logging/Logger", "entering",
59                          "(Ljava/lang/String;Ljava/lang/String;)V", false);
60                      loggerName = null;
61                  }
62              }
63          };
64      }
65
66      /**
67       * Adds entry logging code to the given class.
68       * @param args the name of the class file to patch
69       */
70      public static void main(String[] args) throws IOException
71      {
72          if (args.length == 0)
73          {
74              System.out.println("USAGE: java bytecodeAnnotations.EntryLogger classfile");
75              System.exit(1);
76          }
77          Path path = Paths.get(args[0]);
78          var reader = new ClassReader(Files.newInputStream(path));
79          var writer = new ClassWriter(
80              ClassWriter.COMPUTE_MAXS | ClassWriter.COMPUTE_FRAMES);
81          var entryLogger = new EntryLogger(writer,
82              path.toString().replaceAll("[/\\\\]", "."));
83          reader.accept(entryLogger, ClassReader.EXPAND_FRAMES);
84          Files.write(Paths.get(args[0]), writer.toByteArray());
85      }
86  }
```



#### 代码清单 8.10 `set/Item.java`

```java
package set;

import java.util.*;
import bytecodeAnnotations.*;

/**
 * An item with a description and a part number.
 * @version 1.01 2012-01-26
 * @author Cay Horstmann
 */
public class Item
{
   private String description;
   private int partNumber;

   /**
    * Constructs an item.
    * @param aDescription the item's description
    * @param aPartNumber the item's part number
    */
   public Item(String aDescription, int aPartNumber)
   {
      description = aDescription;
      partNumber = aPartNumber;
   }

   /**
    * Gets the description of this item.
    * @return the description
    */
   public String getDescription()
   {
      return description;
   }

   public String toString()
   {
      return "[description=" + description + ", partNumber=" + partNumber + "]";
   }

   @LogEntry(logger = "com.horstmann")
   public boolean equals(Object otherObject)
   {
      if (this == otherObject) return true;
      if (otherObject == null) return false;
      if (getClass() != otherObject.getClass()) return false;
      var other = (Item) otherObject;
      return Objects.equals(description, other.description) && partNumber == other.partNumber;
   }

   @LogEntry(logger = "com.horstmann")
   public int hashCode()
   {
      return Objects.hash(description, partNumber);
   }
}
```

#### 代码清单 8.11 `set/SetTest.java`

```java
package set;

import java.util.*;
import java.util.logging.*;

/**
 * @version 1.03 2018-05-01
 * @author Cay Horstmann
 */
public class SetTest
{
    public static void main(String[] args)
    {
        Logger.getLogger("com.horstmann").setLevel(Level.FINEST);
        var handler = new ConsoleHandler();
        handler.setLevel(Level.FINEST);
        Logger.getLogger("com.horstmann").addHandler(handler);

        var parts = new HashSet<Item>();
        parts.add(new Item("Toaster", 1279));
        parts.add(new Item("Microwave", 494));
        parts.add(new Item("Toaster", 1279));
        System.out.println(parts);
    }
}
```

### 8.7.2 在加载时修改字节码

上一节中，你看到了一个编辑类文件的工具。然而，在构建过程中再添加一个工具可能会很麻烦。一个有吸引力的替代方案是将字节码工程推迟到*加载时*，也就是类加载器加载类的时候。

*插桩 API* 提供了一个用于安装字节码转换器的钩子。转换器必须在程序的 main 方法被调用之前安装。你可以通过定义一个*代理*来满足这一要求，代理是一个被加载以某种方式监视程序的库。代理代码可以在 premain 方法中执行初始化。

以下是构建代理所需的步骤：

- 1. 实现一个包含如下方法的类

  ```java
  public static void premain(String arg, Instrumentation instr)
  ```

  该方法在代理加载时被调用。代理可以获取一个命令行参数，该参数通过 arg 参数传入。instr 参数可用于安装各种钩子。

- 2. 创建一个清单文件 `EntryLoggingAgent.mf`，设置 Premain-Class 属性，例如：

  ```text
  Premain-Class: bytecodeAnnotations.EntryLoggingAgent
  ```

- 3. 将代理代码和清单打包到一个 JAR 文件中：

  ```shell
  javac -classpath .:asm/lib/* bytecodeAnnotations/EntryLoggingAgent.java
  jar cvfm EntryLoggingAgent.jar bytecodeAnnotations/EntryLoggingAgent.mf \
      bytecodeAnnotations/EntryLoggingAgent*.class
  ```

要连同代理一起启动 Java 程序，请使用以下命令行选项：

```shell
java -javaagent:AgentJARFile=agentArgument
```

例如，要使用入口日志代理运行 SetTest 程序，请调用

```shell
javac set/SetTest.java
java -javaagent:EntryLoggingAgent.jar=set.Item -classpath .:asm/lib/* set.SetTest
```

Item 参数是代理应修改的类的名称。

代码清单 8.12 展示了代理代码。代理安装了一个类文件转换器。转换器首先检查类名是否与代理参数匹配。如果匹配，它就使用上一节中的 EntryLogger 类来修改字节码。不过，修改后的字节码不会保存到文件中。相反，转换器会返回它们，以便加载到虚拟机中（见图 8.3）。换句话说，这种技术对字节码执行“即时”修改。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_519_0.png)

**图 8.3** 在加载时修改类

#### 代码清单 8.12 `bytecodeAnnotations/EntryLoggingAgent.java`

```
1 package bytecodeAnnotations;
2
3 import java.lang.instrument.*;
4
5 import org.objectweb.asm.*;
6
7 /**
8  * @version 1.11 2018-05-01
9  * @author Cay Horstmann
10  */
11 public class EntryLoggingAgent
12 {
13    public static void premain(final String arg, Instrumentation instr)
14    {
15       instr.addTransformer((loader, className, cl, pd, data) ->
16       {
17          if (!className.replace("/", ".").equals(arg)) return null;
18          var reader = new ClassReader(data);
19          var writer = new ClassWriter(
20             ClassWriter.COMPUTE_MAXS | ClassWriter.COMPUTE_FRAMES);
21          var el = new EntryLogger(writer, className);
22          reader.accept(el, ClassReader.EXPAND_FRAMES);
23          return writer.toByteArray();
24       });
25    }
26 }
```

本章中，你学习了如何

- 向 Java 程序添加注解
- 设计自己的注解接口
- 实现利用注解的工具

你已经了解了三种处理代码的技术：脚本编写、编译 Java 程序以及处理注解。前两种相当直接。另一方面，构建注解工具无疑是复杂的，并不是大多数开发者需要处理的事情。本章为你提供了理解你将遇到的注解工具内部工作原理的背景知识，或许还激发了你开发自己的工具的兴趣。

下一章讨论 Java 平台模块系统，这是 Java 9 的关键特性，对于推动 Java 平台向前发展很重要。

# 第 9 章：Java 平台模块系统

## 本章内容

- 9.1 模块概念，第 500 页
- 9.2 命名模块，第 501 页
- 9.3 模块化的“Hello, World!”程序，第 502 页
- 9.4 依赖模块，第 504 页
- 9.5 导出包，第 506 页
- 9.6 模块化 JAR，第 510 页
- 9.7 模块与反射访问，第 511 页
- 9.8 自动模块，第 515 页
- 9.9 未命名模块，第 517 页
- 9.10 迁移的命令行标志，第 518 页
- 9.11 传递性和静态需求，第 519 页
- 9.12 限定导出和开放，第 521 页
- 9.13 服务加载，第 522 页
- 9.14 使用模块的工具，第 524 页

面向对象编程的一个重要特征是封装。类声明由公共接口和私有实现组成。类可以通过更改实现来演化，而不会影响其使用者。模块系统为大规模编程提供了相同的好处。模块可以选择性地提供类和包，从而可以控制其演化。

现有的几个 Java 模块系统依赖类加载器来隔离类。然而，Java 9 引入了一个新系统，称为 Java 平台模块系统，它由 Java 编译器和虚拟机支持。它旨在将 Java 平台的大型代码库模块化。如果你愿意，也可以使用该系统将自己的应用程序模块化。

无论你是否在自己的应用程序中使用 Java 平台模块，你都可能受到模块化 Java 平台的影响。本章展示如何声明和使用 Java 平台模块。你还将学习如何迁移应用程序，使其与模块化的 Java 平台和第三方模块协同工作。

## 9.1 模块概念

在面向对象编程中，基本的构建块是类。类提供封装。私有特性只能由具有明确权限的代码访问——也就是该类的方法。这使得对访问进行推理成为可能。如果某个私有变量发生了变化，你可以列出所有可能的“罪魁祸首”。如果你需要修改私有表示，你知道哪些方法会受影响。

在 Java 中，包提供了下一层更大的组织分组。包是类的集合。包还提供了一定程度的封装。任何具有包访问权限（既不是 public 也不是 private）的特性，只能从同一包中的方法访问。

然而，在大型系统中，这种级别的访问控制还不够。任何公共特性（即可以从包外访问的特性）在任何地方都可访问。假设你想修改或删除一个很少使用的特性。一旦它成为公共的，就无法推断该更改的影响。

这正是 Java 平台设计者面临的情况。二十多年来，JDK 飞速发展，但显然有些特性现在基本上已经过时。大家最喜欢的例子是 CORBA。你上次使用它是什么时候？然而，直到 Java 10，每个 JDK 都附带 `org.omg.CORBA` 包。从 Java 11 开始，少数仍然需要它的人必须将所需的 JAR 文件添加到他们的项目中。



那 java.awt 呢？在服务端应用中不应该需要它，对吧？除非类 `java.awt.DataFlavor` 被用于实现 SOAP——一种基于 XML 的 Web 服务协议。

Java 平台的设计者面对一团乱麻般的代码，决定需要一种提供更多控制力的结构化机制。他们研究了现有的模块系统（如 OSGi），发现它们不适合解决他们的问题。于是，他们设计了一个新系统，称为 *Java 平台模块系统*，现在它已经成为 Java 语言和虚拟机的一部分。该系统已成功用于将 Java API 模块化，如果你愿意，也可以将它用于自己的应用程序。

一个 Java 平台模块由以下内容组成：

- 一组包
- 可选地，资源文件和其他文件，如本地库
- 模块中可访问包的列表
- 该模块所依赖的所有模块的列表

Java 平台在编译时和虚拟机中都强制实施封装和依赖关系。

为什么你应该考虑在自己的程序中使用 Java 平台模块系统，而不是沿用传统的在类路径上使用 JAR 文件的方法呢？有两个优点。

- 1. 强封装：你可以控制哪些包是可访问的，而不必担心维护那些你本不打算公开使用的代码。
- 2. 可靠的配置：你可以避免常见的类路径问题，例如类重复或缺失。

Java 平台模块系统没有解决一些问题，例如模块的版本管理。它不支持指定需要哪个版本的模块，也不支持在同一程序中使用多个版本的模块。这些可能是有用的特性，但如果需要它们，你必须使用 Java 平台模块系统之外的机制。

## 9.2 命名模块

模块是包的集合。模块中的包名不必相关。例如，模块 `java.sql` 包含包 `java.sql`、`javax.sql` 和 `javax.transaction.xa`。此外，从这个例子可以看出，模块名与包名相同是完全可接受的。

就像路径名一样，模块名由字母、数字、下划线和句点组成。同样，与路径名一样，模块之间没有层次关系。如果你有一个模块 com.horstmann 和另一个模块 com.horstmann.corejava，就模块系统而言，它们是不相关的。

在创建供他人使用的模块时，确保其名称全局唯一非常重要。预计大多数模块名将遵循“反向域名”约定，就像包名一样。

最简单的方法是以模块提供的顶级包来命名模块。例如，SLF4J 日志门面有一个模块 org.slf4j，包含包 org.slf4j、org.slf4j.spi、org.slf4j.event 和 org.slf4j.helpers。

这种约定可以防止模块中的包名冲突。任何给定的包只能放在一个模块中。如果你的模块名是唯一的，并且包名以模块名开头，那么你的包名也将是唯一的。

对于不打算供其他程序员使用的模块（例如包含应用程序的模块），可以使用较短的模块名。为了展示这一点，本章中我也会这样做。那些可能包含库代码的模块将使用诸如 com.horstmann.util 之类的名称，而包含程序（带有 main 方法的类）的模块将使用如 v2ch09.hellomod 这样好记的名称。

> **注意：** 模块名仅用于模块声明中。在 Java 类的源文件中，你永远不会引用模块名；而是像以往一样使用包名。

## 9.3 模块化的“Hello, World!”程序

让我们把传统的“Hello, World!”程序放入一个模块。首先，我们需要把类放入一个包中——“未命名包”不能包含在模块中。如下所示：

```java
package com.horstmann.hello;

public class HelloWorld
{
   public static void main(String[] args)
   {
      System.out.println("Hello, Modular World!");
   }
}
```

到目前为止，一切都没有改变。要创建一个包含该包的模块 `v2ch09.hellomod`，你需要添加模块声明。你将它放在名为 `module-info.java` 的文件中，该文件位于基础目录（即包含 `com` 目录的同一目录）中。按照惯例，基础目录的名称与模块名相同。

```
v2ch09.hellomod/
  └ module-info.java
  com/
    └ horstmann/
      └ hello/
        └ HelloWorld.java
```

`module-info.java` 文件包含模块声明：

```java
module v2ch09.hellomod
{
}
```

这个模块声明是空的，因为该模块没有任何对外提供的内容，也不需要任何东西。

现在，像往常一样编译：

```
javac v2ch09.hellomod/module-info.java v2ch09.hellomod/com/horstmann/hello/HelloWorld.java
```

`module-info.java` 文件看起来不像 Java 源文件，而且当然不可能有名为 `module-info` 的类，因为类名不能包含连字符。关键字 `module` 以及你将在后续章节中看到的关键字 `requires`、`exports` 等，都是“受限关键字”，只在模块声明中具有特殊含义。该文件会被编译成类文件 `module-info.class`，其中以二进制形式包含模块定义。

要将此程序作为模块化应用程序运行，你需要指定模块路径，它与类路径类似，但包含的是模块。还需要按 `modulename/classname` 的格式指定主类：

```
java --module-path v2ch09.hellomod --module v2ch09.hellomod/com.horstmann.hello.HelloWorld
```

你可以使用单字母选项 `-p` 和 `-m` 来代替 `--module-path` 和 `--module`：

```
java -p v2ch09.hellomod -m v2ch09.hellomod/com.horstmann.hello.HelloWorld
```

无论采用哪种方式，都会显示“Hello, Modular World”的问候语，这证明你已经成功地将第一个应用程序模块化。

**注意：** 编译此模块时，你会得到一条警告：

```text
warning: {module} module name component v2ch09 should avoid terminal digits
```

这条警告旨在劝阻程序员不要向模块名添加版本号。你可以忽略该警告，也可以使用注解来抑制它：

```java
@SuppressWarnings("module")
module v2ch09.hellomod
{
}
```

在这一点上，模块声明就像类声明一样：你可以为其添加注解。（注解类型的目标必须是 `ElementType.MODULE`。）

## 9.4 要求模块

让我们创建一个新模块 `v2ch09.requiremod`，其中的程序使用 `JOptionPane` 来显示“Hello, Modular World”消息：

```java
package com.horstmann.hello;

import javax.swing.JOptionPane;

public class HelloWorld
{
   public static void main(String[] args)
   {
      JOptionPane.showMessageDialog(null, "Hello, Modular World");
   }
}
```

现在编译会失败，并显示以下消息：

```text
error: package javax.swing is not visible
  (package javax.swing is declared in module java.desktop,
  but module v2ch09.requiremod does not read it)
```

JDK 已经被模块化，`javax.swing` 包现在包含在 `java.desktop` 模块中。我们的模块需要声明它依赖该模块：

```java
module v2ch09.requiremod
{
   requires java.desktop;
}
```

模块系统的一个设计目标是让模块明确声明其需求，这样虚拟机就可以在启动程序之前确保所有需求都得到满足。

在前一节中，并不需要显式需求，因为只使用了 `java.lang` 和 `java.io` 包。这些包包含在 `java.base` 模块中，该模块默认是必需的。

请注意，我们的 `v2ch09.requiremod` 模块只列出了它自己的模块需求。它需要 `java.desktop` 模块，以便使用 `javax.swing` 包。`java.desktop` 模块本身声明它需要另外三个模块，即 `java.datatransfer`、`java.prefs` 和 `java.xml`。

图 9.1 展示了 *模块图*，其节点是模块。图的边——连接模块节点的箭头——要么是声明的需求，要么是在没有声明任何需求时对 `java.base` 的隐含需求。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_527_0.png)

**图 9.1** Swing “Hello, Modular World” 应用程序的模块图

模块图中不能有环——也就是说，模块不能直接或间接地依赖自身。



模块不会自动将访问权限传递给其他模块。在我们的示例中，`java.desktop` 模块声明它需要 `java.prefs`，而 `java.prefs` 模块声明它需要 `java.xml`。这并不会赋予 `java.desktop` 使用 `java.xml` 模块中包的权利。它需要显式声明该需求。用数学术语来说，requires 关系不是“传递的”。一般来说，这种行为是可取的，因为它使需求变得显式，但正如你将在第 519 页的 9.11 节“传递性和静态需求”中看到的那样，在某些情况下可以放宽这一限制。

> **注意：** 本节开头的错误消息指出，我们的 `v2ch09.requires` 模块没有“读取” `java.desktop` 模块。用 Java 平台模块系统的话来说，在以下情况中，模块 *M* 读取模块 *N*：
> 
> 1. *M* requires *N*。
> 2. *M* requires 某个模块，而该模块传递地 requires *N*（见第 519 页的 9.11 节“传递性和静态需求”）。
> 3. *N* 是 *M* 或 `java.base`。

## 9.5 导出包

上一节中，你看到如果模块想要使用另一个模块的包，它就必须 require 另一个模块。然而，这并不会自动使被 require 的模块中的所有包都可用。模块使用 `exports` 关键字声明其哪些包可访问。例如，下面是 `java.xml` 模块声明的一部分：

```
module java.xml
{
    exports javax.xml;
    exports javax.xml.catalog;
    exports javax.xml.datatype;
    exports javax.xml.namespace;
    exports javax.xml.parsers;
    ...
}
```

该模块使许多包可用，但通过不导出它们来隐藏其他包（例如 `jdk.xml.internal`）。

当一个包被导出时，它的 public 和 protected 类和接口，以及它们的 public 和 protected 成员，在模块外部可访问。（一如既往，protected 类型和成员只能在子类中访问。）

然而，未导出的包在其自身模块外部不可访问。这与引入模块之前的 Java 大不相同。过去，你可以使用任何包中的 public 类，即使它不属于公共 API。例如，当公共 API 未提供适当功能时，通常建议使用 `sun.misc.BASE64Encoder` 或 `com.sun.rowset.CachedRowSetImpl` 之类的类。

如今，你不能再访问 Java 平台 API 中未导出的包，因为它们全都包含在模块内部。因此，一些程序将无法再在 Java 9 中运行。当然，从来没有人承诺会一直提供非公共 API，所以这不应令人震惊。

让我们在一个简单情形中使用 exports。我们将准备一个模块 `com.horstmann.greet`，它导出一个包，该包也叫 `com.horstmann.greet`，遵循这样的约定：为他人提供代码的模块应以其内部的顶层包命名。还有一个包 `com.horstmann.greet.internal`，我们不导出它。

第一个包中有一个 public 的 Greeter 接口。

```java
package com.horstmann.greet;

public interface Greeter
{
    static Greeter newInstance()
    {
        return new com.horstmann.greet.internal.GreeterImpl();
    }

    String greet(String subject);
}
```

第二个包中有一个实现该接口的类。该类是 public 的，因为它在第一个包中被访问。

```java
package com.horstmann.greet.internal;

import com.horstmann.greet.Greeter;

public class GreeterImpl implements Greeter
{
    public String greet(String subject)
    {
        return "Hello, " + subject + "!";
    }
}
```

`com.horstmann.greet` 模块包含这两个包，但只导出第一个：

```java
module com.horstmann.greet
{
    exports com.horstmann.greet;
}
```

第二个包在模块外部不可访问。

我们将应用程序放入第二个模块，该模块将 require 第一个模块：

```java
module v2ch09.exportedpkg
{
    requires com.horstmann.greet;
}
```

> **注意：** `exports` 语句后跟包名，而 `requires` 后跟模块名。

我们的应用程序现在使用 Greeter 来获取问候语：

```java
package com.horstmann.hello;

import com.horstmann.greet.Greeter;

public class HelloWorld
{
    public static void main(String[] args)
    {
        Greeter greeter = Greeter.newInstance();
        System.out.println(greeter.greet("Modular World"));
    }
}
```

下面是这两个模块的源文件结构：

```text
com.horstmann.greet
├── module-info.java
└── com
    └── horstmann
        └── greet
            ├── Greeter.java
            └── internal
                └── GreeterImpl.java
v2ch09.exportedpkg
├── module-info.java
└── com
    └── horstmann
        └── hello
            └── HelloWorld.java
```

要构建此应用程序，首先编译 `com.horstmann.greet` 模块：

```bash
javac -d com.horstmann.greet com.horstmann.greet/module-info.java \
    com.horstmann.greet/com/horstmann/greet/Greeter.java \
    com.horstmann.greet/com/horstmann/greet/internal/GreeterImpl.java
```

然后，在模块路径上包含第一个模块的情况下编译应用程序模块：

```bash
javac -p com.horstmann.greet v2ch09.exportedpkg/module-info.java \
    v2ch09.exportedpkg/com/horstmann/hello/HelloWorld.java
```

最后，在模块路径上包含这两个模块的情况下运行程序：

```bash
java -p v2ch09.exportedpkg:com.horstmann.greet \
    -m v2ch09.exportedpkg/com.horstmann.hello.HelloWorld
```

> **提示：** 要使用 Eclipse 构建此应用程序，请为每个模块创建一个单独的项目。在 `v2ch09.exportedpkg` 项目中，编辑项目属性。在 Projects 选项卡中，将 `com.horstmann.greet` 模块添加到模块路径——见图 9.2。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_531_0.png)

**图 9.2** 向 Eclipse 项目添加依赖模块

```bash
jar -c -v -f v2ch09.exportedpkg.jar -e com.horstmann.hello.HelloWorld \
  -C modules/v2ch09.exportedpkg .
```

启动程序时，需要指定包含主类的模块：

```bash
java -p com.horstmann.greet.jar:v2ch09.exportedpkg.jar -m v2ch09.exportedpkg
```

创建 JAR 文件时，可以选择指定版本号。使用 `--module-version` 参数，并在 JAR 文件名中添加 `@` 和版本号：

```bash
jar -c -v -f com.horstmann.greet@1.0.jar --module-version 1.0 -C com.horstmann.greet .
```

如前所述，Java 平台模块系统在解析模块时不使用版本号，但其他工具和框架可以查询它。

> **注意：** 你可以通过反射 API 找出该版本号。在我们的示例中：
> 
> ```java
> Optional<String> version = Greeter.class.getModule().getDescriptor().rawVersion();
> ```
> 
> ……会得到一个包含版本字符串 "1.0" 的 Optional。

> **注意：** 与类加载器对应的模块概念是 *层*。Java 平台模块系统将 JDK 模块和应用程序模块分层放入 *引导层*。程序可以使用层 API（本书未涵盖）加载其他模块。这样的程序可以选择考虑模块版本。预计诸如 Java EE 应用服务器之类的程序开发者会利用层 API 来提供对模块的支持。

> **提示：** 如果要将模块加载到 JShell 中，请将该 JAR 包含在模块路径中，并使用 `--add-modules` 选项：
> 
> ```bash
> jshell --module-path com.horstmann.greet@1.0.jar --add-modules com.horstmann.greet
> ```

## 9.7 模块与反射访问

在前面的几节中，你看到模块系统强制执行封装。模块只能访问另一个模块中显式导出的包。过去，总是可以通过使用反射来克服烦人的访问限制。正如你在第 I 卷第 5 章中所见，反射可以访问任何类的私有成员。

然而，在模块化世界中，这不再成立。如果类位于模块内部，对非 public 成员的反射访问将失败。具体来说，回想一下我们如何访问私有字段：

```
Field f = obj.getClass().getDeclaredField("salary");
f.setAccessible(true);
double value = f.getDouble(obj);
f.setDouble(obj, value * 1.1);
```

调用 f.setAccessible(true) 会成功，除非安全管理器不允许私有字段访问。然而，使用安全管理器运行 Java 应用程序并不常见，而且有许多使用反射访问的库。典型示例是对象关系映射器（如 JPA），它们自动将对象持久化到数据库中，以及在对象与 XML 或 JSON 之间转换的库（如 JAXB 和 JSON-B）。

如果你使用这样的库，并且还想使用模块，就必须小心。为了演示这个问题，让我们把第 I 卷第 5 章中的 ObjectAnalyzer 类放入模块 com.horstmann.util。该类有一个 toString 方法，它使用反射打印对象的字段。

另一个模块 v2ch09.openpkg 包含一个简单的 Country 类：

```java
package com.horstmann.places;

public class Country
{
    private String name;
    private double area;

    public Country(String name, double area)
    {
        this.name = name;
        this.area = area;
    }
    // . . .
}
```

一个简短的程序演示如何分析 Country 对象：

```java
package com.horstmann.places;

import com.horstmann.util.*;

public class Demo
{
```



```java
public static void main(String[] args) throws ReflectiveOperationException
{
    var belgium = new Country("Belgium", 30510);
    var analyzer = new ObjectAnalyzer();
    System.out.println(analyzer.toString(belgium));
}
```

现在编译这两个模块和演示程序：

```bash
javac com.horstmann.util/module-info.java \
    com.horstmann.util/com/horstmann/util/ObjectAnalyzer.java
javac -p com.horstmann.openpkg/module-info.java \
    v2ch09.openpkg/com/horstmann/places/*.java
java -p v2ch09.openpkg:com.horstmann.util -m v2ch09.openpkg/com.horstmann.places.Demo
```

程序将因异常而失败：

```text
Exception in thread "main" java.lang.reflect.InaccessibleObjectException:
    Unable to make field private java.lang.String com.horstmann.places.Country.name
accessible: module v2ch09.openpkg does not "opens com.horstmann.places" to module
com.horstmann.util
```

当然，在纯粹的理论上，违背封装并窥探对象的私有成员是不对的。但对象关系映射或XML/JSON绑定这类机制非常普遍，模块系统必须支持它们。

使用`opens`关键字，模块可以*打开*一个包，从而允许对给定包中所有类的实例进行反射访问。下面就是我们的模块需要做的：

```java
module v2ch09.openpkg
{
    requires com.horstmann.util;
    opens com.horstmann.places;
}
```

经过这个修改，`ObjectAnalyzer` 就能正确工作。

模块可以被声明为`open`，例如：

```java
open module v2ch09.openpkg
{
    requires com.horstmann.util;
}
```

开放模块在运行时授予对其所有包的访问权限，就像所有包都被声明为`exports`和`opens`一样。然而，在编译时只能访问显式导出的包。开放模块将模块系统的编译时安全性与经典的宽松运行时行为结合在了一起。

回顾卷I第5章，JAR文件除了类文件和清单外，还可以包含*文件资源*，这些资源可以使用`Class.getResourceAsStream`方法加载，现在也可以使用`Module.getResourceAsStream`。如果资源存储在模块中与某个包匹配的目录中，那么该包必须向调用者开放。其他目录中的资源以及类文件和清单，任何人都可以读取。

**注意：** 举一个更实际的例子，我们可以将`Country`对象转换为XML或JSON。Java 9和10包含了用于XML转换的`java.xml.bind`模块。该模块已从Java 11中移除（连同`java.activation`、`java.corba`、`java.transaction`、`java.xml.ws`和`java.xml.ws.annotation`模块）。这些模块包含的包也是Jakarta EE（以前称为Java EE）规范的一部分，该规范中的API比Java SE中的更全面。如果JDK中存在冲突的包，企业应用服务器就无法模块化。不幸的是，在本书写作时，还没有XML绑定的模块化替代品。

不过，如果从源代码构建，JSON-B实现会提供模块化JAR文件。希望在你读到本文时，这些JAR文件能出现在Maven Central中。将JAR文件放到模块路径上，然后运行`com.horstmann.places.Demo2`程序。当`com.horstmann.places`包被开放时，转换为JSON的操作就会成功。

**注意：** 未来的库可能会使用*变量句柄*而非反射来读写字段。`VarHandle`类似于`Field`。你可以使用它来读取或写入某个特定类的任意实例的特定字段。然而，要获得`VarHandle`，库代码需要一个`Lookup`对象：

```java
public Object getFieldValue(Object obj, String fieldName, Lookup lookup)
        throws NoSuchFieldException, IllegalAccessException
{
    Class<?> cl = obj.getClass();
    Field field = cl.getDeclaredField(fieldName);
    VarHandle handle = MethodHandles.privateLookupIn(cl, lookup)
            .unreflectVarHandle(field);
    return handle.get(obj);
}
```

只要`Lookup`对象是在有权访问该字段的模块中生成的，这种做法就有效。模块中的某个方法只需调用`MethodHandles.lookup()`，该方法会生成一个封装调用者访问权限的对象。这样，一个模块就可以授予另一个模块访问私有成员的权限。实际问题是如何以最少的麻烦授予这些权限。

## 9.8 自动模块

现在你已经知道如何使用Java平台模块系统了。如果从全新项目开始，自己编写所有代码，你可以设计模块、声明模块依赖，并将应用程序打包为模块化JAR文件。

然而，这是一种极其罕见的情况。几乎所有项目都依赖第三方库。当然，你可以等到所有库的提供者将它们变成模块，然后再对自己的代码进行模块化。

但如果你不想等待呢？Java平台模块系统提供了两种机制，用于跨越当前前模块化世界与完全模块化应用之间的鸿沟：*自动模块*和*未命名模块*。

为了迁移，你可以将任何JAR文件变成模块，只需将它放到模块路径中的某个目录而不是类路径中。模块路径上没有`module-info.class`的JAR文件被称为*自动模块*。自动模块具有以下属性：

- 1. 该模块隐式包含`requires`子句，要求所有其他模块。
- 2. 它的所有包都被导出和开放。
- 3. 如果JAR文件清单`META-INF/MANIFEST.MF`中有键为`Automatic-Module-Name`的条目，则该条目的值将成为模块名称。
- 4. 否则，模块名称从JAR文件名获取，去掉末尾的版本号，并将非字母数字字符序列替换为点。

前两条规则意味着，自动模块中的包的行为方式与它们在类路径上时相同。使用模块路径的原因是为了其他模块的利益，使它们能够表达对此模块的依赖。

例如，假设你正在实现一个处理CSV文件并使用Apache Commons CSV库的模块。你希望在`module-info.java`文件中表明你的模块依赖于Apache Commons CSV。

如果将`commons-csv-1.5.jar`放到模块路径中，那么你的模块就可以引用这个模块。它的名称是`commons.csv`，因为尾部的版本号`-1.5`被移除，非字母数字字符`-`被替换为点。

这个名字可能是一个可接受的模块名，因为Commons CSV广为人知，其他人不太可能尝试将同一名称用于不同的模块。但更好的是，这个JAR文件的维护者能尽快同意保留一个反向DNS名称，最好是顶层包名`org.apache.commons.csv`作为模块名。他们只需在JAR内的`META-INF/MANIFEST.MF`文件中添加一行`Automatic-Module-Name: org.apache.commons.csv`。最终，希望他们能通过添加带有保留模块名的`module-info.java`将JAR文件变为真正的模块——所有使用该名称引用CSV模块的其他模块将继续正常工作。

**注意：** 通向模块化的迁移计划是一场伟大的社会实验，没有人知道它是否会以好的结果告终。在将第三方JAR放入模块路径之前，请检查它们是否为模块化；如果不是，检查它们的清单是否有模块名。如果没有，你仍然可以将JAR变成自动模块，但要准备好稍后更新模块名。

在本书写作时，Commons CSV JAR文件的1.5版本既没有模块描述符，也没有自动模块名。尽管如此，它在模块路径上也能正常工作。你可以从 https://commons.apache.org/proper/commons-csv 下载该库。解压缩并将`commons-csv-1.5.jar`文件放入`v2ch09.automod`模块的目录中。该模块包含一个简单的程序，用于读取带有国家数据的CSV文件：

```java
package com.horstmann.places;

import java.io.*;
import org.apache.commons.csv.*;

public class CSVDemo
{
   public static void main(String[] args) throws IOException
   {
      var in = new FileReader("countries.csv");
      Iterable<CSVRecord> records = CSVFormat.EXCEL.withDelimiter(';')
            .withHeader().parse(in);
      for (CSVRecord record : records)
      {
         String name = record.get("Name");
         double area = Double.parseDouble(record.get("Area"));
         System.out.println(name + " has area " + area);
      }
   }
}
```



由于我们将使用 `commons-csv-1.5.jar` 作为一个自动模块，我们需要require它：

```
@SuppressWarnings("module")
module v2ch09.automod
{
    requires commons.csv;
}
```

这里是编译和运行该程序的命令：

```
javac -p v2ch09.automod:commons-csv-1.5.jar \
    v2ch09.automod/com/horstmann/places/CSVDemo.java \
    v2ch09.automod/module-info.java
java -p v2ch09.automod:commons-csv-1.5.jar \
    -m v2ch09.automod/com.horstmann.places.CSVDemo
```

## 9.9 未命名模块

任何不在模块路径上的类都是*未命名模块*的一部分。从技术上讲，可能存在多个未命名模块，但它们全部加在一起的行为就像一个单一的模块，称为未命名模块。与自动模块一样，未命名模块可以访问所有其他模块，并且其所有包都是导出和开放的。

然而，*任何显式模块*都无法访问未命名模块。（显式模块是指既不是自动模块也不是未命名模块的模块——即模块路径上带有 `module-info.class` 的模块。）换句话说，显式模块总是免于“类路径地狱”的困扰。

例如，考虑上一节中的程序。假设你将 `commons-csv-1.5.jar` 放到类路径上而不是模块路径上：

```
java --module-path v2ch09.automod \
    --class-path commons-csv-1.5.jar \
    -m v2ch09.automod/com.horstmann.places.CSVDemo
```

现在程序将无法启动：

```
Error occurred during initialization of boot layer
java.lang.module.FindException: Module commons.csv not found, required by v2ch09.automod
```

因此，迁移到Java平台模块系统必然是一个自底向上的过程：

- 1. Java平台本身被模块化。
- 2. 接下来，库被模块化，要么通过使用自动模块，要么将它们转变为显式模块。
- 3. 一旦你的应用程序使用的所有库都被模块化，你就可以将应用程序的代码变成一个模块。

> **注意：** 自动模块可以读取未命名模块，因此它们的依赖项可以放在类路径上。

## 9.10 用于迁移的命令行标志

即使你的程序不使用模块，在使用Java 9及更高版本时，你也不能逃避模块化的世界。即使应用程序代码位于类路径上的未命名模块中，并且所有包都已导出和开放，它仍然会与已模块化的Java平台交互。

在Java 11之前，默认行为是允许非法模块访问，但会在控制台上为每种违规行为的第一次实例显示警告。在未来的Java版本中，默认行为将改变，非法访问将被拒绝。为了让你有时间为此变化做准备，你应该使用 `--illegal-access` 标志测试你的应用程序。有四种可能的设置：

- 1. `--illegal-access=permit` 是Java 9的默认行为，会在第一次非法访问时打印一条消息。
- 2. `--illegal-access=warn` 每次非法访问时都会打印一条消息。
- 3. `--illegal-access=debug` 每次非法访问时都会打印一条消息和堆栈跟踪。
- 4. `--illegal-access=deny` 是未来的默认行为，拒绝所有非法访问。

现在是时候使用 `--illegal-access=deny` 进行测试了，这样当该行为成为默认行为时，你就能做好准备。

考虑一个使用不再可访问的内部API的应用程序，例如 `com.sun.rowset.CachedRowSetImpl`。最好的补救方法是更改实现。（从Java 7开始，你可以从 `RowSetProvider` 获取缓存行集。）但假设你无法访问源代码。

在这种情况下，使用 `--add-exports` 标志启动应用程序。指定要导出的模块和包，以及要将包导出到的模块，在我们的例子中，这个模块是未命名模块。

```
java --illegal-access=deny --add-exports java.sql.rowset/com.sun.rowset=ALL-UNNAMED \
    -jar MyApp.jar
```

现在，假设你的应用程序使用反射来访问私有字段或方法。未命名模块内部的反射是可以的，但不再可能通过反射访问Java平台类的非公共成员。例如，一些动态生成Java类的库会通过反射调用受保护的 `ClassLoader.defineClass` 方法。如果应用程序使用了这样的库，请添加标志

```
--add-opens java.base/java.lang=ALL-UNNAMED
```

当添加所有这些命令行选项以使遗留应用程序正常工作时，你很可能会得到“地狱命令行”。为了更好地管理多个选项，你可以将它们放在一个或多个以 `@` 前缀指定的文件中。例如

```
java @options1 @options2 -jar MyProg.jar
```

其中 options1 和 options2 文件包含 java 命令的选项。

选项文件有一些语法规则：

- 使用空格、制表符或换行符分隔选项。
- 对于包含空格的参数使用双引号，例如"Program Files"。
- 以 `\` 结尾的行将与下一行合并。
- 反斜杠必须转义，例如 `C:\\Users\\Fred`。
- 注释行以 `#` 开头。

## 9.11 传递性与静态需求

在9.4节“需求模块”（第504页）中，你已经看到了 `requires` 语句的基本形式。在本节中，你将看到两个偶尔有用的变体。

在某些情况下，给定模块的用户声明所有必需的模块可能会很繁琐。例如，考虑包含JavaFX用户界面元素（如按钮）的 `javafx.controls` 模块。`javafx.controls` 需要 `javafx.base` 模块，每个使用 `javafx.controls` 的人也需要 `javafx.base`。（如果你没有 `javafx.base` 模块中的包可用，那么像Button这样的用户界面控件就没什么用处。）因此，`javafx.controls` 模块使用 transitive 修饰符声明该需求：

```java
module javafx.controls
{
    requires transitive javafx.base;
    . . .
}
```

任何声明对 `javafx.controls` 有需求的模块现在都会自动要求 `javafx.base`。

> **注意：** 一些程序员建议，当另一个模块中的包被用于公共API时，你应该始终使用 `requires transitive`。但这并不是Java语言的规则。例如，考虑 `java.sql` 模块：
>
> ```java
> module java.sql
> {
>     requires transitive java.logging;
>     . . .
> }
> ```
>
> 在整个 `java.sql` API中，只有一个地方使用了 `java.logging` 模块中的包，即返回 `java.util.logging.Logger` 的 `java.sql.Driver.getParentLogger` 方法。不将此模块需求声明为传递性的也完全可以接受。那么，那些实际使用该方法的模块——且只有这些模块——才需要声明它们需要 `java.logging`。

`requires transitive` 语句的一个引人注目的用途是*聚合器*模块——一个没有包且只有传递需求的模块。这样的模块之一是 `java.se` 模块，声明如下：

```
module java.se
{
    requires transitive java.compiler;
    requires transitive java.datatransfer;
    requires transitive java.desktop;
    . . .
    requires transitive java.sql;
    requires transitive java.sql.rowset;
    requires transitive java.xml;
    requires transitive java.xml.crypto;
}
```

对细粒度模块依赖不感兴趣的程序员可以简单地要求 `java.se`，从而获得Java SE平台的所有模块。

最后，还有一个不常见的 `requires static` 变体，它声明一个模块在编译时必须在场，但在运行时是可选的。有两个用例：

- 1. 访问在编译时处理且在不同的模块中声明的*注解*。
- 2. 如果某个类在另一个模块中可用，则使用它，否则执行其他操作，例如：

```
try
{
    new oracle.jdbc.driver.OracleDriver();
    . . .
}
catch (NoClassDefFoundError e)
{
    // Do something else
}
```

## 9.12 限定导出与开放

在本节中，你将看到 exports 和 opens 语句的一种变体，它将它们的范围缩小到指定的一组模块。例如，`javafx.base` 模块包含一条语句

```
exports com.sun.javafx.collections to
    javafx.controls, javafx.graphics, javafx.fxml, javafx.swing;
```

这样的语句被称为*限定导出*。列出的模块可以访问该包，但其他模块不能。

过度使用限定导出可能表明模块结构不佳。然而，在模块化现有代码库时，它们可能会出现。在这里，Java平台设计者将JavaFX的代码分发到多个模块中，这是一个好主意，因为并非所有JavaFX应用程序都需要FXML或Swing互操作性。然而，JavaFX实现者在其代码中大量使用了诸如 `com.sun.javafx.collections.ListListenerHelper` 之类的内部类。在一个全新项目中，人们可以转而设计一个更健壮的公共API。

类似地，你可以将 opens 语句限制到特定的模块。例如，在第511页的9.7节“模块与反射式访问”中，我们可以使用限定 opens 语句，如下所示：

```
module v2ch09.openpkg
{
    requires com.horstmann.util;
    opens com.horstmann.places to com.horstmann.util;
}
```

现在，`com.horstmann.places` 包只对 `com.horstmann.util` 模块开放。




## 9.13 服务加载

ServiceLoader 类（参见卷 I 的第 6 章）提供了一种轻量级机制，用于将服务接口与实现进行匹配。Java 平台模块系统使这种机制更易于使用。

下面快速回顾一下服务加载。一个服务有一个接口和一个或多个可能的实现。下面是一个简单的接口示例：

```java
public interface GreeterService
{
    String greet(String subject);
    Locale getLocale();
}
```

一个或多个模块提供实现，例如

```java
public class FrenchGreeter implements GreeterService
{
    public String greet(String subject) { return "Bonjour " + subject; }
    public Locale getLocale() { return Locale.FR; }
}
```

服务消费者必须在所有提供的实现中，根据其认为合适的任何标准，选择一个实现。

```java
ServiceLoader<GreeterService> greeterLoader = ServiceLoader.load(GreeterService.class);
GreeterService chosenGreeter;
for (GreeterService greeter : greeterLoader)
{
    if (...)
    {
        chosenGreeter = greeter;
    }
}
```

过去，通过将文本文件放入包含实现类的 JAR 文件的 META-INF/services 目录中来提供实现。模块系统提供了一种更好的方法。无需文本文件，您可以向模块描述符中添加语句。

提供服务实现的模块会添加一个 provides 语句，该语句列出服务接口（可以在任何模块中定义）和实现类（必须是该模块的一部分）。下面是一个来自 jdk.security.auth 模块的示例：

```java
module jdk.security.auth
{
    . . .
    provides javax.security.auth.spi.LoginModule with
        com.sun.security.auth.module.Krb5LoginModule,
        com.sun.security.auth.module.UnixLoginModule,
        com.sun.security.auth.module.JndiLoginModule,
        com.sun.security.auth.module.KeyStoreLoginModule,
        com.sun.security.auth.module.LdapLoginModule,
        com.sun.security.auth.module.NTLoginModule;
}
```

这相当于 META-INF/services 文件。

消费模块包含一个 uses 语句。

```java
module java.base
{
    . . .
    uses javax.security.auth.spi.LoginModule;
}
```

当消费模块中的代码调用 ServiceLoader.load(ServiceInterface.class) 时，匹配的提供者类将被加载，即使它们可能不在可访问的包中。

在我们的代码示例中，我们在 com.horstmann.greetsvc.internal 包中提供了德语和法语问候语的实现。服务模块导出了 com.horstmann.greetsvc 包，但没有导出包含实现的包。provides 语句在未导出的包中声明服务及其实现类：

```java
module com.horstmann.greetsvc
{
    exports com.horstmann.greetsvc;

    provides com.horstmann.greetsvc.GreeterService with
        com.horstmann.greetsvc.internal.FrenchGreeter,
        com.horstmann.greetsvc.internal.GermanGreeterFactory;
}
```

v2ch09.userservice 模块消费该服务。使用 ServiceLoader 工具，我们遍历提供的服务并选择与所需语言匹配的服务：

```java
package com.horstmann.hello;

import java.util.*;
import com.horstmann.greetsvc.*;

public class HelloWorld
{
    public static void main(String[] args)
    {
        ServiceLoader<GreeterService> greeterLoader
              = ServiceLoader.load(GreeterService.class);
        String desiredLanguage = args.length > 0 ? args[0] : "de";
        GreeterService chosenGreeter = null;
        for (GreeterService greeter : greeterLoader)
        {
            if (greeter.getLocale().getLanguage().equals(desiredLanguage))
                chosenGreeter = greeter;
        }
        if (chosenGreeter == null)
            System.out.println("No suitable greeter.");
        else
            System.out.println(chosenGreeter.greet("Modular World"));
    }
}
```

模块声明需要服务模块，并声明正在使用 GreeterService。

```java
module v2ch09.userservice
{
   requires com.horstmann.greetsvc;
   uses com.horstmann.greetsvc.GreeterService;
}
```

由于 provides 和 uses 声明，消费服务的模块被允许访问私有实现类。

要构建并运行该程序，首先编译服务：

```bash
javac com.horstmann.greetsvc/module-info.java \
      com.horstmann.greetsvc/com/horstmann/greetsvc/GreeterService.java \
      com.horstmann.greetsvc/com/horstmann/greetsvc/internal/*.java
```

然后编译并运行消费模块：

```bash
javac -p com.horstmann.greetsvc \
      v2ch09.userservice/com/horstmann/hello/HelloWorld.java \
      v2ch09.userservice/module-info.java
java -p com.horstmann.greetsvc:v2ch09.userservice \
      -m v2ch09.userservice/com.horstmann.hello.HelloWorld
```

## 9.14 用于处理模块的工具

jdeps 工具分析给定一组 JAR 文件的依赖关系。例如，假设您想要模块化 JUnit 4。运行

```bash
jdeps -s junit-4.12.jar hamcrest-core-1.3.jar
```

“-s” 标志会生成摘要输出：

## WALL·E

你还希望将二进制文件（例如本机代码库）与模块捆绑在一起。

> **注意：** 由于 Java 9 不再包含 `rt.jar` 和 `tools.jar` 文件，您需要更新对它们的任何引用。例如，如果您在安全策略文件中引用了 `tools.jar`，请将其改为对模块的引用：
> 
> `jrt:` 语法表示 Java 运行时文件。

```text
grant codeBase "jrt:/jdk.compiler"
{
    permission java.security.AllPermission;
};
```

至此，我们结束了关于 Java 平台模块系统的一章。下一章将讨论另一个重要主题：安全。安全一直是 Java 平台的核心特性。随着我们生活和计算的世界变得越来越危险，深入理解 Java 安全对于许多开发人员来说将变得越来越重要。

*此页有意留白*

# 第 10 章 安全

## 本章目录

- 10.1 类加载器，第 530 页
- 10.2 安全管理器与权限，第 546 页
- 10.3 用户认证，第 566 页
- 10.4 数字签名，第 582 页
- 10.5 加密，第 599 页

当 Java 技术首次出现时，令人兴奋的不是一种精心设计的编程语言，而是安全执行通过互联网传输的小程序的可能性。显然，只有当接收者能够确信代码不会破坏他们的机器时，提供可执行小程序才有实际意义。因此，安全过去是，现在也仍然是 Java 技术设计者和用户的主要关注点。这意味着，与其他语言和系统不同，安全不是事后才考虑的问题，也不是对入侵的被动反应，而是 Java 技术不可分割的一部分。

三种机制有助于确保安全：

- 语言设计特性（数组边界检查、无未经检查的类型转换、无指针算术等）。
- 访问控制机制，控制代码可以执行哪些操作（文件访问、网络访问等）。
- 代码签名，代码作者可以使用标准加密算法对 Java 代码进行身份验证。这样，代码用户可以准确确定谁创建了代码，以及代码在签名后是否被更改。

我们将首先讨论*类加载器*，它们在类文件被加载到虚拟机时检查其完整性。我们将演示该机制如何检测对类文件的篡改。

为了获得最大安全性，加载类的默认机制和自定义类加载器都需要与*安全管理器*协同工作，安全管理器控制代码可以执行哪些操作。您将详细了解如何配置 Java 平台安全性。

最后，您将看到 java.security 包中提供的加密算法，这些算法支持代码签名和用户认证。

与往常一样，我们将重点关注应用程序程序员最感兴趣的主题。若要深入了解，我们推荐 Li Gong、Gary Ellison 和 Mary Dageforde 合著的《Inside Java™ 2 Platform Security: Architecture, API Design, and Implementation, Second Edition》（Prentice Hall，2003 年）。

## 10.1 类加载器

Java 编译器将源代码指令转换为 Java 虚拟机的代码。虚拟机代码存储在扩展名为 .class 的类文件中。每个类文件包含一个类或接口的定义和实现代码。在下一节中，您将看到虚拟机如何加载这些类文件。

### 10.1.1 类加载过程

虚拟机仅加载执行程序所需的类文件。例如，假设程序执行从 MyProgram.class 开始。以下是虚拟机执行的步骤：

- 1. 虚拟机有一种加载类文件的机制——例如，从磁盘读取文件或从 Web 请求文件；它使用这种机制来加载 MyProgram 类文件的内容。
- 2. 如果 MyProgram 类具有另一个类类型的字段或超类，则也会加载它们的类文件。（加载给定类所依赖的所有类的过程称为*解析*该类。）
- 3. 然后虚拟机执行 MyProgram 中的 main 方法（该方法是静态的，因此无需创建类的实例）。




### 10.1.2 类加载器层次结构

类加载器之间具有*父/子*关系。除引导类加载器外，每个类加载器都有一个父类加载器。类加载器会让其父加载器有机会加载任何给定类，并且只有在父加载器加载失败时才会自行加载。例如，当系统类加载器被要求加载一个系统类（比如 `java.lang.StringBuilder`）时，它首先询问平台类加载器。该平台类加载器首先询问引导类加载器。引导类加载器找到并加载了该类，因此另外两个类加载器都不再继续搜索。

有些程序采用插件架构，其中代码的某些部分被打包为可选插件。如果插件打包为 JAR 文件，你只需使用 `URLClassLoader` 的实例加载插件类即可。

```java
var url = new URL("file:///path/to/plugin.jar");
var pluginLoader = new URLClassLoader(new URL[] { url });
Class<?> cl = pluginLoader.loadClass("mypackage.MyClass");
```

由于在 `URLClassLoader` 构造函数中没有指定父加载器，`pluginLoader` 的父加载器就是系统类加载器。图 10.1 展示了这种层次结构。

> **警告：** 在 Java 9 之前，系统类加载器是 `URLClassLoader` 的一个实例。一些程序员通过强制类型转换来访问 `getURLs` 方法，或通过反射调用受保护的 `addURL` 方法来将 JAR 文件添加到类路径。这已不再可行。

大多数时候，你无需担心类加载器层次结构。通常，类之所以被加载，是因为其他类需要它们，而这个过程对你来说是透明的。

然而，有时你需要介入并指定一个类加载器。考虑下面这个例子：

- 你的应用程序代码包含一个辅助方法，该方法调用 `Class.forName(classNameString)`。
- 该方法由一个插件类调用。
- `classNameString` 指定了插件 JAR 中包含的一个类。

插件作者希望这个类被加载。然而，辅助方法所属的类是由系统类加载器加载的，而 `Class.forName` 使用的正是这个类加载器。插件 JAR 中的类对它来说不可见。这种现象称为*类加载器倒置*。

为了克服这个问题，辅助方法需要使用正确的类加载器。它可以要求将类加载器作为参数传入。或者，它可以使用上下文类加载器。辅助方法随后可以获取上下文类加载器：

```java
Thread t = Thread.currentThread();
ClassLoader loader = t.getContextClassLoader();
Class<?> cl = loader.loadClass(className);
```

> **提示：** 如果你编写一个按名称加载类的方法，最好让调用者在传入显式类加载器和使用上下文类加载器之间做出选择。不要简单地使用方法所在类的类加载器。

### 10.1.3 将类加载器用作命名空间

每个 Java 程序员都知道，包名用于消除名称冲突。标准库中有两个名为 `Date` 的类，但当然，它们的真实名称是 `java.util.Date` 和 `java.sql.Date`。简单名称只是为程序员提供方便，并且需要包含适当的 import 语句。在运行中的程序里，所有类名都包含其包名。

然而，可能会令你惊讶的是，同一个虚拟机中可以有两个类具有相同的类名和包名。一个类由其完整名称和类加载器共同确定。这种技术对于从多个来源加载代码很有用。例如，应用服务器为每个应用使用单独的类加载器。这使虚拟机能够区分来自不同应用的类，无论它们叫什么名字。图 10.2 展示了一个示例。假设一个应用服务器加载两个不同的应用，而每个应用都有一个名为 `Util` 的类。由于每个类都由单独的类加载器加载，这些类完全不同，彼此不会冲突。

### 10.1.4 编写自己的类加载器

你可以为特定目的编写自己的类加载器。这让你能够在将字节码传递给虚拟机之前执行自定义检查。例如，你的类加载器可以拒绝加载未标记为“已付费”的类。

要编写自己的类加载器，只需扩展 `ClassLoader` 类并重写以下方法：

```java
findClass(String className)
```

`ClassLoader` 超类的 `loadClass` 方法负责将加载委托给父加载器，并且仅在该类尚未被加载且父类加载器无法加载该类时，才调用 `findClass`。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_557_0.png)

**图 10.2** 两个类加载器加载具有相同名称的不同类。

你对这个方法的实现必须完成以下操作：

1. 从本地文件系统或其他来源加载该类的字节码。
2. 调用 `ClassLoader` 超类的 `defineClass` 方法，将字节码呈现给虚拟机。

在清单 10.1 的程序中，我们实现了一个加载加密类文件的类加载器。该程序要求用户输入要加载的第一个类的名称（即包含 `main` 的类）以及解密密钥。然后，它使用一个特殊的类加载器来加载指定的类并调用 `main` 方法。该加载器会解密指定的类以及它引用的所有非系统类。最后，程序调用已加载类的 `main` 方法（见图 10.3）。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_558_0.png)

**图 10.3** ClassLoaderTest 程序

为简单起见，我们忽略密码学领域两千年的进展，使用古老的凯撒密码来加密类文件。

> **注意：** David Kahn 的精彩著作 *《密码破译者》*（Macmillan，1967 年，第 84 页）将 Suetonius 视为凯撒密码的历史来源。凯撒将罗马字母表的 24 个字母移动了 3 个字母，这在当时令他的对手困惑不已。
>
> 本章最初编写时，美国政府限制强加密方法的出口。因此，我们在示例中使用凯撒的方法，因为它显然可以合法出口。

我们的凯撒密码版本使用 1 到 255 之间的数字作为密钥。解密时，只需将密钥加到每个字节上，然后对 256 取模。清单 10.2 中的 `Caesar.java` 程序执行加密。

为了不使常规类加载器混淆，我们对加密的类文件使用不同的扩展名 `.caesar`。

解密时，类加载器只需从每个字节中减去密钥。在本书的配套代码中，你会找到四个类文件，它们使用密钥值 3 加密——这是传统选择。要运行加密后的程序，你需要使用我们 `ClassLoaderTest` 程序中定义的自定义类加载器。

加密类文件有许多实际用途（当然，前提是你使用比凯撒密码更强的方法）。没有解密密钥，这些类文件就毫无用处。它们既不能由标准虚拟机执行，也不容易反汇编。

这意味着你可以使用自定义类加载器来认证类的用户，或确保程序在获准运行之前已经付费。当然，加密只是自定义类加载器的一种应用。你可以使用其他类型的类加载器来解决其他问题——例如，将类文件存储在数据库中。

#### 清单 10.1 ClassLoader/ClassLoaderTest.java

```java
package classLoader;

import java.io.*;
import java.lang.reflect.*;
import java.nio.file.*;
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

/**
 * This program demonstrates a custom class loader that decrypts class files.
 * @version 1.25 2018-05-01
 * @author Cay Horstmann
 */
public class ClassLoaderTest
{
    public static void main(String[] args)
    {
        EventQueue.invokeLater(() ->
            {
                var frame = new ClassLoaderFrame();
                frame.setTitle("ClassLoaderTest");
                frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
                frame.setVisible(true);
            });
    }
}
```




#### 清单 10.1 *（续）*

```java
29  /**
30   * This frame contains two text fields for the name of the class to load and the decryption
31   * key.
32   */
33  class ClassLoaderFrame extends JFrame
34  {
35      private JTextField keyField = new JTextField("3", 4);
36      private JTextField nameField = new JTextField("Calculator", 30);
37      private static final int DEFAULT_WIDTH = 300;
38      private static final int DEFAULT_HEIGHT = 200;
39
40      public ClassLoaderFrame()
41      {
42          setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);
43          setLayout(new GridBagLayout());
44          add(new JLabel("Class"), new GBC(0, 0).setAnchor(GBC.EAST));
45          add(nameField, new GBC(1, 0).setWeight(100, 0).setAnchor(GBC.WEST));
46          add(new JLabel("Key"), new GBC(0, 1).setAnchor(GBC.EAST));
47          add(keyField, new GBC(1, 1).setWeight(100, 0).setAnchor(GBC.WEST));
48          var loadButton = new JButton("Load");
49          add(loadButton, new GBC(0, 2, 2, 1));
50          loadButton.addActionListener(event -> runClass(nameField.getText(), keyField.getText()));
51          pack();
52      }
53
54  /**
55   * Runs the main method of a given class.
56   * @param name the class name
57   * @param key the decryption key for the class files
58   */
59  public void runClass(String name, String key)
60  {
61      try
62      {
63          var loader = new CryptoClassLoader(Integer.parseInt(key));
64          Class<?> c = loader.loadClass(name);
65          Method m = c.getMethod("main", String[].class);
66          m.invoke(null, (Object) new String[] {});
67      }
68      catch (Throwable t)
69      {
70          JOptionPane.showMessageDialog(this, t);
71      }
72  }
73  }

/**
 * This class loader loads encrypted class files.
 */
class CryptoClassLoader extends ClassLoader
{
    private int key;

    /**
     * Constructs a crypto class loader.
     * @param k the decryption key
     */
    public CryptoClassLoader(int k)
    {
        key = k;
    }

    protected Class<?> findClass(String name) throws ClassNotFoundException
    {
        try
        {
            byte[] classBytes = null;
            classBytes = loadClassBytes(name);
            Class<?> cl = defineClass(name, classBytes, 0, classBytes.length);
            if (cl == null) throw new ClassNotFoundException(name);
            return cl;
        }
        catch (IOException e)
        {
            throw new ClassNotFoundException(name);
        }
    }

    /**
     * Loads and decrypts the class file bytes.
     * @param name the class name
     * @return an array with the class file bytes
     */
    private byte[] loadClassBytes(String name) throws IOException
    {
        String cname = name.replace('.', '/') + ".caesar";
        byte[] bytes = Files.readAllBytes(Paths.get(cname));
        for (int i = 0; i < bytes.length; i++)
            bytes[i] = (byte) (bytes[i] ^ key);
        return bytes;
    }
}
```

#### **清单 10.2** classloader/Caesar.java

```java
1  package classloader;
2
3  import java.io.*;
4
5  /**
6   * Encrypts a file using the Caesar cipher.
7   * @version 1.02 2018-05-01
8   * @author Cay Horstmann
9   */
10 public class Caesar
11 {
12     public static void main(String[] args) throws Exception
13     {
14         if (args.length != 3)
15         {
16             System.out.println("USAGE: java classloader.Caesar in out key");
17             return;
18         }
19
20         try (var in = new FileInputStream(args[0]);
21              var out = new FileOutputStream(args[1]))
22         {
23             int key = Integer.parseInt(args[2]);
24             int ch;
25             while ((ch = in.read()) != -1)
26             {
27                 byte c = (byte) (ch + key);
28                 out.write(c);
29             }
30         }
31     }
32 }
```

| **java.lang.Class** 1.0 |
| --- |
| • `ClassLoader getClassLoader()`<br>获取加载了该类的类加载器。 |

| **java.lang.ClassLoader** 1.0 |
| --- |
| • `ClassLoader getParent()` 1.2<br>返回父类加载器；如果父类加载器是引导类加载器，则返回 null。 |

#### java.lang.ClassLoader 1.0 *（续）*

- `static ClassLoader getSystemClassLoader() 1.2`<br>获取系统类加载器——即用于加载第一个应用程序类的类加载器。
- `protected Class findClass(String name) 1.2`<br>类加载器应重写此方法，以查找类的字节码，并通过调用 `defineClass` 方法将字节码提交给虚拟机。在类名中，使用 `.` 作为包名分隔符，且不要使用 `.class` 后缀。
- `Class defineClass(String name, byte[] bytecodeData, int offset, int length)`<br>向虚拟机添加一个新类，其字节码由给定数据范围提供。

#### java.net.URLClassLoader 1.2

- `URLClassLoader(URL[] urls)`
- `URLClassLoader(URL[] urls, ClassLoader parent)`<br>构造一个从给定 URL 加载类的类加载器。如果 URL 以 `/` 结尾，则假定它是一个目录，否则假定它是一个 JAR 文件。

#### java.lang.Thread 1.0

- `ClassLoader getContextClassLoader() 1.2`<br>获取线程创建者指定的、在执行此线程时最适合使用的类加载器。
- `void setContextClassLoader(ClassLoader loader) 1.2`<br>为此线程中的代码设置一个类加载器，以便在加载类时获取使用。如果线程启动时未显式设置上下文类加载器，则使用父线程的上下文类加载器。

### 10.1.5 字节码验证

当类加载器将新加载的 Java 平台类的字节码提交给虚拟机时，这些字节码首先会经过*验证器*检查。验证器检查这些指令是否会执行明显具有破坏性的操作。除系统类之外，所有类都会经过验证。

以下是验证器执行的部分检查：

- 变量在使用之前已经初始化。
- 方法调用与对象引用的类型匹配。
- 没有违反访问私有数据和私有方法的规则。
- 局部变量访问在运行时栈的范围内。
- 运行时栈不会溢出。

如果上述任何一项检查失败，该类就被视为已损坏，并且不会被加载。

> **注意：** 如果你熟悉哥德尔定理，你可能会好奇验证器如何能证明一个类文件不存在类型不匹配、未初始化变量和栈溢出问题。哥德尔定理指出，不可能设计出这样的算法：它能处理一个程序并判定它是否具有某种特定属性（例如不存在栈溢出）。这是否意味着 Oracle 公关部门与逻辑定律之间存在冲突？不——事实上，验证器并非哥德尔意义上的判定算法。如果验证器接受了一个程序，那么该程序确实是安全的。然而，即使某些虚拟机指令实际上是安全的，验证器也可能拒绝它们。（你或许遇到过这样的问题：因为验证器无法看出某个变量会被正确初始化，所以你不得不为它赋一个哑值来初始化。）

这种严格的验证是一项重要的安全考虑。诸如未初始化变量之类的意外错误，如果不被捕获，很容易造成严重破坏。更重要的是，在广袤开放的互联网世界中，我们必须防范那些故意制造恶意影响的程序员。例如，通过修改运行时栈上的值，或者向系统对象的私有数据字段写入内容，程序可以突破浏览器的安全系统。

不过，你可能会想，为什么需要一个专门的验证器来检查所有这些特性呢？毕竟，编译器绝不会允许你生成一个使用未初始化变量或从其他类访问私有数据字段的类文件。确实，由 Java 编程语言编译器生成的类文件总是能通过验证。然而，类文件中的字节码格式有详细的文档说明，对于有汇编编程经验并会使用十六进制编辑器的人来说，手动生成一个包含对 Java 虚拟机有效但不安全指令的类文件是轻而易举的事。验证器始终在防范被恶意篡改的类文件——而不仅仅是在检查编译器生成的类文件。




下面是一个如何构造这种修改过的类文件的示例。我们从清单 10.3 中的程序 VerifierTest.java 开始。这是一个简单的程序，它调用一个方法并显示该方法的结果。该程序既可以作为控制台程序运行，也可以作为 applet 运行。fun 方法本身只是计算 1 + 2。

```
static int fun()
{
    int m;
    int n;
    m = 1;
    n = 2;
    int r = m + n;
    return r;
}
```

作为实验，尝试编译下面这个对该程序的修改版本：

```
static int fun()
{
    int m = 1;
    int n;
    m = 1;
    m = 2;
    int r = m + n;
    return r;
}
```

这里，n 未初始化，因此它可能具有任意随机值。当然，编译器会检测到该问题并拒绝编译该程序。要创建一个有问题的类文件，我们必须多费一点功夫。首先，运行 javap 程序，查明编译器如何翻译 fun 方法。命令

```
javap -c verifier.VerifierTest
```

以助记符形式显示类文件中的字节码。

```
Method int fun()
 0 iconst_1
 1 istore_0
 2 iconst_2
 3 istore_1
 4 iload_0
 5 iload_1
 6 iadd
 7 istore_2
 8 iload_2
 9 ireturn
```

使用十六进制编辑器将指令 3 从 istore 1 改为 istore 0。也就是说，局部变量 0（即 m）被初始化两次，而局部变量 1（即 n）根本没有初始化。我们需要知道这些指令的十六进制值；这些值可以从 Java 虚拟机规范（[https://docs.oracle.com/javase/specs/jvms/se11/html/index.html](https://docs.oracle.com/javase/specs/jvms/se11/html/index.html)）中直接获得。

```
0 iconst_1 04
1 istore_0 3B
2 iconst_2 05
3 istore_1 3C
4 iload_0 1A
5 iload_1 1B
6 iadd 60
7 istore_2 3D
8 iload_2 1C
9 ireturn AC
```

你可以使用任何十六进制编辑器来执行修改。在图 10.4 中，可以看到类文件 VerifierTest.class 被加载到 Gnome 十六进制编辑器中，fun 方法的字节码被高亮显示。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_566_0.png)

**图 10.4** 使用十六进制编辑器修改字节码

将 3C 改为 3B，并保存类文件。然后尝试运行 VerifierTest 程序。你会得到一条错误消息：

```
Exception in thread "main" java.lang.VerifyError: (class: VerifierTest, method: fun signature:
()I) Accessing value from uninitialized register 1
```

这很好——虚拟机检测到了我们的修改。

现在使用 -noverify（或 -Xverify:none）选项运行该程序：

```
java -noverify verifier.VerifierTest
```

fun 方法返回一个看似随机的值。实际上，它是 2 加上变量 n 中恰好存储的值，而该变量从未被初始化。下面是一个典型的输出：

```
1 + 2 == 15102330
```

#### 清单 10.3  verifier/VerifierTest.java

```
package verifier;

import java.awt.*;

/**
 * This application demonstrates the bytecode verifier of the virtual machine. If you use a
 * hex editor to modify the class file, then the virtual machine should detect the tampering.
 * @version 1.10 2018-05-05
 * @author Cay Horstmann
 */
public class VerifierTest
{
   public static void main(String[] args)
   {
      System.out.println("1 + 2 == " + fun());
   }

   /**
    * A function that computes 1 + 2.
    * @return 3, if the code has not been corrupted
    */
   public static int fun()
   {
      int m;
      int n;
      m = 1;
      n = 2;
      // use hex editor to change to "m = 2" in class file
      int r = m + n;
      return r;
   }
}
```

安全管理器现在会检查退出请求是来自浏览器还是单个 applet。如果安全管理器同意该退出请求，checkExit 方法就直接返回，正常处理继续。然而，如果安全管理器不想批准该请求，checkExit 方法就会抛出 SecurityException。

只有在没有发生异常时，exit 方法才会继续。随后它调用 *私有原生* exitInternal 方法，该方法实际终止虚拟机。没有其他方式可以终止虚拟机，而且由于 exitInternal 方法是私有的，它不能被任何其他类调用。因此，任何试图退出虚拟机的代码都必须经过 exit 方法，从而经过 checkExit 安全检查，且不能触发安全异常。

显然，安全策略的完整性取决于谨慎的编码。标准库中系统服务的提供者在尝试任何敏感操作之前，必须始终咨询安全管理器。

Java 平台的安全管理器允许程序员和系统管理员对各个安全权限进行细粒度控制。我们将在下一节描述这些特性。首先，我们将总结 Java 2 平台安全模型。然后，我们将展示如何通过*策略文件*控制权限。最后，我们将解释如何定义自己的权限类型。

### 10.2.2 Java 平台安全

JDK 1.0 有一个非常简单的安全模型：本地类拥有完整权限，远程类则被限制在*沙箱*中。就像一个只能在沙箱里玩耍的孩子，远程代码只被允许在屏幕上绘制并与用户交互。applet 安全管理器拒绝所有对本地资源的访问。JDK 1.1 做了一个轻微修改：由受信任实体签名的远程代码被授予与本地类相同的权限。然而，两个版本的 JDK 都采用全有或全无的方法。程序要么拥有完整访问权限，要么必须在沙箱中运行。

从 Java 1.2 开始，Java 平台有了灵活得多的机制。一个*安全策略*将代码源映射到权限集（见图 10.5）。

一个*代码源*由*代码基*和一组*证书*指定。代码基指定代码的来源。例如，某些远程 applet 代码的代码基是加载该 applet 的 HTTP URL。JAR 文件中代码的代码基是该文件的 URL。证书（如果存在）是某一方对代码未被篡改的保证。我们将在本章后面介绍证书。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_570_0.png)

**图 10.5** 一个安全策略

*权限*是由安全管理器检查的任何属性。Java 平台支持许多权限类，每个权限类封装特定权限的细节。例如，下面这个 *FilePermission* 类的实例表示可以读取和写入 /tmp 目录中的任何文件：

```
var p = new FilePermission("/tmp/*", "read,write");
```

更重要的是，*Policy* 类的默认实现从*权限文件*中读取权限。在权限文件内部，同一个读权限表示为

```
permission java.io.FilePermission "/tmp/*", "read,write";
```

我们将在下一节讨论权限文件。

图 10.6 展示了 Java 1.2 附带的权限类层次结构。后续 Java 版本中又添加了许多权限类。

在上一节中，你看到 *SecurityManager* 类有诸如 *checkExit* 这样的安全检查方法。这些方法的存在只是为了方便程序员并保持向后兼容性。它们都映射到标准的

FileReader 构造函数调用 FileInputStream 构造函数，后者调用安全管理器的 checkRead 方法，该方法最终用一个 FilePermission(name, "read") 对象调用 checkPermission。表 10.1 展示了调用栈。

**表 10.1** 权限检查期间的调用栈

| 类 | 方法 | 代码源 | 权限 |
|---|---|---|---|
| SecurityManager | checkPermission | null | AllPermission |
| SecurityManager | checkRead | null | AllPermission |
| FileInputStream | 构造函数 | null | AllPermission |
| FileReader | 构造函数 | null | AllPermission |
| Servlet | init | Servlet 代码源 | Tomcat Web 应用权限 |

FileInputStream 和 SecurityManager 类是*系统类*，其 `CodeSource` 为 null，权限由一个 `AllPermission` 类的实例组成，该实例允许所有操作。显然，仅凭它们的权限无法决定检查结果。如你所见，`checkPermission` 方法必须考虑 applet 类受限的权限。通过检查整个调用栈，安全机制确保一个类永远不能要求另一个类代表它执行敏感操作。

> **注意：** 这段关于权限检查的简要讨论解释了基本概念。然而，我们在这里省略了许多技术细节。在安全方面，细节决定成败，我们鼓励你阅读 Li Gong 的书以获取更多信息。若想更批判性地看待 Java 平台的安全模型，请参阅 Gary McGraw 和 Ed W. Felten 所著的 *Securing Java: Getting Down to Business with Mobile Code, Second Edition*（Wiley，1999）。你可以在 www.securingjava.com 找到该书的在线版本。

**java.lang.SecurityManager** 1.0

- `void checkPermission(Permission p)` 1.2
  
  检查此安全管理器是否授予给定权限。如果未授予该权限，该方法抛出 `SecurityException`。




| 类 | 成员和描述 |
|---|---|
| **java.lang.Class 1.0** | • `ProtectionDomain getProtectionDomain()` 1.2<br>获取此类的保护域；如果此类在未指定保护域的情况下加载，则返回 null。 |

| 类 | 成员和描述 |
|---|---|
| **java.security.ProtectionDomain 1.2** | • `ProtectionDomain(CodeSource source, PermissionCollection permissions)`<br>使用给定的代码源和权限构造保护域。<br>• `CodeSource getCodeSource()`<br>获取此保护域的代码源。<br>• `boolean implies(Permission p)`<br>如果给定权限被此保护域允许，则返回 true。 |

| 类 | 成员和描述 |
|---|---|
| **java.security.CodeSource 1.2** | • `Certificate[] getCertificates()`<br>获取与此代码源关联的类文件签名的证书链。<br>• `URL getLocation()`<br>获取与此代码源关联的类文件的代码基。 |

### 10.2.3 安全策略文件

*策略管理器*读取*策略文件*，这些文件包含将代码源映射到权限的指令。下面是一个典型的策略文件：

```text
grant codeBase "http://www.horstmann.com/classes"
{
    permission java.io.FilePermission "/tmp/*", "read,write";
};
```

此文件向从 www.horstmann.com/classes 下载的所有代码授予读取和写入 /tmp 目录中文件的权限。

可以将策略文件安装在标准位置。默认情况下有两个位置：

- Java 平台主目录中的 `java.policy` 文件
- 用户主目录中的 `.java.policy` 文件（注意文件名开头的句点）

> **注意：** 可以在 `jdk/conf/security` 目录中的 `java.security` 配置文件里更改这些文件的位置。默认值指定为
>
> ```text
> policy.url.1=file:${java.home}/lib/security/java.policy
> policy.url.2=file:${user.home}/.java.policy
> ```
>
> 系统管理员可以修改 `java.security` 文件，并指定位于另一台服务器上、用户无法编辑的策略 URL。策略文件中可以有任意数量的策略 URL（使用连续编号）。所有文件的权限会合并。
>
> 如果要将策略存储在文件系统之外，可以实现 `Policy` 类的子类来收集权限。然后更改 `java.security` 配置文件中的以下行：
>
> ```text
> policy.provider=sun.security.provider.PolicyFile
> ```

在测试期间，我们不喜欢不断修改标准策略文件。因此，我们更愿意为每个应用程序显式指定所需的策略文件。将权限放入单独的文件——比如 `MyApp.policy`。要应用该策略，有两种选择。可以在应用程序的 main 方法中设置系统属性：

```java
System.setProperty("java.security.policy", "MyApp.policy");
```

或者，可以这样启动虚拟机：

```text
java -Djava.security.policy=MyApp.policy MyApp
```

在这些示例中，`MyApp.policy` 文件会添加到其他生效的策略中。如果添加第二个等号，例如：

```text
java -Djava.security.policy==MyApp.policy MyApp
```

那么应用程序将*仅*使用指定的策略文件，标准策略文件将被忽略。

> **警告：** 测试期间一个容易犯的错误是意外地在主目录中留下一个授予大量权限（甚至可能是 `AllPermission`）的 `.java.policy` 文件。如果发现应用程序似乎没有遵循策略文件中的限制，请检查主目录中是否有遗留的 `.java.policy` 文件。如果使用 UNIX 系统，尤其容易犯这个错误，因为以句点开头的文件默认不显示。

如之前所见，Java 应用程序默认不安装安全管理器。因此，在安装安全管理器之前，看不到策略文件的效果。当然，可以添加一行

```java
System.setSecurityManager(new SecurityManager());
```

到 `main` 方法中。或者在启动虚拟机时添加命令行选项 `-Djava.security.manager`。

```text
java -Djava.security.manager -Djava.security.policy=MyApp.policy MyApp
```

在本节剩余部分，我们将详细展示如何在策略文件中描述权限。我们将描述整个策略文件格式，但代码证书除外，本章后面会介绍。

策略文件包含一系列 grant 条目。每个条目的形式如下：

```text
grant codesource
{
   permission1;
   permission2;
   . . .
};
```

代码源包含代码基（如果条目适用于来自所有源的代码，则可省略）以及受信任主体和证书签名者的名称（如果此条目不需要签名，则可省略）。代码基指定为

```text
codeBase "url"
```

如果 URL 以 / 结尾，则指目录。否则，它被视为 JAR 文件的名称。例如，

```text
grant codeBase "www.horstmann.com/classes/" { . . . };
grant codeBase "www.horstmann.com/classes/MyApp.jar" { . . . };
```

代码基是一个 URL，应始终包含正斜杠作为文件分隔符，即使对于 Windows 中的文件 URL 也是如此。例如，

```text
grant codeBase "file:C:/myapps/classes/" { . . . };
```

> **注意：** 众所周知，http URL 以两个斜杠（`http://`）开头。但文件 URL 存在足够多的混淆，因此策略文件读取器接受两种形式的文件 URL——即 `file://localFile` 和 `file:localFile`。此外，Windows 驱动器盘符前的斜杠是可选的。也就是说，以下所有形式都可接受：
>
> ```text
> file:C:/dir/filename.ext
> file://C:/dir/filename.ext
> file:///C:/dir/filename.ext
> ```

实际上，在我们的测试中，`file:///C:/dir/filename.ext` 也可接受，我们对此没有解释。

> **注意：** 考虑一个编译一些 Java 代码的应用程序，它需要大量权限。在 JDK 9 之前，可以授予 `tools.jar` 文件中的代码所有权限。此 JAR 文件已不存在。相反，应像这样向相应模块授予权限：
>
> ```text
> grant codeBase "jrt:/jdk.compiler"
> {
>     permission java.security.AllPermission;
> };
> ```

权限具有以下结构：

```text
permission className targetName, actionList;
```

className 是权限类的完全限定类名（例如 `java.io.FilePermission`）。targetName 是权限特定的值——例如，文件权限的文件或目录名，或套接字权限的主机和端口。actionList 也是权限特定的。它是以逗号分隔的动作列表，例如 read 或 connect。某些权限类不需要目标名称和动作列表。表 10.2 列出了常用的权限类及其动作。

**表 10.2 权限及其关联的目标和动作**

| 权限 | 目标 | 动作 |
|---|---|---|
| `java.io.FilePermission` | 文件目标（见正文） | read, write, execute, delete |
| `java.net.SocketPermission` | 套接字目标（见正文） | accept, connect, listen, resolve |
| `java.util.PropertyPermission` | 属性目标（见正文） | read, write |
| `java.lang.RuntimePermission` | createClassLoader<br>getClassLoader<br>setContextClassLoader<br>enableContextClassLoaderOverride<br>createSecurityManager<br>setSecurityManager<br>exitVM<br>getenv.variableName<br>shutdownHooks<br>setFactory<br>setIO<br>modifyThread<br>stopThread<br>modifyThreadGroup<br>getProtectionDomain<br>readFileDescriptor<br>writeFileDescriptor<br>loadLibrary.libraryName<br>accessClassInPackage.packageName<br>defineClassInPackage.packageName<br>accessDeclaredMembers.className<br>queuePrintJob<br>getStackTrace<br>setDefaultUncaughtExceptionHandler<br>preferences<br>usePolicy | 无 |
| `java.awt.AWTPermission` | showWindowWithoutWarningBanner<br>accessClipboard<br>accessEventQueue<br>createRobot<br>fullScreenExclusive<br>listenToAllAWTEvents<br>readDisplayPixels<br>replaceKeyboardFocusManager<br>watchMousePointer<br>setWindowAlwaysOnTop<br>setAppletStub | 无 |





#### 表 10.2

| 权限 | 目标 | 操作 |
|---|---|---|
| java.net.NetPermission | setDefaultAuthenticator<br>specifyStreamHandler<br>requestPasswordAuthentication<br>setProxySelector<br>getProxySelector<br>setCookieHandler<br>getCookieHandler<br>setResponseCache<br>getResponseCache | 无 |
| java.lang.reflect.ReflectPermission | suppressAccessChecks | 无 |
| java.io.SerializablePermission | enableSubclassImplementation<br>enableSubstitution | 无 |
| java.security.SecurityPermission | createAccessControlContext<br>getDomainCombiner<br>getPolicy<br>setPolicy<br>getProperty.keyName<br>setProperty.keyName<br>insertProvider.providerName<br>removeProvider.providerName<br>setSystemScope<br>setIdentityPublicKey<br>setIdentityInfo<br>addIdentityCertificate<br>removeIdentityCertificate<br>printIdentity<br>clearProviderProperties.providerName<br>putProviderProperty.providerName<br>removeProviderProperty.providerName<br>getSignerPrivateKey<br>setSignerKeyPair | 无 |
| java.security.AllPermission | None | 无 |
| `javax.sound.sampled.AudioPermission` | `play,record` | 无 |
| `javax.security.auth.AuthPermission` | `doAs`<br>`doAsPrivileged`<br>`getSubject`<br>`getSubjectFromDomainCombiner`<br>`setReadOnly`<br>`modifyPrincipals`<br>`modifyPublicCredentials`<br>`modifyPrivateCredentials`<br>`refreshCredential`<br>`destroyCredential`<br>`createLoginContext.contextName`<br>`getLoginConfiguration`<br>`setLoginConfiguration`<br>`refreshLoginConfiguration` | 无 |
| `java.util.logging.LoggingPermission` | `control` | 无 |
| `java.sql.SQLPermission` | `setLog` | 无 |

从表 10.2 可以看出，大多数权限只是允许某个特定操作。你可以把该操作视为带有隐含动作“permit”的目标。这些权限类都扩展了 `BasicPermission` 类（见图 10.6）。然而，文件、套接字和属性权限的目标更复杂，我们需要详细研究它们。

文件权限目标可以采用以下形式：

- `file` — 一个文件
- `directory/` — 一个目录
- `directory/*` — 该目录中的所有文件
- `*` — 当前目录中的所有文件
- `directory/-` — 该目录或其某个子目录中的所有文件
- `-` — 当前目录或其某个子目录中的所有文件
- `<<ALL FILES>>` — 文件系统中的所有文件

例如，以下权限条目授予对目录 `/myapp` 及其任意子目录中所有文件的访问权限：

```
permission java.io.FilePermission "/myapp/-", "read,write,delete";
```

必须使用 `\\` 转义序列来表示 Windows 文件名中的反斜杠。

```
permission java.io.FilePermission "c:\\myapp\\*", "read,write,delete";
```

套接字权限目标由主机和端口范围组成。主机规范采用以下形式：

- `hostname or IP address` — 单个主机
- `localhost or the empty string` — 本地主机
- `*.domainSuffix` — 域名以给定后缀结尾的任何主机
- `*` — 所有主机

端口范围是可选的，采用以下形式：

- `:n` — 单个端口
- `:n-` — 编号为 n 及以上的所有端口
- `:-n` — 编号为 n 及以下的所有端口
- `:n1-n2` — 给定范围内的所有端口

下面是一个示例：

```
permission java.net.SocketPermission "*.horstmann.com:8000-8999", "connect";
```

最后，属性权限目标可以采用以下两种形式之一：

- `property` — 特定属性
- `propertyPrefix.*` — 具有给定前缀的所有属性

示例包括 "java.home" 和 "java.vm.*"。

例如，以下权限条目允许程序读取所有以 java.vm 开头的属性：

```
permission java.util.PropertyPermission "java.vm.*", "read";
```

可以在策略文件中使用系统属性。标记 ${property} 会被替换为属性值。例如，${user.home} 会被替换为用户的主目录。下面是一个在权限条目中使用该系统属性的典型示例：

```
permission java.io.FilePermission "${user.home}", "read,write";
```

为了创建与平台无关的策略文件，最好使用 file.separator 属性，而不是显式的 `/` 或 `\\` 分隔符。为简化此操作，特殊表示法 ${/} 是 ${file.separator} 的快捷方式。例如，

```
permission java.io.FilePermission "${user.home}${/}-", "read,write";
```

是一个可移植条目，用于授予在用户主目录及其任意子目录中读写的权限。

### 10.2.4 自定义权限

在本节中，你将了解如何提供自己的权限类，以便用户可以在其策略文件中引用。

要实现你的权限类，请扩展 Permission 类并提供以下方法：

- 一个带有两个 String 参数的构造器，分别用于目标和动作列表
- `String getActions()`
- `boolean equals(Object other)`
- `int hashCode()`
- `boolean implies(Permission other)`

最后一个方法最重要。权限具有一种*顺序关系*，其中更通用的权限会*蕴含*更具体的权限。考虑以下文件权限

```
p1 = new FilePermission("/tmp/-", "read,write");
```

此权限允许读取和写入 /tmp 目录及其任意子目录中的任何文件。

此权限蕴含其他更具体的权限：

```
p2 = new FilePermission("/tmp/-", "read");
p3 = new FilePermission("/tmp/aFile", "read, write");
p4 = new FilePermission("/tmp/directory/-", "write");
```

换言之，文件权限 p1 蕴含另一个文件权限 p2，如果

- 1. p1 的目标文件集包含 p2 的目标文件集。
- 2. p1 的动作集包含 p2 的动作集。

考虑以下 `implies` 方法的使用示例。当 `FileInputStream` 构造器想要打开文件进行读取时，它会检查自己是否有权限这样做。为进行该检查，会将一个*特定的*文件权限对象传递给 `checkPermission` 方法：

```
checkPermission(new FilePermission(fileName, "read"));
```

安全管理器现在会询问所有适用的权限是否蕴含该权限。如果其中任何一个蕴含它，检查就会通过。

特别地，`AllPermission` 蕴含所有其他权限。

如果你定义自己的权限类，就需要为你的权限对象定义合适的蕴含概念。例如，假设你为一台由 Java 技术驱动的机顶盒定义一个 `TVPermission`。一个权限

```
new TVPermission("Tommy:2-12:19:00-2200", "watch,record")
```

可能允许 Tommy 在 19:00 到 22:00 之间观看和录制电视频道 2–12。你需要实现 `implies` 方法，使此权限蕴含一个更具体的权限，例如

```
new TVPermission("Tommy:4:2000-2100", "watch")
```

### 10.2.5 权限类的实现

在下一个示例程序中，我们实现一个新权限，用于监控向文本区域插入文本。该程序确保你不能将 *sex*、*drugs* 和 C++ 等不良词汇添加到文本区域中。我们使用自定义权限类，以便可以在策略文件中提供不良词汇列表。

以下 JTextArea 的子类会询问安全管理器是否可以添加新文本：

```
class WordCheckTextArea extends JTextArea
{
    public void append(String text)
    {
        var p = new WordCheckPermission(text, "insert");
        SecurityManager manager = System.getSecurityManager();
        if (manager != null) manager.checkPermission(p);
        super.append(text);
    }
}
```

如果安全管理器授予 WordCheckPermission，则追加该文本。否则，checkPermission 方法抛出异常。

单词检查权限有两个可能的动作：insert（插入特定文本的权限）和 avoid（添加避开某些不良词汇的任何文本的权限）。应使用以下策略文件运行此程序：

```
grant
{
    permission permissions.WordCheckPermission "sex,drugs,C++", "avoid";
};
```

此策略文件授予插入任何避开不良词汇 *sex*、*drugs* 和 C++ 的文本的权限。




#### 代码清单 10.4（续）

```java
public class WordCheckPermission extends Permission
{
   private String action;

   /**
    * Constructs a word check permission.
    * @param target a comma separated word list
    * @param action "insert" or "avoid"
    */
   public WordCheckPermission(String target, String action)
   {
      super(target);
      this.action = action;
   }

   public String getActions()
   {
      return action;
   }

   public boolean equals(Object other)
   {
      if (other == null) return false;
      if (!getClass().equals(other.getClass())) return false;
      var b = (WordCheckPermission) other;
      if (!Objects.equals(action, b.action)) return false;
      if ("insert".equals(action)) return Objects.equals(getName(), b.getName());
      else if ("avoid".equals(action)) return badWordSet().equals(b.badWordSet());
      else return false;
   }

   public int hashCode()
   {
      return Objects.hash(getName(), action);
   }

   public boolean implies(Permission other)
   {
      if (!(other instanceof WordCheckPermission)) return false;
      var b = (WordCheckPermission) other;
      if (action.equals("insert"))
      {
         return b.action.equals("insert") && getName().indexOf(b.getName()) >= 0;
      }
      else if (action.equals("avoid"))
      {
         if (b.action.equals("avoid")) return badWordSet().containsAll(b.badWordSet());
         else if (b.action.equals("insert"))
         {
            for (String badWord : badWordSet())
               if (b.getName().indexOf(badWord) >= 0) return false;
            return true;
         }
         else return false;
      }
      else return false;
   }

   /**
    * Gets the bad words that this permission rule describes.
    * @return a set of the bad words
    */
   public Set<String> badWordSet()
   {
      var set = new HashSet<String>();
      set.addAll(List.of(getName().split(",")));
      return set;
   }
}
```

#### 代码清单 10.5 permissions/PermissionTest.java

```java
package permissions;

import java.awt.*;

import javax.swing.*;

/**
 * This class demonstrates the custom WordCheckPermission.
 * @version 1.05 2018-05-01
 * @author Cay Horstmann
 */
public class PermissionTest
{
   public static void main(String[] args)
   {
      System.setProperty("java.security.policy", "permissions/PermissionTest.policy");
      System.setSecurityManager(new SecurityManager());
      EventQueue.invokeLater(() ->
      {
         var frame = new PermissionTestFrame();
         frame.setTitle("PermissionTest");
         frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
         frame.setVisible(true);
      });
   }
}

/**
 * This frame contains a text field for inserting words into a text area that is protected
 * from "bad words".
 */
class PermissionTestFrame extends JFrame
{
   private JTextField textField;
   private WordCheckTextArea textArea;
   private static final int TEXT_ROWS = 20;
   private static final int TEXT_COLUMNS = 60;

   public PermissionTestFrame()
   {
      textField = new JTextField(20);
      var panel = new JPanel();
      panel.add(textField);
      var openButton = new JButton("Insert");
      panel.add(openButton);
      openButton.addActionListener(event -> insertWords(textField.getText()));

      add(panel, BorderLayout.NORTH);

      textArea = new WordCheckTextArea();
      textArea.setRows(TEXT_ROWS);
      textArea.setColumns(TEXT_COLUMNS);
      add(new JScrollPane(textArea), BorderLayout.CENTER);
      pack();
   }

   /**
    * Tries to insert words into the text area. Displays a dialog if the attempt fails.
    * @param words the words to insert
    */
   public void insertWords(String words)
   {
      try
      {
         textArea.append(words + "\n");
      }
      catch (SecurityException ex)
      {
         JOptionPane.showMessageDialog(this, "I am sorry, but I cannot do that.");
         ex.printStackTrace();
      }
   }
}
```

#### 代码清单 10.5（续）

```java
/**
 * A text area whose append method makes a security check to see that no bad words are added.
 */
class WordCheckTextArea extends JTextArea
{
   public void append(String text)
   {
      var p = new WordCheckPermission(text, "insert");
      SecurityManager manager = System.getSecurityManager();
      if (manager != null) manager.checkPermission(p);
      super.append(text);
   }
}
```

#### java.security.Permission 1.2

- `Permission(String name)` 使用给定的目标名称构造一个权限。
- `String getName()` 返回此权限的目标名称。
- `boolean implies(Permission other)` 检查此权限是否蕴含另一个权限。如果另一个权限描述的是由本权限所描述条件推导出的更具体条件，则属于这种情况。

## 10.3 用户认证

Java API 提供了一个名为 Java 认证与授权服务（JAAS）的框架，它将平台提供的认证与权限管理集成在一起。我们将在以下各节讨论 JAAS 框架。

### 10.3.1 JAAS 框架

顾名思义，JAAS 框架有两个组成部分。“认证”部分关注确定程序用户身份。“授权”部分将用户映射到权限。

JAAS 是一个“可插拔”API，它将 Java 应用程序与用于实现认证的特定技术隔离开来。它支持 UNIX 登录、Windows 登录、Kerberos 认证和基于证书的认证等。

一旦用户通过认证，就可以附加一组权限。例如，这里我们授予 Harry 一组其他用户没有的特定权限：

```
grant principal com.sun.security.auth.UnixPrincipal "harry"
{
    permission java.util.PropertyPermission "user.*", "read";
    . . .
};
```

`com.sun.security.auth.UnixPrincipal` 类检查正在运行此程序的 UNIX 用户名。其 `getName` 方法返回 UNIX 登录名，我们检查该名称是否等于 `"harry"`。

使用 `LoginContext` 允许安全管理器检查此类 grant 语句。以下是登录代码的基本轮廓：

```java
try
{
    System.setSecurityManager(new SecurityManager());
    var context = new LoginContext("Login1"); // defined in JAAS configuration file
    context.login();
    // get the authenticated Subject
    Subject subject = context.getSubject();
    . . .
    context.logout();
}
catch (LoginException exception) // thrown if login was not successful
{
    exception.printStackTrace();
}
```

现在，subject 表示已通过认证的个体。

`LoginContext` 构造函数中的字符串参数 `"Login1"` 引用 JAAS 配置文件中具有相同名称的条目。以下是一个示例配置文件：

```
Login1
{
    com.sun.security.auth.module.UnixLoginModule required;
    com.whizzbang.auth.module.RetinaScanModule sufficient;
};

Login2
{
    . . .
};
```

当然，JDK 不包含生物识别登录模块。`com.sun.security.auth.module` 包中提供了以下模块：

- `UnixLoginModule`
- `NTLoginModule`
- `Krb5LoginModule`
- `JndiLoginModule`
- `KeyStoreLoginModule`

登录策略由一系列登录模块组成，每个模块都标记为 required、sufficient、requisite 或 optional。这些关键字的含义由以下算法给出。

登录会对 subject 进行认证，而 subject 可以有多个 principal。principal 描述 subject 的某些属性，例如用户名、组 ID 或角色。正如你在 grant 语句中所见，principal 支配权限。`com.sun.security.auth.UnixPrincipal` 描述 UNIX 登录名，而 `UnixNumericGroupPrincipal` 可以测试是否为 UNIX 组成员。

grant 子句可以使用以下语法测试 principal：

```
grant principalClass "principalName"
```

例如：

```
grant com.sun.security.auth.UnixPrincipal "harry"
```

当用户登录后，你随后在一个单独的访问控制上下文中运行需要检查 principal 的代码。使用静态 `doAs` 或 `doAsPrivileged` 方法启动一个新的 `PrivilegedAction`，其 `run` 方法执行该代码。

这两个方法都通过调用实现 `PrivilegedAction` 接口的对象的 `run` 方法来执行一个操作，并使用 subject 的 principal 的权限：

```java
PrivilegedAction<T> action = () -> {
    // run with permissions of subject principals
    ...
};
T result
    = Subject.doAs(subject, action); // or Subject.doAsPrivileged(subject, action, null)
```

如果这些操作可以抛出受检异常，则需要改为实现 `PrivilegedExceptionAction` 接口。

`doAs` 和 `doAsPrivileged` 方法之间的区别很微妙。`doAs` 方法从当前访问控制上下文开始，而 `doAsPrivileged` 方法从新的上下文开始。后一种方法允许

你需要将登录代码的权限与“业务逻辑”的权限分开。在我们的示例应用程序中，登录代码具有以下权限

```
permission javax.security.auth.AuthPermission "createLoginContext.Login1";
permission javax.security.auth.AuthPermission "doAsPrivileged";
```

已认证用户具有以下权限

```
permission java.util.PropertyPermission "user.*", "read";
```

如果我们使用 doAs 而不是 doAsPrivileged，那么登录代码也会需要该权限！

清单 10.6 和 10.7 中的程序演示了如何将权限限制为特定用户。AuthTest 程序认证一个用户，并运行一个检索系统属性的简单操作。

要使此示例正常工作，请将登录代码和操作代码打包到两个单独的 JAR 文件中：

```
javac auth/*.java
jar cvf login.jar auth/AuthTest.class
jar cvf action.jar auth/SysPropAction.class
```

如果你查看清单 10.8 中的策略文件，你会看到名为 harry 的 UNIX 用户具有读取所有文件的权限。将 harry 改为你的登录名。然后运行命令

```
java -classpath login.jar:action.jar \
    -Djava.security.policy=auth/AuthTest.policy \
    -Djava.security.auth.login.config=auth/jaas.config \
    auth.AuthTest
```

清单 10.9 显示了登录配置。

在 Windows 上，将 AuthTest.policy 中的 UnixPrincipal 改为 NTUserPrincipal，并将 jaas.config 中的 UnixLoginModule 改为 NTLoginModule。运行程序时，使用分号分隔 JAR 文件：

```
java -classpath login.jar;action.jar . . .
```

现在，AuthTest 程序应显示 user.home 属性的值。不过，如果你使用不同的名称登录，则应抛出安全异常，因为你不再拥有所需的权限。

> **注意：** 请务必严格遵循这些说明。很容易因为一些看似无害的更改而把设置弄错。

#### 清单 10.6  auth/AuthTest.java

```java
package auth;

import javax.security.auth.*;
import javax.security.auth.login.*;

/**
 * This program authenticates a user via a custom login and then executes the SysPropAction
 * with the user's privileges.
 * @version 1.02 2018-05-01
 * @author Cay Horstmann
 */
public class AuthTest
{
   public static void main(final String[] args)
   {
      System.setSecurityManager(new SecurityManager());
      try
      {
         var context = new LoginContext("Login1");
         context.login();
         System.out.println("Authentication successful.");
         Subject subject = context.getSubject();
         System.out.println("subject = " + subject);
         var action = new SysPropAction("user.name");
         String result = Subject.doAsPrivileged(subject, action, null);
         System.out.println(result);
         context.logout();
      }
      catch (LoginException e)
      {
         e.printStackTrace();
      }
   }
}
```

#### 清单 10.7  auth/SysPropAction.java

```java
package auth;

import java.security.*;

/**
 * This action looks up a system property.
 * @version 1.01 2007-10-06
 * @author Cay Horstmann
 */
public class SysPropAction implements PrivilegedAction<String>
{
    private String propertyName;

    /**
     * Constructs an action for looking up a given property.
     * @param propertyName the property name (such as "user.home")
     */
    public SysPropAction(String propertyName)
    {
        this.propertyName = propertyName;
    }

    public String run()
    {
        return System.getProperty(propertyName);
    }
}
```

#### 清单 10.8  `auth/AuthTest.policy`

```text
grant codebase "file:login.jar"
{
    permission javax.security.auth.AuthPermission "createLoginContext.Login1";
    permission javax.security.auth.AuthPermission "doAsPrivileged";
};

grant principal com.sun.security.auth.UnixPrincipal "harry"
{
    permission java.util.PropertyPermission "user.*", "read";
};
```

#### 清单 10.9  `auth/jaas.config`

```text
Login1
{
    com.sun.security.auth.module.UnixLoginModule required;
};
```

#### `javax.security.auth.login.LoginContext` 1.4

- `LoginContext(String name)`

  构造一个登录上下文。该名称对应于 JAAS 配置文件中的登录描述符。

| `java.security.Principal` | 1.1 |
|---|---|
| • `String getName()` | 返回此主体的标识名称。 |

### 10.3.2 JAAS 登录模块

在本节中，我们将看一个 JAAS 示例，它向你展示

- 如何实现你自己的登录模块
- 如何实现*基于角色的*认证

如果你将登录信息存储在数据库中，那么提供自己的登录模块是很有用的。即使你对默认模块感到满意，研究自定义模块也有助于你理解 JAAS 配置文件的选项。

如果你管理大量用户，那么基于角色的认证是必不可少的。将所有合法用户的名称放入策略文件是不切实际的。相反，登录模块应将用户映射到“admin”或“HR”等角色，并且权限应基于这些角色。

登录模块的一项工作是填充正在认证的 subject 的主体集。如果登录模块支持角色，它会添加描述角色的 Principal 对象。Java 库没有为此目的提供类，因此我们编写了自己的类（见清单 10.10）。该类仅存储一个描述/值对，例如 role=admin。它的 getName 方法返回该对，因此我们可以将基于角色的权限添加到策略文件中：

```
grant principal SimplePrincipal "role=admin" { ... }
```

我们的登录模块在一个文本文件中查找用户、密码和角色，该文件包含如下行：

```
harry|secret|admin
carl|guessme|HR
```

当然，在现实的登录模块中，你会将此信息存储在数据库或目录中。

你可以在清单 10.11 中找到 SimpleLoginModule 的代码。checkLogin 方法检查用户名和密码是否与密码文件中的记录匹配。如果匹配，我们会向 subject 的主体集中添加两个 SimplePrincipal 对象：

```
Set<Principal> principals = subject.getPrincipals();
principals.add(new SimplePrincipal("username", username));
principals.add(new SimplePrincipal("role", role));
```

`SimpleLoginModule` 的其余部分是直截了当的管道代码。`initialize` 方法接收

- 正在认证的 Subject
- 用于检索登录信息的处理器
- 可用于登录模块之间通信的 sharedState 映射
- 包含登录配置中设置的名称/值对的 options 映射

例如，我们按如下方式配置模块：

```
SimpleLoginModule required pwfile="password.txt";
```

登录模块从 options 映射中检索 `pwfile` 设置。

登录模块不收集用户名和密码；那是单独处理器的职责。这种分离允许你使用同一个登录模块，而不必担心登录信息来自 GUI 对话框、控制台提示还是配置文件。

处理器在构造 `LoginContext` 时指定，例如：

```
var context = new LoginContext("Login1",
    new com.sun.security.auth.callback.DialogCallbackHandler());
```

`DialogCallbackHandler` 会弹出一个简单的 GUI 对话框来获取用户名和密码。`com.sun.security.auth.callback.TextCallbackHandler` 类从控制台获取信息。

不过，在我们的应用程序中，我们有自己的 GUI 来收集用户名和密码（见图 10.8）。我们编写了一个简单的处理器，它仅存储并返回该信息（见清单 10.12）。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_596_0.png)

**图 10.8** 自定义登录模块

该处理器有一个方法 `handle`，它处理 `Callback` 对象数组。许多预定义类（例如 `NameCallback` 和 `PasswordCallback`）实现了 `Callback` 接口。你也可以添加自己的类，例如

RetinaScanCallback。处理程序代码有点不美观，因为它需要分析回调对象的类型：

```java
public void handle(Callback[] callbacks)
{
   for (Callback callback : callbacks)
   {
      if (callback instanceof NameCallback) . . .
      else if (callback instanceof PasswordCallback) . . .
      else . . .
   }
}
```

登录模块准备一个它进行身份验证所需的回调数组：

```java
var nameCall = new NameCallback("username: ");
var passCall = new PasswordCallback("password: ", false);
callbackHandler.handle(new Callback[] { nameCall, passCall });
```

然后它从回调中检索信息。

清单 10.13 中的程序显示一个用于输入登录信息和系统属性名称的表单。如果用户通过身份验证，则会在 PrivilegedAction 中检索属性值。从清单 10.14 中的策略文件可以看出，只有拥有 admin 角色的用户才有权限读取属性。如前一节所述，你必须将登录代码和操作代码分开。创建两个 JAR 文件：

```bash
javac *.java
jar cvf login.jar JAAS*.class Simple*.class
jar cvf action.jar SysPropAction.class
```

然后按如下方式运行程序：

```bash
java -classpath login.jar:action.jar \
    -Djava.security.policy=JAASTest.policy \
    -Djava.security.auth.login.config=jaas.config \
    JAASTest
```

清单 10.14 显示了策略文件。

> **注意：** 可以支持更复杂的两阶段协议，如果登录配置中的所有模块都成功，则登录会被*提交*。
>
> 更多信息，请参阅 http://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASLMDevGuide.html 上的登录模块开发者指南。

#### 清单 10.10 `jaas/SimplePrincipal.java`

```java
package jaas;

import java.security.*;
import java.util.*;

/**
 * A principal with a named value (such as "role=HR" or "username=harry").
 */
public class SimplePrincipal implements Principal
{
    private String descr;
    private String value;

    /**
     * Constructs a SimplePrincipal to hold a description and a value.
     * @param descr the description
     * @param value the associated value
     */
    public SimplePrincipal(String descr, String value)
    {
        this.descr = descr;
        this.value = value;
    }

    /**
     * Returns the role name of this principal.
     * @return the role name
     */
    public String getName()
    {
        return descr + "=" + value;
    }

    public boolean equals(Object otherObject)
    {
        if (this == otherObject) return true;
        if (otherObject == null) return false;
        if (getClass() != otherObject.getClass()) return false;
        var other = (SimplePrincipal) otherObject;
        return Objects.equals(getName(), other.getName());
    }

    public int hashCode()
    {
        return Objects.hashCode(getName());
    }
}
```

#### 清单 10.11 `jaas/SimpleLoginModule.java`

```java
package jaas;

import java.io.*;
import java.nio.charset.*;
import java.nio.file.*;
import java.security.*;
import java.util.*;
import javax.security.auth.*;
import javax.security.auth.callback.*;
import javax.security.auth.login.*;
import javax.security.auth.spi.*;

/**
 * This login module authenticates users by reading usernames, passwords, and roles from
 * a text file.
 */
public class SimpleLoginModule implements LoginModule
{
    private Subject subject;
    private CallbackHandler callbackHandler;
    private Map<String, ?> options;

    public void initialize(Subject subject, CallbackHandler callbackHandler,
        Map<String, ?> sharedState, Map<String, ?> options)
    {
        this.subject = subject;
        this.callbackHandler = callbackHandler;
        this.options = options;
    }

    public boolean login() throws LoginException
    {
        if (callbackHandler == null) throw new LoginException("no handler");

        var nameCall = new NameCallback("username: ");
        var passCall = new PasswordCallback("password: ", false);
        try
        {
            callbackHandler.handle(new Callback[] { nameCall, passCall });
        }
        catch (UnsupportedCallbackException e)
        {
            var e2 = new LoginException("Unsupported callback");
            e2.initCause(e);
            throw e2;
        }
```

*（续）*

#### 清单 10.12 *（续）*

```java
30            ((NameCallback) callback).setName(username);
31        }
32        else if (callback instanceof PasswordCallback)
33        {
34            ((PasswordCallback) callback).setPassword(password);
35        }
36    }
37  }
38 }
```

#### 清单 10.13 `jaas/JAASTest.java`

```java
1 package jaas;
2
3 import java.awt.*;
4 import javax.swing.*;
5
6 /**
7  * This program authenticates a user via a custom login and then looks up a system property
8  * with the user's privileges.
9 * @version 1.03 2018-05-01
10 * @author Cay Horstmann
11 */
12 public class JAASTest
13 {
14    public static void main(String[] args)
15    {
16        System.setSecurityManager(new SecurityManager());
17        EventQueue.invokeLater(() ->
18        {
19            var frame = new JAAFrame();
20            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
21            frame.setTitle("JAASTest");
22            frame.setVisible(true);
23        });
24    }
25 }
```

#### 清单 10.14 `jaas/JAASTest.policy`

```java
1 grant codebase "file:login.jar"
2 {
3    permission java.awt.AWTPermission "showWindowWithoutWarningBanner";
4    permission java.awt.AWTPermission "accessEventQueue";
5    permission javax.security.auth.AuthPermission "createLoginContext.Login1";
6    permission javax.security.auth.AuthPermission "doAsPrivileged";
7    permission javax.security.auth.AuthPermission "modifyPrincipals";
8    permission java.io.FilePermission "jaas/password.txt", "read";
9 };
10
11 grant principal jaas.SimplePrincipal "role=admin"
12 {
13    permission java.util.PropertyPermission "*", "read";
14 };
```

#### 清单 10.15 `jaas/jaas.config`

```java
1 Login1
2 {
3    jaas.SimpleLoginModule required pwfile="jaas/password.txt" debug=true;
4 };
```

#### javax.security.auth.callback.CallbackHandler 1.4

- `void handle(Callback[] callbacks)` 处理给定的回调，如果需要可与用户交互，并将安全信息存储到回调对象中。

#### javax.security.auth.callback.NameCallback 1.4

- `NameCallback(String prompt)`
- `NameCallback(String prompt, String defaultName)` 使用给定的提示和默认名构造一个 NameCallback。
- `String getName()`
- `String setName(String name)` 获取或设置此回调收集的名称。
- `String getPrompt()` 获取查询此名称时要使用的提示。
- `String getDefaultName()` 获取查询此名称时要使用的默认名称。

#### javax.security.auth.callback.PasswordCallback 1.4

- `PasswordCallback(String prompt, boolean echoOn)` 使用给定的提示和回显标志构造一个 PasswordCallback。

```console
Last login: Thu Nov 12 11:16:24 on ttys003
shiyu@ShiyudeMacBook-Pro ~ % npx create-expo-app@latest
Need to install the following packages:
create-expo-app@3.4.1
Ok to proceed? (y) y
npm warn config global '--global', '--local' are deprecated. Use '--location=global' instead.
npm warn config global '--global', '--local' are deprecated. Use '--location=global' instead.

> create-expo-app@3.4.1 npx
> create-expo-app

npx: installed 31 in 2.396s
✔ Fetching & extracting latest Expo template...
npm warn exec The following package was not found and will be installed: create-expo-app@3.4.1
✔ Creating project: /Users/shiyu/MyApp

✔ Installing packages... This may take a couple of minutes, which might make the command seem to be hanging.
```




在严密监督下，它们在企业内联网上无法发挥多大作用，尽管从公司安全的内联网执行小程序所带来的风险相对较小。Sun 很快意识到，要让小程序真正有用，用户需要能够根据小程序的来源为其指定不同级别的安全性。如果小程序来自可信供应商且未被篡改，则该小程序的用户就可以决定是否授予该小程序更多权限。

为了更信任一个小程序，我们需要知道两件事：

- 小程序来自哪里？
- 代码在传输过程中是否被损坏？

在过去的50年里，数学家和计算机科学家已经开发出复杂的算法，用于确保数据完整性和创建电子签名。java.security 包包含其中许多算法的实现。幸运的是，你不需要理解底层数学，就能使用 java.security 包中的算法。在接下来的几节中，我们将展示消息摘要如何检测数据文件中的变化，以及数字签名如何证明签名者的身份。

### 10.4.1 消息摘要

消息摘要是一块数据的数字指纹。例如，所谓的 SHA-1（安全散列算法 #1）会将任意数据块（无论多长）压缩成 160 位（20 字节）的序列。就像真实指纹一样，人们希望没有两条不同消息具有相同的 SHA-1 指纹。当然，这不可能完全成立——SHA-1 指纹只有 2^160 个，因此必然有一些消息具有相同指纹。但 2^160 如此之大，以至于发生碰撞的概率可以忽略不计。多小才算可忽略？根据 James Walsh 在 *True Odds: How Risks Affect Your Everyday Life*（Merritt Publishing, 1996）中的说法，你被闪电击中致死的概率约为三万分之一。现在，再想想另外九个人——例如，你最亲近的九位百万富翁或教授。你和*他们所有人*都死于雷击的概率，要高于一条伪造消息具有与原消息相同的 SHA-1 指纹的概率。（当然，会有超过十个人死于雷击，而你很可能一个都不认识。不过，我们讨论的是*你所特别选出的*那些人全部被雷击致死的、要小得多的概率。）

消息摘要有两个基本特性：

- 如果数据中的一位或多位发生变化，消息摘要也会变化。

在获得 `MessageDigest` 对象后，通过反复调用 update 方法，将消息中的所有字节喂给它。例如，以下代码将文件中的所有字节传递给刚创建的 `alg` 对象以进行指纹计算：

```
InputStream in = ...;
int ch;
while ((ch = in.read()) != -1)
    alg.update((byte) ch);
```

或者，如果字节位于数组中，也可以一次性更新整个数组：

```
byte[] bytes = ...;
alg.update(bytes);
```

完成后，调用 digest 方法。此方法会按照指纹算法要求填充输入，执行计算，并以字节数组形式返回摘要。

```
byte[] hash = alg.digest();
```

清单 10.16 中的程序会计算消息摘要。你可以在命令行中指定文件和算法：

```
java hash.Digest hash/input.txt SHA-1
```

如果未提供命令行参数，系统将提示你输入文件名和算法名称。

**清单 10.16** `hash/Digest.java`

```java
package hash;

import java.io.*;
import java.nio.file.*;
import java.security.*;
import java.util.*;

/**
 * This program computes the message digest of a file.
 * @version 1.21 2018-04-10
 * @author Cay Horstmann
 */
public class Digest
{
   /**
    * @param args args[0] is the filename, args[1] is optionally the algorithm
    * (SHA-1, SHA-256, or MD5)
    */
   public static void main(String[] args) throws IOException, GeneralSecurityException
   {
      var in = new Scanner(System.in);
      String filename;
      if (args.length >= 1)
         filename = args[0];
      else
      {
         System.out.print("File name: ");
         filename = in.nextLine();
      }
      String algname;
      if (args.length >= 2)
         algname = args[1];
      else
      {
         System.out.println("Select one of the following algorithms: ");
         for (Provider p : Security.getProviders())
            for (Provider.Service s : p.getServices())
               if (s.getType().equals("MessageDigest"))
                  System.out.println(s.getAlgorithm());
         System.out.print("Algorithm: ");
         algname = in.nextLine();
      }
      MessageDigest alg = MessageDigest.getInstance(algname);
      byte[] input = Files.readAllBytes(Paths.get(filename));
      byte[] hash = alg.digest(input);
      for (int i = 0; i < hash.length; i++)
         System.out.printf("%02X ", hash[i] & 0xFF);
      System.out.println();
   }
}
```

**java.security.MessageDigest 1.1**

- `static MessageDigest getInstance(String algorithmName)`  
  返回一个实现指定算法的 MessageDigest 对象。如果未提供该算法，则抛出 `NoSuchAlgorithmException`。
- `void update(byte[] input)`
- `void update(byte[] input, int offset, int len)`  
  使用指定的字节更新摘要。

| java.security.MessageDigest 1.1（续） |
| --- |
| • `byte[] digest()`<br>完成散列计算，返回计算得到的摘要，并重置算法对象。<br>• `void reset()`<br>重置摘要。 |

### 10.4.2 消息签名

上一节中，你了解了如何计算消息摘要——原消息的指纹。如果消息被更改，更改后消息的指纹将不会与原消息的指纹匹配。如果消息及其指纹分开传送，接收方可以检查消息是否被篡改。然而，如果消息和指纹都被截获，那么修改消息并重新计算指纹就是一件轻而易举的事。毕竟，消息摘要算法是公开的，而且它们不需要密钥。在这种情况下，收到伪造消息和重新计算出的指纹的接收方将永远不知道消息已被更改。数字签名解决了这个问题。

为了帮助你理解数字签名的工作原理，我们将解释几个来自*公钥密码学*领域的概念。公钥密码学基于*公钥*和*私钥*的概念。其思想是，你向世界上每个人告知你的公钥。然而，只有你持有私钥，并且保护私钥、不将其泄露给任何其他人非常重要。这些密钥通过数学关系匹配，尽管这些关系的确切性质对我们并不重要。（如果你感兴趣，可以在 www.cacr.math.uwaterloo.ca/hac 的 *The Handbook of Applied Cryptography* 中查阅。）

这些密钥又长又复杂。例如，下面是一对匹配的 Digital Signature Algorithm（DSA）公钥和私钥。

公钥：

```
p: fca682ce8e12caba26efccf7110e526db078b05edecbcd1eb4a208f3ae1617ae01f35b91a47e6df63413c5e12
  ed0899bcd132acd50d99151bdc43ee737592e17

q: 962eddcc369cba8ebb260ee6b6a1266d9346e38c5

g: 678471b27a9cf44ee91a49c5147db1a9aaf244f05a434d6486931d2d14271b9e35030b71fd73da179069b32e
  2935630e1c2062354d0da20a6c416e50be794ca4

y: c0b6e67b4ac098eb1a32c5f8c1c0f9e6fb3d8322e27d0bdab9ca2d2a8123ce5a8018b8161a760480fadd0
  40b927281ddb22cb9bc4df596d7de4d1b97d50
```

私钥：

```
p: fca682ce8e12caba26efccf7110e526db078b05edecbcd1eb4a208f3ae1617ae01f35b91a47e6df63413c5e12
  ed0899bcd132acd50d99151bdc43ee737592e17

q: 962eddcc369cba8ebb260ee6b6a1266d9346e38c5

g: 678471b27a9cf44ee91a49c5147db1a9aaf244f05a434d6486931d2d14271b9e35030b71fd73da179069b32e
  2935630e1c2062354d0da20a6c416e50be794ca4

x: 146c09f881656cc6c51f27ea6c3a91b85ed1d70a
```

人们认为，实际上不可能从其中一个密钥计算出另一个密钥。也就是说，即使每个人都知道你的公钥，无论他们拥有多少计算资源，在你的有生之年也无法计算出你的私钥。

可能很难相信私钥无法从公钥计算出来——但对于当今常用的加密算法，还没有人找到能做到这一点的算法。如果密钥足够长，暴力破解——即简单地尝试所有可能的密钥——将需要比用太阳系所有原子制造出的计算机还要多的计算机，持续计算数千年。当然，有人可能会提出比暴力破解聪明得多的密钥计算算法。例如，RSA 算法（由 Rivest、Shamir 和 Adleman 发明的加密算法）依赖于大数分解的难度。在过去20年里，许多最优秀的数学家都试图提出好的分解算法，但迄今为止没有成功。因此，大多数密码学家认为，目前“模数”为2000位或更长的密钥完全能够抵御任何攻击。DSA 被认为同样安全。

图10.9展示了该过程在实践中如何运作。

假设 Alice 想给 Bob 发送一条消息，而 Bob 想知道这条消息来自 Alice，而不是冒名顶替者。Alice 写下消息，并用她的私钥对消息摘要进行*签名*。Bob 获得她的公钥副本。然后，Bob 使用该公钥来*验证*签名。如果验证通过，Bob 就可以确信两件事：

- 原始消息未被更改。
- 消息由 Alice 签名，Alice 是持有与 Bob 用于验证的公钥相匹配的私钥的人。

你可以看出为什么私钥的安全性如此重要。如果有人窃取了 Alice 的私钥，或者政府能够要求她交出私钥，那么她就有麻烦了。窃贼或政府代理人现在可以冒充


通过发送消息（例如转账指令），让其他人相信这些消息来自 Alice，从而冒充她。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_611_0.png)

**图 10.9** 使用 DSA 的公钥签名交换

### 10.4.3 验证签名

JDK 自带 keytool 程序，这是一个用于生成和管理一组证书的命令行工具。我们期望最终该工具的功能会嵌入到其他更友好的程序中。但现在，我们将使用 keytool 来演示 Alice 如何对文档签名并将其发送给 Bob，以及 Bob 如何验证该文档确实是由 Alice 而非冒名顶替者签名的。

keytool 程序管理密钥库——即证书和私钥/公钥对的数据库。密钥库中的每个条目都有一个别名。下面展示了 Alice 如何创建密钥库 alice.certs，并生成别名为 alice 的密钥对：

```text
keytool -genkeypair -keystore alice.certs -alias alice
```

创建或打开密钥库时，系统会提示你输入密钥库口令。在本例中，直接使用 secret 即可。如果你使用由 keytool 生成的

如果 Bob 想检查自己拿到的证书是否正确，他可以打电话给 Alice，在电话中核对证书指纹。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_613_0.png)

> **注意：** 一些证书颁发机构会在其网站上公布证书指纹。例如，要检查 `jre/lib/security/cacerts` 目录中的 DigiCert 证书，可使用 `-list` 选项：

```text
keytool -list -v -keystore jre/lib/security/cacerts
```

此密钥库的口令是 changeit。该密钥库中的其中一张证书是：

```text
Owner: CN=DigiCert Assured ID Root G3, OU=www.digicert.com, O=DigiCert Inc, C=US
Issuer: CN=DigiCert Assured ID Root G3, OU=www.digicert.com, O=DigiCert Inc, C=US
Serial number: ba15afa1ddfa0b54944afdc24a06cec
Valid from: Thu Aug 01 14:00:00 CEST 2013 until: Fri Jan 15 13:00:00 CET 2038
Certificate fingerprints:
         SHA1:  F5:17:A2:4F:9A:48:C6:C9:F8:A2:00:26:9F:DC:0F:48:2C:AB:30:89
         SHA256: 75:37:CB:88:4C:47:09:0C:AB:36:55:1B:A6:F4:5D:B8:40:68:0F:BA:
                 16:6A:95:2D:B1:00:71:7A:35:3F:C2
```

你可以访问网站 www.digicert.com/digicert-root-certificates.htm 来检查你的证书是否有效。

一旦 Bob 信任了该证书，他就可以将其导入自己的密钥库。

```text
keytool -importcert -keystore bob.certs -alias alice -file alice.cer
```

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_613_1.png)

> **警告：** 永远不要将你不完全信任的证书导入密钥库。一旦证书被添加到密钥库中，任何使用该密钥库的程序都会认定该证书可用于验证签名。

现在，Alice 可以开始向 Bob 发送已签名的文档了。jarsigner 工具用于对 JAR 文件进行签名和验证。Alice 只需将要签名的文档添加到一个 JAR 文件中。

```text
jar cvf document.jar document.txt
```

然后，她使用 jarsigner 工具向文件添加签名。她需要指定密钥库、JAR 文件以及要使用的密钥别名。

```text
jarsigner -keystore alice.certs document.jar alice
```

Bob 收到文件后，使用 jarsigner 程序的 -verify 选项。

```text
jarsigner -verify -keystore bob.certs document.jar
```

Bob 无需指定密钥别名。jarsigner 程序会在数字签名中找到密钥所有者的 X.500 名称，并在密钥库中查找匹配的证书。

如果 JAR 文件未被破坏且签名匹配，jarsigner 程序会输出：

```text
jar verified.
```

否则，程序会显示一条错误消息。

### 10.4.4 身份验证问题

假设你收到了朋友 Alice 发来的一条消息，它使用我们刚刚展示的方法，用她的私钥签名。你可能已经有她的公钥，或者可以轻松地向她要一份副本，或从她的网页上获取。然后，你可以验证这条消息确实是由 Alice 撰写且未被篡改。现在，假设你收到一个陌生人的消息，他声称代表一家知名软件公司，敦促你运行消息附带的程序。这个陌生人甚至把他的公钥副本发给你，以便你验证消息确实是他撰写的。你检查后发现签名有效。这证明该消息是用匹配的私钥签名的，且未被破坏。

小心：*你仍然不知道消息是谁写的。* 任何人都可以生成一对公私钥，用私钥对消息签名，然后将签名后的消息和公钥发送给你。确定发送者身份的问题被称为*身份验证问题*。

解决身份验证问题的通常方法很简单。假设陌生人和你有一个你们都信任的共同熟人。假设陌生人当面与你的熟人见面，并交给他一张存有公钥的磁盘。你的熟人后来见到你，向你保证他见过那个陌生人，而且那个陌生人确实在那家知名软件公司工作，然后把磁盘交给你（见图 10.10）。这样，你的熟人就为陌生人的真实性做了担保。

事实上，你的熟人并不需要真的见到你。他可以用自己的私钥对陌生人的公钥文件签名（见图 10.11）。

当你拿到公钥文件时，你可以验证朋友的签名；因为你信任他，所以你有理由相信他在签名之前确实核实过陌生人的身份凭证。

然而，你也许没有这样的共同熟人。某些信任模型假定总是存在一条“信任链”——一条由相互熟识的人组成的链——因此你信任该链中的每一个成员。当然，在实践中，

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_616_0.png)

图 10.11  通过受信任中间人的签名进行身份验证

### 10.4.5 证书签名

在 10.4.3 节“验证签名”（第 589 页）中，你看到了 Alice 如何使用自签名证书向 Bob 分发公钥。然而，Bob 需要与 Alice 核对指纹，以确保证书有效。

假设 Alice 想给同事 Cindy 发送一条签名消息，但 Cindy 不想费心去验证大量的签名指纹。现在假设有一个 Cindy 信任的实体来验证签名。在本例中，Cindy 信任 ACME 软件公司的信息资源部（Information Resources Department）。

该部门运营着一个*证书颁发机构*（CA）。ACME 的每位员工的密钥库中都有 CA 的公钥，这些公钥由系统管理员安装，管理员仔细核对了密钥指纹。CA 会对 ACME 员工的密钥进行签名。当他们安装彼此的密钥时，密钥库会隐式信任这些密钥，因为它们是由受信任的密钥签名的。

下面你可以模拟这个过程。创建一个密钥库 `acmesoft.certs`。生成密钥对并导出公钥：

```text
keytool -genkeypair -keystore acmesoft.certs -alias acmeroot
keytool -exportcert -keystore acmesoft.certs -alias acmeroot -file acmeroot.cer
```

公钥被导出到一张“自签名”证书中。然后，将它添加到每个员工的密钥库中：

```text
keytool -importcert -keystore cindy.certs -alias acmeroot -file acmeroot.cer
```

为了让 Alice 能向 Cindy 以及 ACME 软件公司的其他所有人发送消息，她需要将自己的证书带到信息资源部并请其签名。遗憾的是，`keytool` 程序缺少这一功能。在本书的配套代码中，我们提供了一个 CertificateSigner 类来弥补这一空缺。ACME 软件公司的一名授权工作人员会验证 Alice 的身份，并生成一张已签名的证书，如下所示：

```text
java CertificateSigner -keystore acmesoft.certs -alias acmeroot \
  -infile alice.cer -outfile alice_signedby_acmeroot.cer
```

证书签名程序必须能够访问 ACME 软件公司的密钥库，并且工作人员必须知道密钥库口令。显然，这是一项敏感操作。

Alice 将文件 `alice_signedby_acmeroot.cer` 交给 Cindy 以及 ACME 软件公司的其他任何人。或者，ACME 软件公司可以直接将该文件存放在公司目录中。请记住，此文件包含 Alice 的公钥，以及 ACME 软件公司关于该密钥确实属于 Alice 的声明。

现在，Cindy 将已签名的证书导入她的密钥库：

```text
keytool -importcert -keystore cindy.certs -alias alice -file alice_signedby_acmeroot.cer
```

密钥库会验证该密钥是否由密钥库中已有的受信任根密钥签名。系统*不会*要求 Cindy 验证证书指纹。

一旦 Cindy 添加了根证书以及那些经常给她发送文档的人的证书，她就再也不必为密钥库操心了。




### 10.4.6 证书请求

在上一节中，我们使用密钥库和 certificateSigner 工具模拟了一个 CA。然而，大多数 CA 运行更复杂的软件来管理证书，并且它们使用的证书格式略有不同。本节展示与这些软件包交互所需的额外步骤。

我们将以 OpenSSL 软件包为例。该软件已预装在许多 Linux 系统和 Mac OS X 上，Windows 也有 Cygwin 移植版可用。你可以从 www.openssl.org 下载该软件。要创建 CA，请运行 ca 脚本。确切位置取决于你的操作系统。在 Ubuntu 上，运行

```
/usr/lib/ssl/misc/CA.pl -newca
```

该脚本在当前目录中创建一个名为 demoCA 的子目录。该目录包含一个根密钥对，以及用于存储证书和证书吊销列表的存储区。

你可能希望将公钥导入所有员工的 Java 密钥库，但它采用隐私增强邮件（PEM）格式，而不是密钥库容易接受的 DER 格式。将文件 demoCA/cacert.pem 复制为文件 acmeroot.pem，并在文本编辑器中打开该文件。删除以下行之前的所有内容

```
-----BEGIN CERTIFICATE-----
```

以及以下行之后的所有内容

```
-----END CERTIFICATE-----
```

现在可以按常规方式将 acmeroot.pem 导入每个密钥库：

```
keytool -importcert -keystore cindy.certs -alias alice -file acmeroot.pem
```

keytool 本身无法执行此编辑操作，这似乎相当不可思议。

要签署 Alice 的公钥，首先生成一个包含 PEM 格式证书的证书请求：

```
keytool -certreq -keystore alice.store -alias alice -file alice.pem
```

要签署证书，运行

```
openssl ca -in alice.pem -out alice_signedby_acmeroot.pem
```

和之前一样，从 alice_signedby_acmeroot.pem 中剪掉 BEGIN CERTIFICATE/END CERTIFICATE 标记之外的所有内容。然后将其导入密钥库：

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_620_0.png)

**图10.12** 启动已签名的小程序

对于内网部署，证书更合理。管理员可以在本地机器上安装策略文件和证书，从而启动受信任代码时无需用户交互。每当 Java 插件工具加载已签名代码时，它会查询策略文件以获取权限，并查询密钥库以获取签名。

在本节剩余部分，我们将描述如何构建策略文件，向受信任代码授予特定权限。

假设 ACME Software 希望其员工运行某些需要本地文件访问的程序，并希望通过浏览器以 Web Start 应用程序方式部署这些程序。

如本章前面所述，ACME 可以通过代码库识别程序。但这意味着每次程序移到不同 Web 服务器时，ACME 都需要更新策略文件。于是，ACME 决定对包含程序代码的 JAR 文件进行*签名*。

首先，ACME 生成根证书：

```
keytool -genkeypair -keystore acmesoft.certs -alias acmeroot
```

当然，包含私有根密钥的密钥库必须保存在安全的地方。因此，我们创建第二个密钥库 client.certs 用于存放公共证书，并将公共 acmeroot 证书加入其中。

```
keytool -exportcert -keystore acmesoft.certs -alias acmeroot -file acmeroot.cer
keytool -importcert -keystore client.certs -alias acmeroot -file acmeroot.cer
```

ACME 的一名受信任人员运行 jarsigner 工具来签署他们希望签署的任何应用程序，并指定 JAR 文件和私钥别名：

```
jarsigner -keystore acmesoft.certs ACMEApp.jar acmeroot
```

已签名的 Web Start 应用程序现在可以部署到 Web 服务器上。

接下来，我们转向客户端机器配置。必须将策略文件分发到每台客户端机器。

要引用密钥库，策略文件以以下行开头：

```
keystore "keystoreURL", "keystoreType";
```

URL 可以是绝对或相对。相对 URL 相对于策略文件的位置。如果密钥库由 keytool 生成，则类型为 JKS。例如，

```
keystore "client.certs", "JKS";
```

然后，grant 子句可以带有 signedBy "alias" 后缀，例如：

```
grant signedBy "acmeroot"
{
  ...
};
```

任何可以使用与该别名关联的公钥验证的已签名代码，现在都会被授予 grant 子句内的权限。

## 10.5 加密

到目前为止，我们讨论了一种在 Java 安全 API 中实现的重要密码技术——即通过数字签名进行认证。安全的第二个重要方面是**加密**。即使经过认证，信息本身仍是明文可见的。数字签名仅验证

包装（wrap）和解包（unwrap）模式使用一个密钥加密另一个密钥——示例见下一节。

现在可以反复调用 `update` 方法来加密数据块：

```
int blockSize = cipher.getBlockSize();
var inBytes = new byte[blockSize];
. . . // read inBytes
int outputSize = cipher.getOutputSize(blockSize);
var outBytes = new byte[outputSize];
int outLength = cipher.update(inBytes, 0, outputSize, outBytes);
. . . // write outBytes
```

完成后，必须调用一次 `doFinal` 方法。如果还有最后一块输入数据（少于 `blockSize` 字节），调用

```
outBytes = cipher.doFinal(inBytes, 0, inLength);
```

如果所有输入数据都已加密，则改为调用

```
outBytes = cipher.doFinal();
```

调用 `doFinal` 是为了对最后一个块执行*填充*。考虑 DES 密码。它的块大小为 8 字节。假设输入数据的最后一块少于 8 字节。当然，我们可以用 0 填充剩余字节，得到最后一个 8 字节块并加密它。但当这些块被解密时，结果末尾会附加若干 0 字节，因此会与原始输入文件略有不同。为避免此问题，我们需要一种*填充*方案。一种常用*填充*方案是 RSA Security, Inc. 在公钥密码标准（PKCS）#5 中描述的方案（https://tools.ietf.org/html/rfc2898）。

在此方案中，最后一个块不是用零填充值填充，而是用等于填充字节数的填充值填充。换句话说，如果 *L* 是最后一个（不完整）块，则按如下方式填充：

|    |    |
|----|----|
| L 01 | 如果 length(L) = 7 |
| L 02 02 | 如果 length(L) = 6 |
| L 03 03 03 | 如果 length(L) = 5 |
| . . . |  |
| L 07 07 07 07 07 07 07 | 如果 length(L) = 1 |

最后，如果输入长度实际上可被 8 整除，则向输入追加一个块

```
08 08 08 08 08 08 08 08
```

并加密。解密后，明文的最后一个字节是要丢弃的填充字符数。

### 10.5.2 密钥生成

要加密，需要生成密钥。每种密码的密钥格式不同，并且需要确保密钥生成是随机的。请按以下步骤操作：

- 1. 获取用于你的算法的 `KeyGenerator`。
- 2. 用随机源初始化生成器。如果密码的块长度可变，还要指定所需的块长度。
- 3. 调用 `generateKey` 方法。

例如，下面生成 AES 密钥：

```java
KeyGenerator keygen = KeyGenerator.getInstance("AES");
var random = new SecureRandom(); // see below
keygen.init(random);
Key key = keygen.generateKey();
```

或者，你可以从一组固定的原始数据（也许源自密码或击键时间）生成密钥。像这样构造一个 `SecretKeySpec`（它实现了 `SecretKey` 接口）：

```java
byte[] keyData = . . .; // 16 bytes for AES
var key = new SecretKeySpec(keyData, "AES");
```

生成密钥时，请确保使用*真正随机*的数字。例如，`Random` 类中的常规随机数生成器以当前日期和时间作为种子，随机性不够。假设计算机时钟精确到 1/10 秒，那么每天最多有 864,000 个种子。如果攻击者知道密钥签发的日期（通常可以从消息日期或证书到期日期推断出来），那么生成该日期所有可能的种子就很容易。

`SecureRandom` 类生成的随机数远比 `Random` 类生成的随机数安全。你仍然需要提供一个种子，以便从随机位置开始数字序列。最好的方法是从硬件设备（如白噪声生成器）获取随机输入。另一种合理的随机输入来源是让用户在键盘上漫无目的地输入，每次击键只向随机序列贡献一两个比特。一旦你在字节数组中收集了这样的随机比特，就将其传递给 `setSeed` 方法：

```java
var secrand = new SecureRandom();
var b = new byte[20];
// fill with truly random bits
secrand.setSeed(b);
```




如果没有为随机数生成器设置种子，它就会通过启动线程、让线程休眠，并测量线程被唤醒的精确时间来计算自己的 20 字节种子。

> **注意：** 该算法*不*被认为是安全的。过去，依赖计算机某些组件（例如硬盘访问时间）计时的算法已被证明并非完全随机。

本节末尾的示例程序将使用 AES 密码（见代码清单 10.17）。代码清单 10.18 中的 crypt 工具方法将在其他示例中复用。要使用该程序，首先需要生成一个秘密密钥。运行

```java
java aes.AESTest -genkey secret.key
```

秘密密钥保存在文件 secret.key 中。

现在可以使用以下命令进行加密：

```java
java aes.AESTest -encrypt plaintextFile encryptedFile secret.key
```

使用以下命令解密：

```java
java aes.AESTest -decrypt encryptedFile decryptedFile secret.key
```

该程序很直接。-genkey 选项会生成一个新的秘密密钥，并将其序列化到给定文件中。该操作耗时较长，因为安全随机数生成器的初始化很耗时。-encrypt 和 -decrypt 选项都会调用同一个 crypt 方法，而该方法会调用密码的 update 和 doFinal 方法。请注意，只要输入块具有完整长度，就会调用 update 方法；而 doFinal 方法要么在输入块不完整时被调用（随后会进行填充），要么在没有额外数据时被调用（以生成一个填充块）。

### 代码清单 10.17 `aes/AESTest.java`

```java
1  package aes;
2
3  import java.io.*;
4  import java.security.*;
5  import javax.crypto.*;
6
```

### 代码清单 10.18 `aes/Util.java`

```java
package aes;

import java.io.*;
import java.security.*;
import java.security.spec.*;

public class Util
{
    /**
     * Uses a cipher to transform the bytes in an input stream and sends the transformed bytes
     * to an output stream.
     * @param in the input stream
     * @param out the output stream
     * @param cipher the cipher that transforms the bytes
     */
    public static void crypt(InputStream in, OutputStream out, Cipher cipher)
        throws IOException, GeneralSecurityException
    {
        int blockSize = cipher.getBlockSize();
        int outputSize = cipher.getOutputSize(blockSize);
        var inBytes = new byte[blockSize];
        var outBytes = new byte[outputSize];

        int inLength = 0;
        var done = false;
        while (!done)
        {
            inLength = in.read(inBytes);
            if (inLength == blockSize)
            {
                int outLength = cipher.update(inBytes, 0, blockSize, outBytes);
                out.write(outBytes, 0, outLength);
            }
            else done = true;
        }
        if (inLength > 0) outBytes = cipher.doFinal(inBytes, 0, inLength);
        else outBytes = cipher.doFinal();
        out.write(outBytes);
    }
}
```

| javax.crypto.KeyGenerator 1.4（续） |
| --- |
| • `SecretKey generateKey()`<br>生成一个新密钥。 |

| javax.crypto.spec.SecretKeySpec 1.4 |
| --- |
| • `SecretKeySpec(byte[] key, String algorithmName)`<br>构造一个密钥规范。 |

### 10.5.3 密码流

JCE 库提供了一组方便的流类，可以自动加密或解密流数据。例如，下面是将数据加密到文件的方法：

```java
Cipher cipher = . . .;
cipher.init(Cipher.ENCRYPT_MODE, key);
var out = new CipherOutputStream(new FileOutputStream(outputFileName), cipher);
var bytes = new byte[BLOCK_SIZE];
int inLength = getData(bytes); // get data from data source
while (inLength != -1)
{
    out.write(bytes, 0, inLength);
    inLength = getData(bytes); // get more data from data source
}
out.flush();
```

类似地，你可以使用 CipherInputStream 从文件中读取并解密数据：

```java
Cipher cipher = . . .;
cipher.init(Cipher.DECRYPT_MODE, key);
var in = new CipherInputStream(new FileInputStream(inputFileName), cipher);
var bytes = new byte[BLOCK_SIZE];
int inLength = in.read(bytes);
while (inLength != -1)
{
    putData(bytes, inLength); // put data to destination
    inLength = in.read(bytes);
}
```

密码流类会透明地处理对 update 和 doFinal 的调用，这显然很方便。

| `javax.crypto.CipherInputStream` | 1.4 |
| --- |
| • `CipherInputStream(InputStream in, Cipher cipher)`<br>构造一个输入流，该流从 *in* 读取数据，并使用给定密码对其进行解密或加密。<br><br>• `int read()`<br>• `int read(byte[] b, int off, int len)`<br>从输入流读取数据，数据会被自动解密或加密。 | |

| `javax.crypto.CipherOutputStream` | 1.4 |
| --- |
| • `CipherOutputStream(OutputStream out, Cipher cipher)`<br>构造一个输出流，该流将数据写入 *out*，并使用给定密码对其进行加密或解密。<br><br>• `void write(int ch)`<br>• `void write(byte[] b, int off, int len)`<br>将数据写入输出流，数据会被自动加密或解密。<br><br>• `void flush()`<br>刷新密码缓冲区，并在必要时执行填充。 | |

### 10.5.4 公钥密码

上一节中见到的 AES 密码是一种*对称*密码。加密和解密使用同一个密钥。对称密码的致命弱点在于密钥分发。如果 Alice 向 Bob 发送加密消息，Bob 就需要 Alice 使用的同一个密钥。如果 Alice 更改了密钥，她需要把消息以及新密钥（通过安全通道）都发送给 Bob。但也许她根本没有通往 Bob 的安全通道——而这正是她一开始要加密发给他的消息的原因。

公钥密码学解决了这个问题。在公钥密码中，Bob 拥有一对密钥，由一个公钥和一个匹配的私钥组成。Bob 可以把公钥发布到任何地方，但必须严密保管私钥。Alice 只需使用公钥来加密她发给 Bob 的消息。

实际上，事情并没有那么简单。所有已知的公钥算法都比 DES 或 AES 等对称密钥算法*慢得多*。使用公钥算法加密大量信息并不实际。不过，通过将公钥密码与快速对称密码结合，可以轻松克服这个问题，如下所示：

1. Alice 生成一个随机对称加密密钥。她用该密钥加密自己的明文。
2. Alice 用 Bob 的公钥加密该对称密钥。
3. Alice 将加密后的对称密钥和加密后的明文都发送给 Bob。
4. Bob 使用自己的私钥解密对称密钥。
5. Bob 使用解密后的对称密钥解密消息。

除 Bob 之外，没有人能解密该对称密钥，因为只有 Bob 拥有用于解密的私钥。因此，昂贵的公钥加密只应用于少量密钥数据。

最常用的公钥算法是由 Rivest、Shamir 和 Adleman 发明的 RSA 算法。直到 2000 年 10 月，该算法一直受一项专利保护，该专利转让给了 RSA Security, Inc.。许可证并不便宜——通常是 3% 的版税，每年最低支付 50,000 美元。现在该算法已进入公有领域。

要使用 RSA 算法，你需要一个公钥/私钥对。像这样使用 KeyPairGenerator：

```java
KeyPairGenerator pairgen = KeyPairGenerator.getInstance("RSA");
var random = new SecureRandom();
pairgen.initialize(KEYSIZE, random);
KeyPair keyPair = pairgen.generateKeyPair();
Key publicKey = keyPair.getPublic();
Key privateKey = keyPair.getPrivate();
```

代码清单 10.19 中的程序有三个选项。-genkey 选项生成一个密钥对。-encrypt 选项生成一个 AES 密钥，并用公钥将其包装。

```java
Key key = . . .; // an AES key
Key publicKey = . . .; // a public RSA key
Cipher cipher = Cipher.getInstance("RSA");
cipher.init(Cipher.WRAP_MODE, publicKey);
byte[] wrappedKey = cipher.wrap(key);
```

然后它会生成一个文件，其中包含

- 被包装密钥的长度
- 被包装密钥的字节
- 用 AES 密钥加密后的明文

-decrypt 选项用于解密这样的文件。要试用该程序，首先生成 RSA 密钥：



java rsa.RSATest -genkey public.key private.key

然后加密一个文件：

```text
java rsa.RSATest -encrypt plaintextFile encryptedFile public.key
```

最后，解密该文件并验证解密后的文件与明文匹配：

```text
java rsa.RSATest -decrypt encryptedFile decryptedFile private.key
```

#### 清单 10.19 `rsa/RSATest.java`

```java
package rsa;

import java.io.*;
import java.security.*;
import javax.crypto.*;

/**
 * This program tests the RSA cipher. Usage:<br>
 * java rsa.RSATest -genkey public private<br>
 * java rsa.RSATest -encrypt plaintext encrypted public<br>
 * java rsa.RSATest -decrypt encrypted decrypted private<br>
 * @author Cay Horstmann
 * @version 1.02 2018-05-01
 */
public class RSATest
{
    private static final int KEYSIZE = 512;

    public static void main(String[] args)
            throws IOException, GeneralSecurityException, ClassNotFoundException
    {
        if (args[0].equals("-genkey"))
        {
            KeyPairGenerator pairgen = KeyPairGenerator.getInstance("RSA");
            var random = new SecureRandom();
            pairgen.initialize(KEYSIZE, random);
            KeyPair keyPair = pairgen.generateKeyPair();
            try (var out = new ObjectOutputStream(new FileOutputStream(args[1])))
            {
                out.writeObject(keyPair.getPublic());
            }
            try (var out = new ObjectOutputStream(new FileOutputStream(args[2])))
            {
                out.writeObject(keyPair.getPrivate());
            }
        }
        else if (args[0].equals("-encrypt"))
        {
            KeyGenerator keygen = KeyGenerator.getInstance("AES");
            var random = new SecureRandom();
            keygen.init(random);
            SecretKey key = keygen.generateKey();

            // wrap with RSA public key
            try (var keyIn = new ObjectInputStream(new FileInputStream(args[3]));
                 var out = new DataOutputStream(new FileOutputStream(args[2]));
                 var in = new FileInputStream(args[1]))
            {
                var publicKey = (Key) keyIn.readObject();
                Cipher cipher = Cipher.getInstance("RSA");
                cipher.init(Cipher.WRAP_MODE, publicKey);
                byte[] wrappedKey = cipher.wrap(key);
                out.writeInt(wrappedKey.length);
                out.write(wrappedKey);

                cipher = Cipher.getInstance("AES");
                cipher.init(Cipher.ENCRYPT_MODE, key);
                Util.crypt(in, out, cipher);
            }
        }
        else
        {
            try (var in = new DataInputStream(new FileInputStream(args[1]));
                 var keyIn = new ObjectInputStream(new FileInputStream(args[3]));
                 var out = new FileOutputStream(args[2]))
            {
                int length = in.readInt();
                var wrappedKey = new byte[length];
                in.read(wrappedKey, 0, length);

                // unwrap with RSA private key
                var privateKey = (Key) keyIn.readObject();

                Cipher cipher = Cipher.getInstance("RSA");
                cipher.init(Cipher.UNWRAP_MODE, privateKey);
                Key key = cipher.unwrap(wrappedKey, "AES", Cipher.SECRET_KEY);

                cipher = Cipher.getInstance("AES");
                cipher.init(Cipher.DECRYPT_MODE, key);

                Util.crypt(in, out, cipher);
            }
        }
    }
}

你现在已经看到了 Java 安全模型如何允许对代码进行受控执行，这是 Java 平台一个独特且日益重要的方面。你也看到了 Java 库提供的认证和加密服务。

在下一章中，我们将深入探讨高级 Swing 和图形编程。

# 高级 Swing 和图形

## 本章内容

- 11.1 表格，第 613 页
- 11.2 树，第 652 页
- 11.3 高级 AWT，第 693 页
- 11.4 光栅图像，第 744 页
- 11.5 打印，第 772 页

在本章中，我们将继续第一卷中关于 Swing 用户界面工具包和 AWT 图形的讨论。我们重点介绍既适用于客户端用户界面，也适用于服务器端图形和图像生成的技术。Swing 拥有用于渲染表格和树的复杂组件。借助 2D 图形 API，你可以生成任意复杂度的矢量图。ImageIO API 允许你操作光栅图像。最后，你可以使用打印 API 生成打印输出和 PostScript 文件。

## 11.1 表格

JTable 组件显示对象的二维网格。表格在用户界面中很常见，Swing 团队在表格控件上投入了大量精力。表格本质上很复杂，但——也许比其他 Swing 类更成功——JTable 组件隐藏了大部分复杂性。你只需编写几行代码，就能生成功能齐全、行为丰富的表格。你也可以编写更多代码，为你的特定应用定制显示和行为。

在接下来的几节中，我们将解释如何创建简单的表格、用户如何与其交互，以及如何进行一些最常见的调整。与其他复杂的 Swing 控件一样，不可能完整地涵盖所有方面。欲了解更多信息，请参阅 David M. Geary 所著的 *Graphic Java™, Third Edition*（Prentice Hall, 1999），或 Kim Topley 所著的 *Core Swing*（Prentice Hall, 1999）。

### 11.1.1 简单表格

JTable 不存储自身的数据，而是从*表格模型*中获取这些数据。JTable 类有一个构造函数，可以把对象的二维数组包装到默认模型中。这就是我们在第一个例子中使用的策略；在本章后面，我们将讨论表格模型。

图 11.1 显示了一个典型表格，描述了太阳系行星的属性。（如果一颗行星主要由氢和氦组成，那么它就是*气态的*。对于“Color”列中的条目，你不必太当真——该列之所以被添加，是因为它将在后面的代码示例中用到。）

如清单 11.1 的代码所示，表格数据以 Object 值的二维数组形式存储：

```java
Object[][] cells =
{
    { "Mercury", 2440.0, 0, false, Color.YELLOW },
    { "Venus", 6052.0, 0, false, Color.YELLOW },
    . . .
}
```

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_636_0.png)

图 11.1 简单表格

> **注意：** 这里我们利用了自动装箱。第二、三、四列中的条目会自动转换为类型为 `Double`、`Integer` 和 `Boolean` 的对象。

表格只是简单地对每个对象调用 `toString` 方法来显示它。这就是为什么颜色会显示为 `java.awt.Color[r=...,g=...,b=...]`。

在一个单独的字符串数组中提供列名：

```java
String[] columnNames = { "Planet", "Radius", "Moons", "Gaseous", "Color" };
```

然后，根据单元格数组和列名数组构造一个表格：

```java
var table = new JTable(cells, columnNames);
```

你可以用通常的方式添加滚动条——将表格包装在 `JScrollPane` 中：

```java
var pane = new JScrollPane(table);
```

滚动表格时，表头不会滚出视野。接下来，单击某个列标题并将其向左或向右拖动。你会看到整个列脱离（见图 11.2）。你可以将其放到其他位置。这仅在*视图*中重新排列列，数据模型不受影响。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_637_0.png)

**图 11.2** 移动列

要调整列的大小，只需将光标放在两列之间，直到光标形状变为箭头。然后，将列边界拖到所需位置（见图 11.3）。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_638_0.png)

**图 11.3** 调整列大小

你应该让单元格不可编辑，或者处理单元格编辑事件并更新模型。我们将在本节后面讨论这些主题。

最后，单击列标题。行会自动排序。再次单击，排序顺序反转。此行为由以下调用激活：

```java
table.setAutoCreateRowSorter(true);
```

你可以通过以下调用打印表格：

```java
table.print();
```

> **警告：** 如果你没有将表格包装到滚动窗格中，则需要显式添加表头：
>
> ```java
> add(table.getTableHeader(), BorderLayout.NORTH);
> ```

#### 清单 11.1 `table/TableTest.java`

```java
package table;

import java.awt.*;
import java.awt.print.*;

import javax.swing.*;

/**
 * This program demonstrates how to show a simple table.
 * @version 1.14 2015-05-01
 * @author Cay Horstmann
 */
```




```java
13 public class TableTest
14 {
15     public static void main(String[] args)
16     {
17         EventQueue.invokeLater(() ->
18             {
19                 var frame = new PlanetTableFrame();
20                 frame.setTitle("TableTest");
21                 frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
22                 frame.setVisible(true);
23             });
24     }
25 }
26
27 /**
28  * This frame contains a table of planet data.
29  */
30 class PlanetTableFrame extends JFrame
31 {
32     private String[] columnNames = { "Planet", "Radius", "Moons", "Gaseous", "Color" };
33     private Object[][] cells =
34         {
35             { "Mercury", 2440.0, 0, false, Color.YELLOW },
36             { "Venus", 6052.0, 0, false, Color.YELLOW },
37             { "Earth", 6378.0, 1, false, Color.BLUE },
38             { "Mars", 3397.0, 2, false, Color.RED },
39             { "Jupiter", 71492.0, 16, true, Color.ORANGE },
40             { "Saturn", 60268.0, 18, true, Color.ORANGE },
41             { "Uranus", 25559.0, 17, true, Color.BLUE },
42             { "Neptune", 24766.0, 8, true, Color.BLUE },
43             { "Pluto", 1137.0, 1, false, Color.BLACK }
44         };
45
46     public PlanetTableFrame()
47     {
48         var table = new JTable(cells, columnNames);
49         table.setAutoCreateRowSorter(true);
50         add(new JScrollPane(table), BorderLayout.CENTER);
51         var printButton = new JButton("Print");
52         printButton.addActionListener(event ->
53             {
54                 try { table.print(); }
55                 catch (SecurityException | PrinterException ex) { ex.printStackTrace(); }
56             });
57         var buttonPanel = new JPanel();
58         buttonPanel.add(printButton);
59         add(buttonPanel, BorderLayout.SOUTH);
60         pack();
61     }
62 }
```

| `javax.swing.JTable` | `1.2` |
| --- | --- |
| `JTable(Object[][] entries, Object[] columnNames)` | 用默认表模型构造一个表。 |
| `void print()` `5.0` | 显示打印对话框并打印该表。 |
| `boolean getAutoCreateRowSorter()` `6` |  |
| `void setAutoCreateRowSorter(boolean newValue)` `6` | 获取或设置 autoCreateRowSorter 属性。默认值为 false。设置后，每当模型发生变化时，都会自动设置一个默认行排序器。 |
| `boolean getFillsViewportHeight()` `6` |  |
| `void setFillsViewportHeight(boolean newValue)` `6` | 获取或设置 fillsViewportHeight 属性。默认值为 false。设置后，表始终填满其所在的视口。 |

### 11.1.2 表模型

在前面的示例中，表数据存储在一个二维数组中。不过，在你自己的代码中通常不应采用这种策略。与其将数据倾倒进数组再以表的形式显示，不如考虑实现你自己的表模型。

表模型实现起来特别简单，因为你可以利用实现了大多数所需方法的 AbstractTableModel 类。你只需要提供三个方法：

```java
public int getRowCount();
public int getColumnCount();
public Object getValueAt(int row, int column);
```

实现 getValueAt 方法有很多方式。例如，如果你想显示一个包含数据库查询结果的 RowSet 的内容，只需提供这个方法：

```java
public Object getValueAt(int r, int c)
{
    try
    {
        rowSet.absolute(r + 1);
        return rowSet.getObject(c + 1);
    }
    catch (SQLException e)
    {
        e.printStackTrace();
        return null;
    }
}
```

我们的示例程序甚至更简单。我们构造一个表来显示一些计算得到的值——即投资在不同利率情景下的增长（见图 11.4）。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_641_0.png)

**图 11.4** 投资的增长

`getValueAt` 方法计算相应的值并对其进行格式化：

```java
public Object getValueAt(int r, int c)
{
    double rate = (c + minRate) / 100.0;
    int periods = r;
    double futureBalance = INITIAL_BALANCE * Math.pow(1 + rate, periods);
    return String.format("%.2f", futureBalance);
}
```

`getRowCount` 和 `getColumnCount` 方法只是返回行数和列数：

```java
public int getRowCount() { return years; }
public int getColumnCount() { return maxRate - minRate + 1; }
```

如果你不提供列名，`AbstractTableModel` 的 `getColumnName` 方法会将列命名为 A、B、C 等。要更改默认列名，请重写 `getColumnName` 方法。在这个例子中，我们只是用利率来标记每一列。

```java
public String getColumnName(int c) { return (c + minRate) + "%"; }
```

你可以在程序清单 11.2 中找到完整的源代码。

**程序清单 11.2** `tableModel/InvestmentTable.java`

```java
1  package tableModel;
2
3  import java.awt.*;
4
5  import javax.swing.*;
6  import javax.swing.table.*;
7
8  /**
9   * This program shows how to build a table from a table model.
10  * @version 1.04 2018-05-01
11  * @author Cay Horstmann
12  */
13 public class InvestmentTable
14 {
15    public static void main(String[] args)
16    {
17       EventQueue.invokeLater(() ->
18          {
19             var frame = new InvestmentTableFrame();
20             frame.setTitle("InvestmentTable");
21             frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
22             frame.setVisible(true);
23          });
24    }
25 }
26
27 /**
28  * This frame contains the investment table.
29  */
30 class InvestmentTableFrame extends JFrame
31 {
32    public InvestmentTableFrame()
33    {
34       var model = new InvestmentTableModel(30, 5, 10);
35       var table = new JTable(model);
36       add(new JScrollPane(table));
37       pack();
38    }
39 }
40
41 /**
42  * This table model computes the cell entries each time they are requested. The table contents
43  * shows the growth of an investment for a number of years under different interest rates.
44  */
45 class InvestmentTableModel extends AbstractTableModel
46 {
47    private static double INITIAL_BALANCE = 100000.0;
48
49    private int years;
50    private int minRate;
51    private int maxRate;
52
53    /**
54     * Constructs an investment table model.
55     * @param y the number of years
56     * @param r1 the lowest interest rate to tabulate
57     * @param r2 the highest interest rate to tabulate
58     */
59    public InvestmentTableModel(int y, int r1, int r2)
60    {
61       years = y;
62       minRate = r1;
63       maxRate = r2;
64    }
65
66    public int getRowCount()
67    {
68       return years;
69    }
70
71    public int getColumnCount()
72    {
73       return maxRate - minRate + 1;
74    }
75
76    public Object getValueAt(int r, int c)
77    {
78       double rate = (c + minRate) / 100.0;
79       int nperiods = r;
80       double futureBalance = INITIAL_BALANCE * Math.pow(1 + rate, nperiods);
81       return String.format("%.2f", futureBalance);
82    }
83
84    public String getColumnName(int c)
85    {
86       return (c + minRate) + "%";
87    }
88 }
```

| `javax.swing.table.TableModel` | `1.2` |
| --- | --- |
| `int getRowCount()`<br>`int getColumnCount()` | 获取表模型中的行数和列数。 |
| `Object getValueAt(int row, int column)` | 获取给定行和列处的值。 |
| `void setValueAt(Object newValue, int row, int column)` | 在给定行和列处设置新值。 |
| `boolean isCellEditable(int row, int column)` | 如果给定行和列处的单元格可编辑，则返回 true。 |
| `String getColumnName(int column)` | 获取列标题。 |

### 11.1.3 处理行和列

在本小节中，你将看到如何操作表中的行和列。阅读这些内容时，请记住 Swing 表是相当不对称的——你可以对行和列执行的操作是不同的。表组件经过优化，用于显示结构相同的信息行，例如数据库查询的结果，而不是任意的二维对象网格。你将在整个小节中看到这种不对称性。

#### 11.1.3.1 列类

在下一个示例中，我们再次显示行星数据，但这一次我们想向表提供更多关于列类型的信息。这是通过定义表模型的 `Class<?> getColumnClass(int columnIndex)` 方法返回描述列类型的类来实现的。

JTable 类使用此信息为该类选择合适的渲染器。表 11.1 显示了默认的渲染操作。

你可以在图 11.5 中看到复选框和图像。（感谢 Jim Evins 提供行星图像！）

要渲染其他类型，你可以安装自定义渲染器——参见第 639 页的 11.1.4 节“单元格渲染与编辑”。



#### 表 11.1 默认渲染操作

| 类型 | 渲染为 |
|---|---|
| 布尔值 | 复选框 |
| 图标 | 图像 |
| 对象 | 字符串 |

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_645_0.png)

图 11.5 包含行星数据的表格

#### 11.1.3.2 访问表列

JTable 类将有关表列的信息存储在 TableColumn 类型的对象中。TableColumnModel 对象管理这些列。（图 11.6 显示了最重要的表类之间的关系。）如果你不想动态插入或删除列，就不会太多地使用列模型。列模型最常见的用途就是获取一个 TableColumn 对象：

```java
int columnIndex = . . . ;
TableColumn column = table.getColumnModel().getColumn(columnIndex);
```

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_646_0.png)

图 11.6 表类之间的关系

#### 11.1.3.3 调整列大小

TableColumn 类让你可以控制列的大小调整行为。你可以使用以下方法设置首选宽度、最小宽度和最大宽度：

```java
void setPreferredWidth(int width)
void setMinWidth(int width)
void setMaxWidth(int width)
```

表组件使用这些信息来布局各列。

使用以下方法

```java
void setResizable(boolean resizable)
```

控制是否允许用户调整列的大小。

你可以通过以下方法以编程方式调整列的大小：

```java
void setWidth(int width)
```

当调整某一列的大小时，默认情况下表的总体大小保持不变。当然，被调整列的宽度增减必须分配到其他列上。默认行为是更改被调整列右侧所有列的大小。这是一个很好的默认设置，因为它允许用户从左到右将所有列调整到所需宽度。

你可以使用以下方法设置表 11.2 中的另一种行为：

```java
void setAutoResizeMode(int mode)
```

这是 JTable 类的方法。

##### 表 11.2 调整大小模式

| 模式 | 行为 |
|---|---|
| `AUTO_RESIZE_OFF` | 不调整其他列的大小；更改表宽度。 |
| `AUTO_RESIZE_NEXT_COLUMN` | 仅调整下一列的大小。 |
| `AUTO_RESIZE_SUBSEQUENT_COLUMNS` | 平均调整所有后续列的大小；这是默认行为。 |
| `AUTO_RESIZE_LAST_COLUMN` | 仅调整最后一列的大小。 |
| `AUTO_RESIZE_ALL_COLUMNS` | 调整表中的所有列；这不是一个好的选择，因为它会阻止用户将多列调整到所需大小。 |

#### 11.1.3.4 调整行大小

行高由 JTable 类直接管理。如果你的单元格高于默认高度，可能需要设置行高：

```java
table.setRowHeight(height);
```

默认情况下，表中所有行具有相同高度。你可以通过以下调用设置各单独行的高度：

```java
table.setRowHeight(row, height);
```

实际行高等于用这些方法设置的行高减去行边距。默认行边距为 1 像素，但你可以通过以下调用更改它：

```java
table.setRowMargin(margin);
```

红色。当你单击 Color 列时，会看到蓝色行星移到表格底部。这是通过以下调用实现的：

```java
sorter.setComparator(COLOR_COLUMN, new Comparator<Color>()
{
   public int compare(Color c1, Color c2)
   {
      int d = c1.getBlue() - c2.getBlue();
      if (d != 0) return d;
      d = c1.getGreen() - c2.getGreen();
      if (d != 0) return d;
      return c1.getRed() - c2.getRed();
   }
});
```

如果没有为某一列指定比较器，则排序顺序按如下方式确定：

- 1. 如果列类是 `String`，则使用 `Collator.getInstance()` 返回的默认排序器。它按照适合当前区域设置的方式对字符串排序。（有关区域设置和排序器的更多信息，请参见第 7 章。）
- 2. 如果列类实现了 `Comparable`，则使用其 `compareTo` 方法。
- 3. 如果已为排序器设置 `TableStringConverter`，则使用默认排序器对转换器的 `toString` 方法返回的字符串进行排序。如果你想使用这种方法，请按如下方式定义转换器：

    ```java
    sorter.setStringConverter(new TableStringConverter()
    {
       public String toString(TableModel model, int row, int column)
       {
          Object value = model.getValueAt(row, column);
          convert value to a string and return it
       }
    });
    ```

- 4. 否则，对单元格值调用 `toString` 方法，并使用默认排序器对它们进行排序。

#### 11.1.3.5 过滤行

除了对行排序之外，`TableRowSorter` 还可以有选择地隐藏行——这一过程称为过滤。要激活过滤，请设置一个 `RowFilter`。例如，要包含所有至少有一颗卫星的行，请调用

```java
sorter.setRowFilter(RowFilter.numberFilter(ComparisonType.NOT_EQUAL, 0, MOONS_COLUMN));
```

这里，我们使用一个预定义的数字过滤器。要构造数字过滤器，请提供

- 比较类型（EQUAL、NOT_EQUAL、AFTER 或 BEFORE 之一）。
- Number 子类的对象（例如 Integer 或 Double）。只考虑与给定 Number 对象具有相同类的对象。
- 零个或多个列索引值。如果未提供索引值，则搜索所有列。

静态方法 RowFilter.dateFilter 以相同方式构造日期过滤器；你需要提供 Date 对象而不是 Number 对象。

最后，静态方法 RowFilter.regexFilter 构造一个过滤器，用于查找与正则表达式匹配的字符串。例如，

```java
sorter.setRowFilter(RowFilter.regexFilter(".*[^s]$", PLANET_COLUMN));
```

仅显示名称不以“s”结尾的行星。（有关正则表达式的更多信息，请参见第 2 章。）

你还可以使用 andFilter、orFilter 和 notFilter 方法组合过滤器。要过滤名称不以“s”结尾且至少有一颗卫星的行星，可以使用以下过滤器组合：

```java
sorter.setRowFilter(RowFilter.andFilter(List.of(
    RowFilter.regexFilter(".*[^s]$", PLANET_COLUMN),
    RowFilter.numberFilter(ComparisonType.NOT_EQUAL, 0, MOONS_COLUMN))));
```

要实现自己的过滤器，请提供 RowFilter 的子类，并实现 include 方法以指示应显示哪些行。这很容易做到，但 RowFilter 类那种宏大的通用性会让人有点望而生畏。

`RowFilter<M, I>` 类有两个类型参数——分别用于模型和行标识符的类型。处理表时，模型始终是 TableModel 的子类型，标识符类型是 Integer。（将来某个时候，其他组件也可能支持行过滤。例如，要在 JTree 中过滤行，可能会使用 `RowFilter<TreeModel, TreePath>`。）

行过滤器必须实现以下方法

```java
public boolean include(RowFilter.Entry<? extends M, ? extends I> entry)
```

`RowFilter.Entry` 类提供了获取模型、行标识符以及给定索引处值的方法。因此，你可以按行标识符和行内容进行过滤。

例如，这个过滤器每隔一行显示一行：

```java
var filter = new RowFilter<TableModel, Integer>()
{
    public boolean include(Entry<? extends TableModel, ? extends Integer> entry)
    {
        return entry.getIdentifier() % 2 == 0;
    }
};
```

如果你只想包含卫星数量为偶数的行星，则应改为检查

```java
((Integer) entry.getValue(MOONS_COLUMN)) % 2 == 0
```

在我们的示例程序中，我们允许用户隐藏任意行。我们将隐藏的行索引存储在一个集合中。该行过滤器显示索引不在该集合中的所有行。

过滤机制并非为条件随时间变化的过滤器而设计。在我们的示例程序中，每当隐藏行集合发生变化时，我们都会不断调用

```java
sorter.setRowFilter(filter);
```

设置过滤器会使其立即生效。

#### 11.1.3.6 隐藏和显示列

如你在上一节中所见，你可以按表行的内容或行标识符来过滤表行。隐藏表列使用完全不同的机制。

JTable 类的 removeColumn 方法从表视图中移除一列。列数据实际上并未从模型中移除——它们只是从视图中隐藏。removeColumn 方法接受一个 TableColumn 参数。如果你有列号（例如，通过调用 getSelectedColumns 获得），则需要向表模型请求实际的表列对象：

```java
TableColumnModel columnModel = table.getColumnModel();
TableColumn column = columnModel.getColumn(i);
table.removeColumn(column);
```

如果你记得该列，稍后可以将其重新添加回来：

```java
table.addColumn(column);
```

此方法将列添加到末尾。如果你希望它出现在其他位置，请调用 moveColumn 方法。

你也可以通过添加新的 TableColumn 对象来添加一个与表模型中列索引对应的新列：

```java
table.addColumn(new TableColumn(modelColumnIndex));
```

可以让多个表列查看模型中的同一列。

代码清单 11.3 中的程序演示了行和列的选择与过滤。

##### 代码清单 11.3 `tableRowColumn/PlanetTableFrame.java`

```java
package tableRowColumn;

import java.awt.*;
import java.util.*;

import javax.swing.*;
import javax.swing.table.*;

/**
 * This frame contains a table of planet data.
 */
public class PlanetTableFrame extends JFrame
{
    private static final int DEFAULT_WIDTH = 600;
    private static final int DEFAULT_HEIGHT = 500;

    public static final int COLOR_COLUMN = 4;
    public static final int IMAGE_COLUMN = 5;

    private JTable table;
    private HashSet<Integer> removedRowIndices;
    private ArrayList<TableColumn> removedColumns;
    private JCheckBoxMenuItem rowsItem;
    private JCheckBoxMenuItem columnsItem;
    private JCheckBoxMenuItem cellsItem;

    private String[] columnNames = { "Planet", "Radius", "Moons", "Gaseous", "Color", "Image" };

    private Object[][] cells =
    {
        { "Mercury", 2440.0, 0, false, Color.YELLOW,
            new ImageIcon(getClass().getResource("Mercury.gif")) },
        { "Venus", 6052.0, 0, false, Color.YELLOW,
            new ImageIcon(getClass().getResource("Venus.gif")) },
        { "Earth", 6378.0, 1, false, Color.BLUE,
            new ImageIcon(getClass().getResource("Earth.gif")) },
        { "Mars", 3397.0, 2, false, Color.RED,
            new ImageIcon(getClass().getResource("Mars.gif")) },
        { "Jupiter", 71492.0, 16, true, Color.ORANGE,
            new ImageIcon(getClass().getResource("Jupiter.gif")) },
        { "Saturn", 60268.0, 18, true, Color.ORANGE,
            new ImageIcon(getClass().getResource("Saturn.gif")) },
        { "Uranus", 25559.0, 17, true, Color.BLUE,
            new ImageIcon(getClass().getResource("Uranus.gif")) },
        { "Neptune", 24760.0, 8, true, Color.BLUE,
            new ImageIcon(getClass().getResource("Neptune.gif")) },
        { "Pluto", 1137.0, 1, false, Color.BLACK,
            new ImageIcon(getClass().getResource("Pluto.gif")) }
    };

    public PlanetTableFrame()
    {
        setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);

        var model = new DefaultTableModel(cells, columnNames)
        {
            public Class<?> getColumnClass(int c)
            {
                return cells[0][c].getClass();
            }
        };

        table = new JTable(model);

        table.setRowHeight(100);

        table.getColumnModel().getColumn(COLOR_COLUMN).setMinWidth(250);
        table.getColumnModel().getColumn(IMAGE_COLUMN).setMinWidth(100);

        var sorter = new TableRowSorter<TableModel>(model);
        table.setRowSorter(sorter);
        sorter.setComparator(COLOR_COLUMN, Comparator.comparing(Color::getBlue)
            .thenComparing(Color::getGreen).thenComparing(Color::getRed));
        sorter.setSortable(IMAGE_COLUMN, false);
        add(new JScrollPane(table), BorderLayout.CENTER);

        removedRowIndices = new HashSet<>();
        removedColumns = new ArrayList<>();

        var filter = new RowFilter<TableModel, Integer>()
        {
            public boolean include(Entry<? extends TableModel, ? extends Integer> entry)
            {
                return !removedRowIndices.contains(entry.getIdentifier());
            }
        };

        // create menu

        var menuBar = new JMenuBar();
        setJMenuBar(menuBar);

        var selectionMenu = new JMenu("Selection");
        menuBar.add(selectionMenu);

        rowsItem = new JCheckBoxMenuItem("Rows");
        columnsItem = new JCheckBoxMenuItem("Columns");
        cellsItem = new JCheckBoxMenuItem("Cells");

        rowsItem.setSelected(table.getRowSelectionAllowed());
        columnsItem.setSelected(table.getColumnSelectionAllowed());
        cellsItem.setSelected(table.getCellSelectionEnabled());

        rowsItem.addActionListener(event ->
        {
            table.clearSelection();
            table.setRowSelectionAllowed(rowsItem.isSelected());
            updateCheckboxMenuItems();
        });
        selectionMenu.add(rowsItem);

        columnsItem.addActionListener(event ->
        {
            table.clearSelection();
            table.setColumnSelectionAllowed(columnsItem.isSelected());
            updateCheckboxMenuItems();
        });
        selectionMenu.add(columnsItem);

        cellsItem.addActionListener(event ->
        {
            table.clearSelection();
            table.setCellSelectionEnabled(cellsItem.isSelected());
            updateCheckboxMenuItems();
        });
        selectionMenu.add(cellsItem);

        var tableMenu = new JMenu("Edit");
        menuBar.add(tableMenu);

        var hideColumnsItem = new JMenuItem("Hide Columns");
        hideColumnsItem.addActionListener(event ->
        {
            int[] selected = table.getSelectedColumns();
            TableColumnModel columnModel = table.getColumnModel();

            // remove columns from view, starting at the last
            // index so that column numbers aren't affected

            for (int i = selected.length - 1; i >= 0; i--)
            {
                TableColumn column = columnModel.getColumn(selected[i]);
                table.removeColumn(column);

                // store removed columns for "show columns" command

                removedColumns.add(column);
            }
        });
        tableMenu.add(hideColumnsItem);

        var showColumnsItem = new JMenuItem("Show Columns");
        showColumnsItem.addActionListener(event ->
        {
            // restore all removed columns
            for (TableColumn tc : removedColumns)
                table.addColumn(tc);
            removedColumns.clear();
        });
        tableMenu.add(showColumnsItem);

        var hideRowsItem = new JMenuItem("Hide Rows");
        hideRowsItem.addActionListener(event ->
        {
            int[] selected = table.getSelectedRows();
            for (int i : selected)
                removedRowIndices.add(table.convertRowIndexToModel(i));
            sorter.setRowFilter(filter);
        });
        tableMenu.add(hideRowsItem);

        var showRowsItem = new JMenuItem("Show Rows");
        showRowsItem.addActionListener(event ->
        {
            removedRowIndices.clear();
            sorter.setRowFilter(filter);
        });
        tableMenu.add(showRowsItem);

        var printSelectionItem = new JMenuItem("Print Selection");
        printSelectionItem.addActionListener(event ->
        {
            int[] selected = table.getSelectedRows();
            System.out.println("Selected rows: " + Arrays.toString(selected));
            selected = table.getSelectedColumns();
            System.out.println("Selected columns: " + Arrays.toString(selected));
        });
        tableMenu.add(printSelectionItem);
    }

    private void updateCheckboxMenuItems()
    {
        rowsItem.setSelected(table.getRowSelectionAllowed());
        columnsItem.setSelected(table.getColumnSelectionAllowed());
        cellsItem.setSelected(table.getCellSelectionEnabled());
    }
}
```

| **javax.swing.table.TableModel 1.2** |
| --- |
| • `Class getColumnClass(int columnIndex)`<br>获取此列中值的类。该信息用于排序和渲染。 |

| **javax.swing.JTable 1.2** |
| --- |
| • `TableColumnModel getColumnModel()`<br>获取描述表列排列的列模型。<br><br>• `void setAutoResizeMode(int mode)`<br>设置表列自动调整大小的模式。<br>*参数：* mode&nbsp;&nbsp;AUTO_RESIZE_OFF、AUTO_RESIZE_NEXT_COLUMN、AUTO_RESIZE_SUBSEQUENT_COLUMNS、AUTO_RESIZE_LAST_COLUMN 和 AUTO_RESIZE_ALL_COLUMNS 之一<br><br>• `int getRowMargin()`<br><br>• `void setRowMargin(int margin)`<br>获取或设置相邻行中单元格之间的空白量。<br><br>• `int getRowHeight()`<br><br>• `void setRowHeight(int height)`<br>获取或设置表中所有行的默认高度。<br><br>• `int getRowHeight(int row)`<br><br>• `void setRowHeight(int row, int height)`<br>获取或设置表中给定行的高度。 |

| **javax.swing.table.TableColumn 1.2** |
| --- |
| • `TableColumn(int modelColumnIndex)`<br>构造一个表列，用于查看具有给定索引的模型列。<br>• `void setPreferredWidth(int width)`<br>• `void setMinWidth(int width)`<br>• `void setMaxWidth(int width)`<br>将此表列的首选宽度、最小宽度和最大宽度设置为 width。<br>• `void setWidth(int width)`<br>将此列的实际宽度设置为 width。<br>• `void setResizable(boolean b)`<br>如果 b 为 true，则此列可调整大小。 |

| **javax.swing.ListSelectionModel 1.2** |
| --- |
| • `void setSelectionMode(int mode)`<br>*参数：* mode 取值为 SINGLE_SELECTION、SINGLE_INTERVAL_SELECTION 和 MULTIPLE_INTERVAL_SELECTION 之一 |

| **`javax.swing.DefaultRowSorter<R, I>` 6** |
| --- |
| • `void setComparator(int column, Comparator<?> comparator)`<br>设置要与给定列一起使用的比较器。<br>• `void setSortable(int column, boolean enabled)`<br>启用或禁用给定列的排序。<br>• `void setRowFilter(RowFilter<? super M, ? super I> filter)`<br>设置行过滤器。 |

| **`javax.swing.table.TableRowSorter<R extends TableModel>` 6** |
| --- |
| • `void setStringConverter(TableStringConverter stringConverter)`<br>设置用于排序和过滤的字符串转换器。 |

| **javax.swing.table.TableStringConverter 6** |
| --- |
| • `abstract String toString(TableModel model, int row, int column)`<br>将给定位置处的模型值转换为字符串；可以重写此方法。 |




##### `javax.swing.RowFilter<M, I>`

- `boolean include(RowFilter.Entry<? extends M, ? extends I> entry)`  
  指定要保留的行；你可以重写此方法。
- `static <M, I> RowFilter<M, I> numberFilter(RowFilter.ComparisonType type, Number number, int... indices)`
- `static <M, I> RowFilter<M, I> dateFilter(RowFilter.ComparisonType type, Date date, int... indices)`  
  返回一个过滤器，其中包含的值与给定比较条件、给定数字或日期匹配的行。比较类型为 `EQUAL`、`NOT_EQUAL`、`AFTER` 或 `BEFORE` 之一。如果给出了任何列模型索引，则只搜索这些列；否则搜索所有列。对于数字过滤器，单元格值的类必须与 number 的类匹配。
- `static <M, I> RowFilter<M, I> regexFilter(String regex, int... indices)`  
  返回一个过滤器，其中包含具有与给定正则表达式匹配的字符串值的行。如果给出了任何列模型索引，则只搜索这些列；否则搜索所有列。注意，匹配的是 `RowFilter.Entry` 的 `getStringValue` 方法返回的字符串。
- `static <M, I> RowFilter<M, I> andFilter(Iterable<? extends RowFilter<? super M, ? super I>> filters)`
- `static <M, I> RowFilter<M, I> orFilter(Iterable<? extends RowFilter<? super M, ? super I>> filters)`  
  返回一个过滤器，其中包含所有过滤器都包含的条目，或至少一个过滤器包含的条目。
- `static <M, I> RowFilter<M, I> notFilter(RowFilter<M, I> filter)`  
  返回一个过滤器，其中包含未被给定过滤器包含的条目。

##### `javax.swing.RowFilter.Entry<M, I>`

- `I getIdentifier()`  
  返回此行条目的标识符。
- `M getModel()`  
  返回此行条目的模型。
- `Object getValue(int index)`  
  返回此行中给定索引处存储的值。

##### `javax.swing.RowFilter.Entry<M, I>`（续）

- `int getValueCount()`  
  返回此行中存储的值的数量。
- `String getStringValue()`  
  返回此行中存储的值，并转换为字符串。`TableRowSorter` 生成条目，其 `getStringValue` 调用排序器的字符串转换器。

### 11.1.4 单元格渲染与编辑

正如你在第 623 页的 11.1.3.2 节“访问表格列”中所见，列类型决定单元格的渲染方式。对于 Boolean 和 Icon 类型，有默认渲染器，分别渲染复选框或图标。对于所有其他类型，需要安装自定义渲染器。

#### 11.1.4.1 渲染单元格

表格单元格渲染器与之前看到的列表单元格渲染器类似。它们实现 TableCellRenderer 接口，该接口只有一个方法：

```java
Component getTableCellRendererComponent(JTable table, Object value,
        boolean isSelected, boolean hasFocus, int row, int column)
```

该方法在表格需要绘制单元格时被调用。你返回一个组件，随后调用其 paint 方法来填充单元格区域。

图 11.8 中的表格包含 Color 类型的单元格。渲染器只返回一个面板，其背景色是单元格中存储的颜色对象。颜色作为 value 参数传入。

```java
class ColorTableCellRenderer extends JPanel implements TableCellRenderer
{
    public Component getTableCellRendererComponent(JTable table, Object value,
            boolean isSelected, boolean hasFocus, int row, int column)
    {
        setBackground((Color) value);
        if (hasFocus)
            setBorder(UIManager.getBorder("Table.focusCellHighlightBorder"));
        else
            setBorder(null);
        return this;
    }
}
```

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_662_0.png)

**图 11.8** 带单元格渲染器的表格

如你所见，当单元格获得焦点时，渲染器会绘制边框。（我们向 UIManager 询问正确的边框。为了找到查找键，我们查看了 `DefaultTableCellRenderer` 类的源代码。）

> **提示：** 如果你的渲染器只绘制文本字符串或图标，可以扩展 `DefaultTableCellRenderer` 类。它会为你处理焦点和选中状态的渲染。

你需要告诉表格对所有 `Color` 类型的对象使用此渲染器。`JTable` 类的 `setDefaultRenderer` 方法可让你建立这种关联。提供一个 `Class` 对象和渲染器。

```java
table.setDefaultRenderer(Color.class, new ColorTableCellRenderer());
```

现在，该渲染器会用于此表格中给定类型的所有对象。

如果想根据其他某些条件选择渲染器，需要子类化 `JTable` 类并重写 `getCellRenderer` 方法。

#### 11.1.4.2 渲染表头

要在表头中显示图标，请设置表头值：

```java
moonColumn.setHeaderValue(new ImageIcon("Moons.gif"));
```

然而，表头不够智能，无法为表头值选择合适的渲染器。必须手动安装渲染器。例如，要在列标题中显示图像图标，请调用：

```java
moonColumn.setHeaderRenderer(table.getDefaultRenderer(ImageIcon.class));
```

#### 11.1.4.3 编辑单元格

要启用单元格编辑，表格模型必须通过定义 isCellEditable 方法来指明哪些单元格可编辑。最常见的情况是，你会希望让某些列可编辑。在示例程序中，我们允许编辑四列。

```java
public boolean isCellEditable(int r, int c)
{
    return c == PLANET_COLUMN || c == MOONS_COLUMN || c == GASEOUS_COLUMN
        || c == COLOR_COLUMN;
}
```

> **注意：** `AbstractTableModel` 将 `isCellEditable` 方法定义为始终返回 false。`DefaultTableModel` 重写该方法，使其始终返回 true。

如果运行程序（程序清单 11.4 至 11.7），请注意你可以单击 Gaseous 列中的复选框，并打开或关闭复选标记。如果单击 Moons 列中的单元格，会出现一个组合框（见图 11.9）。你很快就会看到如何安装这样的组合框作为单元格编辑器。

最后，单击第一列中的单元格。该单元格获得焦点。你可以开始输入，单元格内容会发生变化。

你刚刚看到的是 DefaultCellEditor 类的三种变体。可以用 JTextField、JCheckBox 或 JComboBox 构造 DefaultCellEditor。JTable 类会自动为 Boolean 单元格安装复选框编辑器，并为所有未提供自己的渲染器的可编辑单元格安装文本字段编辑器。文本字段让用户可以编辑这些字符串：它们是对表格模型的 getValueAt 方法的返回值应用 toString 后得到的字符串。

编辑完成后，通过调用编辑器的 getCellEditorValue 方法获取编辑后的值。该方法应返回正确类型的值（即模型的 `getColumnClass` 方法返回的类型）。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_664_0.png)

要获得组合框编辑器，请手动设置单元格编辑器——JTable 组件不知道对于特定类型哪些值可能是合适的。对于 Moons 列，我们希望让用户选择 0 到 20 之间的任意值。以下是初始化组合框的代码：

```java
var moonCombo = new JComboBox();
for (int i = 0; i <= 20; i++)
    moonCombo.addItem(i);
```

要构造 DefaultCellEditor，请在构造函数中提供组合框：

```java
var moonEditor = new DefaultCellEditor(moonCombo);
```

接下来，我们需要安装编辑器。与颜色单元格渲染器不同，此编辑器不依赖于对象类型——我们不一定想把它用于所有 Integer 类型的对象。相反，我们需要将它安装到特定列中：

```java
moonColumn.setCellEditor(moonEditor);
```

#### 11.1.4.4 自定义编辑器

再次运行示例程序，并单击一种颜色。会弹出一个颜色选择器，让你为行星选择新颜色。选择一种颜色并单击“确定”。单元格颜色会更新（见图 11.10）。



![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_665_0.png)

**图 11.10** 使用颜色选择器编辑单元格颜色

颜色单元格编辑器并不是标准的表格单元格编辑器，而是一种自定义实现。要创建自定义单元格编辑器，需要实现 TableCellEditor 接口。该接口使用起来有些繁琐，从 Java SE 1.3 开始，提供了 AbstractCellEditor 类来处理事件处理的细节。

TableCellEditor 接口的 getTableCellEditorComponent 方法要求提供一个用于渲染该单元格的组件。它与 TableCellRenderer 接口的 getTableCellRendererComponent 方法完全相同，只是没有焦点参数。当单元格正在被编辑时，假定它拥有焦点。编辑进行时，编辑器组件会临时替代渲染器。在我们的示例中，我们返回一个没有颜色的空白面板，这向用户表明该单元格当前正在被编辑。

总而言之，你的自定义编辑器应完成以下工作：

- 1. 扩展 `AbstractCellEditor` 类并实现 `TableCellEditor` 接口。
- 2. 定义 `getTableCellEditorComponent` 方法来提供组件。该组件可以是虚拟组件（如果你弹出对话框），也可以是用于就地编辑的组件，例如组合框或文本字段。
- 3. 定义 `shouldSelectCell`、`stopCellEditing` 和 `cancelCellEditing` 方法来处理编辑过程的开始、完成和取消。`stopCellEditing` 和 `cancelCellEditing` 方法应调用父类方法，以确保监听器得到通知。
- 4. 定义 `getTableCellEditorValue` 方法来返回编辑过程的结果值。

最后，通过调用 `stopCellEditing` 和 `cancelCellEditing` 方法来表示用户已完成编辑。在构造颜色对话框时，我们安装了触发这些事件的接受和取消回调。

```java
colorDialog = JColorChooser.createDialog(null, "Planet Color", false, colorChooser,
    EventHandler.create(ActionListener.class, this, "stopCellEditing"),
    EventHandler.create(ActionListener.class, this, "cancelCellEditing"));
```

至此，自定义编辑器的实现就完成了。

现在你已经知道如何让单元格可编辑，以及如何安装编辑器。还有一个问题尚未解决——如何用用户编辑的值更新模型。当编辑完成时，JTable 类会调用表模型的以下方法：

```java
void setValueAt(Object value, int r, int c)
```

你需要重写该方法以存储新值。value 参数是单元格编辑器返回的对象。如果你实现了单元格编辑器，你就知道从 getCellEditorValue 方法返回的对象的类型。对于 DefaultCellEditor，该值有三种可能：如果单元格编辑器是复选框，则它是 Boolean；如果是文本字段，则它是字符串；如果值来自组合框，则它是用户选中的对象。

如果 value 对象的类型不合适，你需要对其进行转换。最常见的情况是在文本字段中编辑数字时。在我们的示例中，我们用 Integer 对象填充组合框，因此无需转换。

#### 清单 11.4 `tableCellRender/TableCellRenderFrame.java`

```java
package tableCellRender;

import java.awt.*;
import javax.swing.*;
import javax.swing.table.*;

/**
 * This frame contains a table of planet data.
 */
public class TableCellRenderFrame extends JFrame
{
    private static final int DEFAULT_WIDTH = 600;
    private static final int DEFAULT_HEIGHT = 400;

    public TableCellRenderFrame()
    {
        setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);

        var model = new PlanetTableModel();
        var table = new JTable(model);
        table.setRowSelectionAllowed(false);

        // set up renderers and editors

        table.setDefaultRenderer(Color.class, new ColorTableCellRenderer());
        table.setDefaultEditor(Color.class, new ColorTableCellEditor());

        var moonCombo = new JComboBox<Integer>();
        for (int i = 0; i <= 20; i++)
            moonCombo.addItem(i);

        TableColumnModel columnModel = table.getColumnModel();
        TableColumn moonColumn = columnModel.getColumn(PlanetTableModel.MOONS_COLUMN);
        moonColumn.setCellEditor(new DefaultCellEditor(moonCombo));
        moonColumn.setHeaderRenderer(table.getDefaultRenderer(ImageIcon.class));
        moonColumn.setHeaderValue(new ImageIcon(getClass().getResource("Moons.gif")));

        // show table

        table.setRowHeight(100);
        add(new JScrollPane(table), BorderLayout.CENTER);
    }
}
```

#### 清单 11.5 tableCellRenderer/PlanetTableModel.java

```java
package tableCellRenderer;

import java.awt.*;
import javax.swing.*;
import javax.swing.table.*;

/**
 * The planet table model specifies the values, rendering and editing properties for the
 * planet data.
 */
public class PlanetTableModel extends AbstractTableModel
{
    public static final int PLANET_COLUMN = 0;
    public static final int MOONS_COLUMN = 2;
    public static final int GASEOUS_COLUMN = 3;
    public static final int COLOR_COLUMN = 4;

    private Object[][] cells =
    {
        { "Mercury", 2440.0, 0, false, Color.YELLOW,
          new ImageIcon(getClass().getResource("Mercury.gif")) },
        { "Venus", 6052.0, 0, false, Color.YELLOW,
          new ImageIcon(getClass().getResource("Venus.gif")) },
        { "Earth", 6378.0, 1, false, Color.BLUE,
          new ImageIcon(getClass().getResource("Earth.gif")) },
        { "Mars", 3397.0, 2, false, Color.RED,
          new ImageIcon(getClass().getResource("Mars.gif")) },
        { "Jupiter", 71492.0, 16, true, Color.ORANGE,
          new ImageIcon(getClass().getResource("Jupiter.gif")) },
        { "Saturn", 60268.0, 18, true, Color.ORANGE,
          new ImageIcon(getClass().getResource("Saturn.gif")) },
        { "Uranus", 25559.0, 17, true, Color.BLUE,
          new ImageIcon(getClass().getResource("Uranus.gif")) },
        { "Neptune", 24766.0, 8, true, Color.BLUE,
          new ImageIcon(getClass().getResource("Neptune.gif")) },
        { "Pluto", 1137.0, 1, false, Color.BLACK,
          new ImageIcon(getClass().getResource("Pluto.gif")) }
    };

    private String[] columnNames = { "Planet", "Radius", "Moons", "Gaseous",
                                     "Color", "Image" };

    public String getColumnName(int c)
    {
        return columnNames[c];
    }

48 public Class<?> getColumnClass(int c)
49 {
50     return cells[0][c].getClass();
51 }
52
53 public int getColumnCount()
54 {
55     return cells[0].length;
56 }
57
58 public int getRowCount()
59 {
60     return cells.length;
61 }
62
63 public Object getValueAt(int r, int c)
64 {
65     return cells[r][c];
66 }
67
68 public void setValueAt(Object obj, int r, int c)
69 {
70     cells[r][c] = obj;
71 }
72
73 public boolean isCellEditable(int r, int c)
74 {
75     return c == PLANET_COLUMN || c == MOONS_COLUMN || c == GASEOUS_COLUMN
76            || c == COLOR_COLUMN;
77 }
78 }
```

#### 清单 11.6 tableCellRenderer/ColorTableCellRenderer.java

```java
1 package tableCellRenderer;
2
3 import java.awt.*;
4 import javax.swing.*;
5 import javax.swing.table.*;
6
7 /**
8  * This renderer renders a color value as a panel with the given color.
9  */
10 public class ColorTableCellRenderer extends JPanel implements TableCellRenderer
11 {
```

#### 清单 11.7 *（续）*

```java
colorChooser.setColor((Color) value);
return panel;
}

public boolean shouldSelectCell(EventObject anEvent)
{
    // start editing
    colorDialog.setVisible(true);

    // tell caller it is ok to select this cell
    return true;
}

public void cancelCellEditing()
{
    // editing is canceled--hide dialog
    colorDialog.setVisible(false);
    super.cancelCellEditing();
}

public boolean stopCellEditing()
{
    // editing is complete--hide dialog
    colorDialog.setVisible(false);
    super.stopCellEditing();

    // tell caller it is ok to use color value
    return true;
}

public Object getCellEditorValue()
{
    return colorChooser.getColor();
}
```

| javax.swing.JTable 1.2 |
| --- |
| - `TableCellRenderer getDefaultRenderer(Class<?> type)`<br>获取给定类型的默认渲染器。 |
| - `TableCellEditor getDefaultEditor(Class<?> type)`<br>获取给定类型的默认编辑器。 |



| 成员/方法 | 说明 |
|---|---|
| `javax.swing.CellEditor` | 版本 `1.2` |
| `boolean isCellEditable(EventObject event)` | 如果该事件适合启动此单元格的编辑过程，则返回 true。 |
| `boolean shouldSelectCell(EventObject anEvent)` | 启动编辑过程。如果应选中被编辑的单元格，则返回 true。通常希望返回 true，但如果不希望编辑过程改变单元格选择，可以返回 false。 |
| `void cancelCellEditing()` | 取消编辑过程。可以放弃部分编辑。 |
| `boolean stopCellEditing()` | 停止编辑过程，意图使用编辑结果。如果编辑后的值处于可检索的正确状态，则返回 true。 |
| `Object getCellEditorValue()` | 返回编辑后的结果。 |
| `void addCellEditorListener(CellEditorListener l)` | 添加必需的单元格编辑器监听器。 |
| `void removeCellEditorListener(CellEditorListener l)` | 移除必需的单元格编辑器监听器。 |

## 11.2 树

每位使用过分层文件系统的计算机用户都见过树形显示。当然，目录和文件只是众多树状组织示例之一。许多树结构出现在日常生活中，例如图 11.11 所示的国家、州和城市的层级结构。

作为程序员，我们经常需要显示树结构。幸运的是，Swing 库为此提供了 `JTree` 类。`JTree` 类（及其辅助类）负责布置树，并处理用户展开和折叠节点的请求。在本节中，你将学习如何使用 `JTree` 类。

与其他复杂的 Swing 组件一样，我们必须关注常见且有用的情形，无法涵盖每个细节。如果你想实现某些不寻常的功能，我们建议查阅 David M. Geary 所著的 *Graphic Java™, 第三版* 或 Kim Topley 所著的 *Core Swing*。

在继续之前，我们先确定一些术语（见图 11.12）。树由节点组成。每个节点要么是叶节点，要么有子节点。除根节点外，每个节点恰好有一个父节点。一棵树恰好有一个根节点。有时你会有一组树，每棵树都有自己的根节点。这样的集合称为*森林*。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_675_0.png)

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_675_1.png)

### 11.2.1 简单的树

在第一个示例程序中，我们将简单地显示一棵包含几个节点的树（见图 11.14）。与许多其他 Swing 组件一样，你需要提供数据模型，组件会为你显示它。要构造 JTree，请在构造函数中提供树模型：

```
TreeModel model = . . . ;
var tree = new JTree(model);
```

> **注意：** 还有一些构造函数可以从元素集合构造树：
>
> ```java
> JTree(Object[] nodes)
> JTree(Vector<?> nodes)
> JTree(Hashtable<?, ?> nodes) // the values become the nodes
> ```
>
> 这些构造函数不太有用。它们只是构建一个由树组成的森林，每棵树只有一个节点。第三个构造函数似乎尤其无用，因为节点似乎以由键的哈希码决定的随机顺序出现。

如何获得树模型？你可以通过创建一个实现 TreeModel 接口的类来构造自己的模型。本章后面你将看到如何做到这一点。目前，我们将沿用 Swing 库提供的 DefaultTreeModel。

要构造默认树模型，必须提供根节点。

```
TreeNode root = . . . ;
var model = new DefaultTreeModel(root);
```

TreeNode 是另一个接口。用任何实现该接口的类的对象填充默认树模型。目前，我们将使用 Swing 提供的具体节点类——即 DefaultMutableTreeNode。该类实现 MutableTreeNode 接口，而该接口是 TreeNode 的子接口（见图 11.13）。

默认可变树节点包含一个对象——用户对象。树会为所有节点渲染用户对象。除非指定渲染器，否则树显示 toString 方法的结果字符串。

在第一个示例中，我们使用字符串作为用户对象。实践中，你通常会用更具表现力的用户对象填充树。例如，显示目录树时，为节点使用文件对象是合理的。

你可以在构造函数中指定用户对象，也可以稍后使用 setUserObject 方法设置它。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_677_0.png)

**图 11.13** 树类

```
var node = new DefaultMutableTreeNode("Texas");
. . .
node.setUserObject("California");
```

接下来，需要建立节点之间的父/子关系。从根节点开始，使用 add 方法添加子节点：

```
var root = new DefaultMutableTreeNode("World");
var country = new DefaultMutableTreeNode("USA");
root.add(country);
var state = new DefaultMutableTreeNode("California");
country.add(state);
```

图 11.14 展示了树的外观。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_678_0.png)

**图 11.14** 一棵简单的树

按这种方式连接所有节点。然后，用根节点构造 DefaultTreeModel。最后，用树模型构造 JTree。

```
var treeModel = new DefaultTreeModel(root);
var tree = new JTree(treeModel);
```

或者，作为一种快捷方式，你可以直接将根节点传给 JTree 构造函数。这样树会自动构造默认树模型：

```
var tree = new JTree(root);
```

清单 11.8 包含完整代码。

**清单 11.8** `tree/SimpleTreeFrame.java`

```java
package tree;

import javax.swing.*;
import javax.swing.tree.*;

/**
 * This frame contains a simple tree that displays a manually constructed tree model.
 */
public class SimpleTreeFrame extends JFrame
{
    private static final int DEFAULT_WIDTH = 300;
    private static final int DEFAULT_HEIGHT = 200;

    public SimpleTreeFrame()
    {
        setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);

        // set up tree model data

        var root = new DefaultMutableTreeNode("World");
        var country = new DefaultMutableTreeNode("USA");
        root.add(country);
        var state = new DefaultMutableTreeNode("California");
        country.add(state);
        var city = new DefaultMutableTreeNode("San Jose");
        state.add(city);
        city = new DefaultMutableTreeNode("Cupertino");
        state.add(city);
        state = new DefaultMutableTreeNode("Michigan");
        country.add(state);
        city = new DefaultMutableTreeNode("Ann Arbor");
        state.add(city);
        country = new DefaultMutableTreeNode("Germany");
        root.add(country);
        state = new DefaultMutableTreeNode("Schleswig-Holstein");
        country.add(state);
        city = new DefaultMutableTreeNode("Kiel");
        state.add(city);

        // construct tree and put it in a scroll pane

        var tree = new JTree(root);
        add(new JScrollPane(tree));
    }
}
```

运行程序时，树最初如图 11.15 所示。只有根节点及其子节点可见。单击圆形图标（即*控制柄*）以展开子树。当子树折叠时，从控制柄图标伸出的线指向右；当子树展开时，该线指向下（见图 11.16）。我们不知道 Metal 外观风格的设计者当时是怎么想的，但我们把这个图标看作门把手。向下按把手即可打开子树。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_679_0.png)

**图 11.15** 初始树显示

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_680_0.png)

**图 11.16** 折叠和展开的子树

> **注意：** 当然，树的显示取决于所选的外观风格。我们刚才描述的是 Metal 外观风格。在 Windows 外观风格中，控制柄具有更熟悉的外观——方框中的“−”或“+”（见图 11.17）。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_680_1.png)

**图 11.17** 采用 Windows 外观风格的树

你可以使用以下神奇咒语关闭连接父节点和子节点的线（见图 11.18）：

```java
tree.putClientProperty("JTree.lineStyle", "None");
```



![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_681_0.png)

**图 11.10** 没有连接线的树

反过来，要确保显示线条，请使用

```java
tree.putClientProperty("JTree.lineStyle", "Angled");
```

另一种线型“Horizontal”如图 11.19 所示。该树用水平线仅分隔根节点的子节点。我们不太确定它有什么用处。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_681_1.png)

**图 11.19** 使用水平线样式的树

默认情况下，没有用于折叠树根的控制柄。如果愿意，可以通过以下调用添加一个：

```java
tree.setShowsRootHandles(true);
```

图 11.20 显示了结果。现在可以将整棵树折叠到根节点中。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_682_0.png)

**图 11.20** 带根控制柄的树

反过来，你也可以完全隐藏根。这样将显示一个*森林*——一组树，每棵树都有自己的根。你仍然必须将森林中的所有树连接到一个公共根；然后，使用以下指令隐藏该根：

```java
tree.setRootVisible(false);
```

看看图 11.21。看起来有两个根，分别标记为“USA”和“Germany”。连接两者的实际根被设为不可见。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_682_1.png)

**图 11.21** 森林

让我们从树的根转向叶子。注意，叶子的图标与其他节点不同（见图 11.22）。

## 一瞬间的选择

我们在生活中会遇到无数个选择的瞬间。有些选择重大而重要，有些选择琐碎而轻微。然而，每一个选择都会一点一点地改变我们的人生。

一瞬间的选择有时甚至会改变人生的方向。我们做出的决定无法回到过去，因此必须更加慎重。但不必过于害怕，因为不存在完美的选择。

重要的不是选择本身，而是选择之后如何行动。如果做出了最好的选择，就要对结果负责；如果结果不好，就把它当作教训，朝着更好的方向前进。

> 每一个选择都有意义，每一个瞬间都有价值。

人生是选择的连续。我们通过这些选择成长、学习，并塑造更好的自己。不要忘记，今天的小选择会造就明天的大变化。

**javax.swing.tree.TreeModel** *1.2*

- `boolean isLeaf(Object node)`
  如果节点应显示为叶节点，则返回 true。

**javax.swing.tree.DefaultTreeModel** *1.2*

- `void setAsksAllowsChildren(boolean b)`
  如果 b 为 true，则当节点的 `getAllowsChildren` 方法返回 false 时，节点显示为叶节点。否则，当节点的 `isLeaf` 方法返回 true 时，节点显示为叶节点。

**javax.swing.tree.DefaultMutableTreeNode** *1.2*

- `DefaultMutableTreeNode(Object userObject)`
  使用给定的用户对象构造一个可变树节点。
- `void add(MutableTreeNode child)`
  将一个子节点添加为此节点的最后一个子节点。
- `void setAllowsChildren(boolean b)`
  如果 b 为 true，则可以向此节点添加子节点。

**javax.swing.JComponent** *1.2*

- `void putClientProperty(Object key, Object value)`
  向每个组件管理的小表中添加一个键/值对。这是一种“逃生舱口”机制，某些 Swing 组件用它来存储特定于外观的属性。

### 11.2.2 编辑树和树路径

在下一个示例程序中，你将看到如何编辑树。图 11.23 显示了用户界面。如果单击 Add Sibling 或 Add Child 按钮，程序会向树中添加一个新节点（标题为 New）。如果单击 Delete 按钮，程序会删除当前选中的节点。

要实现此行为，你需要找出当前选中的是哪个树节点。JTree 类识别树中节点的方式令人惊讶。它不处理树节点，而是处理*对象路径*，称为树路径。一个

自动通知是使用 `DefaultTreeModel` 的一大优势。如果提供自己的树模型，就必须手动实现自动通知。（详情见 Kim Topley 的 *Core Swing*。）

> **注意：** `DefaultTreeModel` 类有一个 reload 方法，可重新加载整个模型。但是，不要仅仅为了在做出少量更改后更新树而调用 reload。当树重新生成时，根节点的子节点之外的所有节点都会再次折叠。如果用户每次更改后都必须不断展开树，他们会感到相当不安。

当视图收到节点结构发生更改的通知时，它会更新显示，但不会自动展开节点以显示新添加的子节点。特别是，如果示例程序中的用户向当前折叠了子节点的节点添加新的子节点，新节点会被静默添加到折叠的子树中。这不会给用户任何反馈，表明命令实际上已执行。在这种情况下，你应特意展开所有父节点，使新添加的节点可见。为此，请使用 `JTree` 类的 `makeVisible` 方法。`makeVisible` 方法需要一个指向应变为可见节点的树路径。

因此，需要构造一条从根到新插入节点的树路径。要获得树路径，首先调用 `DefaultTreeModel` 类的 `getPathToRoot` 方法。它返回一个 `TreeNode[]` 数组，包含从某个节点到根节点的所有节点。将该数组传递给 `TreePath` 构造函数。

例如，下面展示了如何使新节点可见：

```java
TreeNode[] nodes = model.getPathToRoot(newNode);
var path = new TreePath(nodes);
tree.makeVisible(path);
```

> **注意：** 奇怪的是，`DefaultTreeModel` 类几乎完全假装不了解 `TreePath` 类，尽管它的职责是与 `JTree` 通信。`JTree` 类大量使用树路径，而从不使用节点对象数组。

现在，假设你的树包含在滚动窗格中。展开树节点后，新节点可能仍然不可见，因为它落在视口之外。要解决该问题，请调用

```java
tree.scrollPathToVisible(path);
```

而不是调用 `makeVisible`。此调用会展开路径上的所有节点，并告诉所在的滚动窗格将路径末端的节点滚动到视图中（见图 11.25）。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_689_0.png)

**图 11.25** 滚动窗格滚动以显示新节点。

默认情况下，树节点不可编辑。但是，如果你调用

```java
tree.setEditable(true);
```

用户只需双击、编辑字符串并按 Enter 键，即可编辑节点。双击会调用*默认单元格编辑器*，它由 `DefaultCellEditor` 类实现（见图 11.26）。也可以安装其他单元格编辑器，使用与我们在讨论表格单元格编辑器时看到的相同过程。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_689_1.png)

**图 11.26** 默认单元格编辑器

清单 11.9 显示了树编辑程序的完整源代码。运行该程序，添加几个节点，并通过双击编辑它们。观察折叠的节点如何展开以显示添加的子节点，以及滚动窗格如何将添加的节点保持在视口中。

#### 清单 11.9 treeEdit/TreeEditFrame.java

```java
package treeEdit;

import java.awt.*;
import javax.swing.*;
import javax.swing.tree.*;

/**
 * A frame with a tree and buttons to edit the tree.
 */
public class TreeEditFrame extends JFrame
{
   private static final int DEFAULT_WIDTH = 400;
   private static final int DEFAULT_HEIGHT = 200;

   private DefaultTreeModel model;
   private JTree tree;

   public TreeEditFrame()
   {
      setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);

      // construct tree

      TreeNode root = makeSampleTree();
      model = new DefaultTreeModel(root);
      tree = new JTree(model);
      tree.setEditable(true);

      // add scroll pane with tree

      var scrollPane = new JScrollPane(tree);
      add(scrollPane, BorderLayout.CENTER);

      makeButtons();
   }

   public TreeNode makeSampleTree()
   {
      var root = new DefaultMutableTreeNode("World");
      var country = new DefaultMutableTreeNode("USA");
      root.add(country);
      var state = new DefaultMutableTreeNode("California");
```



#### 清单 11.9 *（续）*

```java
addChildButton.addActionListener(event ->
{
    var selectedNode = (DefaultMutableTreeNode) tree.getLastSelectedPathComponent();

    if (selectedNode == null) return;

    var newNode = new DefaultMutableTreeNode("New");
    model.insertNodeInto(newNode, selectedNode, selectedNode.getChildCount());

    // now display new node

    TreeNode[] nodes = model.getPathToRoot(newNode);
    var path = new TreePath(nodes);
    tree.scrollPathToVisible(path);
});
panel.add(addChildButton);

var deleteButton = new JButton("Delete");
deleteButton.addActionListener(event ->
{
    var selectedNode = (DefaultMutableTreeNode) tree.getLastSelectedPathComponent();

    if (selectedNode != null && selectedNode.getParent() != null) model
        .removeNodeFromParent(selectedNode);
});
panel.add(deleteButton);
add(panel, BorderLayout.SOUTH);
}
```

**javax.swing.JTree 1.2**

- `TreePath getSelectionPath()`  
  获取当前所选节点的路径；如果选择了多个节点，则获取第一个所选节点的路径。如果没有选中任何节点，则返回 null。
- `Object getLastSelectedPathComponent()`  
  获取表示当前所选节点的节点对象；如果选择了多个节点，则获取第一个节点。如果没有选中任何节点，则返回 null。
- `void makeVisible(TreePath path)`  
  展开该路径上的所有节点。
- `void scrollPathToVisible(TreePath path)`  
  展开该路径上的所有节点，并且如果树位于滚动窗格中，则滚动以确保该路径上的最后一个节点可见。

**javax.swing.tree.TreePath** 1.2

- `Object getLastPathComponent()`  
  获取此路径上的最后一个对象——也就是该路径所表示的节点对象。

**javax.swing.tree.TreeNode** 1.2

- `TreeNode getParent()`  
  返回此节点的父节点。
- `TreeNode getChildAt(int index)`  
  查找给定索引处的子节点。索引必须介于 0 和 `getChildCount() − 1` 之间。
- `int getChildCount()`  
  返回此节点的子节点数量。
- `Enumeration children()`  
  返回一个枚举对象，用于遍历此节点的所有子节点。

**javax.swing.tree.DefaultTreeModel** 1.2

- `void insertNodeInto(MutableTreeNode newChild, MutableTreeNode parent, int index)`  
  将 newChild 作为 parent 的新子节点插入到给定索引处，并通知树模型监听器。
- `void removeNodeFromParent(MutableTreeNode node)`  
  从该模型中移除 node，并通知树模型监听器。
- `void nodeChanged(TreeNode node)`  
  通知树模型监听器 node 已更改。
- `void nodesChanged(TreeNode parent, int[] changedChildIndices)`  
  通知树模型监听器：parent 中具有给定索引的所有子节点均已更改。
- `void reload()`  
  将所有节点重新加载到模型中。这是一个剧烈的操作，只有在节点因某些外部影响而完全改变时才应使用。

### 11.2.3 节点枚举

有时，你需要从根节点开始遍历树中的所有子节点，直到找到匹配项，以此在树中查找节点。`DefaultMutableTreeNode` 类提供了几个用于遍历节点的便捷方法。

`breadthFirstEnumeration` 和 `depthFirstEnumeration` 方法返回枚举对象，其 `nextElement` 方法会使用广度优先或深度优先遍历来访问当前节点的所有子节点。图 11.27 展示了一棵示例树的遍历过程——节点标签表示节点的遍历顺序。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_694_0.png)

**图 11.27** 树的遍历顺序

广度优先枚举最容易可视化。树按层遍历。首先访问根节点，然后是其所有子节点，接着是孙节点，依此类推。

要直观理解深度优先枚举，可以想象一只老鼠被困在树形迷宫中。它沿着第一条路径一路冲到叶子节点，然后回溯，转向下一条路径，依此类推。

计算机科学家也称其为后序遍历，因为搜索过程先访问子节点，再访问父节点。`postOrderEnumeration` 方法是 `depthFirstEnumeration` 的同义词。为完整起见，还有一个 `preOrderEnumeration`，它是一种先枚举父节点再枚举子节点的深度优先搜索。

下面是典型用法模式：

```
Enumeration breadthFirst = node.breadthFirstEnumeration();
while (breadthFirst.hasMoreElements())
    do something with breadthFirst.nextElement();
```

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_695_0.png)

图 11.28  继承树

最后，一个相关方法 `pathFromAncestorEnumeration` 会查找从某个祖先节点到给定节点的路径，并枚举该路径上的节点。这没什么复杂的——它只是不断调用 `getParent` 直到找到祖先节点，然后按相反顺序呈现该路径。

在下一个示例程序中，我们将节点枚举付诸实践。该程序显示类的继承树。在框架底部的文本字段中输入类名。该类及其所有超类都会被添加到树中（参见图 11.28）。

在这个示例中，我们利用了树节点的用户对象可以是任意类型对象这一特性。由于我们的节点描述的是类，因此我们在节点中存储类对象。

我们不希望同一个类对象被添加两次，因此需要检查树中是否已存在某个类。如果树中存在具有给定用户对象的节点，下面的方法会找到该节点：

```
public DefaultMutableTreeNode findUserObject(Object obj)
{
    Enumeration e = root.breadthFirstEnumeration();
    while (e.hasMoreElements())
    {
        DefaultMutableTreeNode node = (DefaultMutableTreeNode) e.nextElement();
        if (node.getUserObject().equals(obj))
            return node;
    }
    return null;
}
```

### 11.2.4 渲染节点

在应用程序中，你经常需要改变树组件绘制节点的方式。最常见的更改当然是为节点和叶子节点选择不同的图标。其他更改可能包括更改节点标签的字体或在节点处绘制图像。通过向树中安装新的树单元格渲染器，所有这些更改都可以实现。默认情况下，`JTree` 类使用 `DefaultTreeCellRenderer` 对象绘制每个节点。`DefaultTreeCellRenderer` 类扩展了 `JLabel` 类。该标签包含节点图标和节点标签。

> **注意：** 单元格渲染器不绘制用于展开和折叠子树的“手柄”。这些手柄是外观风格的一部分，建议不要更改它们。

可以通过三种方式自定义显示。

- 可以更改 `DefaultTreeCellRenderer` 使用的图标、字体和背景色。这些设置会用于树中的所有节点。
- 可以安装一个扩展 `DefaultTreeCellRenderer` 类的渲染器，并为每个节点设置不同的图标、字体和背景色。
- 可以安装一个实现 `TreeCellRenderer` 接口的渲染器，为每个节点绘制自定义图像。

让我们逐一了解这些可能性。最简单的自定义方式是构造一个 `DefaultTreeCellRenderer` 对象，更改图标，然后将其安装到树中：

```
var renderer = new DefaultTreeCellRenderer();
renderer.setLeafIcon(new ImageIcon("blue-ball.gif")); // used for leaf nodes
renderer.setClosedIcon(new ImageIcon("red-ball.gif")); // used for collapsed nodes
renderer.setOpenIcon(new ImageIcon("yellow-ball.gif")); // used for expanded nodes
tree.setCellRenderer(renderer);
```

你可以在图 11.28 中看到效果。我们只是使用“球”图标作为占位符——想必你的用户界面设计人员会为你提供适合应用程序使用的图标。

我们不建议更改整棵树的字体或背景色——那实际上是外观风格的职责。

不过，更改树中某些节点的字体以突出显示它们可能很有用。如果仔细观察图 11.28，你会注意到*抽象*类以斜体显示。




若要改变单个节点的外观，可以安装一个树单元格渲染器。树单元格渲染器与我们本章前面讨论的列表单元格渲染器非常相似。`TreeCellRenderer` 接口只有一个方法：

```java
Component getTreeCellRendererComponent(JTree tree, Object value, boolean selected,
    boolean expanded, boolean leaf, int row, boolean hasFocus)
```

`DefaultTreeCellRenderer` 类的 `getTreeCellRendererComponent` 方法返回 `this`——换句话说，返回一个标签。（`DefaultTreeCellRenderer` 类继承自 `JLabel` 类。）要定制该组件，需要继承 `DefaultTreeCellRenderer` 类。并按如下方式重写 `getTreeCellRendererComponent` 方法：先调用父类方法，以便其准备标签数据；然后定制标签属性；最后返回 `this`。

```java
class MyTreeCellRenderer extends DefaultTreeCellRenderer
{
    public Component getTreeCellRendererComponent(JTree tree, Object value, boolean selected,
            boolean expanded, boolean leaf, int row, boolean hasFocus)
    {
        Component comp = super.getTreeCellRendererComponent(tree, value, selected,
                expanded, leaf, row, hasFocus);
        DefaultMutableTreeNode node = (DefaultMutableTreeNode) value;
        look at node.getUserObject();
        Font font = appropriate font;
        comp.setFont(font);
        return comp;
    }
}
```

> **警告：** `getTreeCellRendererComponent` 方法的 `value` 参数是节点对象，而不是用户对象！请回顾，用户对象是 `DefaultMutableTreeNode` 的一个特性，而 `JTree` 可以包含任意类型的节点。如果你的树使用 `DefaultMutableTreeNode` 节点，则必须像前面代码示例中那样，在第二步中获取用户对象。

> **警告：** `DefaultTreeCellRenderer` 对所有节点使用*同一个*标签对象，只是针对每个节点更改标签文本。如果你为某个特定节点更改了字体，那么当方法再次被调用时，你必须将其恢复为默认值。否则，所有后续节点都会以更改后的字体绘制！请查看清单 11.10 中的代码，了解如何将字体恢复为默认值。

清单 11.10 中的 `ClassNameTreeCellRenderer` 根据 `Class` 对象的 `ABSTRACT` 修饰符，将类名设置为普通字体或斜体字体。我们不想设置特定字体，因为我们不想改变外观（look-and-feel）通常用于标签的任何字体。因此，我们使用标签中的字体，并从中*派生出*斜体字体。请回顾，所有调用只返回一个共享的 `JLabel` 对象。我们需要保留原始字体，并在下一次调用 `getTreeCellRendererComponent` 方法时将其恢复。

此外，请注意我们如何在 `ClassTreeFrame` 构造函数中更改节点图标。

#### `javax.swing.tree.DefaultMutableTreeNode` 1.2

- `Enumeration breadthFirstEnumeration()`
- `Enumeration depthFirstEnumeration()`
- `Enumeration preOrderEnumeration()`
- `Enumeration postOrderEnumeration()`

返回枚举对象，用于按特定顺序访问树模型中的所有节点。在广度优先遍历中，离根较近的子节点会在较远的子节点之前被访问。在深度优先遍历中，一个节点的所有子节点会先于其兄弟节点被完整枚举。`postOrderEnumeration` 方法是 `depthFirstEnumeration` 的同义词。前序遍历与后序遍历相同，只是父节点先于其子节点被枚举。

#### `javax.swing.tree.TreeCellRenderer` 1.2

- `Component getTreeCellRendererComponent(JTree tree, Object value, boolean selected, boolean expanded, boolean leaf, int row, boolean hasFocus)`

返回一个组件，其 `paint` 方法被调用来渲染一个树单元格。

**参数：**

| 参数 | 描述 |
| --- | --- |
| tree | 包含要渲染节点的树 |
| value | 要渲染的节点 |
| selected | 如果节点当前被选中，则为 true |
| expanded | 如果节点的子节点可见，则为 true |
| leaf | 如果节点需要显示为叶节点，则为 true |
| row | 包含节点的显示行 |
| hasFocus | 如果节点当前具有输入焦点，则为 true |

#### `javax.swing.tree.DefaultTreeCellRenderer` 1.2

- `void setLeafIcon(Icon icon)`
- `void setOpenIcon(Icon icon)`
- `void setClosedIcon(Icon icon)`

设置要显示的叶节点、展开节点和折叠节点的图标。

### 11.2.5 监听树事件

最常见的是，树组件与某个其他组件配对使用。当用户选择树节点时，一些信息会显示在另一个窗口中。参见图 11.29 中的示例。当用户选择一个类时，该类的实例变量和静态变量会显示在右侧的文本区域中。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_699_0.png)

**图 11.29** 一个类浏览器

若要获得此行为，你需要安装一个*树选择监听器*。该监听器必须实现 `TreeSelectionListener` 接口——一个只有一个方法的接口：

```java
void valueChanged(TreeSelectionEvent event)
```

每当用户选择或取消选择树节点时，都会调用该方法。

以常规方式将监听器添加到树中：

```java
tree.addTreeSelectionListener(listener);
```

你可以指定允许用户选择单个节点、连续节点范围，还是任意（可能不连续）的节点集。`JTree` 类使用 `TreeSelectionModel` 来管理节点选择。你需要获取该模型，以将选择状态设置为 `SINGLE_TREE_SELECTION`、`CONTIGUOUS_TREE_SELECTION` 或 `DISCONTIGUOUS_TREE_SELECTION` 之一。（不连续选择模式是默认设置。）例如，在我们的类浏览器中，我们希望只允许选择单个类：

当你选择一个树节点时，右侧的文本区域会填充所选类的字段。在框架构造函数中，我们将用户限制为单项选择，并添加一个树选择监听器。当调用 `valueChanged` 方法时，我们忽略其事件参数，而只是向树询问当前的选择路径。与往常一样，我们需要获取路径的最后一个节点，并查找其用户对象。然后我们调用 `getFieldDescription` 方法，该方法使用反射来组装一个包含所选类所有字段的字符串。

#### 清单 11.10 `treeRender/ClassTreeFrame.java`

```java
package treeRender;

import java.awt.*;
import java.awt.event.*;
import java.lang.reflect.*;
import java.util.*;

import javax.swing.*;
import javax.swing.tree.*;

/**
 * This frame displays the class tree, a text field, and an "Add" button to add more classes
 * into the tree.
 */
public class ClassTreeFrame extends JFrame
{
    private static final int DEFAULT_WIDTH = 400;
    private static final int DEFAULT_HEIGHT = 300;

    private DefaultMutableTreeNode root;
    private DefaultTreeModel model;
    private JTree tree;
    private JTextField textField;
    private JTextArea textArea;

    public ClassTreeFrame()
    {
        setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);

        // the root of the class tree is Object
        root = new DefaultMutableTreeNode(java.lang.Object.class);
        model = new DefaultTreeModel(root);
        tree = new JTree(model);

        // add this class to populate the tree with some data
        addClass(getClass());
    }
}
```

（续）

#### 清单 11.10 （续）

```java
38  // set up node icons
39  var renderer = new ClassNameTreeCellRenderer();
40  renderer.setClosedIcon(new ImageIcon(getClass().getResource("red-ball.gif")));
41  renderer.setOpenIcon(new ImageIcon(getClass().getResource("yellow-ball.gif")));
42  renderer.setLeafIcon(new ImageIcon(getClass().getResource("blue-ball.gif")));
43  tree.setCellRenderer(renderer);
44
45  // set up selection mode
46  tree.addTreeSelectionListener(event ->
47  {
48      // the user selected a different node--update description
49      TreePath path = tree.getSelectionPath();
50      if (path == null) return;
51      var selectedNode = (DefaultMutableTreeNode) path.getLastPathComponent();
52      Class<?> c = (Class<?>) selectedNode.getUserObject();
53      String description = getFieldDescription(c);
54      textArea.setText(description);
55  });
56  int mode = TreeSelectionModel.SINGLE_TREE_SELECTION;
57  tree.getSelectionModel().setSelectionMode(mode);
58
59  // this text area holds the class description
60  textArea = new JTextArea();
61
62  // add tree and text area
63  var panel = new JPanel();
64  panel.setLayout(new GridLayout(1, 2));
65  panel.add(new JScrollPane(tree));
66  panel.add(new JScrollPane(textArea));
67
68  add(panel, BorderLayout.CENTER);
69
70  addTextField();
71  }
72
73  /**
74   * Add the text field and "Add" button to add a new class.
75   */
76  public void addTextField()
77  {
78      var panel = new JPanel();
79
80      ActionListener addListener = event ->
81      {
82          // add the class whose name is in the text field
83          try
84          {
```




#### 清单 11.10 *(续)*

```java
// skip non-class types
if (c.isInterface() || c.isPrimitive()) return null;

// if the class is already in the tree, return its node
DefaultMutableTreeNode node = findUserObject(c);
if (node != null) return node;

// class isn't present--first add class parent recursively

Class<?> s = c.getSuperclass();

DefaultMutableTreeNode parent;
if (s == null) parent = root;
else parent = addClass(s);

// add the class as a child to the parent
var newNode = new DefaultMutableTreeNode(c);
model.insertNodeInto(newNode, parent, parent.getChildCount());

// make node visible
var path = new TreePath(model.getPathToRoot(newNode));
tree.makeVisible(path);

return newNode;
}

/**
 * Returns a description of the fields of a class.
 * @param c the class to be described
 * @return a string containing all field types and names
 */
public static String getFieldDescription(Class<?> c)
{
    // use reflection to find types and names of fields
    var r = new StringBuilder();
    Field[] fields = c.getDeclaredFields();
    for (int i = 0; i < fields.length; i++)
    {
        Field f = fields[i];
        if ((f.getModifiers() & Modifier.STATIC) != 0) r.append("static ");
        r.append(f.getType().getName());
        r.append(" ");
        r.append(f.getName());
        r.append("\n");
    }
    return r.toString();
}
}
```

| `javax.swing.event.TreeSelectionListener` | 1.2 |
|---|---|
| • `void valueChanged(TreeSelectionEvent event)`<br>每当选择或取消选择节点时调用。 | |

| `javax.swing.event.TreeSelectionEvent` | 1.2 |
|---|---|
| • `TreePath getPath()`<br>• `TreePath[] getPaths()`<br>获取此选择事件中*发生变化*的第一个路径或所有路径。如果你想了解当前选择，而不是选择变化，请改为调用 `JTree.getSelectionPaths`。 | |

### 11.2.6 自定义树模型

在最后一个示例中，我们实现了一个检查对象内容的程序，就像调试器所做的那样（见图 11.30）。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_706_0.png)

**图 11.30** 对象检查树

在继续之前，请编译并运行示例程序。每个节点对应一个实例字段。如果该字段是一个对象，请展开它以查看其实例字段。该程序检查框架窗口的内容。如果你随便查看几个实例字段，应该能够找到一些

TreeModelEvent 对象描述变化的位置。组装描述插入或移除事件的树模型事件的细节相当技术化。只有当你的树实际上可以添加和移除节点时，你才需要担心触发这些事件。在清单 11.12 中，我们展示了如何通过用新对象替换根来触发一个事件。

> **提示：** 为了简化事件触发的代码，请使用收集监听器的 `javax.swing.event.EventListenerList` 便捷类。清单 11.13 的最后三个方法展示了如何使用该类。

最后，如果用户编辑树节点，你的模型会以该变化为参数被调用：

```java
    void valueForPathChanged(TreePath path, Object newValue)
```

如果你不允许编辑，则永远不会调用此方法。

如果你不需要支持编辑，构造树模型很容易完成。实现以下三个方法：

```java
    Object getRoot()
    int getChildCount(Object parent)
    Object getChild(Object parent, int index)
```

这些方法描述树的结构。为其他五个方法提供常规实现，如清单 11.12 所示。然后你就可以显示你的树了。

现在让我们转向示例程序的实现。我们的树将包含 Variable 类型的对象。

> **注意：** 如果我们使用了 `DefaultTreeModel`，我们的节点就会是 `DefaultMutableTreeNode` 类型的对象，其用户对象类型为 `Variable`。

例如，假设你检查变量

```java
    Employee joe;
```

该变量具有类型 Employee.class、名称“joe”和一个值——即对象引用 joe 的值。在清单 11.14 中，我们定义了一个描述程序中变量的 Variable 类：

```java
    var v = new Variable(Employee.class, "joe", joe);
```

如果变量的类型是基本类型，则必须为值使用对象包装器。

```java
return null;
}
}
```

这三个方法向 JTree 组件揭示对象树的结构。其余方法是常规的——参见清单 11.13 中的源代码。

关于这个树模型有一个显著的事实：它实际上描述了一棵*无限*树。你可以通过跟踪其中一个 *WeakReference* 对象来验证这一点。单击名为 `referent` 的变量。它会直接把你带回原始对象。你会得到一个完全相同的子树，并且可以再次打开它的 *WeakReference* 对象，如此无限重复。当然，你无法存储无限多的节点；树模型只会在用户展开父节点时按需生成节点。清单 11.12 展示了示例程序的框架类。

#### 清单 11.12 `treeModel/ObjectInspectorFrame.java`

```java
package treeModel;

import java.awt.*;
import javax.swing.*;

/**
 * This frame holds the object tree.
 */
public class ObjectInspectorFrame extends JFrame
{
   private JTree tree;
   private static final int DEFAULT_WIDTH = 400;
   private static final int DEFAULT_HEIGHT = 300;

   public ObjectInspectorFrame()
   {
      setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);

      // we inspect this frame object

      var v = new Variable(getClass(), "this", this);
      var model = new ObjectTreeModel();
      model.setRoot(v);

      // construct and show tree

      tree = new JTree(model);
      add(new JScrollPane(tree), BorderLayout.CENTER);
   }
}
```

#### 清单 11.13 `treeModel/ObjectTreeModel.java`

```java
package treeModel;

import java.lang.reflect.*;
import java.util.*;
import javax.swing.event.*;
import javax.swing.tree.*;

/**
 * This tree model describes the tree structure of a Java object. Children are the objects
 * that are stored in instance variables.
 */
public class ObjectTreeModel implements TreeModel
{
   private Variable root;
   private EventListenerList listenerList = new EventListenerList();

   /**
    * Constructs an empty tree.
    */
   public ObjectTreeModel()
   {
      root = null;
   }

   /**
    * Sets the root to a given variable.
    * @param v the variable that is described by this tree
    */
   public void setRoot(Variable v)
   {
      Variable oldRoot = root;
      root = v;
      fireTreeStructureChanged(oldRoot);
   }

   public Object getRoot()
   {
      return root;
   }

   public int getChildCount(Object parent)
   {
      return ((Variable) parent).getFields().size();
   }

   public Object getChild(Object parent, int index)
   {
```

#### 清单 11.14 *(续)*

```java
48 /**
49  * Gets the value of this variable.
50  * @return the value
51  */
52 public Object getValue()
53 {
54     return value;
55 }
56 
57 /**
58  * Gets all nonstatic fields of this variable.
59  * @return an array list of variables describing the fields
60  */
61 public ArrayList<Field> getFields()
62 {
63     return fields;
64 }
65 
66 public String toString()
67 {
68     String r = type + " " + name;
69     if (type.isPrimitive()) r += "=" + value;
70     else if (type.equals(String.class)) r += "=" + value;
71     else if (value == null) r += "=null";
72     return r;
73 }
74 }
```

#### `javax.swing.tree.TreeModel` 1.2

- `Object getRoot()`  
  返回根节点。
- `int getChildCount(Object parent)`  
  获取父节点的子节点数量。
- `Object getChild(Object parent, int index)`  
  获取给定索引处父节点的子节点。
- `int getIndexOfChild(Object parent, Object child)`  
  获取子节点在父节点中的索引；如果 child 在此树模型中不是 parent 的子节点，则返回 -1。





**`javax.swing.tree.TreeModel` 1.2（续）**

| 方法 | 描述 |
| --- | --- |
| `boolean isLeaf(Object node)` | 如果节点在概念上是树的叶子，则返回 true。 |
| `void addTreeModelListener(TreeModelListener l)`<br>`void removeTreeModelListener(TreeModelListener l)` | 添加或移除监听器，当树模型中的信息发生变化时会通知这些监听器。 |
| `void valueForPathChanged(TreePath path, Object newValue)` | 当单元格编辑器修改了节点的值时调用。<br>*参数：* `path` 已被编辑的节点的路径；`newValue` 编辑器返回的替换值。 |

**`javax.swing.event.TreeModelListener` 1.2**

| 方法 | 描述 |
| --- | --- |
| `void treeNodesChanged(TreeModelEvent e)`<br>`void treeNodesInserted(TreeModelEvent e)`<br>`void treeNodesRemoved(TreeModelEvent e)`<br>`void treeStructureChanged(TreeModelEvent e)` | 当树已被修改时由树模型调用。 |

**`javax.swing.event.TreeModelEvent` 1.2**

| 方法 | 描述 |
| --- | --- |
| `TreeModelEvent(Object eventSource, TreePath node)` | 构造一个树模型事件。<br>*参数：* `eventSource` 生成此事件的树模型；`node` 正在被更改的节点的路径。 |

## 11.3 高级 AWT

你可以使用 `Graphics` 类的方法创建简单绘图。这些方法对于简单应用已经足够，但当需要创建复杂形状或需要完全控制图形外观时，它们就不够用了。Java 2D API 是一个更复杂的类库，可用于生成高质量绘图。在以下各节中，我们将概述该 API。

### 11.3.1 渲染管线

最初的 JDK 1.0 有一种非常简单的绘制形状机制。你选择颜色和绘制模式，然后调用 `Graphics` 类的方法，例如 `drawRect` 或 `fillOval`。Java 2D API 支持更多选项。

- 你可以轻松生成各种各样的*形状*。
- 你可以控制*描边*——描绘形状边界的笔。
- 你可以用纯色、变化的色调和重复图案*填充*形状。
- 你可以使用*变换*来移动、缩放、旋转或拉伸形状。
- 你可以*裁剪*形状，将其限制在任意区域内。
- 你可以选择*合成规则*，描述如何将新形状的像素与现有像素组合。

要绘制形状，请执行以下步骤：

1. 获取 `Graphics2D` 类的对象。该类是 `Graphics` 类的子类。从 Java SE 1.2 起，`paint` 和 `paintComponent` 等方法会自动接收 `Graphics2D` 类的对象。只需按如下方式使用强制转换：

   ```
   public void paintComponent(Graphics g)
   {
       var g2 = (Graphics2D) g;
       . . . .
   }
   ```

2. 使用 `setRenderingHints` 方法设置*渲染提示*——在速度与绘图质量之间的权衡。

   ```
   RenderingHints hints = . . .;
   g2.setRenderingHints(hints);
   ```

3. 使用 `setStroke` 方法设置*描边*。描边绘制形状的轮廓。你可以选择粗细，并在实线和虚线之间选择。

   ```
   Stroke stroke = . . .;
   g2.setStroke(stroke);
   ```

4. 使用 `setPaint` 方法设置*绘图*。绘图填充诸如描边或形状内部等区域。你可以创建纯色绘图、色调变化的绘图或平铺填充图案。

   ```
   Paint paint = . . .;
   g2.setPaint(paint);
   ```

5. 使用 `clip` 方法设置*裁剪区域*。

   ```
   Shape clip = . . .;
   g2.clip(clip);
   ```

6. 使用 `transform` 方法设置从用户空间到设备空间的*变换*。如果使用自定义坐标系定义形状比使用像素坐标更方便，就使用变换。

   ```
   AffineTransform transform = . . .;
   g2.transform(transform);
   ```

7. 使用 `setComposite` 方法设置*合成规则*，该规则描述如何将新像素与现有像素组合。

   ```
   Composite composite = . . .;
   g2.setComposite(composite);
   ```

8. 创建形状。Java 2D API 提供了许多形状对象和用于组合形状的方法。

   ```
   Shape shape = . . .;
   ```

9. 绘制或填充形状。如果绘制形状，则对其轮廓进行描边。如果填充形状，则对其内部进行绘制。

   ```
   g2.draw(shape);
   g2.fill(shape);
   ```

当然，在许多实际情况下，你不需要所有这些步骤。2D 图形上下文的设置都有合理的默认值；只有当你想要偏离默认值时，才需要更改设置。

在以下各节中，你将看到如何描述形状、描边、绘图、变换和合成规则。

各种 set 方法只是设置 2D 图形上下文的状态。它们不会引起任何绘制。同样，当你构造 `Shape` 对象时，也不会进行绘制。只有当你调用 `draw` 或 `fill` 时，才会渲染形状。此时，新形状会在*渲染管线*中计算（参见图 11.31）。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_718_0.png)

**图 11.31** 渲染管线

在渲染管线中，渲染形状要经过以下步骤：

1. 对形状的路径进行描边。
2. 对形状进行变换。
3. 对形状进行裁剪。如果形状与裁剪区域没有交集，则过程停止。
4. 填充裁剪后形状的剩余部分。
5. 将填充后形状的像素与现有像素合成。（在图 11.31 中，圆形是现有像素的一部分，而杯子形状叠加在其上。）

在下一节中，你将看到如何定义形状。然后，我们将转向 2D 图形上下文设置。

**`java.awt.Graphics2D` 1.2**

| 方法 | 描述 |
| --- | --- |
| `void draw(Shape s)` | 使用当前绘图绘制给定形状的轮廓。 |
| `void fill(Shape s)` | 使用当前绘图填充给定形状的内部。 |

### 11.3.2 形状

以下是 `Graphics` 类中用于绘制形状的一些方法：

```
drawLine
drawRect
drawRoundRect
draw3DRect
drawPolygon
drawPolyline
drawOval
drawArc
```

也有相应的填充方法。自 JDK 1.0 起，这些方法就一直存在于 `Graphics` 类中。Java 2D API 使用一种完全不同的、面向对象的方法。它不使用方法，而是使用类：

- `Line2D`
- `Rectangle2D`
- `RoundRectangle2D`
- `Ellipse2D`
- `Arc2D`
- `QuadCurve2D`
- `CubicCurve2D`
- `GeneralPath`

这些类都实现了 `Shape` 接口，我们将在以下各节中考察该接口。

#### 11.3.2.1 Shape 类层次结构

`Line2D`、`Rectangle2D`、`RoundRectangle2D`、`Ellipse2D` 和 `Arc2D` 类分别对应于 `drawLine`、`drawRect`、`drawRoundRect`、`drawOval` 和 `drawArc` 方法。（“3D 矩形”这一概念已经消亡，这是它完全应得的下场——没有与 `draw3DRect` 方法对应的方法。）Java 2D API 还提供了两个额外的类：二次曲线和三次曲线，我们将在本节中讨论。没有 `Polygon2D` 类；取而代之的是，`GeneralPath` 类描述由直线、二次曲线和三次曲线构成的路径。你可以使用 `GeneralPath` 描述多边形；我们将在本节后面向你展示如何操作。

要绘制形状，首先创建实现 `Shape` 接口的类的对象，然后调用 `Graphics2D` 类的 `draw` 方法。

这些类

- `Rectangle2D`
- `RoundRectangle2D`
- `Ellipse2D`
- `Arc2D`

都继承自一个共同的超类 `RectangularShape`。诚然，椭圆和弧不是矩形的，但它们有一个边界矩形（参见图 11.32）。

每个名称以“2D”结尾的类都有两个子类，用于将坐标指定为 float 或 double 量。在第 I 卷中，你已经遇到过 `Rectangle2D.Float` 和 `Rectangle2D.Double`。

其他类也使用相同的方案，例如 `Arc2D.Float` 和 `Arc2D.Double`。





![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_720_0.png)

**图 11.32** 椭圆和弧的边界矩形

在内部，所有图形类都使用 float 坐标，因为 float 数占用的存储空间更少，但对于几何计算具有足够的精度。然而，Java 编程语言使操作 float 数有点繁琐。因此，图形类的大多数方法使用 double 参数并返回 double 值。只有在构造 2D 对象时，才需要在带 float 和 double 坐标的构造器之间进行选择。例如，

```
var floatRect = new Rectangle2D.Float(5F, 10F, 7.5F, 15F);
var doubleRect = new Rectangle2D.Double(5, 10, 7.5, 15);
```

Xxx2D.Float 和 Xxx2D.Double 类是 Xxx2D 类的子类。对象构造完成后，记住该子类本质上没有任何好处，你可以像上面的代码示例那样，只需将构造的对象存储在超类变量中。

正如你从这些奇怪的名称中看到的，Xxx2D.Float 和 Xxx2D.Double 类也是 Xxx2D 类的内部类。这只是一个微小的语法便利，以避免外部类名膨胀。

最后，Point2D 类描述一个具有 x 和 y 坐标的点。点用于定义形状，但它们本身不是形状。

图 11.33 展示了形状类之间的关系。但是，Double 和 Float 子类被省略了。来自 2D 之前库的遗留类用灰色填充标记。

#### 11.3.2.2 使用形状类

你在第 I 卷第 10 章中已经看到如何使用 Rectangle2D、Ellipse2D 和 Line2D 类。在本节中，你将学习如何使用其余的 2D 形状。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_721_0.png)

图 11.33 形状类之间的关系

对于 `RoundRectangle2D` 形状，指定左上角、宽度、高度，以及应倒圆的角区域的 *x* 和 *y* 尺寸（见图 11.34）。例如，调用

```
var r = new RoundRectangle2D.Double(150, 200, 100, 50, 20, 20);
```

会生成一个圆角矩形，每个角上都有半径为 20 的圆。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_722_0.png)

**图 11.34** 构造一个 RoundRectangle2D

要构造弧，指定边界框、起始角、弧扫过的角度（见图 11.35）以及闭合类型——Arc2D.OPEN、Arc2D.PIE 或 Arc2D.CHORD 之一。

```
var a = new Arc2D(x, y, width, height, startAngle, arcAngle, closureType);
```

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_722_1.png)

**图 11.35** 构造一条椭圆弧

图 11.36 说明了弧的类型。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_723_0.png)

**图 11.36** 弧的类型

> **警告：** 如果弧是椭圆形的，那么弧角的计算一点也不简单。API 文档指出：“这些角度是相对于非正方形框架矩形指定的，因此 45 度总是落在从椭圆中心到框架矩形右上角的连线上。结果，如果框架矩形沿一个轴明显比另一个轴长，那么弧段起点和终点的角度将沿框架较长的轴偏斜得更远。”遗憾的是，文档没有说明如何计算这种“偏斜”。以下是细节：

假设弧的中心为原点，点 (x, y) 位于弧上。你可以用以下公式得到偏斜角：

```
skewAngle = Math.toDegrees(Math.atan2(-y * height, x * width));
```

要构造二次曲线和三次曲线，请给出端点坐标和控制点坐标。例如：

```
var q = new QuadCurve2D.Double(startX, startY, controlX, controlY, endX, endY);
var c = new CubicCurve2D.Double(startX, startY, controlX1, controlY1,
    controlX2, controlY2, endX, endY);
```

二次曲线不是很灵活，在实践中也不常用。然而，三次曲线（例如由 CubicCurve2D 类绘制的贝塞尔曲线）非常常见。通过组合许多三次曲线，使连接点处的斜率匹配，你可以创建复杂且看起来平滑的曲线形状。有关更多信息，我们建议你参考 James D. Foley、Andries van Dam、Steven K. Feiner 等人所著的 *《计算机图形学：原理与实践（第三版）》*（Addison-Wesley，2013）。

你可以构建任意序列的线段、二次曲线和三次曲线，并将它们存储在一个 GeneralPath 对象中。用 moveTo 方法指定路径的第一个坐标，例如：

```
var path = new GeneralPath();
path.moveTo(10, 20);
```

然后，你可以通过调用 lineTo、quadTo 或 curveTo 方法之一来扩展路径。这些方法分别用一条直线、一条二次曲线或一条三次曲线来扩展路径。要调用 lineTo，请提供端点。对于两个曲线方法，请提供控制点，然后提供端点。例如，

```
path.lineTo(20, 30);
path.curveTo(controlX, controlY, control2X, control2Y, endX, endY);
```

通过调用 closePath 方法闭合路径。它会画一条直线回到路径的起点。

要制作多边形，只需调用 moveTo 转到第一个角点，然后重复调用 lineTo 访问其他角点。最后，调用 closePath 闭合多边形。程序清单 11.15 中的程序更详细地展示了这一点。

通用路径不必是连通的。你可以随时调用 moveTo 来开始一个新的路径段。

最后，你可以使用 append 方法将任意形状对象添加到一个通用路径中。该形状的轮廓会被添加到路径末尾。如果新形状应连接到路径上的最后一个点，则 append 方法的第二个参数为 true，否则为 false。例如，

```
Rectangle2D r = ...;
path.append(r, false);
```

会将一个矩形的轮廓追加到路径中，而不将其连接到现有路径。但是

```
path.append(r, true);
```

会添加一条从路径端点到矩形起点的直线，然后将矩形轮廓添加到路径中。

程序清单 11.15 中的程序让你创建示例路径。图 11.37 和图 11.38 展示了该程序的示例运行结果。你可以从组合框中选择一个形状生成器。该程序包含用于以下形状的生成器：

- 直线
- 矩形、圆角矩形和椭圆
- 弧（除弧本身外，还显示边界矩形以及起始角和终止角的线）
- 多边形（使用 `GeneralPath`）
- 二次曲线和三次曲线

使用鼠标调整控制点。当你移动它们时，形状会不断重新绘制自身。

该程序有点复杂，因为它处理多个形状并支持拖动控制点。

一个抽象超类 `ShapeMaker` 封装了各形状生成器类的共性。每个形状都有固定数量的控制点，用户可以移动这些控制点。`getPointCount` 方法返回该值。抽象方法

```
Shape makeShape(Point2D[] points)
```

根据控制点的当前位置计算实际形状。`toString` 方法返回类名，以便 `ShapeMaker` 对象可以简单地放入 `JComboBox`。

为了能够拖动控制点，`ShapePanel` 类同时处理鼠标事件和鼠标移动事件。如果鼠标在某个矩形上按下，后续的鼠标拖动会移动该矩形。

大多数形状生成器类都很简单——它们的 `makeShape` 方法只是构造并返回所请求的形状。然而，`ArcMaker` 类需要计算畸变后的起始角和终止角。此外，为了证明该计算确实正确，返回的形状是一个 `GeneralPath`，其中包含弧本身、边界矩形，以及从弧中心到角度控制点的线（见图 11.39）。




![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_727_0.png)

##### 代码清单 11.15 shape/ShapeTest.java

```java
package shape;

import java.awt.*;
import java.awt.event.*;
import java.awt.geom.*;
import java.util.*;
import javax.swing.*;

/**
 * This program demonstrates the various 2D shapes.
 * @version 1.04 2018-05-01
 * @author Cay Horstmann
 */
public class ShapeTest
{
   public static void main(String[] args)
   {
      EventQueue.invokeLater(() ->
         {
            var frame = new ShapeTestFrame();
            frame.setTitle("ShapeTest");
            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            frame.setVisible(true);
         });
   }
}

/**
 * This frame contains a combo box to select a shape and a component to draw it.
 */
class ShapeTestFrame extends JFrame
{
   public ShapeTestFrame()
   {
      var comp = new ShapeComponent();
      add(comp, BorderLayout.CENTER);
      var comboBox = new JComboBox<ShapeMaker>();
      comboBox.addItem(new LineMaker());
      comboBox.addItem(new RectangleMaker());
      comboBox.addItem(new RoundRectangleMaker());
      comboBox.addItem(new EllipseMaker());
      comboBox.addItem(new ArcMaker());
      comboBox.addItem(new PolygonMaker());
      comboBox.addItem(new QuadCurveMaker());
      comboBox.addItem(new CubicCurveMaker());
      comboBox.addActionListener(event ->
         {
            ShapeMaker shapeMaker = comboBox.getItemAt(comboBox.getSelectedIndex());
            comp.setShapeMaker(shapeMaker);
         });
      add(comboBox, BorderLayout.NORTH);
      comp.setShapeMaker((ShapeMaker) comboBox.getItemAt(0));
      pack();
   }
}

/**
 * This component draws a shape and allows the user to move the points that define it.
 */
class ShapeComponent extends JComponent
{
   private static final Dimension PREFERRED_SIZE = new Dimension(300, 200);
   private Point2D[] points;
   private static final Random generator = new Random();
   private static int SIZE = 10;
   private int current;
   private ShapeMaker shapeMaker;

   public ShapeComponent()
   {
      addMouseListener(new MouseAdapter()
         {
            public void mousePressed(MouseEvent event)
            {
               Point p = event.getPoint();
               for (int i = 0; i < points.length; i++)
               {
                  double x = points[i].getX() - SIZE / 2;
                  double y = points[i].getY() - SIZE / 2;
                  var r = new Rectangle2D.Double(x, y, SIZE, SIZE);
                  if (r.contains(p))
                  {
                     current = i;
                     return;
                  }
               }
            }

            public void mouseReleased(MouseEvent event)
            {
               current = -1;
            }
         });
      addMouseMotionListener(new MouseMotionAdapter()
         {
            public void mouseDragged(MouseEvent event)
            {
               if (current == -1) return;
               points[current] = event.getPoint();
               repaint();
            }
         });
      current = -1;
   }

   /**
    * Set a shape maker and initialize it with a random point set.
    * @param aShapeMaker a shape maker that defines a shape from a point set
    */
   public void setShapeMaker(ShapeMaker aShapeMaker)
   {
      shapeMaker = aShapeMaker;
      int n = shapeMaker.getPointCount();
      points = new Point2D[n];
      for (int i = 0; i < n; i++)
      {
         double x = generator.nextDouble() * getWidth();
         double y = generator.nextDouble() * getHeight();
         points[i] = new Point2D.Double(x, y);
      }
      repaint();
   }
}
```

```java
public abstract Shape makeShape(Point2D[] p);
public String toString()
{
   return getClass().getName();
}
}

/**
 * Makes a line that joins two given points.
 */
class LineMaker extends ShapeMaker
{
   public LineMaker()
   {
      super(2);
   }

   public Shape makeShape(Point2D[] p)
   {
      return new Line2D.Double(p[0], p[1]);
   }
}

/**
 * Makes a rectangle that joins two given corner points.
 */
class RectangleMaker extends ShapeMaker
{
   public RectangleMaker()
   {
      super(2);
   }

   public Shape makeShape(Point2D[] p)
   {
      var s = new Rectangle2D.Double();
      s.setFrameFromDiagonal(p[0], p[1]);
      return s;
   }
}

/**
 * Makes a round rectangle that joins two given corner points.
 */
class RoundRectangleMaker extends ShapeMaker
{
   public RoundRectangleMaker()
   {
```

```java
double width = Math.abs(p[1].getX() - p[0].getX());
double height = Math.abs(p[1].getY() - p[0].getY());

double skewedStartAngle = Math.toDegrees(Math.atan2(-(p[2].getY() - centerY) * width,
   (p[2].getX() - centerX) * height));
double skewedEndAngle = Math.toDegrees(Math.atan2(-(p[3].getY() - centerY) * width,
   (p[3].getX() - centerX) * height));
double skewedAngleDifference = skewedEndAngle - skewedStartAngle;
if (skewedStartAngle < 0) skewedStartAngle += 360;
if (skewedAngleDifference < 0) skewedAngleDifference += 360;

var s = new Arc2D.Double(0, 0, 0, 0,
   skewedStartAngle, skewedAngleDifference, Arc2D.OPEN);
s.setFrameFromDiagonal(p[0], p[1]);

var g = new GeneralPath();
g.append(s, false);
var r = new Rectangle2D.Double();
r.setFrameFromDiagonal(p[0], p[1]);
g.append(r, false);
var center = new Point2D.Double(centerX, centerY);
g.append(new Line2D.Double(center, p[2]), false);
g.append(new Line2D.Double(center, p[3]), false);
return g;
}
}

/**
 * Makes a polygon defined by six corner points.
 */
class PolygonMaker extends ShapeMaker
{
   public PolygonMaker()
   {
      super(6);
   }

   public Shape makeShape(Point2D[] p)
   {
      var s = new GeneralPath();
      s.moveTo((float) p[0].getX(), (float) p[0].getY());
      for (int i = 1; i < p.length; i++)
         s.lineTo((float) p[i].getX(), (float) p[i].getY());
      s.closePath();
      return s;
   }
}

/**
 * Makes a quad curve defined by two end points and a control point.
 */
class QuadCurveMaker extends ShapeMaker
{
   public QuadCurveMaker()
   {
      super(3);
   }

   public Shape makeShape(Point2D[] p)
   {
      return new QuadCurve2D.Double(p[0].getX(), p[0].getY(), p[1].getX(), p[1].getY(),
         p[2].getX(), p[2].getY());
   }
}

/**
 * Makes a cubic curve defined by two end points and two control points.
 */
class CubicCurveMaker extends ShapeMaker
{
   public CubicCurveMaker()
   {
      super(4);
   }

   public Shape makeShape(Point2D[] p)
   {
      return new CubicCurve2D.Double(p[0].getX(), p[0].getY(), p[1].getX(), p[1].getY(),
         p[2].getX(), p[2].getY(), p[3].getX(), p[3].getY());
   }
}
```

- **java.awt.geom.RoundRectangle2D.Double** 1.2
  - `RoundRectangle2D.Double(double x, double y, double width, double height, double arcWidth, double arcHeight)` 使用给定的边界矩形和弧尺寸构造一个圆角矩形。arcWidth 和 arcHeight 参数的解释见图 11.34。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_737_0.png)

**图 11.40** 构造区域几何操作

Area 类实现了 Shape 接口。可以使用 Graphics2D 类的 draw 方法描边区域边界，或使用 fill 方法填充内部。

| `java.awt.geom.Area` |
|---|
| - `void add(Area other)`<br>- `void subtract(Area other)`<br>- `void intersect(Area other)`<br>- `void exclusiveOr(Area other)`<br><br>使用此区域和另一个区域执行构造区域几何操作，并将此区域设置为结果。 |

### 11.3.4 描边

Graphics2D 类的 draw 操作使用当前选定的描边绘制形状边界。默认情况下，描边是宽度为 1 像素的实线。可以通过调用 setStroke 方法并提供实现 Stroke 接口的类的对象来选择不同的描边。Java 2D API 只定义了一个这样的类，称为 BasicStroke。本节将介绍 BasicStroke 类的功能。




你可以构造任意厚度的笔画。例如，以下代码演示如何绘制 10 像素宽的线条：

```java
g2.setStroke(new BasicStroke(10.0F));
g2.draw(new Line2D.Double(...));
```

当笔画的宽度超过一个像素时，笔画的末端可以有不同的样式。图 11.41 展示了这些所谓的端点样式。你有三种选择：

- *平头端点* 简单地在笔画的终点结束。
- *圆头端点* 在笔画末端加一个半圆。
- *方头端点* 在笔画末端加一个半个正方形。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_738_0.png)

**图 11.41** 端点样式

当两条粗笔画相接时，*连接样式*有三种选择（见图 11.42）。

- *斜角连接* 用一条垂直于两条笔画夹角平分线的直线连接它们。
- *圆角连接* 将每条笔画延伸为圆头。
- *尖角连接* 通过添加一个“尖峰”来延伸两条笔画。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_739_0.png)

**图 11.42** 连接样式

如果两条线以非常小的角度形成尖角连接，就会改用斜角连接，以避免产生极长的尖峰。*斜接限制*控制这种转换。从技术上讲，它是尖峰内角与外角之间的距离除以笔画宽度。默认的斜接限制为 10，对应约 11 度的角度。

你可以在 BasicStroke 构造函数中指定这些选择，例如：

```java
g2.setStroke(new BasicStroke(10.0F, BasicStroke.CAP_ROUND, BasicStroke.JOIN_ROUND));
g2.setStroke(new BasicStroke(10.0F, BasicStroke.CAP_BUTT, BasicStroke.JOIN_MITER,
    15.0F /* miter limit */));
```

最后，你可以通过设置*虚线模式*来创建虚线。在清单 11.16 的程序中，你可以选择一种用摩尔斯电码拼写出 SOS 的虚线模式。虚线模式是一个 float[] 数组，包含“开”和“关”间隔的长度（见图 11.43）。

在构造 BasicStroke 时，你可以指定虚线模式和*虚线相位*。虚线相位指示每条线应在虚线模式中的何处开始。通常，你将该值设置为 0。

```java
float[] dashPattern = { 10, 10, 10, 10, 10, 10, 10, 30, 10, 30, ... };
g2.setStroke(new BasicStroke(10.0F, BasicStroke.CAP_BUTT, BasicStroke.JOIN_MITER,
    10.0F /* miter limit */, dashPattern, 0 /* dash phase */));
```

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_740_0.png)

**图 11.43** 虚线模式

> **注意：** 端点样式会应用于虚线模式中每段虚线的端点。

清单 11.16 中的程序允许你指定端点样式、连接样式和虚线（见图 11.44）。你可以移动线段端点来测试斜接限制：选择尖角连接，然后移动线段形成非常尖锐的角度，你会看到尖角连接转变为斜角连接。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_740_1.png)

**图 11.44** StrokeTest 程序

该程序与清单 11.15 中的程序类似。鼠标监听器记录你对线段端点的点击，鼠标移动监听器监视端点的拖动。一组单选按钮用于表示用户对端点样式、连接样式以及实线或虚线的选择。`StrokeComponent` 类的 `paintComponent` 方法构造一个 `GeneralPath`，它由连接三个点的两条线段组成，用户可以用鼠标移动这些点。然后，它根据用户所做的选择构造一个 `BasicStroke`，最后绘制该路径。

#### 清单 11.16 `stroke/StrokeTest.java`

```java
package stroke;

import java.awt.*;
import java.awt.event.*;
import java.awt.geom.*;
import javax.swing.*;

/**
 * This program demonstrates different stroke types.
 * @version 1.05 2018-05-01
 * @author Cay Horstmann
 */
public class StrokeTest
{
   public static void main(String[] args)
   {
      EventQueue.invokeLater(() ->
         {
            var frame = new StrokeTestFrame();
            frame.setTitle("StrokeTest");
            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            frame.setVisible(true);
         });
   }
}

/**
 * This frame lets the user choose the cap, join, and line style, and shows the resulting
 * stroke.
 */
class StrokeTestFrame extends JFrame
{
   private StrokeComponent canvas;
   private JPanel buttonPanel;

   public StrokeTestFrame()
   {
      canvas = new StrokeComponent();
      add(canvas, BorderLayout.CENTER);

      buttonPanel = new JPanel();
      buttonPanel.setLayout(new GridLayout(3, 3));
      add(buttonPanel, BorderLayout.NORTH);

      var group1 = new ButtonGroup();
      makeCapButton("Butt Cap", BasicStroke.CAP_BUTT, group1);
      makeCapButton("Round Cap", BasicStroke.CAP_ROUND, group1);
      makeCapButton("Square Cap", BasicStroke.CAP_SQUARE, group1);

      var group2 = new ButtonGroup();
      makeJoinButton("Miter Join", BasicStroke.JOIN_MITER, group2);
      makeJoinButton("Bevel Join", BasicStroke.JOIN_BEVEL, group2);
      makeJoinButton("Round Join", BasicStroke.JOIN_ROUND, group2);

      var group3 = new ButtonGroup();
      makeDashButton("Solid Line", false, group3);
      makeDashButton("Dashed Line", true, group3);
   }

   /**
    * Makes a radio button to change the cap style.
    * @param label the button label
    * @param style the cap style
    * @param group the radio button group
    */
   private void makeCapButton(String label, final int style, ButtonGroup group)
   {
      // select first button in group
      boolean selected = group.getButtonCount() == 0;
      var button = new JRadioButton(label, selected);
      buttonPanel.add(button);
      group.add(button);
      button.addActionListener(event -> canvas.setCap(style));
      pack();
   }

   /**
    * Makes a radio button to change the join style.
    * @param label the button label
    * @param style the join style
    * @param group the radio button group
    */
   private void makeJoinButton(String label, final int style, ButtonGroup group)
   {
      // select first button in group
      boolean selected = group.getButtonCount() == 0;
      var button = new JRadioButton(label, selected);
      buttonPanel.add(button);
      group.add(button);
      button.addActionListener(event -> canvas.setJoin(style));
   }

   /**
    * Makes a radio button to set solid or dashed lines.
    * @param label the button label
    * @param style false for solid, true for dashed lines
    * @param group the radio button group
    */
   private void makeDashButton(String label, final boolean style, ButtonGroup group)
   {
      // select first button in group
      boolean selected = group.getButtonCount() == 0;
      var button = new JRadioButton(label, selected);
      buttonPanel.add(button);
      group.add(button);
      button.addActionListener(event -> canvas.setDash(style));
   }
}

/**
 * This component draws two joined lines, using different stroke objects, and allows the user
 * to drag the three points defining the lines.
 */
class StrokeComponent extends JComponent
{
   private static final Dimension PREFERRED_SIZE = new Dimension(400, 400);
   private static int SIZE = 10;

   private Point2D[] points;
   private int current;
   private float width;
   private int cap;
   private int join;
   private boolean dash;

   public StrokeComponent()
   {
      addMouseListener(new MouseAdapter()
      {
```

```java
            for (int i = 1; i < points.length; i++)
                path.lineTo((float) points[i].getX(),
                            (float) points[i].getY());
            BasicStroke stroke;
            if (dash)
            {
                float miterLimit = 10.0F;
                float[] dashPattern = { 10F, 10F, 10F, 10F, 10F, 30F, 10F, 30F, 10F, 30F, 10F,
                                        10F, 10F, 10F, 10F, 30F };
                float dashPhase = 0;
                stroke = new BasicStroke(width, cap, join, miterLimit, dashPattern, dashPhase);
            }
            else stroke = new BasicStroke(width, cap, join);
            g2.setStroke(stroke);
            g2.draw(path);
         }

         /**
          * Sets the join style.
          * @param j the join style
          */
         public void setJoin(int j)
         {
            join = j;
            repaint();
         }

         /**
          * Sets the cap style.
          * @param c the cap style
          */
         public void setCap(int c)
         {
            cap = c;
            repaint();
         }

         /**
          * Sets solid or dashed lines.
          * @param d false for solid, true for dashed lines
          */
         public void setDash(boolean d)
         {
            dash = d;
            repaint();
         }

         public Dimension getPreferredSize() { return PREFERRED_SIZE; }
      }
```





**java.awt.Graphics2D 1.2**

- `void setStroke(Stroke s)`  
  将此图形上下文的描边设置为给定对象，该对象实现 `Stroke` 接口。

**java.awt.BasicStroke 1.2**

- `BasicStroke(float width)`
- `BasicStroke(float width, int cap, int join)`
- `BasicStroke(float width, int cap, int join, float miterlimit)`
- `BasicStroke(float width, int cap, int join, float miterlimit, float[] dash, float dashPhase)`

使用给定属性构造一个描边对象。

**参数：**

| 参数 | 描述 |
| --- | --- |
| `width` | 画笔的宽度 |
| `cap` | 端点样式——`CAP_BUTT`、`CAP_ROUND` 和 `CAP_SQUARE` 之一 |
| `join` | 连接样式——`JOIN_BEVEL`、`JOIN_MITER` 和 `JOIN_ROUND` 之一 |
| `miterlimit` | 连接处外角与内角之间的比率与描边宽度之比；低于该值时，斜接连接会渲染为斜角连接 |
| `dash` | 虚线描边中交替的实线部分和空白部分的长度数组 |
| `dashPhase` | 虚线模式的“相位”；假定在描边起点之前有一段该长度的线段已经应用了虚线模式。 |

### 11.3.5 Paint

填充一个形状时，其内部会被*绘图*覆盖。使用 `setPaint` 方法将绘图样式设置为某个对象，该对象的类实现 `Paint` 接口。Java 2D API 提供了三个这样的类：

- `Color` 类实现 `Paint` 接口。要用纯色填充形状，只需用一个 `Color` 对象调用 `setPaint`，例如

        ```java
        g2.setPaint(Color.red);
        ```

- `GradientPaint` 类通过在两个给定颜色值之间插值来改变颜色（参见图 11.45）。

    ![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_747_0.png)

    **图 11.45** 渐变填充

- `TexturePaint` 类用图像的重复图案填充区域（参见图 11.46）。

    ![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_747_1.png)

    **图 11.46** 纹理填充

可以通过指定两个点以及希望在这两个点处使用的颜色来构造 `GradientPaint` 对象。

```java
g2.setPaint(new GradientPaint(p1, Color.RED, p2, Color.YELLOW));
```

颜色沿连接这两个点的直线进行插值。颜色在垂直于该连接线的直线上保持不变。超出直线端点的点会使用该端点处的颜色。

或者，如果调用 `GradientPaint` 构造器时将 cyclic 参数设为 true：

```java
g2.setPaint(new GradientPaint(p1, Color.RED, p2, Color.YELLOW, true));
```

那么，颜色变化会循环，并在端点之外继续变化。

要构造 `TexturePaint` 对象，请指定一个 `BufferedImage` 和一个*锚定*矩形。

```java
g2.setPaint(new TexturePaint(bufferedImage, anchorRectangle));
```

我们将在本章后面详细讨论图像时介绍 `BufferedImage` 类。获取缓冲图像的最简单方法是读取图像文件：

```java
bufferedImage = ImageIO.read(new File("blue-ball.gif"));
```

锚定矩形会在 *x* 和 *y* 方向上无限延伸，以平铺整个坐标平面。图像会被缩放以适配锚定矩形，然后复制到每个图块中。

**java.awt.Graphics2D 1.2**

- `void setPaint(Paint s)`  
  将此图形上下文的绘图设置为给定对象，该对象实现 Paint 接口。

**java.awt.GradientPaint 1.2**

- `GradientPaint(float x1, float y1, Color color1, float x2, float y2, Color color2)`
- `GradientPaint(float x1, float y1, Color color1, float x2, float y2, Color color2, boolean cyclic)`
- `GradientPaint(Point2D p1, Color color1, Point2D p2, Color color2)`
- `GradientPaint(Point2D p1, Color color1, Point2D p2, Color color2, boolean cyclic)`

构造一个渐变填充对象，它用颜色填充形状，使得起点使用 color1 着色，终点使用 color2 着色，而两者之间的颜色进行线性插值。颜色在垂直于连接起点和终点的直线的直线上保持不变。默认情况下，渐变填充不是循环的——也就是说，超出起点和终点的点会使用与起点和终点相同的颜色着色。如果渐变填充是循环的，则颜色会继续插值，首先返回起点颜色，然后在两个方向上无限重复。

**java.awt.TexturePaint 1.2**

- `TexturePaint(BufferedImage texture, Rectangle2D anchor)`  
  创建一个纹理填充对象。锚定矩形定义要填充空间的平铺方式；它在 *x* 和 *y* 方向上无限重复，并且纹理图像会被缩放以填充每个图块。

### 11.3.6 坐标变换

假设你需要绘制一个对象，例如一辆汽车。根据制造商规格，你知道高度、轴距和总长度。当然，你可以假定每米多少像素，然后计算出所有像素位置。然而，有一种更简单的方法：你可以让图形上下文为你执行转换。

```java
g2.scale(pixelsPerMeter, pixelsPerMeter);
g2.draw(new Line2D.Double(coordinates in meters)); // converts to pixels and
                                                     // draws scaled line
```

`Graphics2D` 类的 scale 方法将图形上下文的*坐标变换*设置为缩放变换。该变换将*用户坐标*（用户指定的单位）转换为*设备坐标*（像素）。图 11.47 展示了该变换如何工作。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_749_0.png)

坐标变换在实践中非常有用。它们允许你使用方便的坐标值。图形上下文会处理将它们转换为像素的繁琐工作。

有四种基本变换。

- 缩放：放大或缩小所有点到某个固定点的距离
- 旋转：围绕固定中心旋转所有点
- 平移：将所有点移动固定量
- **错切：** 保持一条线固定，并将与其平行的线“滑动”一定量，该量与到固定线的距离成正比

图 11.48 展示了这四种基本变换如何作用于一个单位正方形。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_750_0.png)

**图 11.48** 基本变换

`Graphics2D` 类的 scale、rotate、translate 和 shear 方法将图形上下文的坐标变换设置为这四种基本变换之一。

你可以*组合*这些变换。例如，你可能想旋转形状并将其尺寸加倍；同时提供旋转变换和缩放变换：

```java
g2.rotate(angle);
g2.scale(2, 2);
g2.draw(...);
```

在这种情况下，你提供变换的顺序无关紧要。然而，对于大多数变换，顺序确实很重要。例如，如果你想旋转和错切，那么先提供哪种变换会产生差别。你需要弄清楚自己的意图。图形上下文会按与你提供它们相反的顺序应用变换——也就是说，你最后提供的变换会最先应用。

你可以提供任意多个变换。例如，考虑以下变换序列：

```java
g2.translate(x, y);
g2.rotate(a);
g2.translate(-x, -y);
```

最后一个变换（它最先应用）将点 (x, y) 移到原点。第二个变换围绕原点旋转角度 α。最后一个变换将原点移回 (x, y)。总体效果是围绕中心点 (x, y) 旋转——参见图 11.49。由于绕原点以外的点旋转是如此常见的操作，因此有一个快捷方式：

```java
g2.rotate(a, x, y);
```

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_751_0.png)

**图 11.49** 组合变换

如果你了解一些矩阵理论，你可能知道所有旋转、平移、缩放、错切及其组合都可以用以下形式的变换矩阵表示：

$$\begin{bmatrix}x_{new}\\y_{new}\\1\end{bmatrix}=\begin{bmatrix}a&c&e\\b&d&f\\0&0&1\end{bmatrix}\begin{bmatrix}x\\y\\1\end{bmatrix}$$


这种变换称为*仿射变换*。在 Java 2D API 中，`AffineTransform` 类描述了这种变换。如果你知道某个特定变换矩阵的分量，可以直接按如下方式构造它

```
var t = new AffineTransform(a, b, c, d, e, f);
```

此外，工厂方法 `getRotateInstance`、`getScaleInstance`、`getTranslateInstance` 和 `getShearInstance` 会构造表示这些变换类型的矩阵。例如，以下调用

```
t = AffineTransform.getScaleInstance(2.0F, 0.5F);
```

返回一个对应于以下矩阵的变换

```
[ 2    0    0 ]
[ 0   0.5   0 ]
[ 0    0    1 ]
```

最后，实例方法 `setToRotation`、`setToScale`、`setToTranslation` 和 `setToShear` 会将变换对象设置为新类型。下面是一个示例：

```
t.setToRotation(angle); // sets t to a rotation
```

你可以将图形上下文的坐标变换设置为一个 `AffineTransform` 对象。

```
g2.setTransform(t); // replaces current transformation
```

然而，在实践中，你不应调用 `setTransform` 操作，因为它会替换图形上下文可能已有的任何现有变换。例如，用于横向打印的图形上下文已经包含一个 90 度旋转变换。如果调用 `setTransform`，就会抹掉该旋转。相反，应调用 `transform` 方法。

```
g2.transform(t); // composes current transformation with t
```

它会将现有变换与新的 `AffineTransform` 对象组合起来。

如果你只想临时应用一个变换，首先获取旧变换，将其与新变换组合，最后在完成后恢复旧变换。

```
AffineTransform oldTransform = g2.getTransform(); // save old transform
g2.transform(t); // apply temporary transform
draw on g2
g2.setTransform(oldTransform); // restore old transform
```

#### java.awt.geom.AffineTransform 1.2

- `AffineTransform(double a, double b, double c, double d, double e, double f)`
- `AffineTransform(float a, float b, float c, float d, float e, float f)`  
  使用以下矩阵构造仿射变换

  $$
  \begin{bmatrix}
  a & c & e \\
  b & d & f \\
  0 & 0 & 1
  \end{bmatrix}
  $$

- `AffineTransform(double[] m)`
- `AffineTransform(float[] m)`  
  使用以下矩阵构造仿射变换

  $$
  \begin{bmatrix}
  m[0] & m[2] & m[4] \\
  m[1] & m[3] & m[5] \\
  0 & 0 & 1
  \end{bmatrix}
  $$

- `static AffineTransform getRotateInstance(double a)`  
  创建一个绕原点旋转角度 *a*（以弧度为单位）的旋转。变换矩阵为

  $$
  \begin{bmatrix}
  \cos(a) & -\sin(a) & 0 \\
  \sin(a) & \cos(a) & 0 \\
  0 & 0 & 1
  \end{bmatrix}
  $$

  如果 *a* 介于 0 与 $\pi / 2$ 之间，则该旋转会将正 *x* 轴朝正 *y* 轴方向移动。
- `static AffineTransform getRotateInstance(double a, double x, double y)`  
  创建一个绕点 (*x*, *y*) 旋转角度 *a*（以弧度为单位）的旋转。
- `static AffineTransform getScaleInstance(double sx, double sy)`  
  创建一个缩放变换，将 *x* 轴按 *sx* 缩放，将 *y* 轴按 *sy* 缩放。变换矩阵为

  $$
  \begin{bmatrix}
  sx & 0 & 0 \\
  0 & sy & 0 \\
  0 & 0 & 1
  \end{bmatrix}
  $$

#### java.awt.geom.AffineTransform 1.2 *（续）*

- `static AffineTransform getShearInstance(double shx, double shy)`  
  创建一个剪切变换，将 *x* 轴按 `shx` 剪切，将 *y* 轴按 `shy` 剪切。变换矩阵为：

  ```
  [ 1   shx  0 ]
  [ shy  1   0 ]
  [ 0    0   1 ]
  ```

- `static AffineTransform getTranslateInstance(double tx, double ty)`  
  创建一个平移变换，将 *x* 轴移动 `tx`，将 *y* 轴移动 `ty`。变换矩阵为：

  ```
  [ 1   0   tx ]
  [ 0   1   ty ]
  [ 0   0   1  ]
  ```

- `void setToRotation(double a)`
- `void setToRotation(double a, double x, double y)`
- `void setToScale(double sx, double sy)`
- `void setToShear(double shx, double shy)`
- `void setToTranslation(double tx, double ty)`  
  将此仿射变换设置为具有给定参数的基本变换。有关基本变换及其参数的说明，请参见 `getXxxInstance` 方法。

#### java.awt.Graphics2D 1.2

- `void setTransform(AffineTransform t)`  
  用 `t` 替换此图形上下文的现有坐标变换。
- `void transform(AffineTransform t)`  
  将此图形上下文的现有坐标变换与 `t` 组合。
- `void rotate(double a)`
- `void rotate(double a, double x, double y)`
- `void scale(double sx, double sy)`
- `void shear(double sx, double sy)`
- `void translate(double tx, double ty)`  
  将此图形上下文的现有坐标变换与具有给定参数的基本变换组合。有关基本变换及其参数的说明，请参见 `AffineTransform.getXxxInstance` 方法。

### 11.3.7 裁剪

通过在图形上下文中设置*裁剪形状*，可以将所有绘制操作限制在该裁剪形状的内部。

```
g2.setClip(clipShape); // but see below
g2.draw(shape); // draws only the part that falls inside the clipping shape
```

然而，在实践中，你不想调用 setClip 操作，因为它会替换图形上下文可能已有的任何现有裁剪形状。例如，正如你将在本章后面看到的，用于打印的图形上下文带有一个裁剪矩形，以确保你不会绘制到页边距上。相反，应调用 clip 方法。

```
g2.clip(clipShape); // better
```

clip 方法会将现有裁剪形状与你提供的新裁剪形状相交。

如果你只想临时应用一个裁剪区域，应该首先获取旧裁剪，添加新裁剪，最后在完成后恢复旧裁剪：

```
Shape oldClip = g2.getClip(); // save old clip
g2.clip(clipShape); // apply temporary clip
draw on g2
g2.setClip(oldClip); // restore old clip
```

在图 11.50 中，我们通过一幅相当引人注目的图展示了裁剪功能：一个由复杂形状——即一组字母的轮廓——裁剪出的线条图案。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_755_0.png)

**图 11.50** 使用字母形状裁剪线条图案

要获取字符轮廓，需要一个*字体渲染上下文*。请使用 Graphics2D 类的 getFontRenderContext 方法。

```java
FontRenderContext context = g2.getFontRenderContext();
```

接下来，使用一个字符串、一种字体和该字体渲染上下文，创建一个 `TextLayout` 对象：

```java
var layout = new TextLayout("Hello", font, context);
```

此文本布局对象描述由特定字体渲染上下文渲染的字符序列的布局。布局取决于字体渲染上下文——相同字符在屏幕上和打印机上的外观会有所不同。

对我们的应用更重要的是，`getOutline` 方法返回一个 `Shape` 对象，该对象描述文本布局中字符轮廓的形状。轮廓形状从原点 (0, 0) 开始，这可能不是你想要的。在这种情况下，请向 `getOutline` 操作提供一个仿射变换，以指定你希望轮廓出现的位置。

```java
AffineTransform transform = AffineTransform.getTranslateInstance(0, 100);
Shape outline = layout.getOutline(transform);
```

然后，将轮廓追加到裁剪形状中。

```java
var clipShape = new GeneralPath();
clipShape.append(outline, false);
```

最后，设置裁剪形状并绘制一组线条。这些线条只会出现在字符边界内部。

```java
g2.setClip(clipShape);
var p = new Point2D.Double(0, 0);
for (int i = 0; i < NLINES; i++)
{
   double x = . . .;
   double y = . . .;
   var q = new Point2D.Double(x, y);
   g2.draw(new Line2D.Double(p, q)); // lines are clipped
}
```

| java.awt.Graphics 1.0 |
| :--- |
| • `void setClip(Shape s)` 1.2<br>将当前裁剪形状设置为形状 s。 |
| • `Shape getClip()` 1.2<br>返回当前裁剪形状。 |





#### java.awt.Graphics2D 1.2

- `void clip(Shape s)` — 将当前裁剪形状与形状 s 相交。
- `FontRenderContext getFontRenderContext()` — 返回字体渲染上下文，该上下文是构造 TextLayout 对象所必需的。

#### java.awt.font.TextLayout 1.2

- `TextLayout(String s, Font f, FontRenderContext context)` — 根据给定的字符串和字体构造文本布局对象，并使用字体渲染上下文来获取特定设备的字体属性。
- `float getAdvance()` — 返回此文本布局的宽度。
- `float getAscent()` / `float getDescent()` — 返回此文本布局在基线上方和下方的高度。
- `float getLeading()` — 返回此文本布局所用字体中连续行之间的距离。

### 11.3.8 透明与合成

在标准 RGB 颜色模型中，每种颜色都由其红色、绿色和蓝色分量描述。然而，描述图像中*透明*或*部分透明*的区域也很方便。当你将图像叠加到现有绘图上时，透明像素完全不会遮挡其下的像素，而部分透明的像素则会与其下的像素混合。图 11.51 显示了将部分透明的矩形叠加到图像上的效果。你仍然可以从矩形下方看到图像的细节。

在 Java 2D API 中，透明度由*alpha 通道*描述。每个像素除了红色、绿色和蓝色颜色分量外，还有一个介于 0（完全透明）和 1（完全不透明）之间的 alpha 值。例如，图 11.51 中的矩形填充的是具有 50% 透明度的淡黄色：

```java
new Color(0.7f, 0.7f, 0.0f, 0.5f);
```

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_758_0.png)

**图 11.51** 将部分透明的矩形叠加到图像上

现在让我们看看如果叠加两个形状会发生什么。你需要混合或**合成**源像素和目标像素的颜色与 alpha 值。计算机图形学领域的两位研究人员 Porter 和 Duff 为这种混合过程制定了 12 种可能的*合成规则*。Java 2D API 实现了所有这些规则。在进一步讨论之前，我们想指出，其中只有两个规则具有实际意义。如果你觉得这些规则晦涩难懂或令人困惑，只需使用 `SRC_OVER` 规则。它是 `Graphics2D` 对象的默认规则，并且能给出最直观的结果。

以下是这些规则背后的理论。假设你有一个 alpha 值为 α_S 的*源*像素。在图像中，已经有一个 alpha 值为 α_D 的*目标*像素。你想要合成这两者。图 11.52 中的图示展示了如何设计一条合成规则。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_758_1.png)

**图 11.52** 设计合成规则

Porter 和 Duff 将 alpha 值视为像素颜色应被使用的概率。从源的角度来看，它使用源颜色的概率为 α_S，不关心的概率为 1 − α_S。目标也是如此。在合成颜色时，让我们假设这些概率是独立的。那么有四种情况，如图 11.52 所示。如果源想使用源颜色而目标不关心，那么让源如愿似乎是合理的。这就是图中右上角标记为“S”的原因。该事件的概率是 α_S · (1 − α_D)。类似地，左下角标记为“D”。如果目标和源都想选择自己的颜色，该怎么办？这就是 Porter–Duff 规则发挥作用的地方。如果我们决定源更重要，我们也将右下角标记为“S”。该规则称为 SRC_OVER。在该规则中，你将源颜色与权重 α_S 相结合，将目标颜色与权重 (1 − α_S) · α_D 相结合。

视觉效果是源与目标的混合，并优先考虑源。特别是，如果 α_S 为 1，则完全不考虑目标颜色。如果 α_S 为 0，则源像素完全透明，目标颜色不变。

其他规则取决于你在概率图的方框中放入哪些字母。表 11.3 和图 11.53 展示了 Java 2D API 支持的所有规则。图中的图像显示了当一个 alpha 为 0.75 的矩形源区域与一个 alpha 为 1.0 的椭圆形目标区域组合时的规则结果。

**表 11.3 Porter–Duff 合成规则**

| 规则 | 说明 |
|---|---|
| CLEAR | 源清除目标。 |
| SRC | 源覆盖目标和空像素。 |
| DST | 源不影响目标。 |
| SRC_OVER | 源与目标混合并覆盖空像素。 |
| DST_OVER | 源不影响目标并覆盖空像素。 |
| SRC_IN | 源覆盖目标。 |
| SRC_OUT | 源清除目标并覆盖空像素。 |
| DST_IN | 源 alpha 修改目标。 |
| DST_OUT | 源 alpha 补数修改目标。 |
| SRC_ATOP | 源与目标混合。 |
| DST_ATOP | 源 alpha 修改目标。源覆盖空像素。 |
| XOR | 源 alpha 补数修改目标。源覆盖空像素。 |

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_760_0.png)

**图 11.53** Porter–Duff 合成规则

正如你所看到的，大多数规则并不是很有用。考虑一个极端的例子：`DST_IN` 规则。它完全不考虑源颜色，而是使用源的 alpha 来影响目标。`SRC` 规则可能很有用——它强制使用源颜色，关闭与目标的混合。

关于 Porter–Duff 规则的更多信息，请参阅 James D. Foley、Andries van Dam、Steven K. Feiner 等人所著的 *Computer Graphics: Principles and Practice, Second Edition in C*。

使用 `Graphics2D` 类的 `setComposite` 方法来安装一个实现了 `Composite` 接口的类的对象。Java 2D API 提供了一个这样的类 `AlphaComposite`，它实现了图 11.53 中的所有 Porter–Duff 规则。

`AlphaComposite` 类的工厂方法 `getInstance` 生成一个 `AlphaComposite` 对象。你需要提供规则和用于源像素的 alpha 值。例如，考虑以下代码：

```java
int rule = AlphaComposite.SRC_OVER;
float alpha = 0.5f;
g2.setComposite(AlphaComposite.getInstance(rule, alpha));
g2.setPaint(Color.blue);
g2.fill(rectangle);
```

然后矩形被绘制为蓝色且 alpha 值为 0.5。由于合成规则是 `SRC_OVER`，它会以透明方式叠加在现有图像上。

清单 11.17 中的程序让你探索这些合成规则。从组合框中选择一个规则，并使用滑块设置 `AlphaComposite` 对象的 alpha 值。

此外，该程序会显示每条规则的文字描述。请注意，这些描述是根据合成规则图计算得出的。例如，第二行中的“DS”代表“与目标混合”。

该程序有一个重要的转折。与屏幕对应的图形上下文不保证具有 alpha 通道。（事实上，通常没有。）当像素被放置到没有 alpha 通道的目标上时，像素颜色会乘以 alpha 值，然后 alpha 值被丢弃。现在，几条 Porter–Duff 规则会使用目标的 alpha 值，这意味着目标 alpha 通道很重要。因此，我们使用具有 ARGB 颜色模型的缓冲图像来合成形状。合成图像后，我们再将结果图像绘制到屏幕。

```java
var image = new BufferedImage(getWidth(), getHeight(), BufferedImage.TYPE_INT_ARGB);
Graphics2D gImage = image.createGraphics();
// now draw to image
g2.drawImage(image, null, 0, 0);
```

清单 11.17 和 11.18 展示了框架和组件类。清单 11.19 中的 Rule 类提供了每条规则的简要说明——参见图 11.54。运行该程序时，将 alpha 滑块从左向右移动，观察对合成形状的影响。特别是要注意，`DST_IN` 和 `DST_OUT` 规则之间的唯一区别是当你改变源 alpha 时目标（！）颜色如何变化。





```java
   23
   24  canvas = new CompositeComponent();
   25  add(canvas, BorderLayout.CENTER);
   26
   27  ruleCombo = new JComboBox(new Rule[] { new Rule("CLEAR", "  ", " "),
   28      new Rule("SRC", " S", " S"), new Rule("DST", "  ", " DD"),
   29      new Rule("SRC_OVER", " S", " DS"), new Rule("DST_OVER", " S", " DD"),
   30      new Rule("SRC_IN", "  ", " S"), new Rule("SRC_OUT", " S", "  "),
   31      new Rule("DST_IN", " D", " S"), new Rule("DST_OUT", " D", "  "),
   32      new Rule("SRC_ATOP", "  ", " DS"), new Rule("DST_ATOP", " S", " D"),
   33      new Rule("XOR", " S", " D"), });
   34  ruleCombo.addActionListener(event ->
   35      {
   36          var r = (Rule) ruleCombo.getSelectedItem();
   37          canvas.setRule(r.getValue());
   38          explanation.setText(r.getExplanation());
   39      });
   40
   41  alphaSlider = new JSlider(0, 100, 75);
   42  alphaSlider.addChangeListener(event -> canvas.setAlpha(alphaSlider.getValue()));
   43  var panel = new JPanel();
   44  panel.add(ruleCombo);
   45  panel.add(new JLabel("Alpha"));
   46  panel.add(alphaSlider);
   47  add(panel, BorderLayout.NORTH);
   48
   49  explanation = new JTextField();
   50  add(explanation, BorderLayout.SOUTH);
   51
   52  canvas.setAlpha(alphaSlider.getValue());
   53  Rule r = ruleCombo.getItemAt(ruleCombo.getSelectedIndex());
   54  canvas.setRule(r.getValue());
   55  explanation.setText(r.getExplanation());
   56  }
   57  }
```

#### 清单 11.18 composite/CompositeComponent.java

```java
   1  package composite;
   2
   3  import java.awt.*;
   4  import java.awt.geom.*;
   5  import java.awt.image.*;
   6  import javax.swing.*;
   7
   8  /**
   9   * This component draws two shapes, composed with a composition rule.
   10   */
  11 class CompositeComponent extends JComponent
  12 {
  13    private int rule;
  14    private Shape shape1;
  15    private Shape shape2;
  16    private float alpha;
  17
  18    public CompositeComponent()
  19    {
  20       shape1 = new Ellipse2D.Double(100, 100, 150, 100);
  21       shape2 = new Rectangle2D.Double(150, 150, 150, 100);
  22    }
  23
  24    public void paintComponent(Graphics g)
  25    {
  26       var g2 = (Graphics2D) g;
  27
  28       var image = new BufferedImage(getWidth(), getHeight(), BufferedImage.TYPE_INT_ARGB);
  29       Graphics2D gImage = image.createGraphics();
  30       gImage.setPaint(Color.red);
  31       gImage.fill(shape1);
  32       AlphaComposite composite = AlphaComposite.getInstance(rule, alpha);
  33       gImage.setComposite(composite);
  34       gImage.setPaint(Color.blue);
  35       gImage.fill(shape2);
  36       g2.drawImage(image, null, 0, 0);
  37    }
  38
  39    /**
  40     * Sets the composition rule.
  41     * @param r the rule (as an AlphaComposite constant)
  42     */
  43    public void setRule(int r)
  44    {
  45       rule = r;
  46       repaint();
  47    }
  48
  49    /**
  50     * Sets the alpha of the source.
  51     * @param a the alpha value between 0 and 100
  52     */
  53    public void setAlpha(int a)
  54    {
  55       alpha = (float) a / 100.0F;
  56       repaint();
  57    }
  58 }
```

#### 清单 11.19 `composite/Rule.java`

```java
package composite;

import java.awt.*;

/**
 * This class describes a Porter-Duff rule.
 */
class Rule
{
    private String name;
    private String porterDuff1;
    private String porterDuff2;

    /**
     * Constructs a Porter-Duff rule.
     * @param n the rule name
     * @param pd1 the first row of the Porter-Duff square
     * @param pd2 the second row of the Porter-Duff square
     */
    public Rule(String n, String pd1, String pd2)
    {
        name = n;
        porterDuff1 = pd1;
        porterDuff2 = pd2;
    }

    /**
     * Gets an explanation of the behavior of this rule.
     * @return the explanation
     */
    public String getExplanation()
    {
        var r = new StringBuilder("Source ");
        if (porterDuff2.equals("0")) r.append("clears");
        if (porterDuff2.equals("S")) r.append("overwrites");
        if (porterDuff2.equals("DS")) r.append("blends with");
        if (porterDuff2.equals("D")) r.append("alpha modifies");
        if (porterDuff2.equals("1-D")) r.append("alpha complement modifies");
        if (porterDuff2.equals("1")) r.append("does not affect");
        r.append(" destination");
        if (porterDuff1.equals("S")) r.append(" and overwrites empty pixels");
        r.append(".");
        return r.toString();
    }
}
```

你希望处理颜色数据的“栅格”。以下各节将展示如何在 Java 中处理栅格图像。

### 11.4.1 图像的读取器和写入器

`javax.imageio` 包开箱即用地支持读取和写入几种常见文件格式，并提供了一个框架，使第三方能够为其他格式添加读取器和写入器。支持 GIF、JPEG、PNG、BMP（Windows 位图）和 WBMP（无线位图）文件格式。

该库的基本用法非常简单。要加载图像，请使用 `ImageIO` 类的静态 `read` 方法：

```java
File f = ...;
BufferedImage image = ImageIO.read(f);
```

`ImageIO` 类会根据文件类型选择合适的读取器。为此，它可能会检查文件扩展名以及文件开头的“魔数”。如果找不到合适的读取器，或者读取器无法解码文件内容，read 方法会返回 null。

将图像写入文件同样简单：

```java
File f = ...;
String format = ...;
ImageIO.write(image, format, f);
```

这里的格式字符串是标识图像格式的字符串，例如 "JPEG" 或 "PNG"。`ImageIO` 类会选择合适的写入器并保存文件。

#### 11.4.1.1 获取图像文件类型的读取器和写入器

对于超出自 `ImageIO` 类静态 read 和 write 方法范围的更高级图像读取和写入操作，你首先需要获取合适的 `ImageReader` 和 `ImageWriter` 对象。`ImageIO` 类会枚举符合以下条件之一的读取器和写入器：

- 图像格式（例如 "JPEG"）
- 文件后缀（例如 "jpg"）
- MIME 类型（例如 "image/jpeg"）

> **注意：** MIME 是 Multipurpose Internet Mail Extensions（多用途互联网邮件扩展）标准。MIME 标准定义了常见的数据格式，例如 `image/jpeg` 和 `application/pdf`。

例如，你可以按如下方式获取一个读取 JPEG 文件的读取器：

```java
ImageReader reader = null;
Iterator<ImageReader> iter = ImageIO.getImageReadersByFormatName("JPEG");
if (iter.hasNext()) reader = iter.next();
```

getImageReadersBySuffix 和 getImageReadersByMIMEType 方法会枚举匹配文件扩展名或 MIME 类型的读取器。

`ImageIO` 类可能会找到多个都能读取特定图像类型的读取器。在这种情况下，你必须从中选择一个，但如何决定哪一个最好并不明确。要了解某个读取器的更多信息，请获取它的 *服务提供者接口*：

```java
ImageReaderSpi spi = reader.getOriginatingProvider();
```

然后你可以获取供应商名称和版本号：

```java
String vendor = spi.getVendor();
String version = spi.getVersion();
```

也许这些信息能帮助你在这些选择中做出决定——或者你也可以只向程序用户提供一个读取器列表，让他们自行选择。目前，我们假设第一个枚举出的读取器就足够了。

在清单 11.20 的示例程序中，我们希望找到所有可用读取器的所有文件后缀，以便在文件过滤器中使用它们。为此，请使用静态 ImageIO.getReaderFileSuffixes 方法：

```java
String[] extensions = ImageIO.getReaderFileSuffixes();
chooser.setFileFilter(new FileNameExtensionFilter("Image files", extensions));
```

对于保存文件，我们需要多做一些工作。我们希望向用户呈现一个包含所有受支持图像类型的菜单。不幸的是，`ImageIO` 类的 getWriterFormatNames 返回的列表相当奇怪，其中包含冗余名称，例如

```
jpg, BMP, bmp, JPG, jpeg, wbmp, png, JPEG, PNG, WBMP, GIF, gif
```

这不是人们愿意在菜单中呈现的内容。我们需要的是一个“首选”格式名称列表。为此，我们提供了一个辅助方法 getWriterFormats（见清单 11.20）。我们会查找与每个格式名称关联的第一个写入器。然后询问它有哪些格式名称，希望它会首先列出最流行的名称。确实，对于 JPEG 写入器，这样做效果很好——它会在其他选项之前列出 "JPEG"。（另一方面，PNG 写入器会在 "PNG" 之前列出小写的 "png"。我们希望这种行为将来会在某个时候得到解决。目前，我们强制将所有小写名称转为大写。）一旦我们选定了首选名称，就会从原始集合中移除所有替代名称。我们继续这样做，直到处理完所有格式名称。





#### 11.4.1.2 读写包含多幅图像的文件

有些文件（尤其是动态 GIF 文件）包含多幅图像。`ImageIO` 类的 `read` 方法只能读取单幅图像。要读取多幅图像，需要将输入源（例如输入流或文件）转换为 `ImageInputStream`。

```java
InputStream in = ...;
ImageInputStream imageIn = ImageIO.createImageInputStream(in);
```

然后，将图像输入流连接到读取器：

```java
reader.setInput(imageIn, true);
```

第二个参数表示输入处于“仅向前查找”模式。否则，将使用随机访问，要么在读取时缓冲流输入，要么使用随机文件访问。某些操作需要随机访问。例如，要确定 GIF 文件中的图像数量，需要读取整个文件。如果之后还想获取某幅图像，则必须重新读取输入。

只有在从流中读取、输入包含多幅图像且图像格式在头部没有你所请求的信息（例如图像数量）时，这一考虑才重要。如果从文件读取，只需使用

```java
File f = ...;
ImageInputStream imageIn = ImageIO.createImageInputStream(f);
reader.setInput(imageIn);
```

一旦有了读取器，就可以通过调用以下方法读取输入中的图像：

```java
BufferedImage image = reader.read(index);
```

其中 `index` 是图像索引，从 0 开始。

如果输入处于“仅向前查找”模式，则持续读取图像，直到 `read` 方法抛出 `IndexOutOfBoundsException`。否则，可以调用 `getNumImages` 方法：

```java
int n = reader.getNumImages(true);
```

在这里，该参数表示你允许搜索输入以确定图像数量。如果输入处于“仅向前查找”模式，该方法将抛出 `IllegalStateException`。或者，你可以将“允许搜索”参数设置为 `false`。那么，如果无法在不搜索的情况下确定图像数量，`getNumImages` 方法将返回 -1。在这种情况下，你必须改用备选方案，继续读取图像，直到抛出 `IndexOutOfBoundsException`。

某些文件包含缩略图——用于预览的较小版本图像。你可以通过以下调用获取一幅图像的缩略图数量：

```java
int count = reader.getNumThumbnails(index);
```

然后，你可以按如下方式获取特定的缩略图：

```java
BufferedImage thumbnail = reader.getThumbnail(index, thumbnailIndex);
```

有时，你可能希望在真正获取图像之前先获取图像尺寸——尤其是当图像很大或来自较慢的网络连接时。请使用以下调用：

```java
int width = reader.getWidth(index);
int height = reader.getHeight(index);
```

以获取给定索引图像的尺寸。

要写入包含多幅图像的文件，首先需要 `ImageWriter`。`ImageIO` 类可以枚举能够写入特定图像格式的写入器：

```java
String format = ...;
ImageWriter writer = null;
Iterator<ImageWriter> iter = ImageIO.getImageWritersByFormatName(format);
if (iter.hasNext()) writer = iter.next();
```

接下来，将输出流或文件转换为 `ImageOutputStream`，并将其连接到写入器。例如，

```java
File f = ...;
ImageOutputStream imageOut = ImageIO.createImageOutputStream(f);
writer.setOutput(imageOut);
```

你必须将每幅图像包装到 `IIOImage` 对象中。你可以选择提供缩略图列表和图像元数据（例如压缩算法和颜色信息）。在此示例中，我们对两者都使用 `null`；更多信息请参阅 API 文档。

```java
var iioImage = new IIOImage(images[i], null, null);
```

要写出第一幅图像，请使用 `write` 方法：

```java
writer.write(new IIOImage(images[0], null, null));
```

对于后续图像，请使用：

```java
if (writer.canInsertImage(i))
    writer.writeInsert(i, iioImage, null);
```

第三个参数可以包含 `ImageWriteParam` 对象，用于设置图像写入细节，例如平铺和压缩；对于默认值，使用 `null`。

并非所有文件格式都能处理多幅图像。在这种情况下，对于 `i > 0`，`canInsertImage` 方法返回 `false`，并且只保存单幅图像。

清单 11.20 中的程序允许你加载和保存 Java 库提供读取器和写入器的格式的文件。该程序显示多幅图像（见图 11.55），但不显示缩略图。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_771_0.png)

**图 11.55** 一个动态 GIF 图像

##### 清单 11.20 `imageIO/ImageIOFrame.java`

```java
package imageIO;

import java.awt.image.*;
import java.io.*;
import java.util.*;

import javax.imageio.*;
import javax.imageio.stream.*;

import javax.swing.*;
import javax.swing.filechooser.*;

/**
 * This frame displays the loaded images. The menu has items for loading and saving files.
 */
public class ImageIOFrame extends JFrame
{
   private static final int DEFAULT_WIDTH = 400;
   private static final int DEFAULT_HEIGHT = 400;

   private static Set<String> writerFormats = getWriterFormats();

   private BufferedImage[] images;

   public ImageIOFrame()
   {
      setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);

      var fileMenu = new JMenu("File");
      var openItem = new JMenuItem("Open");
      openItem.addActionListener(event -> openFile());
      fileMenu.add(openItem);

      var saveMenu = new JMenu("Save");
      fileMenu.add(saveMenu);
      Iterator<String> iterator = writerFormats.iterator();
      while (iterator.hasNext())
      {
         final String formatName = iterator.next();
         var formatItem = new JMenuItem(formatName);
         saveMenu.add(formatItem);
         formatItem.addActionListener(event -> saveFile(formatName));
      }

      var exitItem = new JMenuItem("Exit");
      exitItem.addActionListener(event -> System.exit(0));
      fileMenu.add(exitItem);

      var menuBar = new JMenuBar();
      menuBar.add(fileMenu);
      setJMenuBar(menuBar);
   }

   /**
    * Open a file and load the images.
    */
   public void openFile()
   {
      var chooser = new JFileChooser();
      chooser.setCurrentDirectory(new File("."));
      String[] extensions = ImageIO.getReaderFileSuffixes();
      chooser.setFileFilter(new FileNameExtensionFilter("Image files", extensions));
      int r = chooser.showOpenDialog(this);
      if (r != JFileChooser.APPROVE_OPTION) return;
      File f = chooser.getSelectedFile();
      Box box = Box.createVerticalBox();
      try
      {
         String name = f.getName();
         String suffix = name.substring(name.lastIndexOf('.') + 1);
         Iterator<ImageReader> iter = ImageIO.getImageReadersBySuffix(suffix);
         ImageReader reader = iter.next();
         ImageInputStream imageIn = ImageIO.createImageInputStream(f);
         reader.setInput(imageIn);
         int count = reader.getNumImages(true);
         images = new BufferedImage[count];
         for (int i = 0; i < count; i++)
         {
            images[i] = reader.read(i);
            box.add(new JLabel(new ImageIcon(images[i])));
         }
      }
      catch (IOException e)
      {
         JOptionPane.showMessageDialog(this, e);
      }
      setContentPane(new JScrollPane(box));
      validate();
   }

   /**
    * Save the current image in a file.
    * @param formatName the file format
    */
   public void saveFile(String formatName)
   {
      if (images == null) return;
      Iterator<ImageWriter> iter = ImageIO.getImageWritersByFormatName(formatName);
      ImageWriter writer = iter.next();
      var chooser = new JFileChooser();
      chooser.setCurrentDirectory(new File("."));
      String[] extensions = writer.getOriginatingProvider().getFileSuffixes();
      chooser.setFileFilter(new FileNameExtensionFilter("Image files", extensions));
      int r = chooser.showSaveDialog(this);
      if (r != JFileChooser.APPROVE_OPTION) return;
      File f = chooser.getSelectedFile();
      try
      {
         ImageOutputStream imageOut = ImageIO.createImageOutputStream(f);
         writer.setOutput(imageOut);

         writer.write(new IIOImage(images[0], null, null));
         for (int i = 1; i < images.length; i++)
         {
            var iioImage = new IIOImage(images[i], null, null);
            if (writer.canInsertImage(i)) writer.writeInsert(i, iioImage, null);
         }
      }
      catch (IOException e)
      {
         JOptionPane.showMessageDialog(this, e);
      }
   }

   /**
    * Gets a set of "preferred" format names of all image writers. The preferred format name
    * is the first format name that a writer specifies.
    * @return the format name set
    */
   public static Set<String> getWriterFormats()
   {
      var writerFormats = new TreeSet<String>();
      var formatNames = List.of(ImageIO.getWriterFormatNames());
      while (formatNames.size() > 0)
      {
         String name = formatNames.iterator().next();
         Iterator<ImageWriter> iter = ImageIO.getImageWritersByFormatName(name);
         ImageWriter writer = iter.next();
         String[] names = writer.getOriginatingProvider().getFormatNames();
         String format = names[0];
         if (format.equals(format.toLowerCase())) format = format.toUpperCase();
         writerFormats.add(format);
         formatNames.removeAll(List.of(names));
      }
      return writerFormats;
   }
}
```





##### javax.imageio.ImageIO 1.4

| 方法 | 描述 |
|---|---|
| - `static BufferedImage read(File input)`<br>- `static BufferedImage read(InputStream input)`<br>- `static BufferedImage read(URL input)` | 从输入中读取图像。 |
| - `static boolean write(RenderedImage image, String formatName, File output)`<br>- `static boolean write(RenderedImage image, String formatName, OutputStream output)` | 将给定格式的图像写入输出。如果未找到合适的写入器，则返回 false。 |
| - `static Iterator<ImageReader> getImageReadersByFormatName(String formatName)`<br>- `static Iterator<ImageReader> getImageReadersBySuffix(String fileSuffix)`<br>- `static Iterator<ImageReader> getImageReadersByMIMEType(String mimeType)`<br>- `static Iterator<ImageWriter> getImageWritersByFormatName(String formatName)`<br>- `static Iterator<ImageWriter> getImageWritersBySuffix(String fileSuffix)`<br>- `static Iterator<ImageWriter> getImageWritersByMIMEType(String mimeType)` | 获取能够处理给定格式（例如 "JPEG"）、文件后缀（例如 ".jpg"）或 MIME 类型（例如 "image/jpeg"）的所有读取器和写入器。 |
| - `static String[] getReaderFormatNames()`<br>- `static String[] getReaderMIMETypes()`<br>- `static String[] getWriterFormatNames()`<br>- `static String[] getWriterMIMETypes()`<br>- `static String[] getReaderFileSuffixes()`<br>- `static String[] getWriterFileSuffixes()` | 获取读取器和写入器支持的所有格式名称、MIME 类型名称和文件后缀。 |
| - `static ImageInputStream createImageInputStream(Object input)`<br>- `static ImageOutputStream createImageOutputStream(Object output)` | 根据给定对象创建图像输入流或图像输出流。该对象可以是文件、流、`RandomAccessFile`，或存在服务提供者的其他对象。如果没有注册的服务提供者能够处理该对象，则返回 null。 |

##### javax.imageio.ImageReader 1.4

| 方法 | 描述 |
|---|---|
| - `void setInput(Object input)`<br>- `void setInput(Object input, boolean seekForwardOnly)` | 设置读取器的输入源。<br><br>**参数：**<br>`input` — 一个 `ImageInputStream` 对象或此读取器可以接受的其他对象。<br>`seekForwardOnly` — 如果读取器应仅向前读取，则为 true。默认情况下，读取器使用随机访问，并在必要时缓冲图像数据。 |
| - `BufferedImage read(int index)` | 读取具有给定图像索引（从 0 开始）的图像。如果不存在这样的图像，则抛出 `IndexOutOfBoundsException`。 |
| - `int getNumImages(boolean allowSearch)` | 获取此读取器中的图像数量。如果 `allowSearch` 为 false，并且不向前读取就无法确定图像数量，则返回 -1。如果 `allowSearch` 为 true，且读取器处于“仅向前查找”模式，则抛出 `IllegalStateException`。 |
| - `int getNumThumbnails(int index)` | 获取具有给定索引的图像的缩略图数量。 |
| - `BufferedImage readThumbnail(int index, int thumbnailIndex)` | 获取具有给定索引的图像的、具有给定 `thumbnailIndex` 的缩略图。 |
| - `int getWidth(int index)`<br>- `int getHeight(int index)` | 获取图像宽度和高度。如果不存在这样的图像，则抛出 `IndexOutOfBoundsException`。 |
| - `ImageReaderSpi getOriginatingProvider()` | 获取构造此读取器的服务提供者。 |

##### javax.imageio.spi.IIOServiceProvider 1.4

| 方法 | 描述 |
|---|---|
| - `String getVendorName()`<br>- `String getVersion()` | 获取此服务提供者的供应商名称和版本。 |

##### javax.imageio.spi.ImageReaderWriterSpi 1.4

| 方法 | 描述 |
|---|---|
| - `String[] getFormatNames()`<br>- `String[] getFileSuffixes()`<br>- `String[] getMIMETypes()` | 获取此服务提供者创建的读取器或写入器所支持的格式名称、文件后缀和 MIME 类型。 |

##### javax.imageio.ImageWriter 1.4

| 方法 | 描述 |
|---|---|
| - `void setOutput(Object output)` | 设置此写入器的输出目标。<br><br>**参数：**<br>`output` — 一个 `ImageOutputStream` 对象或此写入器可以接受的其他对象 |
| - `void write(IIOImage image)`<br>- `void write(RenderedImage image)` | 将单个图像写入输出。 |
| - `void writeInsert(int index, IIOImage image, ImageWriteParam param)` | 将图像写入多图像文件。 |
| - `boolean canInsertImage(int index)` | 如果可以在给定索引处插入图像，则返回 true。 |
| - `ImageWriterSpi getOriginatingProvider()` | 获取构造此写入器的服务提供者。 |

##### javax.imageio.IIOImage 1.4

| 方法 | 描述 |
|---|---|
| - `IIOImage(RenderedImage image, List thumbnails, IIOMetadata metadata)` | 根据图像、可选缩略图和可选元数据构造一个 IIOImage。 |

### 11.4.2 图像操作

假设你有一幅图像，并希望改善其外观。那么你需要访问图像中的各个像素，并用其他像素替换它们。或者，你可能希望从头计算图像的像素——例如，显示物理测量或数学计算的结果。`BufferedImage` 类让你可以控制图像中的像素，而实现 `BufferedImageOp` 接口的类则让你可以变换图像。

> **注意：** JDK 1.0 有一个完全不同且复杂得多的成像框架，该框架针对从 Web 下载的图像的*增量渲染*进行了优化，每次一行扫描线。然而，操作那些图像很困难。本书不讨论该框架。

#### 11.4.2.1 构造光栅图像

你操作的大多数图像只是从图像文件中读取的——它们要么由数码相机或扫描仪等设备生成，要么由绘图程序构造。在本节中，我们将向你展示一种不同的构造图像的技术——即逐像素构建图像。

要创建图像，按常规方式构造一个 `BufferedImage` 对象。

```java
image = new BufferedImage(width, height, BufferedImage.TYPE_INT_ARGB);
```

现在，调用 `getRaster` 方法获取一个 `WritableRaster` 类型的对象。你将使用该对象访问和修改图像的像素。

```java
WritableRaster raster = image.getRaster();
```

`setPixel` 方法允许你设置单个像素。这里的复杂之处在于，你不能简单地将像素设置为一个 `Color` 值。你必须了解缓冲图像如何指定颜色值。这取决于图像的*类型*。如果你的图像类型为 `TYPE_INT_ARGB`，那么每个像素由四个值描述——红色、绿色、蓝色和 alpha，每个值介于 0 和 255 之间。你必须在由四个整数组成的数组中提供它们：

```java
int[] black = { 0, 0, 0, 255 };
raster.setPixel(i, j, black);
```

在 Java 2D API 的术语中，这些值称为像素的*样本值*。

> **注意：** 也有一些 setPixel 方法接受 `float[]` 和 `double[]` 类型的数组参数。但是，你需要放入这些数组的值**不是**介于 `0.0` 和 `1.0` 之间的归一化颜色值。

```java
float[] red = { 1.0F, 0.0F, 0.0F, 1.0F };
raster.setPixel(i, j, red); // ERROR
```

无论数组是什么类型，你都需要提供 0 到 255 之间的值。

你可以使用 setPixels 方法提供一批像素。指定起始像素位置以及要设置的矩形的宽度和高度。然后，提供一个包含所有像素样本值的数组。例如，如果你的缓冲图像类型为 `TYPE_INT_ARGB`，请提供第一个像素的红色、绿色、蓝色和 alpha 值，然后提供第二个像素的红色、绿色、蓝色和 alpha 值。

```java
var pixels = new int[4 * width * height];
pixels[0] = ...; // red value for first pixel
pixels[1] = ...; // green value for first pixel
pixels[2] = ...; // blue value for first pixel
pixels[3] = ...; // alpha value for first pixel
...
raster.setPixels(x, y, width, height, pixels);
```

反过来，要读取像素，请使用 getPixel 方法。提供一个包含四个整数的数组来保存样本值。

```java
var sample = new int[4];
raster.getPixel(x, y, sample);
var color = new Color(sample[0], sample[1], sample[2], sample[3]);
```

你可以使用 getPixels 方法读取多个像素。

```java
raster.getPixels(x, y, width, height, samples);
```

如果你使用的图像类型不是 `TYPE_INT_ARGB`，并且你知道该类型如何表示像素值，你仍然可以使用 getPixel/setPixel 方法。但是，你必须了解样本值在特定图像类型中的编码方式。

如果你需要处理任意未知图像类型的图像，那么你必须多费点功夫。每种图像类型都有一个颜色模型，可以在样本值数组和标准 RGB 颜色模型之间进行转换。




> **注意：** RGB 颜色模型并不像你可能认为的那样标准。颜色值的确切外观取决于成像设备的特性。数码相机、扫描仪、显示器和 LCD 显示器都有各自的特性。因此，同一个 RGB 值在不同设备上可能看起来差异很大。国际色彩联盟（www.color.org）建议所有颜色数据都附带一个 *ICC 配置文件*，用于指定颜色如何映射到标准形式，例如 1931 CIE XYZ 颜色规范。该规范由国际照明委员会（Commission Internationale de l’Éclairage，简称 CIE，www.cie.co.at）设计，该国际组织负责在照明和颜色的一切事务中提供技术指导。该规范是一种标准方法，用于将人眼可感知的任何颜色表示为称为 X、Y、Z 的坐标三元组。（例如，参见 James D. Foley、Andries van Dam、Steven K. Feiner 等人所著的 *《计算机图形学：原理与实践（第二版，C 语言版）》* 第 13 章，了解关于 1931 CIE XYZ 规范的更多信息。）
>
> 然而，ICC 配置文件很复杂。一个更简单的拟议标准称为 sRGB（www.w3.org/Images/Color/sRGB.html），它规定了 RGB 值与 1931 CIE XYZ 值之间的精确映射，旨在与典型的彩色显示器良好配合。Java 2D API 在 RGB 与其他颜色空间之间转换时使用该映射。

`getColorModel` 方法返回颜色模型：

```java
ColorModel model = image.getColorModel();
```

要查找像素的颜色值，请调用 `Raster` 类的 `getDataElements` 方法。该调用返回一个对象，其中包含特定于颜色模型的对颜色值的描述。

```java
Object data = raster.getDataElements(x, y, null);
```

> **注意：** `getDataElements` 方法返回的对象实际上是一个样本值数组。处理该对象时你不需要知道这一点，但这解释了该方法为何名为 `getDataElements`。

颜色模型可以将该对象转换为标准 ARGB 值。`getRGB` 方法返回一个 int 值，其中 alpha、红、绿、蓝值分别打包在四个 8 位块中。你可以使用 `Color(int argb)` 构造函数根据该整数构造颜色值：

```java
int argb = model.getRGB(data);
var color = new Color(argb, true);
```

要将像素设置为特定颜色，请反向执行这些步骤。`Color` 类的 `getRGB` 方法会生成一个 `int` 值，其中包含 alpha、红、绿、蓝值。将该值提供给 `ColorModel` 类的 `getDataElements` 方法。返回值是一个 `Object`，其中包含特定于颜色模型的对颜色值的描述。将该对象传递给 `WritableRaster` 类的 `setDataElements` 方法。

```java
int argb = color.getRGB();
Object data = model.getDataElements(argb, null);
raster.setDataElements(x, y, data);
```

为了说明如何使用这些方法从单个像素构建图像，我们遵循传统，绘制一个曼德博集合，如图 11.56 所示。

曼德博集合的思想是：平面上的每个点都关联一个数列。如果该数列保持有界，就为该点着色。如果它“逃逸到无穷大”，就将其保留为透明。

下面说明如何构造最简单的曼德博集合。对于每个点 $(a, b)$，考察从 $(x, y) = (0, 0)$ 开始并迭代的序列：

$$x_{new} = x^2 - y^2 + a$$

$$y_{new} = 2 \cdot x \cdot y + b$$

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_781_0.png)

**图 11.56** 曼德博集合

事实证明，如果 $x$ 或 $y$ 一旦大于 2，该序列就会逃逸到无穷大。只有对应于产生有界序列的点 $(a, b)$ 的像素才会着色。（这些数列公式最终来自复数数学；我们这里直接接受它们。）

程序清单 11.21 展示了代码。在这个程序中，我们演示如何使用 `ColorModel` 类将颜色值转换为像素数据。该过程与图像类型无关。只是为了好玩，可以将缓冲图像的颜色类型改为 `TYPE_BYTE_GRAY`。你不需要修改任何其他代码——图像的颜色模型会自动负责从颜色到样本值的转换。

##### 清单 11.21 `rasterImage/RasterImageFrame.java`

```java
package rasterImage;

import java.awt.*;
import java.awt.image.*;
import javax.swing.*;

/**
 * This frame shows an image with a Mandelbrot set.
 */
public class RasterImageFrame extends JFrame
{
    private static final double XMIN = -2;
    private static final double XMAX = 2;
    private static final double YMIN = -2;
    private static final double YMAX = 2;
    private static final int IMAGE_ITERATIONS = 16;
    private static final int IMAGE_WIDTH = 400;
    private static final int IMAGE_HEIGHT = 400;

    public RasterImageFrame()
    {
        BufferedImage image = makeMandelbrot(IMAGE_WIDTH, IMAGE_HEIGHT);
        add(new JLabel(new ImageIcon(image)));
        pack();
    }

    /**
     * Makes the Mandelbrot image.
     * @param width the width
     * @param height the height
     * @return the image
     */
    public BufferedImage makeMandelbrot(int width, int height)
    {
        var image = new BufferedImage(width, height, BufferedImage.TYPE_INT_ARGB);
        WritableRaster raster = image.getRaster();
        ColorModel model = image.getColorModel();

        Color fractalColor = Color.RED;
        int argb = fractalColor.getRGB();
        Object colorData = model.getDataElements(argb, null);

        for (int i = 0; i < width; i++)
        {
            for (int j = 0; j < height; j++)
            {
                double a = XMIN + i * (XMAX - XMIN) / width;
                double b = YMIN + j * (YMAX - YMIN) / height;
                if (!escapesToInfinity(a, b)) raster.setDataElements(i, j, colorData);
            }
        }
        return image;
    }

    private boolean escapesToInfinity(double a, double b)
    {
        double x = 0.0;
        double y = 0.0;
        int iterations = 0;
        while (x <= 2 && y <= 2 && iterations < IMAGE_ITERATIONS)
        {
            double xnew = x * x - y * y + a;
            double ynew = 2 * x * y + b;
            x = xnew;
            y = ynew;
            iterations++;
        }
        return x > 2 || y > 2;
    }
}
```

##### java.awt.image.BufferedImage 1.2

- `BufferedImage(int width, int height, int imageType)`  
  构造一个缓冲图像对象。

| 参数 |  |
| --- | --- |
| `width`、`height` | 图像尺寸 |
| `imageType` | 图像类型。最常见的类型是 `TYPE_INT_RGB`、`TYPE_INT_ARGB`、`TYPE_BYTE_GRAY` 和 `TYPE_BYTE_INDEXED`。 |

##### java.awt.image.BufferedImage 1.2（续）

- `ColorModel getColorModel()`  
  返回此缓冲图像的颜色模型。
- `WritableRaster getRaster()`  
  获取用于访问和修改此缓冲图像像素的栅格。

##### java.awt.image.Raster 1.2

- `Object getDataElements(int x, int y, Object data)`  
  返回栅格点的样本数据，放在一个数组中，其元素类型和长度取决于颜色模型。如果 data 不为 null，则假定它是一个适合保存样本数据的数组，并将其填充。如果 data 为 null，则分配一个新数组。其元素类型和长度取决于颜色模型。
- `int[] getPixel(int x, int y, int[] sampleValues)`
- `float[] getPixel(int x, int y, float[] sampleValues)`
- `double[] getPixel(int x, int y, double[] sampleValues)`
- `int[] getPixels(int x, int y, int width, int height, int[] sampleValues)`
- `float[] getPixels(int x, int y, int width, int height, float[] sampleValues)`
- `double[] getPixels(int x, int y, int width, int height, double[] sampleValues)`

返回栅格点或栅格点矩形的样本值，放在一个数组中，其长度取决于颜色模型。如果 sampleValues 不为 null，则假定它足够长以保存样本值，并将其填充。如果 sampleValues 为 null，则分配一个新数组。只有当你了解某个颜色模型的样本值的含义时，这些方法才有用。

##### java.awt.image.WritableRaster 1.2

- `void setDataElements(int x, int y, Object data)`  
  设置栅格点的样本数据。data 是一个填有像素样本数据的数组。其元素类型和长度取决于颜色模型。
- `void setPixel(int x, int y, int[] sampleValues)`
- `void setPixel(int x, int y, float[] sampleValues)`
- `void setPixel(int x, int y, double[] sampleValues)`
- `void setPixels(int x, int y, int width, int height, int[] sampleValues)`
- `void setPixels(int x, int y, int width, int height, float[] sampleValues)`
- `void setPixels(int x, int y, int width, int height, double[] sampleValues)`

设置栅格点或栅格点矩形的样本值。只有当你了解某个颜色模型的样本值的编码时，这些方法才有用。




| `java.awt.image.ColorModel` | 1.2 |
|---|---|
| `int getRGB(Object data)` | 返回与传入的 data 数组中的样本数据对应的 ARGB 值。其元素类型和长度取决于颜色模型。 |
| `Object getDataElements(int argb, Object data);` | 返回某个颜色值的样本数据。如果 data 不为 null，则假定它是一个适合保存样本数据的数组，并对其进行填充。如果 data 为 null，则分配一个新数组，并用该像素的样本数据填充它。其元素类型和长度取决于颜色模型。 |

| `java.awt.Color` | 1.0 |
|---|---|
| `Color(int argb, boolean hasAlpha)` 1.2 | 如果 hasAlpha 为 true，则创建具有指定组合 ARGB 值的颜色；如果 hasAlpha 为 false，则创建具有指定 RGB 值的颜色。 |
| `int getRGB()` | 返回与此颜色对应的 ARGB 颜色值。 |

#### 11.4.2.2 过滤图像

在上一节中，你了解了如何从零开始构建图像。然而，你常常出于不同的原因想要访问图像数据：你已经有一幅图像，并想以某种方式改进它。

当然，你可以使用上一节中看到的 getPixel/getDataElements 方法来读取图像数据、操作它们并将它们写回。幸运的是，Java 2D API 已经提供了许多滤镜，可以为你执行常见的图像处理操作。

这些图像操作都实现了 `BufferedImageOp` 接口。构造操作后，只需调用 filter 方法即可将一幅图像转换为另一幅图像。

```java
BufferedImageOp op = . . .;
BufferedImage filteredImage
    = new BufferedImage(image.getWidth(), image.getHeight(), image.getType());
op.filter(image, filteredImage);
```

有些操作可以原地变换图像（`op.filter(image, image)`），但大多数操作不能。

有五个类实现了 `BufferedImageOp` 接口：

- `AffineTransformOp`
- `RescaleOp`
- `LookupOp`
- `ColorConvertOp`
- `ConvolveOp`

`AffineTransformOp` 对像素执行仿射变换。例如，下面是如何围绕图像中心旋转图像：

```java
AffineTransform transform = AffineTransform.getRotateInstance(Math.toRadians(angle),
    image.getWidth() / 2, image.getHeight() / 2);
var op = new AffineTransformOp(transform, interpolation);
op.filter(image, filteredImage);
```

`AffineTransformOp` 构造函数需要一个仿射变换和一个插值策略。如果源像素被变换到目标像素之间的某个位置，就需要插值来确定目标图像像素。例如，如果旋转源像素，它们通常不会正好落在目标像素上。有三种插值策略：`AffineTransformOp.TYPE_BICUBIC`、`AffineTransformOp.TYPE_BILINEAR` 和 `AffineTransformOp.TYPE_NEAREST_NEIGHBOR`。双三次插值花费的时间稍长，但看起来比另外两种更好。

代码清单 11.22 中的程序可以让你将图像旋转 5 度（见图 11.57）。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_786_0.png)

**图 11.57** 旋转后的图像

`RescaleOp` 对图像中的每个颜色分量执行重新缩放操作

$$x_{new} = a \cdot x + b$$

（Alpha 分量不受影响。）使用 `a > 1` 进行重新缩放的效果是使图像变亮。通过指定缩放参数和可选的渲染提示来构造 `RescaleOp`。在代码清单 11.22 中，我们使用：

```java
float a = 1.1f;
float b = 20.0f;
var op = new RescaleOp(a, b, null);
```

你还可以为每个颜色分量提供单独的缩放值——参见 API 注释。

`LookupOp` 操作让你可以指定样本值的任意映射。提供一个表，指定每个值应如何映射。在示例程序中，我们计算所有颜色的*负片*，将颜色 `c` 变为 `255 - c`。

`LookupOp` 构造函数需要一个 `LookupTable` 类型的对象和一个可选提示的映射。`LookupTable` 类是抽象类，有两个具体子类：`ByteLookupTable` 和 `ShortLookupTable`。由于 RGB 颜色值是字节，`ByteLookupTable` 应该足够了。然而，由于 http://bugs.sun.com/bugdatabase/view_bug.do?bug_id=4818321 中描述的 bug，我们将改用 `ShortLookupTable`。下面是我们为示例程序构造 `LookupOp` 的方式：

```java
var negative = new short[256];
for (int i = 0; i < 256; i++) negative[i] = (short) (255 - i);
var table = new ShortLookupTable(0, negative);
var op = new LookupOp(table, null);
```

查找会分别应用于每个颜色分量，但不会应用于 Alpha 分量。你还可以为每个颜色分量提供不同的查找表——参见 API 注释。

> **注意：** 不能将 `LookupOp` 应用于具有索引颜色模型的图像。（在这些图像中，每个样本值都是颜色调色板中的偏移量。）

`ColorConvertOp` 可用于颜色空间转换。这里不讨论它。

这些变换中最强大的是 `ConvolveOp`，它执行数学上的*卷积*。我们不会深入讨论数学细节，但基本思想很简单。例如，考虑*模糊滤镜*（见图 11.58）。

模糊是通过将每个像素替换为该像素及其八个邻居的*平均值*来实现的。直观上，可以理解为什么这个操作会使图像变模糊。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_788_0.png)

**图 11.58** 模糊图像

从数学上讲，求平均可以表示为使用以下*核*的卷积操作：

$$\begin{bmatrix} 1/9 & 1/9 & 1/9 \\ 1/9 & 1/9 & 1/9 \\ 1/9 & 1/9 & 1/9 \end{bmatrix}$$

卷积的核是一个矩阵，它说明应对相邻值应用什么权重。上面的核会产生模糊图像。不同的核执行*边缘检测*，定位颜色变化的区域：

$$\begin{bmatrix} 0 & -1 & 0 \\ -1 & 4 & -1 \\ 0 & -1 & 0 \end{bmatrix}$$

边缘检测是分析摄影图像的重要技术（见图 11.59）。

要构造卷积操作，首先设置核值的数组并构造一个 Kernel 对象。然后，从该核构造一个 ConvolveOp 对象，并将其用于过滤。

```java
float[] elements =
{
    0.0f, -1.0f, 0.0f,
   -1.0f,  4.0f, -1.0f,
    0.0f, -1.0f, 0.0f
};
```

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_789_0.png)

**图 11.59** 边缘检测与反色

```java
var kernel = new Kernel(3, 3, elements);
var op = new ConvolveOp(kernel);
op.filter(image, filteredImage);
```

代码清单 11.22 中的程序允许用户加载 GIF 或 JPEG 图像，并执行我们讨论过的图像操作。得益于 Java 2D API 提供的强大操作，这个程序非常简单。

**代码清单 11.22** `ImageProcessing/ImageProcessingFrame.java`

```java
package imageProcessing;

import java.awt.*;
import java.awt.event.*;
import java.awt.image.*;
import java.io.*;

import javax.imageio.*;
import javax.swing.*;
import javax.swing.filechooser.*;

/**
 * This frame has a menu to load an image and to specify various transformations, and a
 * component to show the resulting image.
 */
public class ImageProcessingFrame extends JFrame
{
   private static final int DEFAULT_WIDTH = 400;
   private static final int DEFAULT_HEIGHT = 400;

   private BufferedImage image;

   public ImageProcessingFrame()
   {
      setTitle("ImageProcessingTest");
      setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);

      add(new JComponent()
         {
            public void paintComponent(Graphics g)
            {
               if (image != null) g.drawImage(image, 0, 0, null);
            }
         });

      var fileMenu = new JMenu("File");
      var openItem = new JMenuItem("Open");
      openItem.addActionListener(event -> openFile());
      fileMenu.add(openItem);

      var exitItem = new JMenuItem("Exit");
      exitItem.addActionListener(event -> System.exit(0));
      fileMenu.add(exitItem);

      var editMenu = new JMenu("Edit");
      var blurItem = new JMenuItem("Blur");
      blurItem.addActionListener(event ->
         {
            float weight = 1. / 9.0f;
            float[] elements = new float[9];
            for (int i = 0; i < 9; i++)
               elements[i] = weight;
            convolve(elements);
         });
      editMenu.add(blurItem);

      var sharpenItem = new JMenuItem("Sharpen");
      sharpenItem.addActionListener(event ->
         {
            float[] elements = { 0.0f, -1.0f, 0.0f, -1.0f, 5.f, -1.0f, 0.0f, -1.0f, 0.0f };
            convolve(elements);
         });
      editMenu.add(sharpenItem);
```



```java
var brightenItem = new JMenuItem("Brighten");
brightenItem.addActionListener(event ->
{
    float a = 1.1f;
    float b = 20.0f;
    var op = new RescaleOp(a, b, null);
    filter(op);
});
editMenu.add(brightenItem);

var edgeDetectItem = new JMenuItem("Edge detect");
edgeDetectItem.addActionListener(event ->
{
    float[] elements = { 0.0f, -1.0f, 0.0f, -1.0f, 4.f, -1.0f, 0.0f, -1.0f, 0.0f };
    convolve(elements);
});
editMenu.add(edgeDetectItem);

var negativeItem = new JMenuItem("Negative");
negativeItem.addActionListener(event ->
{
    short[] negative = new short[256 * 1];
    for (int i = 0; i < 256; i++)
        negative[i] = (short) (255 - i);
    var table = new ShortLookupTable(0, negative);
    var op = new LookupOp(table, null);
    filter(op);
});
editMenu.add(negativeItem);

var rotateItem = new JMenuItem("Rotate");
rotateItem.addActionListener(event ->
{
    if (image == null) return;
    var transform = AffineTransform.getRotateInstance(Math.toRadians(5),
        image.getWidth() / 2, image.getHeight() / 2);
    var op = new AffineTransformOp(transform,
        AffineTransformOp.TYPE_BICUBIC);
    filter(op);
});
editMenu.add(rotateItem);

var menuBar = new JMenuBar();
menuBar.add(fileMenu);
menuBar.add(editMenu);
setJMenuBar(menuBar);
}
```

##### 清单 11.22 *（续）*

```java
/**
 * Open a file and load the image.
 */
public void openFile()
{
    var chooser = new JFileChooser(".");
    chooser.setCurrentDirectory(new File(getClass().getPackage().getName()));
    String[] extensions = ImageIO.getReaderFileSuffixes();
    chooser.setFileFilter(new FileNameExtensionFilter("Image files", extensions));
    int r = chooser.showOpenDialog(this);
    if (r != JFileChooser.APPROVE_OPTION) return;

    try
    {
        Image img = ImageIO.read(chooser.getSelectedFile());
        image = new BufferedImage(img.getWidth(null), img.getHeight(null),
                BufferedImage.TYPE_INT_RGB);
        image.getGraphics().drawImage(img, 0, 0, null);
    }
    catch (IOException e)
    {
        JOptionPane.showMessageDialog(this, e);
    }
    repaint();
}

/**
 * Apply a filter and repaint.
 * @param op the image operation to apply
 */
private void filter(BufferedImageOp op)
{
    if (image == null) return;
    image = op.filter(image, null);
    repaint();
}

/**
 * Apply a convolution and repaint.
 * @param elements the convolution kernel (an array of 9 matrix elements)
 */
private void convolve(float[] elements)
{
    var kernel = new Kernel(3, 3, elements);
    var op = new ConvolveOp(kernel);
    filter(op);
}
```

##### java.awt.image.BufferedImageOp 1.2

- `BufferedImage filter(BufferedImage source, BufferedImage dest)`

将图像操作应用于源图像，并将结果存储到目标图像中。如果 dest 为 null，则创建一个新的目标图像。返回目标图像。

##### java.awt.image.AffineTransformOp 1.2

- `AffineTransformOp(AffineTransform t, int interpolationType)`

构造一个仿射变换运算符。插值类型为 `TYPE_BILINEAR`、`TYPE_BICUBIC` 或 `TYPE_NEAREST_NEIGHBOR` 之一。

##### java.awt.image.RescaleOp 1.2

- `RescaleOp(float a, float b, RenderingHints hints)`
- `RescaleOp(float[] a, float[] b, RenderingHints hints)`

构造一个重新缩放运算符，执行缩放操作 \(x_{\mathrm{new}} = a \cdot x + b\)。使用第一个构造函数时，所有颜色分量（但不包括 alpha 分量）都用相同的系数缩放。使用第二个构造函数时，可以提供每个颜色分量的值（此时 alpha 分量不受影响），也可以提供 alpha 分量和颜色分量的值。

##### java.awt.image.LookupOp 1.2

- `LookupOp(LookupTable table, RenderingHints hints)`

为给定的查找表构造一个查找运算符。

##### java.awt.image.ByteLookupTable 1.2

- `ByteLookupTable(int offset, byte[] data)`
- `ByteLookupTable(int offset, byte[][] data)`

构造一个用于转换 byte 值的查找表。在查找之前，从输入中减去偏移量。第一个构造函数中的值应用于所有颜色分量，但不应用于 alpha 分量。使用第二个构造函数时，可以提供每个颜色分量的值（此时 alpha 分量不受影响），也可以提供 alpha 分量和颜色分量的值。

| `java.awt.image.ShortLookupTable` 1.2 |
|:---|
| - `ShortLookupTable(int offset, short[] data)`<br>- `ShortLookupTable(int offset, short[][] data)`<br><br>构造一个用于转换 short 值的查找表。在查找之前，从输入中减去偏移量。第一个构造函数中的值应用于所有颜色分量，但不应用于 alpha 分量。使用第二个构造函数时，可以提供每个颜色分量的值（此时 alpha 分量不受影响），也可以提供 alpha 分量和颜色分量的值。 |

| `java.awt.image.ConvolveOp` 1.2 |
|:---|
| - `ConvolveOp(Kernel kernel)`<br>- `ConvolveOp(Kernel kernel, int edgeCondition, RenderingHints hints)`<br><br>构造一个卷积运算符。指定的边缘条件为 `EDGE_NO_OP` 和 `EDGE_ZERO_FILL` 之一。边缘值需要特殊处理，因为它们没有足够的相邻值来计算卷积。默认值为 `EDGE_ZERO_FILL`。 |

| `java.awt.image.Kernel` 1.2 |
|:---|
| - `Kernel(int width, int height, float[] matrixElements)`<br><br>为给定矩阵构造一个核。 |

## 11.5 打印

在以下各节中，我们将展示如何轻松地将绘图打印到单张纸上、如何管理多页打印输出，以及如何将打印输出保存为 PostScript 文件。

### 11.5.1 图形打印

在本节中，我们将处理可能是最常见的打印情形：打印二维图形。当然，图形可以包含各种字体的文本，甚至可以完全由文本组成。

要生成打印输出，必须处理以下两项任务：

- 提供一个实现 `Printable` 接口的对象
- 启动一个打印作业

Printable 接口只有一个方法：

```java
int print(Graphics g, PageFormat format, int page)
```

每当打印引擎需要格式化页面以便打印时，就会调用该方法。你的代码将要打印的文本和图像绘制到图形上下文中。页面格式告诉你纸张大小和打印边距。页码告诉你应渲染哪一页。

要启动打印作业，请使用 PrinterJob 类。首先，调用静态 getPrinterJob 方法获取打印作业对象。然后设置要打印的 Printable 对象。

```java
Printable canvas = ...;
PrinterJob job = PrinterJob.getPrinterJob();
job.setPrintable(canvas);
```

> **注意：** PrintJob 类处理 JDK 1.1 风格的打印。该类现已过时。不要将其与 PrinterJob 类混淆。

在启动打印作业之前，应调用 printDialog 方法显示打印对话框（参见图 11.60）。该对话框让用户有机会选择要使用的打印机（如果有多个打印机可用）、应打印的页面范围以及各种打印机设置。

将打印机设置收集到实现 PrintRequestAttributeSet 接口的类的对象中，例如 HashPrintRequestAttributeSet 类。

```java
var attributes = new HashPrintRequestAttributeSet();
```

添加属性设置，并将 attributes 对象传递给 printDialog 方法。

如果用户单击“确定”，printDialog 方法返回 true；如果用户取消对话框，则返回 false。如果用户接受，则调用 PrinterJob 类的 print 方法开始打印过程。print 方法可能抛出 PrinterException。以下是打印代码的概要：

```java
if (job.printDialog(attributes))
{
    try
    {
        job.print(attributes);
    }
    catch (PrinterException exception)
    {
        . . .
    }
}
```


![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_796_0.png)

**图 11.60** 跨平台打印对话框

> **注意：** 在 JDK 1.4 之前，打印系统使用宿主平台的原生打印和页面设置对话框。要显示原生打印对话框，请调用不带参数的 `printDialog` 方法。（无法在属性集中收集用户设置。）

在打印过程中，`PrinterJob` 类的 `print` 方法会重复调用与该任务关联的 `Printable` 对象的 `print` 方法。

由于打印任务不知道你要打印多少页，它只会持续调用 `print` 方法。只要 `print` 方法返回 `Printable.PAGE_EXISTS` 值，打印任务就会继续生成页面。当 `print` 方法返回 `Printable.NO_SUCH_PAGE` 时，打印任务停止。

> **警告：** 打印任务传递给 `print` 方法的页码从第 0 页开始。

因此，在打印输出完成之前，打印任务无法获得准确的页数。因此，打印对话框无法显示正确的页面范围，而是显示“第 1 页到第 1 页”。在下一节中，你将看到如何通过向打印任务提供 `Book` 对象来避免这个瑕疵。

在打印过程中，打印任务会重复调用 `Printable` 对象的 `print` 方法。打印任务可能会对*同一页*进行多次调用。因此，你不应在 `print` 方法中统计页数，而应始终依赖页码参数。打印任务对同一页重复调用 `print` 方法是有充分理由的。某些打印机，尤其是针式打印机和喷墨打印机，使用 `banding`。它们一次打印一个条带，进纸，然后再打印下一个条带。即使是每次打印一整页的激光打印机，打印任务也可能使用 banding——这为打印任务提供了一种管理后台打印文件大小的方法。

如果打印任务需要 `Printable` 对象来打印一个条带，它会将 `Graphics` 上下文的裁剪区域设置为所请求的条带，然后调用 `print` 方法。其绘制操作会针对条带矩形进行裁剪，只有出现在条带中的绘制元素才会被渲染。你的 `print` 方法不必意识到这一过程，但有一个注意事项：它*不应*干扰裁剪区域。

> **警告：** 你的 `print` 方法得到的 `Graphics` 对象也会根据页面边距进行裁剪。如果你替换了裁剪区域，可能会在边距之外绘图。尤其是在打印机图形上下文中，必须遵守裁剪区域。请调用 `clip`，*而不是* `setClip`，以进一步限制裁剪区域。如果必须移除裁剪区域，请确保在 `print` 方法开头调用 `getClip` 并恢复该裁剪区域。

`print` 方法的 `PageFormat` 参数包含有关所打印页面的信息。`getWidth` 和 `getHeight` 方法返回纸张尺寸，以*点*为单位。（1 点等于 1/72 英寸；1 英寸等于 25.4 毫米。）例如，A4 纸约为 595 × 842 点，美国信纸为 612 × 792 点。

点是美国印刷行业常用的度量单位。令世界其他地方大为懊恼的是，这个打印包使用点作为单位。这有两个目的：纸张尺寸和纸张边距以*点*为单位，并且点是所有打印图形上下文的默认单位。你可以在本节末尾的示例程序中验证这一点。该程序打印两行间隔为 72 个单位的文本。运行示例程序并测量基线之间的距离；它们恰好相隔 1 英寸或 25.4 毫米。

`PageFormat` 类的 `getWidth` 和 `getHeight` 方法给出完整的纸张尺寸。并非所有纸张区域都可打印。用户通常会选择边距，即使他们不选择，打印机也需要以某种方式夹住要打印的纸张，因此边缘周围会有一小块不可打印区域。

`getImageableWidth` 和 `getImageableHeight` 方法告诉你实际可以填充的区域的尺寸。然而，边距不一定是对称的，因此你还需要知道可成像区域的左上角（见图 11.61），可以通过 `getImageableX` 和 `getImageableY` 方法获取。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_798_0.png)

**图 11.61** 页面格式度量

> **提示：** 在 `print` 方法中收到的图形上下文会被裁剪以排除边距，但坐标系的原点仍然是纸张的左上角。将坐标系平移到可成像区域的左上角是合理的。只需在 `print` 方法开头使用
>
> ```java
> g.translate(pageFormat.getImageableX(), pageFormat.getImageableY());
> ```

如果你希望用户选择页面边距设置，或者在不设置其他打印属性的情况下切换纵向和横向，请调用 `PrinterJob` 类的 `pageDialog` 方法：

```java
PageFormat format = job.pageDialog(attributes);
```

> **注意：** 打印对话框的其中一个选项卡包含页面设置对话框（见图 11.62）。你可能仍然希望让用户可以在打印前设置页面格式，尤其是当你的程序提供“所见即所得”的待打印页面显示时。`pageDialog` 方法返回用户设置的 `PageFormat` 对象视图。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_799_0.png)

**图 11.62** 跨平台页面设置对话框

清单 11.23 和 11.24 中的程序展示了如何在屏幕和打印页面上渲染同一组形状。JPanel 的一个子类实现了 Printable 接口。`paintComponent` 和 `print` 方法都调用同一个方法来执行实际的绘制。

```java
class PrintPanel extends JPanel implements Printable
{
    public void paintComponent(Graphics g)
    {
        super.paintComponent(g);
        var g2 = (Graphics2D) g;
        drawPage(g2);
    }

    public int print(Graphics g, PageFormat pf, int page) throws PrinterException
    {
        if (page >= 1) return Printable.NO_SUCH_PAGE;
        var g2 = (Graphics2D) g;
        g2.translate(pf.getImageableX(), pf.getImageableY());
        drawPage(g2);
        return Printable.PAGE_EXISTS;
    }

    public void drawPage(Graphics2D g2)
    {
        // shared drawing code goes here
        . . .
    }
    . . .
}
```

此示例显示并打印图 11.50 中所示的图像——即“Hello, World”消息的轮廓，用作线条图案的裁剪区域。

单击 Print 按钮开始打印，或单击 Page setup 按钮打开页面设置对话框。清单 11.23 显示了代码。

> **注意：** 要显示原生页面设置对话框，请将默认的 PageFormat 对象传递给 pageDialog 方法。该方法会克隆该对象，根据用户在对话框中的选择对其进行修改，并返回克隆后的对象。
>
> ```java
> PageFormat defaultFormat = printJob.defaultPage();
> PageFormat selectedFormat = printJob.pageDialog(defaultFormat);
> ```

#### **清单 11.23** print/PrintTestFrame.java

```java
1 package print;
2
3 import java.awt.*;
4 import java.awt.print.*;
5
6 import javax.print.attribute.*;
7 import javax.swing.*;
8
9 /**
10 * This frame shows a panel with 2D graphics and buttons to print the graphics and to set up
11 * the page format.
12 */
13 public class PrintTestFrame extends JFrame
14 {
15     private PrintComponent canvas;
16     private PrintRequestAttributeSet attributes;
17
18     public PrintTestFrame()
19     {
        canvas = new PrintComponent();
        add(canvas, BorderLayout.CENTER);

        attributes = new HashPrintRequestAttributeSet();

        var buttonPanel = new JPanel();
        var printButton = new JButton("Print");
        buttonPanel.add(printButton);
        printButton.addActionListener(event ->
        {
            try
            {
                PrinterJob job = PrinterJob.getPrinterJob();
                job.setPrintable(canvas);
                if (job.printDialog(attributes)) job.print(attributes);
            }
            catch (PrinterException ex)
            {
                JOptionPane.showMessageDialog(PrintTestFrame.this, ex);
            }
        });

        var pageSetupButton = new JButton("Page setup");
        buttonPanel.add(pageSetupButton);
        pageSetupButton.addActionListener(event ->
        {
            PrinterJob job = PrinterJob.getPrinterJob();
            job.pageDialog(attributes);
        });

        add(buttonPanel, BorderLayout.NORTH);
        pack();
    }
}
```

#### **清单 11.24** `print/PrintComponent.java`

```java
package print;

import java.awt.*;
import java.awt.font.*;
import java.awt.geom.*;
import java.awt.print.*;
import javax.swing.*;

/**
 * This component generates a 2D graphics image for screen display and printing.
 */
```

（续）


```java
for (int i = 0; i < NLINES; i++)
{
    double x = (2 * getWidth() * i) / NLINES;
    double y = (2 * getHeight() * (NLINES - 1 - i)) / NLINES;
    var q = new Point2D.Double(x, y);
    g2.draw(new Line2D.Double(p, q));
}
}
public Dimension getPreferredSize() { return PREFERRED_SIZE; }
}
```

#### java.awt.print.Printable 1.2

- `int print(Graphics g, PageFormat format, int pageNumber)`

  渲染一个页面并返回 `PAGE_EXISTS`，或返回 `NO_SUCH_PAGE`。

  | 参数 | 描述 |
  |---|---|
  | `g` | 页面渲染到的图形上下文 |
  | `format` | 要绘制页面的格式 |
  | `pageNumber` | 请求的页码 |

#### java.awt.print.PrinterJob 1.2

- `static PrinterJob getPrinterJob()`

  返回一个打印机作业对象。

- `PageFormat defaultPage()`

  返回此打印机的默认页面格式。

- `boolean printDialog(PrintRequestAttributeSet attributes)`
- `boolean printDialog()`

  打开一个打印对话框，允许用户选择要打印的页面并更改打印设置。第一个方法显示跨平台对话框，第二个方法显示原生对话框。第一个方法会修改属性对象以反映用户设置。如果用户接受对话框，两个方法都返回 true。

- `PageFormat pageDialog(PrintRequestAttributeSet attributes)`
- `PageFormat pageDialog(PageFormat defaults)`

  显示一个页面设置对话框。第一个方法显示跨平台对话框，第二个方法显示原生对话框。两个方法都返回一个 PageFormat 对象，其中包含用户在对话框中所请求的格式。第一个方法会修改属性对象以反映用户设置。第二个方法不会修改 defaults 对象。

然后，使用 `setPageable` 方法将 `Book` 对象传递给打印作业。

```java
printJob.setPageable(book);
```

现在打印作业确切知道要打印多少页，因此打印对话框会显示准确的页面范围，用户可以选择整个范围或子范围。

> **注意：** 当打印作业调用 `Printable` 各部分的 `print` 方法时，它传入的是 `Book` 的当前页码，而不是各部分的当前页码，作为当前页码参数。这非常麻烦——每个部分都必须知道前面部分的页数，才能理解页码参数。

从程序员的角度来看，使用 `Book` 类的最大挑战是：打印每个部分时，你必须知道该部分将有多少页。你的 `Printable` 类需要一个*布局算法*，用于计算材料在打印页面上的布局。在打印开始前，调用该算法计算分页位置和页数。你可以保留布局信息，以便在打印过程中随时使用。

你必须防止用户更改页面格式的可能性。如果发生这种情况，即使要打印的信息没有变化，也必须重新计算布局。

清单 11.26 展示了如何生成多页打印输出。该程序在若干页上以非常大的字符打印一条消息（见图 11.63）。然后你可以修剪页边距，并将这些页面粘在一起，形成横幅。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_805_0.png)

**图 11.63** 横幅

`Banner` 类的 `layoutPages` 方法计算布局。我们首先以 72 点字体布局消息字符串。然后计算所得字符串的高度，并将其与页面的可成像高度进行比较。我们根据这两个测量值推导出一个缩放因子。打印字符串时，我们按该缩放因子将其放大。

#### 清单 11.25 `book/BookTestFrame.java`

```java
package book;

import java.awt.*;
import java.awt.print.*;

import javax.print.attribute.*;
import javax.swing.*;

/**
 * This frame has a text field for the banner text and buttons for printing, page setup, and
 * print preview.
 */
public class BookTestFrame extends JFrame
{
   private JTextField text;
   private PageFormat pageFormat;
   private PrintRequestAttributeSet attributes;

   public BookTestFrame()
   {
      text = new JTextField();
      add(text, BorderLayout.NORTH);

      attributes = new HashPrintRequestAttributeSet();

      var buttonPanel = new JPanel();

      var printButton = new JButton("Print");
      buttonPanel.add(printButton);
      printButton.addActionListener(event ->
         {
            try
            {
               PrinterJob job = PrinterJob.getPrinterJob();
               job.setPageable(makeBook());
               if (job.printDialog(attributes))
               {
                  job.print(attributes);
               }
            }
            catch (PrinterException e)
            {
               JOptionPane.showMessageDialog(BookTestFrame.this, e);
            }
         });

      var pageSetupButton = new JButton("Page setup");
      buttonPanel.add(pageSetupButton);
      pageSetupButton.addActionListener(event ->
         {
            PrinterJob job = PrinterJob.getPrinterJob();
            pageFormat = job.pageDialog(attributes);
         });

      var printPreviewButton = new JButton("Print preview");
      buttonPanel.add(printPreviewButton);
      printPreviewButton.addActionListener(event ->
         {
            var dialog = new PrintPreviewDialog(makeBook());
            dialog.setVisible(true);
         });

      add(buttonPanel, BorderLayout.SOUTH);
      pack();
   }

   /**
    * Makes a book that contains a cover page and the pages for the banner.
    */
   public Book makeBook()
   {
      if (pageFormat == null)
      {
         PrinterJob job = PrinterJob.getPrinterJob();
         pageFormat = job.defaultPage();
      }
      var book = new Book();
      String message = text.getText();
      var banner = new Banner(message);
      int pageCount = banner.getPageCount((Graphics2D) getGraphics(), pageFormat);
      book.append(new CoverPage(message + " (" + pageCount + " pages)"), pageFormat);
      book.append(banner, pageFormat, pageCount);
      return book;
   }
}
```

#### 清单 11.26 book/Banner.java

```java
package book;

import java.awt.*;
import java.awt.font.*;
import java.awt.geom.*;
import java.awt.print.*;

/**
 * A banner that prints a text string on multiple pages.
 */
public class Banner implements Printable
{
   private String message;
   private double scale;

   /**
    * Constructs a banner.
    * @param m the message string
    */
   public Banner(String m)
   {
      message = m;
   }

   /**
    * Gets the page count of this section.
    * @param g2 the graphics context
    * @param pf the page format
    * @return the number of pages needed
    */
   public int getPageCount(Graphics2D g2, PageFormat pf)
   {
      if (message.equals("")) return 0;
      FontRenderContext context = g2.getFontRenderContext();
      var f = new Font("Serif", Font.PLAIN, 72);
      Rectangle2D bounds = f.getStringBounds(message, context);
      scale = pf.getImageableHeight() / bounds.getHeight();
      double width = scale * bounds.getWidth();
      int pages = (int) Math.ceil(width / pf.getImageableWidth());
      return pages;
   }

   public int print(Graphics g, PageFormat pf, int page) throws PrinterException
   {
      var g2 = (Graphics2D) g;
      if (page >= getPageCount(g2, pf)) return Printable.NO_SUCH_PAGE;
      g2.translate(pf.getImageableX(), pf.getImageableY());

      drawPage(g2, pf, page);
      return Printable.PAGE_EXISTS;
   }

   public void drawPage(Graphics2D g2, PageFormat pf, int page)
   {
      if (message.equals("")) return;
      page--; // account for cover page

      drawCropMarks(g2, pf);
      g2.clip(new Rectangle2D.Double(0, 0, pf.getImageableWidth(), pf.getImageableHeight()));
      g2.translate(-page * pf.getImageableWidth(), 0);
      g2.scale(scale, scale);
      FontRenderContext context = g2.getFontRenderContext();
      var f = new Font("Serif", Font.PLAIN, 72);
      var layout = new TextLayout(message, f, context);
      AffineTransform transform = AffineTransform.getTranslateInstance(0, layout.getAscent());
      Shape outline = layout.getOutline(transform);
      g2.draw(outline);
   }

   /**
    * Draws 1/2" crop marks in the corners of the page.
    * @param g2 the graphics context
    * @param pf the page format
    */
   public void drawCropMarks(Graphics2D g2, PageFormat pf)
   {
      final double C = 36; // crop mark length = 1/2 inch
      double w = pf.getImageableWidth();
      double h = pf.getImageableHeight();
      g2.draw(new Line2D.Double(0, 0, 0, C));
      g2.draw(new Line2D.Double(0, 0, C, 0));
      g2.draw(new Line2D.Double(w, 0, w - C, 0));
      g2.draw(new Line2D.Double(w, 0, w, C));
      g2.draw(new Line2D.Double(0, h, 0, h - C));
      g2.draw(new Line2D.Double(0, h, C, h));
      g2.draw(new Line2D.Double(w, h, w, h - C));
      g2.draw(new Line2D.Double(w, h, w - C, h));
   }

   /**
    * This class prints a cover page with a title.
    */
   class CoverPage implements Printable
   {
      private String title;

      /**
       * Constructs a cover page.
       * @param t the title
       */
   }
```




```java
102 public CoverPage(String t)
103 {
104     title = t;
105 }
106
107 public int print(Graphics g, PageFormat pf, int page) throws PrinterException
108 {
109     if (page >= 1) return Printable.NO_SUCH_PAGE;
110     var g2 = (Graphics2D) g;
111     g2.setPaint(Color.black);
112     g2.translate(pf.getImageableX(), pf.getImageableY());
113     FontRenderContext context = g2.getFontRenderContext();
114     Font f = g2.getFont();
115     var layout = new TextLayout(title, f, context);
116     float ascent = layout.getAscent();
117     g2.drawString(title, 0, ascent);
118     return Printable.PAGE_EXISTS;
119 }
120 }
```

#### **清单 11.27** `book/PrintPreviewDialog.java`

```java
1 package book;
2
3 import java.awt.*;
4 import java.awt.print.*;
5
6 import javax.swing.*;
7
8 /**
9  * This class implements a generic print preview dialog.
10  */
11 public class PrintPreviewDialog extends JDialog
12 {
13     private static final int DEFAULT_WIDTH = 300;
14     private static final int DEFAULT_HEIGHT = 300;
15
16     private PrintPreviewCanvas canvas;
17
18     /**
19      * Constructs a print preview dialog.
20      * @param p a Printable
21      * @param pf the page format
22      * @param pages the number of pages in p
23      */
```

#### 清单 11.28 `book/PrintPreviewCanvas.java`

```java
package book;

import java.awt.*;
import java.awt.event.*;
import java.awt.print.*;
import javax.swing.*;

/**
 * The canvas for displaying the print preview.
 */
class PrintPreviewCanvas extends JComponent
{
    private Book book;
    private int currentPage;

    /**
     * Constructs a print preview canvas.
     * @param b the book to be previewed
     */
    public PrintPreviewCanvas(Book b)
    {
        book = b;
        currentPage = 0;
    }

    public void paintComponent(Graphics g)
    {
        var g2 = (Graphics2D) g;
        PageFormat pageFormat = book.getPageFormat(currentPage);

        double xoff; // x offset of page start in window
        double yoff; // y offset of page start in window
        double scale; // scale factor to fit page in window
        double px = pageFormat.getWidth();
        double py = pageFormat.getHeight();
        double sx = getWidth() - 1;
        double sy = getHeight() - 1;
        if (px / py < sx / sy) // center horizontally
        {
            scale = sy / py;
            xoff = 0.5 * (sx - scale * px);
            yoff = 0;
        }
        else
            // center vertically
        {
47    scale = sx / px;
48    xoff = 0;
49    yoff = 0.5 * (sy - scale * py);
50  }
51  g2.translate((float) xoff, (float) yoff);
52  g2.scale((float) scale, (float) scale);
53
54  // draw page outline (ignoring margins)
55  var page = new Rectangle2D.Double(0, 0, px, py);
56  g2.setPaint(Color.white);
57  g2.fill(page);
58  g2.setPaint(Color.black);
59  g2.draw(page);
60
61  Printable printable = book.getPrintable(currentPage);
62  try
63  {
64      printable.print(g2, pageFormat, currentPage);
65  }
66  catch (PrinterException e)
67  {
68      g2.draw(new Line2D.Double(0, 0, px, py));
69      g2.draw(new Line2D.Double(px, 0, 0, py));
70  }
71
72
73  /**
74   * Flip the book by the given number of pages.
75   * @param by the number of pages to flip by. Negative values flip backwards.
76   */
77  public void flipPage(int by)
78  {
79      int newPage = currentPage + by;
80      if (0 <= newPage && newPage < book.getNumberOfPages())
81      {
82          currentPage = newPage;
83          repaint();
84      }
85  }
86  }
```

### 11.5.3 打印服务

到目前为止，你已经了解了如何打印 2D 图形。然而，Java SE 1.4 中引入的打印 API 提供了大得多的灵活性。该 API 定义了许多数据类型，并让你能够查找可打印这些数据类型的打印服务。这些数据类型包括

- GIF、JPEG 或 PNG 格式的图像
- 文本、HTML、PostScript 或 PDF 格式的文档
- 原始打印机代码数据
- 实现了 Printable、Pageable 或 RenderableImage 接口的类的对象

数据本身可以存储在字节或字符源中，例如输入流、URL 或数组。文档风格描述数据源和数据类型的组合。DocFlavor 类为各种数据源定义了许多内部类。每个内部类都定义用于指定风格的常量。例如，常量

```java
DocFlavor.INPUT_STREAM.GIF
```

描述从输入流读取的 GIF 图像。表 11.4 列出了这些组合。

假设你想打印位于文件中的 GIF 图像。首先，查明是否存在能够处理该任务的打印服务。PrintServiceLookup 类的静态 lookupPrintServices 方法返回一个 PrintService 对象数组，这些对象能够处理给定的文档风格。

```java
DocFlavor flavor = DocFlavor.INPUT_STREAM.GIF;
PrintService[] services = PrintServiceLookup.lookupPrintServices(flavor, null);
```

lookupPrintServices 方法的第二个参数为 null，表示我们不想通过指定打印机属性来限制搜索。我们将在下一节介绍属性。

如果查找结果产生的数组包含多个元素，请从列出的打印服务中进行选择。你可以调用 PrintService 类的 getName 方法获取打印机名称，并让用户选择。

接下来，从该服务获取文档打印作业：

```java
DocPrintJob job = services[i].createPrintJob();
```

要进行打印，你需要一个实现 Doc 接口的对象。Java 库为此提供了一个 SimpleDoc 类。SimpleDoc 构造函数需要数据源对象、文档风格以及可选的属性集。例如，

```java
var in = new FileInputStream(filename);
var doc = new SimpleDoc(in, flavor, null);
```

最后，就可以进行打印了：

```java
job.print(doc, null);
```

和之前一样，null 参数可以替换为一个属性集。

#### **表 11.4** 打印服务的文档风格

| 数据源 | 数据类型 | MIME 类型 |
|---|---|---|
| INPUT_STREAM | GIF | image/gif |
| URL | JPEG | image/jpeg |
| BYTE_ARRAY | PNG | image/png |
|  | POSTSCRIPT | application/postscript |
|  | PDF | application/pdf |
|  | TEXT_HTML_HOST | text/html（使用主机编码） |
|  | TEXT_HTML_US_ASCII | text/html; charset=us-ascii |
|  | TEXT_HTML_UTF_8 | text/html; charset=utf-8 |
|  | TEXT_HTML_UTF_16 | text/html; charset=utf-16 |
|  | TEXT_HTML_UTF_16LE | text/html; charset=utf-16le（小端序） |
|  | TEXT_HTML_UTF_16BE | text/html; charset=utf-16be（大端序） |
|  | TEXT_PLAIN_HOST | text/plain（使用主机编码） |
|  | TEXT_PLAIN_US_ASCII | text/plain; charset=us-ascii |
|  | TEXT_PLAIN_UTF_8 | text/plain; charset=utf-8 |
|  | TEXT_PLAIN_UTF_16 | text/plain; charset=utf-16 |
|  | TEXT_PLAIN_UTF_16LE | text/plain; charset=utf-16le（小端序） |
|  | TEXT_PLAIN_UTF_16BE | text/plain; charset=utf-16be（大端序） |
|  | PCL | application/vnd.hp-PCL（惠普打印机控制语言） |
|  | AUTOSENSE | application/octet-stream（原始打印机数据） |
| READER | TEXT_HTML | text/html; charset=utf-16 |
| STRING | TEXT_PLAIN | text/plain; charset=utf-16 |
| CHAR_ARRAY |  |  |
| SERVICE_FORMATTED | PRINTABLE | N/A |
|  | PAGEABLE | N/A |
|  | RENDERABLE_IMAGE | N/A |

请注意，这个打印过程与上一节的过程有很大不同。它不通过打印对话框进行用户交互。例如，你可以实现一种服务器端打印机制，让用户通过 Web 表单提交打印作业。

#### `javax.print.PrintServiceLookup` 1.4

- `PrintService[] lookupPrintServices(DocFlavor flavor, AttributeSet attributes)`

  查找能够处理给定文档风格和属性的打印服务。

  **参数：**

  | 名称 | 描述 |
  |---|---|
  | `flavor` | 文档风格 |
  | `attributes` | 所需的打印属性；如果不应考虑属性，则为 null |

#### `javax.print.PrintService` 1.4

- `DocPrintJob createPrintJob()`

  创建一个打印作业，用于打印实现了 `Doc` 接口的类的对象，例如 `SimpleDoc`。

#### `javax.print.DocPrintJob` 1.4

- `void print(Doc doc, PrintRequestAttributeSet attributes)`

  使用给定属性打印给定文档。

  **参数：**

  | 名称 | 描述 |
  |---|---|
  | `doc` | 要打印的 `Doc` |
  | `attributes` | 所需的打印属性；如果不需要打印属性，则为 null |

#### `javax.print.SimpleDoc` 1.4

- `SimpleDoc(Object data, DocFlavor flavor, DocAttributeSet attributes)`

  构造一个可用 `DocPrintJob` 打印的 `SimpleDoc` 对象。

  **参数：**

  | 名称 | 描述 |
  |---|---|
  | `data` | 包含打印数据的对象，例如输入流或 `Printable` |
  | `flavor` | 打印数据的文档风格 |
  | `attributes` | 文档属性；如果不需要属性，则为 null |




### 11.5.4 流打印服务

打印服务将打印数据发送到打印机。流打印服务生成相同的打印数据，但改为将其发送到流，可能是为了延迟打印，或者是因为打印数据格式可由其他程序解释。特别地，如果打印数据格式是 PostScript，将打印数据保存到文件可能很有用，因为许多程序可以处理 PostScript 文件。Java 平台包含一个流打印服务，可以从图像和二维图形生成 PostScript 输出。你可以在所有系统上使用该服务，即使没有本地打印机。

枚举流打印服务比定位常规打印服务要繁琐一些。你需要同时提供要打印对象的 `DocFlavor` 和流输出的 MIME 类型。然后你会得到一个由工厂组成的 `StreamPrintServiceFactory` 数组。

```java
DocFlavor flavor = DocFlavor.SERVICE_FORMATTED.PRINTABLE;
String mimeType = "application/postscript";
StreamPrintServiceFactory[] factories
    = StreamPrintServiceFactory.lookupStreamPrintServiceFactories(flavor, mimeType);
```

`StreamPrintServiceFactory` 类没有任何方法可以帮助我们区分任意一个工厂与另一个工厂，因此我们只取 `factories[0]`。我们用一个输出流参数调用 `getPrintService` 方法，以获得一个 StreamPrintService 对象。

```java
var out = new FileOutputStream(fileName);
StreamPrintService service = factories[0].getPrintService(out);
```

StreamPrintService 类是 PrintService 的子类。要生成打印输出，只需按照上一节的步骤操作。

| `javax.print.StreamPrintServiceFactory` | 1.4 |
|---|---|
| • `StreamPrintServiceFactory[] lookupStreamPrintServiceFactories(DocFlavor flavor, String mimeType)`<br><br>查找能够打印给定文档风格并生成给定 MIME 类型的输出流的流打印服务工厂。<br><br>• `StreamPrintService getPrintService(OutputStream out)`<br><br>获取一个将打印输出发送到给定输出流的打印服务。 | |

清单 11.29 中的程序演示了如何使用流打印服务将 Java 2D 形状打印到 PostScript 文件。你可以用生成任意 Java 2D 形状的代码替换示例绘图代码，并让这些形状转换为 PostScript。然后你可以轻松地将结果转换为 PDF。

**清单 11.29（续）**

```java
34  clipShape.append(outline, false);
35
36  layout = new TextLayout("World", f, context);
37  transform = AffineTransform.getTranslateInstance(0, 144);
38  outline = layout.getOutline(transform);
39  clipShape.append(outline, false);
40
41  g2.draw(clipShape);
42  g2.clip(clipShape);
43
44  final int NLINES = 50;
45  var p = new Point2D.Double(0, 0);
46  for (int i = 0; i < NLINES; i++)
47  {
48    double x = (2 * IMAGE_WIDTH * i) / NLINES;
49    double y = (2 * IMAGE_HEIGHT * (NLINES - 1 - i)) / NLINES;
50    var q = new Point2D.Double(x, y);
51    g2.draw(new Line2D.Double(p, q));
52  }
53
54
55  public static void main(String[] args) throws IOException, PrintException
56  {
57    String fileName = args.length > 0 ? args[0] : "out.ps";
58    DocFlavor flavor = DocFlavor.SERVICE_FORMATTED.PRINTABLE;
59    var mimeType = "application/postscript";
60    StreamPrintServiceFactory[] factories
61        = StreamPrintServiceFactory.lookupStreamPrintServiceFactories(flavor, mimeType);
62    var out = new FileOutputStream(fileName);
63    if (factories.length > 0)
64    {
65      PrintService service = factories[0].getPrintService(out);
66      var doc = new SimpleDoc(new Printable()
67      {
68        public int print(Graphics g, PageFormat pf, int page)
69        {
70          if (page >= 1) return Printable.NO_SUCH_PAGE;
71          else
72          {
73            double sf1 = pf.getImageableWidth() / (IMAGE_WIDTH + 1);
74            double sf2 = pf.getImageableHeight() / (IMAGE_HEIGHT + 1);
75            double s = Math.min(sf1, sf2);
76            var g2 = (Graphics2D) g;
77            g2.translate((pf.getWidth() - pf.getImageableWidth()) / 2,
78                (pf.getHeight() - pf.getImageableHeight()) / 2);
79            g2.scale(s, s);
80
81            draw(g2);
return Printable.PAGE_EXISTS;
}
}, flavor, null);
DocPrintJob job = service.createPrintJob();
var attributes = new HashPrintRequestAttributeSet();
job.print(doc, attributes);
} else {
System.out.println("No factories for " + mimeType);
}
}
}
}
```

### 11.5.5 打印属性

打印服务 API 包含一组复杂的接口和类，用于指定各种属性。属性有四个重要组。前两组指定对打印机的请求。

- 打印请求属性为打印作业中的所有文档对象请求特定功能，例如双面打印或纸张大小。
- 文档属性是仅适用于单个文档对象的请求属性。

另外两组属性包含关于打印机和作业状态的信息。

- 打印服务属性提供关于打印服务的信息，例如打印机的品牌和型号，或者打印机当前是否接受作业。
- 打印作业属性提供关于特定打印作业状态的信息，例如作业是否已经完成。

为了描述各种属性，有一个接口 Attribute，其子接口包括：

- PrintRequestAttribute
- DocAttribute
- PrintServiceAttribute
- PrintJobAttribute
- SupportedValuesAttribute

各个属性类实现这些接口中的一个或多个。例如，Copies 类的对象描述打印输出的副本数。该类同时实现 PrintRequestAttribute 和 PrintJobAttribute 接口。显然，一个打印请求可以包含对多份副本的请求。反过来，打印作业的一个属性可能是这些副本中实际打印了多少份。这个数字可能更低，也许是因为打印机限制，或者因为打印机纸张用完了。

SupportedValuesAttribute 接口表示属性值不反映实际请求或状态数据，而是反映服务的能力。例如，CopiesSupported 类实现 SupportedValuesAttribute 接口。该类的对象可能描述打印机支持一份打印输出的 1 到 99 份副本。

图 11.65 展示了属性层次结构的类图。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_822_0.png)

**图 11.65** 属性层次结构

除了用于各个属性的接口和类之外，打印服务 API 还定义了用于属性集的接口和类。超级接口 AttributeSet 有四个子接口：

- PrintRequestAttributeSet
- DocAttributeSet
- PrintServiceAttributeSet
- PrintJobAttributeSet

这些接口各自都有一个实现类，从而得到五个类：

- HashAttributeSet
- HashPrintRequestAttributeSet
- HashDocAttributeSet
- HashPrintServiceAttributeSet
- HashPrintJobAttributeSet

图 11.66 展示了属性集层次结构的类图。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_823_0.png)

**图 11.66** 属性集层次结构

例如，你可以像这样构造一个打印请求属性集：

```java
var attributes = new HashPrintRequestAttributeSet();
```

构造该集合后，你就不必再担心 Hash 前缀了。

为什么要有所有这些接口？它们使得检查属性用法是否正确成为可能。例如，DocAttributeSet 只接受实现 DocAttribute 接口的对象。任何添加其他属性的尝试都会导致运行时错误。

属性集是一种特殊的映射，其中键的类型为 Class，值属于实现 Attribute 接口的类。例如，如果你插入一个对象

```java
new Copies(10)
```

到一个属性集中，那么它的键就是 Class 对象 Copies.class。该键称为属性的类别。Attribute 接口声明了一个方法

```java
Class getCategory()
```



它返回属性的类别。`Copies` 类定义了返回对象 `Copies.class` 的方法，但类别不必与属性的类相同。

将属性添加到属性集时，会自动提取类别。只需添加属性值：

```
attributes.add(new Copies(10));
```

如果随后添加另一个具有相同类别的属性，它会覆盖第一个属性。

要获取属性，需要使用类别作为键，例如：

```
AttributeSet attributes = job.getAttributes();
var copies = (Copies) attributes.get(Copies.class);
```

最后，属性按其可取值进行组织。`Copies` 属性可以具有任意整数值。`Copies` 类扩展了 `IntegerSyntax` 类，后者负责处理所有整数值属性。`getValue` 方法返回该属性的整数值，例如：

```
int n = copies.getValue();
```

以下类

```
TextSyntax
DateTimeSyntax
URISyntax
```

分别封装字符串、日期时间值或 URI。

最后，许多属性可以取有限个值。例如，`PrintQuality` 属性有三种设置：draft、normal 和 high。它们由三个常量表示：

```
PrintQuality.DRAFT
PrintQuality.NORMAL
PrintQuality.HIGH
```

具有有限个值的属性类扩展了 `EnumSyntax` 类，该类提供了许多便利方法，以类型安全的方式设置这些枚举。使用这类属性时，你不必担心其机制。只需将命名值添加到属性集：

```
attributes.add(PrintQuality.HIGH);
```

下面说明如何检查属性的值：

```
if (attributes.get(PrintQuality.class) == PrintQuality.HIGH)
    . . .
```

表11.5 列出了打印属性。第二列列出属性类的超类（例如，copies 属性的 IntegerSyntax），或者列出具有有限值集合的属性的枚举值集合。最后四列指示该属性类是否实现 DocAttribute（DA）、PrintJobAttribute（PJA）、PrintRequestAttribute（PRA）和 PrintServiceAttribute（PSA）接口。

**表11.5 打印属性**

| 属性 | 超类或枚举常量 | DA | PJA | PRA | PSA |
| --- | --- | :---: | :---: | :---: | :---: |
| Chromaticity | `MONOCHROME`, `COLOR` | ✓ | ✓ | ✓ |  |
| ColorSupported | `SUPPORTED`, `NOT_SUPPORTED` |  |  |  | ✓ |
| Compression | `COMPRESS`, `DEFLATE`, `GZIP`, `NONE` | ✓ |  |  |  |
| Copies | `IntegerSyntax` |  | ✓ | ✓ |  |
| DateTimeAtCompleted | `DateTimeSyntax` |  | ✓ |  |  |
| DateTimeAtCreation | `DateTimeSyntax` |  | ✓ |  |  |
| DateTimeAtProcessing | `DateTimeSyntax` |  | ✓ |  |  |
| Destination | `URISyntax` |  | ✓ | ✓ |  |
| DocumentName | `TextSyntax` | ✓ |  |  |  |
| Fidelity | `FIDELITY_TRUE`, `FIDELITY_FALSE` |  | ✓ | ✓ |  |
| Finishings | `NONE`, `STAPLE`, `EDGE_STITCH`, `BIND`, `SADDLE_STITCH`, `COVER`, ... | ✓ | ✓ | ✓ |  |
| JobHoldUntil | `DateTimeSyntax` |  | ✓ | ✓ |  |
| JobImpressions | `IntegerSyntax` |  | ✓ | ✓ |  |
| JobImpressionsCompleted | `IntegerSyntax` |  | ✓ |  |  |
| JobKOctets | `IntegerSyntax` |  | ✓ | ✓ |  |
| JobKOctetsProcessed | `IntegerSyntax` |  | ✓ |  |  |
| JobMediaSheets | `IntegerSyntax` |  | ✓ | ✓ |  |
| JobMediaSheetsCompleted | `IntegerSyntax` |  | ✓ |  |  |
| JobMessageFromOperator | `TextSyntax` |  | ✓ |  |  |
| JobName | `TextSyntax` |  | ✓ | ✓ |  |
| JobOriginatingUserName | TextSyntax |  | ✓ |  |  |
| JobPriority | IntegerSyntax |  | ✓ | ✓ |  |
| JobSheets | STANDARD, NONE |  | ✓ | ✓ |  |
| JobState | ABORTED, CANCELED, COMPLETED, PENDING, PENDING_HELD, PROCESSING, PROCESSING_STOPPED |  | ✓ |  |  |
| JobStateReason | ABORTED_BY_SYSTEM, DOCUMENT_FORMAT_ERROR, 以及许多其他值 |  | ✓ |  |  |
| JobStateReasons | HashSet |  | ✓ |  |  |
| MediaName | ISO_A4_WHITE, ISO_A4_TRANSPARENT, NA_LETTER_WHITE, NA_LETTER_TRANSPARENT | ✓ | ✓ | ✓ |  |
| MediaSize | ISO_A0–ISO_A10, ISO_B0–ISO_B10, ISO_C0–ISO_C10, NA_LETTER, NA_LEGAL, 各种其他纸张和信封尺寸 |  | ✓ | ✓ |  |
| MediaSizeName | ISO_A0–ISO_A10, ISO_B0–ISO_B10, ISO_C0–ISO_C10, NA_LETTER, NA_LEGAL, 各种其他纸张和信封尺寸名称 | ✓ | ✓ | ✓ |  |
| MediaTray | TOP, MIDDLE, BOTTOM, SIDE, ENVELOPE, LARGE_CAPACITY, MAIN, MANUAL | ✓ | ✓ | ✓ |  |
| MultipleDocumentHandling | SINGLE_DOCUMENT, SINGLE_DOCUMENT_NEW_SHEET, SEPARATE_DOCUMENTS_COLLATED_COPIES, SEPARATE_DOCUMENTS_UNCOLLATED_COPIES |  | ✓ | ✓ |  |
| NumberOfDocuments | IntegerSyntax |  | ✓ |  |  |
| NumberOfInterveningJobs | IntegerSyntax |  | ✓ |  |  |
| NumberUp | IntegerSyntax |  | ✓ | ✓ |  |
| OrientationRequested | PORTRAIT, LANDSCAPE, REVERSE_PORTRAIT, REVERSE_LANDSCAPE |  | ✓ | ✓ |  |
| OutputDeviceAssigned | TextSyntax |  |  | ✓ |  |
| PageRanges | SetOfInteger | ✓ | ✓ | ✓ |  |
| PagesPerMinute | IntegerSyntax |  |  |  | ✓ |
| PagesPerMinuteColor | IntegerSyntax |  |  |  | ✓ |
| PDLOverrideSupported | ATTEMPTED, NOT_ATTEMPTED |  |  |  | ✓ |
| PresentationDirection | TORIGHT_TOTOBOTTOM, TORIGHT_TOTOP, TOBOTTOM_TORIGHT, TOBOTTOM_TOLEFT, TOLEFT_TOTOBOTTOM, TOLEFT_TOTOP, TOTOP_TORIGHT, TOTOP_TOLEFT |  | ✓ | ✓ |  |
| PrinterInfo | TextSyntax |  |  |  | ✓ |
| PrinterIsAcceptingJobs | ACCEPTING_JOBS, NOT_ACCEPTING_JOBS |  |  |  | ✓ |
| PrinterLocation | TextSyntax |  |  |  | ✓ |
| PrinterMakeAndModel | TextSyntax |  |  |  | ✓ |
| PrinterMessageFromOperator | TextSyntax |  |  |  | ✓ |
| PrinterMoreInfo | URISyntax |  |  |  | ✓ |
| PrinterMoreInfoManufacturer | URISyntax |  |  |  | ✓ |
| PrinterName | TextSyntax |  |  |  | ✓ |
| PrinterResolution | ResolutionSyntax |  | ✓ | ✓ | ✓ |
| PrinterState | PROCESSING, IDLE, STOPPED, UNKNOWN |  |  |  | ✓ |
| PrinterStateReason | COVER_OPEN, FUSER_OVER_TEMP, MEDIA_JAM, 以及许多其他值 |  |  |  | ✓ |
| PrinterStateReasons | HashSet |  |  |  | ✓ |
| PrinterURI | URISyntax |  |  |  | ✓ |
| PrintQuality | DRAFT, NORMAL, HIGH |  | ✓ | ✓ | ✓ |
| QueuedJobCount | IntegerSyntax |  |  |  | ✓ |
| ReferenceUriSchemesSupported | FILE, FTP, GOPHER, HTTP, HTTPS, NEWS, NNTP, WAIS |  |  |  |  |

#### `javax.print.attribute.AttributeSet` 1.4

- `boolean remove(Attribute attr)`
- `boolean remove(Class category)`  
  从集合中移除给定属性，或移除具有给定类别的属性。如果该集合因此操作而改变，则返回 true。
- `Attribute[] toArray()`  
  返回包含此集合中所有属性的数组。

#### `javax.print.PrintService` 1.4

- `PrintServiceAttributeSet getAttributes()`  
  获取此打印服务的属性。

#### `javax.print.DocPrintJob` 1.4

- `PrintJobAttributeSet getAttributes()`  
  获取此打印作业的属性。

你现在已经读完了这一长章，内容涵盖高级 Swing 和 AWT 特性。在最后一章中，我们将转向 Java 编程的另一个方面：在同一台机器上，与使用另一种编程语言编写的“本地”代码进行交互。

此页有意留为空白

# 第12章 本地方法

## 本章内容

- 12.1 从 Java 程序调用 C 函数，第810页
- 12.2 数值参数与返回值，第817页
- 12.3 字符串参数，第819页
- 12.4 访问字段，第825页
- 12.5 编码签名，第831页
- 12.6 调用 Java 方法，第832页
- 12.7 访问数组元素，第840页
- 12.8 处理错误，第844页
- 12.9 使用调用 API，第849页
- 12.10 完整示例：访问 Windows 注册表，第855页

虽然“100% 纯 Java”解决方案在原则上很好，但在某些情况下，你会希望用另一种语言编写（或使用）代码。这类代码通常称为*本地*代码。

尤其是在 Java 的早期，许多人认为使用 C 或 C++ 来加速 Java 应用程序的关键部分是个好主意。然而在实践中，这很少有用。1996 年 JavaOne 大会上的一个演讲清楚地说明了这一点。Sun Microsystems 密码学库的开发者报告说，他们的密码学函数的纯 Java 平台实现完全足够。确实，该代码不如 C 实现那么快，但结果……

事实证明这并不重要。Java 平台实现比网络 I/O 快得多。真正的问题其实在于网络 I/O。

当然，使用原生代码也有缺点。如果你的应用有一部分是用另一种语言编写的，你就必须为每个想要支持的平台单独提供一个原生库。用 C 或 C++ 编写的代码无法防止通过无效指针使用而覆盖内存。编写原生方法很容易破坏你的程序或感染操作系统。

因此，我们建议仅在需要时使用原生代码。具体来说，有三种情况可能适合使用原生代码：

- 你的应用需要访问 Java 平台无法访问的系统功能或设备。
- 你有大量用另一种语言编写并已经过测试和调试的代码，并且知道如何将它移植到所有目标平台。
- 你通过基准测试发现，Java 代码比另一种语言编写的等效代码慢得多。

Java 平台有一个用于与原生 C 代码互操作的 API，称为 Java 本地接口（JNI）。我们将在本章讨论 JNI 编程。

> **C++ 注意：** 你也可以使用 C++ 而不是 C 来编写原生方法。这样做有一些优点——类型检查稍微更严格一些，访问 JNI 函数也更方便一点。然而，JNI 不支持 Java 类与 C++ 类之间的任何映射。

## 12.1 从 Java 程序调用 C 函数

假设你有一个 C 函数，它实现了你需要的功能，但由于某种原因，你不想在 Java 中重新实现它。为了便于说明，我们先从一个简单的 C 函数开始，该函数打印一条问候语。

Java 编程语言使用关键字 native 来表示原生方法，显然你需要将一个方法放入一个类中。结果如清单 12.1 所示。

native 关键字提醒编译器该方法将在外部定义。当然，原生方法不会包含任何 Java 代码，方法头后面紧跟一个终止分号。因此，原生方法声明看起来类似于抽象方法声明。

清单 12.1 `HelloNative/HelloNative.java`

```java
/**
 * @version 1.11 2007-10-26
 * @author Cay Horstmann
 */
class HelloNative
{
   public static native void greeting();
}
```

> **注意：** 与上一章一样，这里我们不使用包，以保持示例简单。

在这个特定示例中，原生方法也被声明为 static。原生方法既可以是 static 的，也可以是非 static 的。我们将从 static 方法开始，因为我们还不想处理参数传递。

你实际上可以编译这个类，但如果你尝试在程序中使用它，虚拟机会告诉你它不知道如何找到 greeting——并报告一个 `UnsatisfiedLinkError`。要实现该原生代码，请编写一个相应的 C 函数。你必须按照 Java 虚拟机期望的方式*精确地*命名该函数。规则如下：

- 1. 使用完整的 Java 方法名，例如 `HelloNative.greeting`。如果类在某个包中，则在前面加上包名，例如 `com.horstmann.HelloNative.greeting`。
- 2. 将每个句点替换为下划线，并添加前缀 `Java_`。例如，`Java_HelloNative_greeting` 或 `Java_com_horstmann_HelloNative_greeting`。
- 3. 如果类名包含不是 ASCII 字母或数字的字符——即 `_`、`$` 或 Unicode 代码大于 `\u007F` 的字符——请将它们替换为 `_0xxxx`，其中 `xxxx` 是该字符 Unicode 值的四位十六进制数字序列。

> **注意：** 如果你重载原生方法——也就是说，你提供了多个具有相同名称的原生方法——则必须附加双下划线，后跟编码后的参数类型。（我们将在本章后面描述参数类型的编码方式。）例如，如果你有一个原生方法 `greeting` 和另一个原生方法 `greeting(int repeat)`，那么第一个被称为 `Java_HelloNative_greeting__`，第二个被称为 `Java_HelloNative_greeting__I`。

实际上，没有人会手动这样做；相反，运行带有 `-h` 标志的 `javac`，并提供头文件应放置的目录：

```bash
javac -h . HelloNative.java
```

该命令会在当前目录中创建头文件 `HelloNative.h`，如清单 12.2 所示。

清单 12.2 `HelloNative/HelloNative.h`

```c
/* DO NOT EDIT THIS FILE - it is machine generated */
#include <jni.h>
/* Header for class HelloNative */

#ifndef _Included_HelloNative
#define _Included_HelloNative
#ifdef __cplusplus
extern "C" {
#endif
/*
 * Class:     HelloNative
 * Method:    greeting
 * Signature: ()V
 */
JNIEXPORT void JNICALL Java_HelloNative_greeting
  (JNIEnv *, jclass);

#ifdef __cplusplus
}
#endif
#endif
```

如你所见，该文件包含了函数 `Java_HelloNative_greeting` 的声明。（宏 `JNIEXPORT` 和 `JNICALL` 在头文件 `jni.h` 中定义。它们表示与编译器相关的说明符，用于从动态加载库中导出的函数。）

现在，只需将头文件中的函数原型复制到源文件中，并为该函数提供实现代码，如清单 12.3 所示。

在这个简单函数中，忽略 `env` 和 `cl` 参数。稍后你会看到它们的用途。

清单 12.3 `helloNative/HelloNative.c`

```c
/*
 * @version 1.10 1997-07-01
 * @author Cay Horstmann
 */

#include "HelloNative.h"
#include <stdio.h>

JNIEXPORT void JNICALL Java_HelloNative_greeting(JNIEnv* env, jclass cl)
{
    printf("Hello Native World!\n");
}
```

> **C++ 注意：** 你可以使用 C++ 来实现原生方法。但是，你必须将实现原生方法的函数声明为 extern "C"。（这可以阻止 C++ 编译器“修饰”方法名。）例如，
>
> ```c++
> extern "C"
> JNIEXPORT void JNICALL Java_HelloNative_greeting(JNIEnv* env, jclass cl)
> {
>     cout << "Hello, Native World!" << endl;
> }
> ```

将原生 C 代码编译成动态加载库。具体细节取决于你的编译器。

例如，在 Linux 上使用 GNU C 编译器，可以使用以下命令：

```shell
gcc -fPIC -I jdk/include -I jdk/include/linux -shared -o libHelloNative.so HelloNative.c
```

在 Windows 上使用 Microsoft 编译器，命令是

```shell
cl -I jdk\include -I jdk\include\win32 -LD HelloNative.c -FeHelloNative.dll
```

这里，*jdk* 是包含 JDK 的目录。

> **提示：** 如果你从命令 shell 使用 Microsoft 编译器，请先运行一个批处理文件，例如 `vsvar32.bat` 或 `vcvarsall.bat`。该批处理文件会设置编译器所需的路径和环境变量。你可以在目录 `c:\Program Files\Microsoft Visual Studio 14.0\Common7\Tools` 或类似的复杂路径中找到它。有关详细信息，请参阅 Visual Studio 文档。

你还可以使用来自 www.cygwin.com 的免费 Cygwin 编程环境。它包含用于在 Windows 上进行 UNIX 风格编程的 GNU C 编译器和库。使用 Cygwin 时，请使用以下命令：

```bash
gcc -mno-cygwin -D __int64="long long" -I jdk/include/ -I jdk/include/win32 \
    -shared -Wl,--add-stdcall-alias -o HelloNative.dll HelloNative.c
```

> **注意：** 头文件 `jni_md.h` 的 Windows 版本包含类型声明
>
> ```c
> typedef __int64 jlong;
> ```
>
> 该声明是 Microsoft 编译器所特有的。如果你使用 GNU 编译器，可能需要编辑该文件，例如：
>
> ```c
> #if defined __GNUC__
>     typedef long long jlong;
> #else
>     typedef __int64 jlong;
> #endif
> ```
>
> 或者，使用 `-D __int64="long long"` 进行编译，如示例编译命令所示。

最后，在程序中添加对 System.loadLibrary 方法的调用。为了确保虚拟机在第一次使用该类之前加载库，请使用静态初始化块，如清单 12.4 所示。

清单 12.4 `helloNative/HelloNativeTest.java`

```java
/**
 * @version 1.11 2007-10-26
 * @author Cay Horstmann
 */
class HelloNativeTest
{
    public static void main(String[] args)
    {
        HelloNative.greeting();
    }

    static
    {
        System.loadLibrary("HelloNative");
    }
}
```



图12-1给出了本地代码处理的概要。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_837_0.png)

**图12-1** 处理本地代码

编译并运行该程序后，终端窗口中将显示消息“Hello, Native World!”。

> **注意：** 如果在Linux上运行，必须将当前目录添加到库路径中。可以设置`LD_LIBRARY_PATH`环境变量：
>
>     export LD_LIBRARY_PATH=.:$LD_LIBRARY_PATH
>
> 或者设置`java.library.path`系统属性：
>
>     java -Djava.library.path=. HelloNativeTest

当然，这本身并不特别令人印象深刻。但请记住，这条消息是由C语言的`printf`命令生成的，而不是任何Java代码。我们已经迈出了弥合两种语言之间差距的第一步！

总之，按照以下步骤将本地方法链接到Java程序：

- 1. 在Java类中声明一个本地方法。
- 2. 运行`javah`获取包含该方法的C声明头文件。
- 3. 用C实现该本地方法。
- 4. 将代码放入共享库中。
- 5. 在Java程序中加载该库。

| java.lang.System 1.0 |
| :--- |
| • `void loadLibrary(String libname)`<br>加载具有指定名称的库。该库位于库搜索路径中。定位库的具体方法取决于操作系统。 |

> **注意：** 某些用于本地代码的共享库必须执行特定的初始化。你可以将任何初始化代码放入`JNI_OnLoad`方法中。类似地，当虚拟机（VM）关闭时，如果你提供了`JNI_OnUnload`方法，它将调用该方法。原型如下：
>
>     jint JNI_OnLoad(JavaVM* vm, void* reserved);
>     void JNI_OnUnload(JavaVM* vm, void* reserved);
>
> `JNI_OnLoad`方法需要返回它所需的最低VM版本，例如`JNI_VERSION_1_2`。

## 12.2 数值参数与返回值

在C和Java之间传递数字时，你应该了解哪些类型是相互对应的。例如，尽管C确实有名为int和long的数据类型，但它们的实现是平台相关的。在某些平台上，int是16位的，在其他平台上则是32位的。当然，在Java平台上，int始终是32位整数。因此，JNI定义了jint、jlong等类型。

表12-1展示了Java类型与C类型之间的对应关系。

**表12-1 Java类型与C类型**

| Java编程语言 | C编程语言 | 字节数 |
|---|---:|
| boolean | jboolean | 1 |
| byte | jbyte | 1 |
| char | jchar | 2 |
| short | jshort | 2 |
| int | jint | 4 |
| long | jlong | 8 |
| float | jfloat | 4 |
| double | jdouble | 8 |

在头文件jni.h中，这些类型通过typedef语句声明为目标平台上的等效类型。该头文件还定义了常量JNI_FALSE = 0和JNI_TRUE = 1。

在Java 5之前，Java没有与C的printf函数直接对应的功能。在下面的示例中，我们假设你仍在使用古老的JDK版本，并决定通过在本地方法中调用C的printf函数来实现相同的功能。

清单12-5展示了一个名为Printf1的类，它使用本地方法以指定的字段宽度和精度打印浮点数。

注意，当该方法在C中实现时，所有int和double参数都会变为jint和jdouble，如清单12-6所示。

**清单12-5** `printf1/Printf1.java`

```java
/**
 * @version 1.10 1997-07-01
 * @author Cay Horstmann
 */
class Printf1
{
   public static native void print(int width, int precision, double x);

   static
   {
      System.loadLibrary("Printf1");
   }
}
```

**清单12-6** `printf1/Printf1.c`

```c
/**
 * @version 1.10 1997-07-01
 * @author Cay Horstmann
 */

#include "Printf1.h"
#include <stdio.h>

JNIEXPORT jint JNICALL Java_Printf1_print(JNIEnv* env, jclass cl,
        jint width, jint precision, jdouble x)
{
   char fmt[30];
   jint ret;
   sprintf(fmt, "%%%d.%df", width, precision);
   ret = printf(fmt, x);
   fflush(stdout);
   return ret;
}
```

该函数只是在变量fmt中组装一个格式字符串“%.pf”，然后调用printf。它返回打印的字符数。

清单12-7展示了演示Printf1类的测试程序。

**清单12-7** `printf1/Printf1Test.java`

```java
/**
 * @version 1.10 1997-07-01
 * @author Cay Horstmann
 */
class Printf1Test
{
   public static void main(String[] args)
   {
      int count = Printf1.print(8, 4, 3.14);
      count += Printf1.print(8, 4, count);
      System.out.println();
      for (int i = 0; i < count; i++)
         System.out.print("-");
      System.out.println();
   }
}
```

## 12.3 字符串参数

接下来，我们看看如何将字符串传入和传出本地方法。字符串在两种语言中有很大不同：在Java中，它们是UTF-16码点的序列，而C字符串是以null结尾的字节序列。JNI有两组用于操作字符串的函数：一组将Java字符串转换为“修改版UTF-8”字节序列，另一组将它们转换为UTF-16值数组——即jchar数组。（UTF-8、“修改版UTF-8”和UTF-16格式已在第2章中讨论过。回想一下，UTF-8和“修改版UTF-8”编码保留ASCII字符不变，但所有其他Unicode字符都编码为多字节序列。）

> **注意：** 标准UTF-8编码与“修改版UTF-8”编码仅在码点高于0xFFFF的“增补”字符上有所不同。在标准UTF-8编码中，这些字符被编码为4字节序列。在“修改版”编码中，每个这样的字符首先在UTF-16编码中被编码为一对“代理项”，然后每个代理项用UTF-8编码，总共产生6个字节。这虽然笨拙，但这是一个历史遗留问题——JVM规范编写时Unicode仍然仅限于16位。

如果你的C代码已经使用Unicode，你会希望使用第二组转换函数。另一方面，如果你所有的字符串仅限于ASCII字符，可以使用“修改版UTF-8”转换函数。

具有String参数的本地方法实际上接收到一个称为jstring的不透明类型的值。返回类型为String的本地方法必须返回jstring类型的值。JNI函数读取并构造这些jstring对象。例如，NewStringUTF函数从包含ASCII字符或更一般地说“修改版UTF-8”编码字节序列的char数组创建一个新的jstring对象。

JNI函数有一种有点奇怪的调用约定。以下是对NewStringUTF函数的调用：

```c
JNIEXPORT jstring JNICALL Java_HelloNative_getGreeting(JNIEnv* env, jclass cl)
{
    jstring jstr;
    char greeting[] = "Hello, Native World\n";
    jstr = (*env)->NewStringUTF(env, greeting);
    return jstr;
}
```

> **注意：** 除非另有明确说明，本章中的所有代码都是C代码。

所有对JNI函数的调用都使用env指针，它是每个本地方法的第一个参数。env指针是指向函数指针表的指针（见图12-2）。因此，你必须为每个JNI调用加上(*env)->前缀，以实际解引用函数指针。此外，env是每个JNI函数的第一个参数。

> **C++ 注意：** 在C++中访问JNI函数更简单。C++版本的JNIEnv类具有内联成员函数，可以为你处理函数指针查找。例如，你可以这样调用NewStringUTF函数：
>
> ```cpp
> jstr = env->NewStringUTF(greeting);
> ```
>
> 注意，在调用的参数列表中省略了JNIEnv指针。

NewStringUTF函数让你可以构造一个新的jstring。要读取现有jstring对象的内容，请使用GetStringUTFChars函数。该函数返回一个const jbyte*指针，指向“修改版UTF-8”字符，这些字符描述了



### 从 C 代码访问 Java 字符串

- `jstring NewStringUTF(JNIEnv* env, const char bytes[])`
  从以零字节结尾的“修改版 UTF-8”字节序列返回一个新的 Java 字符串对象；如果无法构造该字符串，则返回 NULL。
- `jsize GetStringUTFLength(JNIEnv* env, jstring string)`
  返回“修改版 UTF-8”编码所需的字节数（不计零字节终止符）。
- `const jbyte* GetStringUTFChars(JNIEnv* env, jstring string, jboolean* isCopy)`
  返回指向字符串“修改版 UTF-8”编码的指针；如果无法构造字符数组，则返回 NULL。该指针在调用 ReleaseStringUTFChars 之前有效。如果进行了复制，isCopy 指向的 jboolean 会被填入 JNI_TRUE；否则填入 JNI_FALSE。
- `void ReleaseStringUTFChars(JNIEnv* env, jstring string, const jbyte bytes[])`
  通知虚拟机，本机代码不再需要通过 bytes（由 GetStringUTFChars 返回的指针）访问该 Java 字符串。
- `void GetStringRegion(JNIEnv* env, jstring string, jsize start, jsize length, jchar* buffer)`
  将字符串中的一段 UTF-16 双字节序列复制到用户提供的缓冲区，其大小至少为 2 × length。
- `void GetStringUTFRegion(JNIEnv* env, jstring string, jsize start, jsize length, jbyte* buffer)`
  将字符串中的一段“修改版 UTF-8”字节序列复制到用户提供的缓冲区。该缓冲区必须足够长以容纳这些字节。最坏情况下会复制 3 × length 个字节。
- `jstring NewString(JNIEnv* env, const jchar chars[], jsize length)`
  从 Unicode 字符串返回一个新的 Java 字符串对象；如果无法构造该字符串，则返回 NULL。
- `jsize GetStringLength(JNIEnv* env, jstring string)`
  返回字符串中的字符数。
- `const jchar* GetStringChars(JNIEnv* env, jstring string, jboolean* isCopy)`
  返回指向字符串 Unicode 编码的指针；如果无法构造字符数组，则返回 NULL。该指针在调用 ReleaseStringChars 之前有效。isCopy 要么为 NULL，要么指向一个 jboolean：如果进行了复制，则填入 JNI_TRUE；否则填入 JNI_FALSE。
- `void ReleaseStringChars(JNIEnv* env, jstring string, const jchar chars[])`
  通知虚拟机，本机代码不再需要通过 chars（由 GetStringChars 返回的指针）访问该 Java 字符串。

让我们运用这些函数，编写一个调用 C 函数 sprintf 的类。我们希望像代码清单 12.8 所示那样调用该函数。

#### 代码清单 12.8 printf2/Printf2Test.java

```java
1  /**
2   * @version 1.10 1997-07-01
3   * @author Cay Horstmann
4   */
5  class Printf2Test
6  {
7     public static void main(String[] args)
8     {
9        double price = 44.95;
10       double tax = 7.75;
11       double amountDue = price * (1 + tax / 100);
12
13       String s = Printf2.sprintf("Amount due = $%.2f", amountDue);
14       System.out.println(s);
15    }
16 }
```

代码清单 12.9 显示了带有本机 sprintf 方法的类。

#### 代码清单 12.9 printf2/Printf2.java

```java
1  /**
2   * @version 1.10 1997-07-01
3   * @author Cay Horstmann
4   */
5  class Printf2
6  {
7     public static native String sprintf(String format, double x);
8
9     static
10    {
11       System.loadLibrary("Printf2");
12    }
13 }
```

因此，用于格式化浮点数的 C 函数具有以下原型

```c
JNIEXPORT jstring JNICALL Java_Printf2_sprintf(JNIEnv* env, jclass cl,
    jstring format, jdouble x)
```

代码清单 12.10 显示了 C 实现的代码。请注意对 GetStringUTFChars 的调用（用于读取 format 参数）、对 NewStringUTF 的调用（用于生成返回值），以及对 ReleaseStringUTFChars 的调用（用于通知虚拟机不再需要访问该字符串）。

#### 代码清单 12.10 printf2/Printf2.c

```c
/**
 * @version 1.10 1997-07-01
 * @author Cay Horstmann
 */

#include "Printf2.h"
#include <string.h>
#include <stdlib.h>
#include <float.h>

/**
 * @param format a string containing a printf format specifier
 *        (such as "%.2f"). Substrings "%%" are skipped.
 * @return a pointer to the format specifier (skipping the '%')
 *         or NULL if there wasn't a unique format specifier
 */
char* find_format(const char format[])
{
   char* p;
   char* q;

   p = strchr(format, '%');
   while (p != NULL && *(p + 1) == '%') /* skip %% */
      p = strchr(p + 2, '%');
   if (p == NULL) return NULL;
   /* now check that % is unique */
   p++;
   q = strchr(p, '%');
   while (q != NULL && *(q + 1) == '%') /* skip %% */
      q = strchr(q + 2, '%');
   if (q != NULL) return NULL; /* % not unique */
   q = p + strspn(p, "0-# "); /* skip past flags */
   q += strspn(q, "0123456789"); /* skip past field width */
   if (*q == '.') { q++; q += strspn(q, "0123456789"); }
      /* skip past precision */
   if (strchr("eEfFgG", *q) == NULL) return NULL;
      /* not a floating-point format */
   return p;
}

JNIEXPORT jstring JNICALL Java_Printf2_sprintf(JNIEnv* env, jclass cl,
         jstring format, jdouble x)
{
const char* cformat;
char* fmt;
jstring ret;

cformat = (*env)->GetStringUTFChars(env, format, NULL);
fmt = find_format(cformat);
if (fmt == NULL)
    ret = format;
else
{
    char* cret;
    int width = atoi(fmt);
    if (width == 0) width = DBL_DIG + 10;
    cret = (char*) malloc(strlen(cformat) + width);
    sprintf(cret, cformat, x);
    ret = (*env)->NewStringUTF(env, cret);
    free(cret);
}
(*env)->ReleaseStringUTFChars(env, format, cformat);
return ret;
}
```

在这个函数中，我们选择保持错误处理简单。如果用于打印浮点数的格式代码不是 %w.pc 形式（其中 c 是字符 e、E、f、g 或 G 之一），那么我们就不格式化该数字。稍后我们将展示如何让本机方法抛出异常。

## 12.4 访问字段

到目前为止你看到的所有本机方法都是带有数字和字符串参数的静态方法。现在我们将考虑操作对象的本机方法。作为一个练习，我们将把第 I 卷第 4 章中介绍的 Employee 类的一个方法重新实现为本机方法。同样，这通常不是你愿意做的事情，但它确实说明了在需要时如何从本机方法访问字段。

### 12.4.1 访问实例字段

为了了解如何从本机方法访问实例字段，我们将重新实现 raiseSalary 方法。以下是 Java 代码：

```java
public void raiseSalary(double byPercent)
{
    salary *= 1 + byPercent / 100;
}
```

这些函数的开销在于，从字段名计算字段 ID——这是最昂贵的步骤——被抽出来作为单独的一步。也就是说，如果你反复获取和设置某个特定字段的值，那么计算字段标识符的成本只需承担一次。

让我们把所有部分组合起来。以下代码将 `raiseSalary` 方法重新实现为本机方法：

```c
JNIEXPORT void JNICALL Java_Employee_raiseSalary(JNIEnv* env, jobject this_obj,
        jdouble byPercent)
{
    /* get the class */
    jclass class_Employee = (*env)->GetObjectClass(env, this_obj);

    /* get the field ID */
    jfieldID id_salary = (*env)->GetFieldID(env, class_Employee, "salary", "D");

    /* get the field value */
    jdouble salary = (*env)->GetDoubleField(env, this_obj, id_salary);

    salary *= 1 + byPercent / 100;

    /* set the field value */
    (*env)->SetDoubleField(env, this_obj, id_salary, salary);
}
```

> **注意：** 类引用仅在本次本机方法返回之前有效。你不能在代码中缓存 `GetObjectClass` 的返回值。不要保存类引用以便在以后的方法调用中复用。每次执行本机方法时都必须调用 `GetObjectClass`。如果无法忍受这一点，可以通过调用 `NewGlobalRef` 锁定该引用：

```c
static jclass class_X = 0;
static jfieldID id_a;
...
if (class_X == 0)
{
    jclass cx = (*env)->GetObjectClass(env, obj);
    class_X = (*env)->NewGlobalRef(env, cx);
    id_a = (*env)->GetFieldID(env, class_X, "a", "...");
}
```

现在你可以在后续调用中使用该类的引用和字段 ID。使用完该类后，请务必调用

```c
(*env)->DeleteGlobalRef(env, class_X);
```



代码清单 12.11 和 12.12 展示了一个测试程序和 Employee 类的 Java 代码。代码清单 12.13 包含本地 raiseSalary 方法的 C 代码。

#### 代码清单 12.11 employee/EmployeeTest.java

```java
/**
 * @version 1.11 2018-05-01
 * @author Cay Horstmann
 */

public class EmployeeTest
{
   public static void main(String[] args)
   {
      var staff = new Employee[3];

      staff[0] = new Employee("Harry Hacker", 35000);
      staff[1] = new Employee("Carl Cracker", 75000);
      staff[2] = new Employee("Tony Tester", 38000);

      for (Employee e : staff)
         e.raiseSalary(5);
      for (Employee e : staff)
         e.print();
   }
}
```

#### 代码清单 12.12 employee/Employee.java

```java
/**
 * @version 1.10 1999-11-13
 * @author Cay Horstmann
 */

public class Employee
{
   private String name;
   private double salary;

   public native void raiseSalary(double byPercent);

   public Employee(String n, double s)
   {
      name = n;
      salary = s;
   }
}
```

## 12.5 编码签名

要访问 Java 编程语言中定义的实例字段并调用方法，你需要学习“改编”数据类型名称和方法签名的规则。（方法签名描述方法的参数和返回类型。）以下是编码方案：

| 代码 | 含义 |
|---|---|
| `B` | 字节型 |
| `C` | 字符型 |
| `D` | 双精度浮点型 |
| `F` | 单精度浮点型 |
| `I` | 整型 |
| `J` | 长整型 |
| `Lclassname;` | 类类型 |
| `S` | 短整型 |
| `V` | 无返回值 |
| `Z` | 布尔型 |

要描述数组类型，请使用 `[`。例如，字符串数组为

```text
[Ljava/lang/String;
```

float[][] 被改编为

```text
[[F
```

要获得方法的完整签名，请在一对括号内列出参数类型，然后列出返回类型。例如，接收两个整数并返回一个整数的方法编码为

```text
(II)I
```

第 819 页第 12.3 节“字符串参数”中的 sprint 方法具有以下改编后的签名：

```text
(Ljava/lang/String;D)Ljava/lang/String;
```

也就是说，该方法接收一个 String 和一个 double，并返回一个 String。

请注意，L 表达式末尾的分号是类型表达式的终止符，而不是参数之间的分隔符。例如，构造函数

```text
Employee(java.lang.String, double, java.util.Date)
```

的签名为

```text
(Ljava/lang/String;DLjava/util/Date;)V
```

请注意，`D` 和 `Ljava/util/Date;` 之间没有分隔符。另请注意，在此编码方案中，必须使用 `/` 而不是 `.` 来分隔包名和类名。末尾的 `V` 表示返回类型为 void。尽管在 Java 中不为构造函数指定返回类型，但仍需在虚拟机签名中添加 `V`。

> **提示：** 可以使用 `javap` 命令及 `-s` 选项从类文件生成方法签名。例如，运行
>
> `javap -s -private Employee`
>
> 将得到以下输出，显示所有字段和方法的签名：

```text
Compiled from "Employee.java"
public class Employee extends java.lang.Object{
  private java.lang.String name;
    Signature: Ljava/lang/String;
  private double salary;
    Signature: D
  public Employee(java.lang.String, double);
    Signature: (Ljava/lang/String;D)V
  public native void raiseSalary(double);
    Signature: (D)V
  public void print();
    Signature: ()V
  static {};
    Signature: ()V
}
```

> **注意：** 强迫程序员对签名使用这种改编方案没有任何道理。本地调用机制的设计者本来也可以轻松编写一个函数，以 Java 编程语言风格读取签名，例如 `void(int,java.lang.String)`，并将其编码为他们偏好的任意内部表示。不过话又说回来，使用改编后的签名可以让你体验贴近虚拟机编程的神秘感。

## 12.6 调用 Java 方法

当然，Java 编程语言函数可以调用 C 函数——这正是本地方法的用途。能否反过来呢？我们究竟为什么要这样做？经常会出现本地方法需要向传给它的对象请求服务的情况。我们将首先展示如何对实例方法执行此操作，然后展示如何对静态方法执行此操作。

### 12.6.1 实例方法

作为从本地代码调用 Java 方法的示例，让我们增强 Printf 类并添加一个类似于 C 函数 fprintf 的方法。也就是说，它应能将字符串打印到任意 PrintWriter 对象上。以下是该方法的 Java 定义：

```java
class Printf3
{
    public native static void fprintf(PrintWriter out, String s, double x);
    . . .
}
```

我们首先将要打印的字符串组装到 String 对象 str 中，就像我们已经实现的 sprint 方法一样。然后，在实现该本地方法的 C 函数中，我们将调用 PrintWriter 类的 print 方法。

可以使用以下函数调用从 C 中调用任何 Java 方法

```c
(*env)->CallXxxMethod(env, implicit parameter, methodID, explicit parameters)
```

根据方法的返回类型，将 Xxx 替换为 Void、Int、Object 等。正如访问对象字段需要 fieldID 一样，调用方法需要方法 ID。要获取方法 ID，请调用 JNI 函数 GetMethodID，并提供类、方法名和方法签名。

在我们的示例中，我们希望获取 PrintWriter 类的 print 方法的 ID。PrintWriter 类有几个名为 print 的重载方法。因此，还必须提供一个字符串，描述要使用的特定函数的参数和返回值。例如，我们想使用 void print(java.lang.String)。如上一节所述，现在必须将签名“改编”为字符串“(Ljava/lang/String;)V”。

以下是进行方法调用的完整代码：

```c
/* get the class of the implicit parameter */
jclass class_PrintWriter = (*env)->GetObjectClass(env, out);

/* get the method ID */
jmethodID id_print = (*env)->GetMethodID(env, class_PrintWriter, "print", "(Ljava/lang/String;)V");

/* call the method */
(*env)->CallVoidMethod(env, out, id_print, str);
```

代码清单 12.14 和 12.15 展示了测试程序和 Printf3 类的 Java 代码。代码清单 12.16 包含本地 printf 方法的 C 代码。

> **注意：** 数值方法 ID 和字段 ID 在概念上类似于反射 API 中的 Method 和 Field 对象。可以使用以下函数在它们之间进行转换：
>
> ```c
> jobject ToReflectedMethod(JNIEnv* env, jclass class, jmethodID methodID);
>     // returns Method object
> methodID FromReflectedMethod(JNIEnv* env, jobject method);
> jobject ToReflectedField(JNIEnv* env, jclass class, jfieldID fieldID);
>     // returns Field object
> fieldID FromReflectedField(JNIEnv* env, jobject field);
> ```

### 12.6.2 静态方法

从本地方法调用静态方法与调用实例方法类似。有两个区别：

- 使用 `GetStaticMethodID` 和 `CallStaticXxxMethod` 函数
- 调用方法时提供 `class` 对象，而不是隐式参数对象

作为示例，让我们从本地方法中调用静态方法

```java
System.getProperty("java.class.path")
```

该调用的返回值是一个给出当前类路径的字符串。

首先，必须找到要使用的类。由于没有现成的 `System` 类对象，我们使用 `FindClass` 而不是 `GetObjectClass`。

```c
jclass class_System = (*env)->FindClass(env, "java/lang/System");
```

接下来，需要静态 `getProperty` 方法的 ID。该方法的编码签名是

```c
"(Ljava/lang/String;)Ljava/lang/String;"
```

因为参数和返回值都是字符串。因此，我们按如下方式获取方法 ID：

```c
jmethodID id_getProperty = (*env)->GetStaticMethodID(env, class_System, "getProperty",
    "(Ljava/lang/String;)Ljava/lang/String;");
```





最后，我们可以进行调用了。请注意，类对象被传递给了 `CallStaticObjectMethod` 函数。

```c
jobject obj_ret = (*env)->CallStaticObjectMethod(env, class_System, id_getProperty,
    (*env)->NewStringUTF(env, "java.class.path"));
```

该方法的返回值是 jobject 类型。如果我们要将它作为字符串来操作，就必须将它转换为 jstring：

```c
jstring str_ret = (jstring) obj_ret;
```

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_857_0.png)

> **C++ 注意事项：** 在 C 语言中，`jstring` 和 `jclass` 类型，以及稍后介绍的数组类型，都与 `jobject` 类型等价。因此，前面示例中的强制转换在 C 语言中并不是严格必需的。但在 C++ 中，这些类型被定义为指向具有正确继承层次的“伪类”的指针。例如，在 C++ 中，将 `jstring` 赋值给 `jobject` 时省略强制转换是合法的，但从 `jobject` 赋值给 `jstring` 时则需要强制转换。

### 12.6.3 构造器

原生方法可以通过调用其构造器来创建一个新的 Java 对象。通过调用 `NewObject` 函数来调用构造器。

```c
jobject obj_new = (*env)->NewObject(env, class, methodID, construction parameters);
```

你可以通过 `GetMethodID` 函数获取此调用所需的方法 ID，只需将方法名指定为“<init>”，并指定构造器的编码签名（返回类型为 void）。例如，下面是一个原生方法创建 `FileOutputStream` 对象的示例：

```c
const char* fileName = "..";
jstring str_fileName = (*env)->NewStringUTF(env, fileName);
jclass class_FileOutputStream = (*env)->FindClass(env, "java/io/FileOutputStream");
jmethodID id_FileOutputStream
    = (*env)->GetMethodID(env, class_FileOutputStream, "<init>", "(Ljava/lang/String;)V");
jobject obj_stream
    = (*env)->NewObject(env, class_FileOutputStream, id_FileOutputStream, str_fileName);
```

注意，构造器的签名接收一个 java.lang.String 类型的参数，并且返回类型为 void。

### 12.6.4 其他方法调用方式

JNI 函数的几个变体可用于从原生代码调用 Java 方法。这些变体虽然不如我们已经讨论过的函数那么重要，但偶尔会很有用。

CallNonvirtualXxxMethod 系列函数接收一个隐式参数、一个方法 ID、一个类对象（必须对应于隐式参数的某个超类）以及显式参数。每个函数调用指定类中的方法版本，绕过正常的动态分派机制。

所有调用函数都有带后缀“A”和“V”的版本，它们以数组或 va_list（在 C 头文件 stdarg.h 中定义）接收显式参数。

**清单 12.14** `printf3/Printf3Test.java`

```java
import java.io.*;

/**
 * @version 1.11 2018-05-01
 * @author Cay Horstmann
 */
class Printf3Test
{
   public static void main(String[] args)
   {
      double price = 44.95;
      double tax = 7.75;
      double amountDue = price * (1 + tax / 100);
      var out = new PrintWriter(System.out);
      Printf3.fprintf(out, "Amount due = %.2f\n", amountDue);
      out.flush();
   }
}
```

**清单 12.15** `printf3/Printf3.java`

```java
import java.io.*;

/**
 * @version 1.10 1997-07-01
 * @author Cay Horstmann
 */
class Printf3
{
   public static native void fprintf(PrintWriter out, String format, double x);

   static
   {
      System.loadLibrary("printf3");
   }
}
```

**清单 12.16** `printf3/Printf3.c`

```c
/**
   @version 1.10 1997-07-01
   @author Cay Horstmann
*/

#include "Printf3.h"
#include <string.h>
#include <stdlib.h>
#include <float.h>

/**
   @param format a string containing a printf format specifier
   (such as "%8.2f"). Substrings "%%" are skipped.
   @return a pointer to the format specifier (skipping the '%')
   or NULL if there wasn't a unique format specifier
*/
char* find_format(const char format[])
{
   char* p;
   char* q;

   p = strchr(format, '%');
   while (p != NULL && *(p + 1) == '%') /* skip %% */
      p = strchr(p + 2, '%');
   if (p == NULL) return NULL;
   /* now check that % is unique */
   p++;
   q = strchr(p, '%');
   while (q != NULL && *(q + 1) == '%') /* skip %% */
      q = strchr(q + 2, '%');
   if (q != NULL) return NULL; /* % not unique */
   q = p + strspn(p, "-+0# "); /* skip past flags */
   q += strspn(q, "0123456789"); /* skip past field width */
   if (*q == '.' && q[1] >= '0' && q[1] <= '9')
   {
      q++;
      q += strspn(q, "0123456789");
   }
   if (strchr("eEfFgG", *q) == NULL) return NULL;
      /* not a floating-point format */
   return p;
}

JNIEXPORT void JNICALL Java_Printf3_fprintf(JNIEnv *env, jclass cl,
      jobject out, jstring format, jdouble x)
{
   const char* cformat;
   char* fmt;
   jstring str;
   jclass class_PrintWriter;
   jmethodID id_print;

   cformat = (*env)->GetStringUTFChars(env, format, NULL);
   fmt = find_format(cformat);
   if (fmt == NULL)
      str = format;
   else
   {
      char* cstr;
      int width = atoi(fmt);
      if (width == 0) width = DBL_DIG + 10;
      cstr = (char*) malloc(strlen(cformat) + width);
      sprintf(cstr, cformat, x);
      str = (*env)->NewStringUTF(env, cstr);
      free(cstr);
   }
   (*env)->ReleaseStringUTFChars(env, format, cformat);

   /* now call ps.print(str) */

   /* get the class */
   class_PrintWriter = (*env)->GetObjectClass(env, out);

   /* get the method ID */
   id_print = (*env)->GetMethodID(env, class_PrintWriter, "print", "(Ljava/lang/String;)V");

   /* call the method */
   (*env)->CallVoidMethod(env, out, id_print, str);
}
```

#### 执行 Java 方法

- `jmethodID GetMethodID(JNIEnv *env, jclass cl, const char methodName[], const char methodSignature[])` 返回类中某个方法的标识符。
- `Xxx CallXxxMethod(JNIEnv *env, jobject obj, jmethodID id, args)`
- `Xxx CallXxxMethodA(JNIEnv *env, jobject obj, jmethodID id, jvalue args[])`
- `Xxx CallXxxMethodV(JNIEnv *env, jobject obj, jmethodID id, va_list args)`

调用一个方法。返回类型 `Xxx` 是 Object、Boolean、Byte、Char、Short、Int、Long、Float 或 Double 之一。第一个函数具有可变数量的参数——只需在方法 ID 后追加方法参数即可。第二个函数以 `jvalue` 数组接收方法参数，其中 `jvalue` 是一个联合体，定义如下：

```c
typedef union jvalue
{
    jboolean z;
    jbyte b;
    jchar c;
    jshort s;
    jint i;
    jlong j;
    jfloat f;
    jdouble d;
    jobject l;
} jvalue;
```

第三个函数以 va_list 接收方法参数，va_list 在 C 头文件 stdarg.h 中定义。

- `Xxx CallNonvirtualXxxMethod(JNIEnv *env, jobject obj, jclass cl, jmethodID id, args)`
- `Xxx CallNonvirtualXxxMethodA(JNIEnv *env, jobject obj, jclass cl, jmethodID id, jvalue args[])`
- `Xxx CallNonvirtualXxxMethodV(JNIEnv *env, jobject obj, jclass cl, jmethodID id, va_list args)`

调用一个方法，绕过动态分派。返回类型 Xxx 是 jObject、jBoolean、jByte、jChar、jShort、jInt、jLong、jFloat 或 jDouble 之一。第一个函数具有可变数量的参数——只需在方法 ID 后追加方法参数即可。第二个函数以 jvalue 数组接收方法参数。第三个函数以 va_list 接收方法参数，va_list 在 C 头文件 stdarg.h 中定义。

- `jmethodID GetStaticMethodID(JNIEnv *env, jclass cl, const char name[], const char methodSignature[])` 返回类中某个静态方法的标识符。
- `Xxx CallStaticXxxMethod(JNIEnv *env, jclass cl, jmethodID id, args)`
- `Xxx CallStaticXxxMethodA(JNIEnv *env, jclass cl, jmethodID id, jvalue args[])`
- `Xxx CallStaticXxxMethodV(JNIEnv *env, jclass cl, jmethodID id, va_list args)`

调用一个静态方法。返回类型 Xxx 是 jObject、jBoolean、jByte、jChar、jShort、jInt、jLong、jFloat 或 jDouble 之一。第一个函数具有可变数量的参数——只需在方法 ID 后追加方法参数即可。第二个函数以 jvalue 数组接收方法参数。第三个函数以 va_list 接收方法参数，va_list 在 C 头文件 stdarg.h 中定义。




#### 执行 Java 方法（续）

- `jobject NewObject(JNIEnv *env, jclass cl, jmethodID id, args)`
- `jobject NewObjectA(JNIEnv *env, jclass cl, jmethodID id, jvalue args[])`
- `jobject NewObjectV(JNIEnv *env, jclass cl, jmethodID id, va_list args)`

调用构造函数。方法 ID 通过 GetMethodID 获取，方法名为 `"<init>"`，返回类型为 void。第一个函数具有可变数量的参数——只需在方法 ID 后追加方法参数。第二个函数在 jvalue 数组中接收方法参数。第三个函数在 va_list 中接收方法参数，如 C 头文件 stdarg.h 所定义。

## 12.7 访问数组元素

Java 编程语言的所有数组类型都有对应的 C 类型，如表 12.2 所示。

**表 12.2** Java 数组类型与 C 类型之间的对应关系

| Java 类型 | C 类型 | Java 类型 | C 类型 |
|---|---|---|---|
| boolean[] | jbooleanArray | long[] | jlongArray |
| byte[] | jbyteArray | float[] | jfloatArray |
| char[] | jcharArray | double[] | jdoubleArray |
| int[] | jintArray | Object[] | jobjectArray |
| short[] | jshortArray |  |  |

> **C++ 注意：** 在 C 中，所有这些数组类型实际上都是 `jobject` 的类型同义词。然而，在 C++ 中，它们按照图 12.3 所示的继承层次结构排列。类型 `jarray` 表示泛型数组。

`GetArrayLength` 函数返回数组的长度。

```c
jarray array = ...;
jsize length = (*env)->GetArrayLength(env, array);
```

如何访问数组中的元素取决于该数组存储的是对象还是基本类型（`bool`、`char` 或数值类型）的值。要访问对象数组中的元素，请使用 `GetObjectArrayElement` 和 `SetObjectArrayElement` 方法。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_863_0.png)

图 12.3 数组类型的继承层次结构

```c
jobjectArray array = ...;
int i, j;
jobject x = (*env)->GetObjectArrayElement(env, array, i);
(*env)->SetObjectArrayElement(env, array, j, x);
```

### 操作 Java 数组（续）

- `void GetXxxArrayRegion(JNIEnv *env, jarray array, jint start, jint length, Xxx elems[])`  
  将元素从 Java 数组复制到 C 数组。字段类型 `Xxx` 是 Boolean、Byte、Char、Short、Int、Long、Float 或 Double 之一。
- `void SetXxxArrayRegion(JNIEnv *env, jarray array, jint start, jint length, Xxx elems[])`  
  将元素从 C 数组复制到 Java 数组。字段类型 `Xxx` 是 Boolean、Byte、Char、Short、Int、Long、Float 或 Double 之一。

## 12.8 处理错误

本地方法对 Java 程序构成重大安全风险。C 运行时系统对数组越界错误、通过错误指针进行间接访问等没有保护。本地方法的程序员处理所有错误条件以保持 Java 平台的完整性尤为重要。特别是，当你的本地方法诊断出它无法处理的问题时，应将该问题报告给 Java 虚拟机。

通常，在这种情况下你会抛出异常。然而，C 没有异常。相反，你必须调用 `Throw` 或 `ThrowNew` 函数来创建新的异常对象。当本地方法退出时，Java 虚拟机会抛出该异常。

要使用 `Throw` 函数，请调用 `NewObject` 创建 `Throwable` 的子类型的对象。例如，这里我们分配一个 `EOFException` 对象并抛出它：

```c
jclass class_EOFException = (*env)->FindClass(env, "java/io/EOFException");
jmethodID id_EOFException = (*env)->GetMethodID(env, class_EOFException, "<init>", "()V");
/* ID of no-argument constructor */
jthrowable obj_exc = (*env)->NewObject(env, class_EOFException, id_EOFException);
(*env)->Throw(env, obj_exc);
```

通常更方便的是调用 `ThrowNew`，它在给定类和“修改版 UTF-8”字节序列的情况下构造异常对象。

```c
(*env)->ThrowNew(env, (*env)->FindClass(env, "java/io/EOFException"),
    "Unexpected end of file");
```

`Throw` 和 `ThrowNew` 都只是发布异常；它们不会中断本地方法的控制流。只有当方法返回时，Java 虚拟机才会抛出异常。因此，每次调用 `Throw` 和 `ThrowNew` 后都应立即跟随一条 `return` 语句。

包含该本地方法。注意，当调用 PrintWriter.print 发生异常时，本地方法不会立即终止——它会先释放 cstr 缓冲区。当本地方法返回时，虚拟机会再次引发该异常。清单 12.19 中的测试程序演示了当格式字符串无效时，本地方法如何抛出异常。

**清单 12.17** printf4/Printf4.c

```c
1 /**
2    @version 1.10 1997-07-01
3    @author Cay Horstmann
4 */
5
6 #include "Printf4.h"
7 #include <string.h>
8 #include <stdlib.h>
9 #include <float.h>
10
11 /**
12    @param format a string containing a printf format specifier
13    (such as "%8.2f"). Substrings "%s" are skipped.
14    @return a pointer to the format specifier (skipping the '%')
15    or NULL if there wasn't a unique format specifier
16 */
17 char* find_format(const char format[])
18 {
19    char* p;
20    char* q;
21
22    p = strchr(format, '%');
23    while (p != NULL && *(p + 1) == '%') /* skip %% */
24       p = strchr(p + 2, '%');
25    if (p == NULL) return NULL;
26    /* now check that % is unique */
27    p++;
28    q = strchr(p, '%');
29    while (q != NULL && *(q + 1) == '%') /* skip %% */
30       q = strchr(q + 2, '%');
31    if (q != NULL) return NULL; /* % not unique */
32    q = p + strspn(p, " -0+#"); /* skip past flags */
33    q += strspn(q, "0123456789"); /* skip past field width */
34    if (*q == '.') { q++; q += strspn(q, "0123456789"); }
35       /* skip past precision */
36    if (strchr("eEfFgG", *q) == NULL) return NULL;
37       /* not a floating-point format */
38    return p;
39 }
89  /* now call ps.print(str) */
90
91  /* get the class */
92  jclass class_PrintWriter = (*env)->GetObjectClass(env, out);
93
94  /* get the method ID */
95  jmethodID id_print = (*env)->GetMethodID(env, class_PrintWriter, "print", "(C)V");
96
97  /* call the method */
98  for (i = 0; str[i] != 0 && !(*env)->ExceptionOccurred(env); i++)
99      (*env)->CallVoidMethod(env, out, id_print, str[i]);
100
101  free(str);
102  }
```

**清单 12.18** `printf4/Printf4.java`

```java
1  import java.io.*;
2
3  /**
4   * @version 1.10 1997-07-01
5   * @author Cay Horstmann
6   */
7  class Printf4
8  {
9      public static native void fprintf(PrintWriter ps, String format, double x);
10
11     static
12     {
13         System.loadLibrary("Printf4");
14     }
15 }
```

**清单 12.19** `printf4/Printf4Test.java`

```java
1  import java.io.*;
2
3  /**
4   * @version 1.11 2018-05-01
5   * @author Cay Horstmann
6   */
7  class Printf4Test
8  {
9      public static void main(String[] args)
10     {
double price = 44.95;
double tax = 7.75;
double amountDue = price * (1 + tax / 100);
var out = new PrintWriter(System.out);
/* This call will throw an exception--note the % */
Printf4.fprintf(out, "Amount due = $%.2f%n", amountDue);
out.flush();
}
}
```

### 处理 Java 异常

- `jint Throw(JNIEnv *env, jthrowable obj)`  
  准备一个在退出本地代码时抛出的异常。成功时返回 0，失败时返回负值。
- `jint ThrowNew(JNIEnv *env, jclass cl, const char msg[])`  
  准备一个类型为 cl 的异常，在退出本地代码时抛出。成功时返回 0，失败时返回负值。msg 是一个“修改版 UTF-8”字节序列，表示异常对象的 String 构造参数。
- `jthrowable ExceptionOccurred(JNIEnv *env)`  
  如果有待处理的异常，则返回异常对象，否则返回 NULL。
- `jboolean ExceptionCheck(JNIEnv *env)`  
  如果有待处理的异常，则返回 true。
- `void ExceptionClear(JNIEnv *env)`  
  清除任何待处理的异常。

## 12.9 使用调用 API

到目前为止，我们考虑的是 Java 编程语言程序进行少量 C 调用的情况，大概是因为 C 更快，或者允许访问 Java 平台无法访问的功能。假设你处于相反的情况。你有一个 C 或 C++ 程序，并希望调用 Java 代码。*调用 API* 使你能够将 Java 虚拟机嵌入 C 或 C++ 程序。以下是初始化虚拟机所需的最少代码：

```c
JavaVMOption options[1];
JavaVMInitArgs vm_args;
JavaVM *jvm;
JNIEnv *env;

options[0].optionString = "-Djava.class.path=.";
```



```c
memset(&vm_args, 0, sizeof(vm_args));
vm_args.version = JNI_VERSION_1_2;
vm_args.nOptions = 1;
vm_args.options = options;

JNI_CreateJavaVM(&jvm, (void**) &env, &vm_args);
```

对 `JNI_CreateJavaVM` 的调用会创建虚拟机，并填入指向虚拟机的指针 `jvm` 和指向执行环境的指针 `env`。

你可以向虚拟机提供任意数量的选项。只需增大 options 数组的大小和 `vm_args.nOptions` 的值即可。例如，

```c
options[1].optionString = "-Djava.compiler=NONE";
```

这会停用即时编译器。

> **提示：** 当你遇到问题，程序崩溃、拒绝初始化 JVM 或无法加载类时，请开启 JNI 调试模式。将某个选项设置为
>
> ```c
> options[1].optionString = "-verbose:jni";
> ```
>
> 你会看到大量消息，指示初始化 JVM 的进度。如果没有看到类被加载，请检查路径和类路径设置。

设置好虚拟机后，就可以像前面几节所述那样调用 Java 方法。只需按通常方式使用 env 指针即可。

只有调用调用 API 中的其他函数时才需要 jvm 指针。目前这样的函数只有四个。最重要的是终止虚拟机的函数：

```c
(*jvm)->DestroyJavaVM(jvm);
```

不幸的是，在 Windows 下，由于 Vista 中更改的链接规则以及 Oracle 对较旧 C 运行时库的依赖，动态链接到 `jre/bin/client/jvm.dll` 库中的 `JNI_CreateJavaVM` 函数已经变得困难。我们的示例程序通过手动加载该库来克服这个问题。这与 Java 程序使用的相同方法——参见 JDK 中 `src.jar` 文件内的 `launcher/java_md.c` 文件。

清单 12.20 中的 C 程序会设置虚拟机并调用 `Welcome` 类的 main 方法，该类在第 I 卷第 2 章中讨论过。（在启动调用测试程序之前，请确保编译 `Welcome.java` 文件。）

### 清单 12.20 invocation/InvocationTest.c

```c
/**
 * @version 1.20 2007-10-26
 * @author Cay Horstmann
 */

#include <jni.h>
#include <stdlib.h>

#ifdef _WINDOWS

#include <windows.h>
static HINSTANCE LoadJVMLibrary(void);
typedef jint (JNICALL *CreateJavaVM_t)(JavaVM **, void **, JavaVMInitArgs *);

#endif

int main()
{
    JavaVMOption options[2];
    JavaVMInitArgs vm_args;
    JavaVM *jvm;
    JNIEnv *env;
    long status;

    jclass class_Welcome;
    jclass class_String;
    jobjectArray args;
    jmethodID id_main;

#ifdef _WINDOWS
    HINSTANCE hjvmlib;
    CreateJavaVM_t CreateJavaVM;
#endif

    options[0].optionString = "-Djava.class.path=.";

    memset(&vm_args, 0, sizeof(vm_args));
    vm_args.version = JNI_VERSION_1_2;
    vm_args.nOptions = 1;
    vm_args.options = options;

#ifdef _WINDOWS
    hjvmlib = LoadJVMLibrary();
    CreateJavaVM = (CreateJavaVM_t) GetProcAddress(hjvmlib, "JNI_CreateJavaVM");
    status = (*CreateJavaVM)(&jvm, (void **) &env, &vm_args);
#else
    status = JNI_CreateJavaVM(&jvm, (void **) &env, &vm_args);
#endif

    if (status == JNI_ERR)
    {
        fprintf(stderr, "Error creating VM\n");
        return 1;
    }

    class_Welcome = (*env)->FindClass(env, "Welcome");
    id_main = (*env)->GetStaticMethodID(env, class_Welcome, "main", "([Ljava/lang/String;)V");

    class_String = (*env)->FindClass(env, "java/lang/String");
    args = (*env)->NewObjectArray(env, 0, class_String, NULL);
    (*env)->CallStaticVoidMethod(env, class_Welcome, id_main, args);

    (*jvm)->DestroyJavaVM(jvm);

    return 0;
}

#ifdef _WINDOWS

static int GetStringFromRegistry(HKEY key, const char *name, char *buf, jint bufsize)
{
    DWORD type, size;

    return RegQueryValueEx(key, name, 0, &type, 0, &size) == 0
        && type == REG_SZ
        && size < (unsigned int) bufsize
        && RegQueryValueEx(key, name, 0, 0, buf, &size) == 0;
}

static void GetPublicJREHome(char *buf, jint bufsize)
{
    HKEY key, subkey;
    char version[MAX_PATH];

    /* Find the current version of the JRE */
    char *JRE_KEY = "Software\\JavaSoft\\Java Runtime Environment";
    if (RegOpenKeyEx(HKEY_LOCAL_MACHINE, JRE_KEY, 0, KEY_READ, &key) != 0)
    {
        fprintf(stderr, "Error opening registry key '%s'\n", JRE_KEY);
        exit(1);
    }

    if (!GetStringFromRegistry(key, "CurrentVersion", version, sizeof(version)))
    {
        fprintf(stderr, "Failed reading value of registry key:\n\t%s\\CurrentVersion\n",
            JRE_KEY);
        RegCloseKey(key);
        exit(1);
    }

    /* Find directory where the current version is installed. */
    if (RegOpenKeyEx(key, version, 0, KEY_READ, &subkey) != 0)
    {
        fprintf(stderr, "Error opening registry key %s\\%s\n", JRE_KEY, version);
        RegCloseKey(key);
        exit(1);
    }

    if (!GetStringFromRegistry(subkey, "JavaHome", buf, bufsize))
    {
        fprintf(stderr, "Failed reading value of registry key:\n\t%s\\%s\\JavaHome\n",
            JRE_KEY, version);
        RegCloseKey(key);
        RegCloseKey(subkey);
        exit(1);
    }

    RegCloseKey(key);
    RegCloseKey(subkey);
}

static HINSTANCE LoadJVMLibrary(void)
{
    HINSTANCE h1, h2;
    char msvcdll[MAX_PATH];
    char javadll[MAX_PATH];
    GetPublicJREHome(msvcdll, MAX_PATH);
    strcpy(javadll, msvcdll);
    strncat(msvcdll, "\\bin\\msvcr71.dll", MAX_PATH - strlen(msvcdll));
    msvcdll[MAX_PATH - 1] = '\0';
    strncat(javadll, "\\bin\\client\\jvm.dll", MAX_PATH - strlen(javadll));
    javadll[MAX_PATH - 1] = '\0';

    h1 = LoadLibrary(msvcdll);
    if (h1 == NULL)
    {
        fprintf(stderr, "Can't load library msvcr71.dll\n");
        exit(1);
    }

    h2 = LoadLibrary(javadll);
    if (h2 == NULL)
    {
        fprintf(stderr, "Can't load library jvm.dll\n");
        exit(1);
    }
    return h2;
}

#endif
```

在 Linux 下编译此程序，请使用

```
gcc -I jdk/include -I jdk/include/linux -o InvocationTest \
    -L jdk/jre/lib/i386/client -ljvm InvocationTest.c
```

在 Windows 中使用 Microsoft 编译器编译时，请使用以下命令行

```
cl -D_WINDOWS -I jdk\include -I jdk\include\win32 InvocationTest.c \
    jdk\lib\jvm.lib advapi32.lib
```

你需要确保 INCLUDE 和 LIB 环境变量包含 Windows API 头文件和库文件的路径。

使用 Cygwin 时，请用以下命令编译

```
gcc -D_WINDOWS -mno-cygwin -I jdk\include -I jdk\include\win32 -D_int64="long long" \
    -I c:\cygwin\usr\include\w32api -o InvocationTest
```

在 Linux/UNIX 下运行程序之前，请确保 LD_LIBRARY_PATH 包含共享库所在目录。例如，如果你在 Linux 上使用 bash shell，请执行以下命令：

```
export LD_LIBRARY_PATH=jdk/jre/lib/i386/client:$LD_LIBRARY_PATH
```

- **调用 API 函数**
  - `jint JNI_CreateJavaVM(JavaVM **p_jvm, void **p_env, JavaVMInitArgs *vm_args)` 初始化 Java 虚拟机。函数成功时返回 0，失败时返回 `JNI_ERR`。
  - `jint DestroyJavaVM(JavaVM *jvm)` 销毁虚拟机。成功时返回 0，失败时返回负数。必须通过虚拟机指针调用此函数，即 `(*jvm)->DestroyJavaVM(jvm)`。

## 12.10 完整示例：访问 Windows 注册表

在本节中，我们描述一个完整可运行的示例，它涵盖本章讨论的所有内容：对字符串、数组、对象、构造函数调用和错误处理使用本地方法。我们将展示如何为用于操作 Windows 注册表的普通基于 C 的 API 的一个子集提供 Java 平台包装器。当然，Windows 注册表是 Windows 特有的功能，因此这样的程序本质上不可移植。因此，标准 Java 库不支持注册表，使用本地方法来访问它是合理的。

### 12.10.1 Windows 注册表概述

Windows 注册表是一个数据仓库，保存 Windows 操作系统和应用程序的配置信息。它为系统和应用程序首选项的管理和备份提供了单一位置。缺点是，注册表也是单点故障——如果你弄乱了注册表，计算机可能出故障，甚至无法启动！

我们不建议你使用注册表来存储 Java 程序的配置参数。Java 首选项 API 是更好的解决方案（更多信息参见第 I 卷第 10 章）。我们只是用注册表来演示如何将非平凡的本地 API 包装到 Java 类中。

检查注册表的主要工具是*注册表编辑器*。由于天真但热心的用户可能会出错，因此没有用于启动注册表编辑器的图标。而应启动 DOS shell（或打开“开始 → 运行”对话框）并输入 regedit。图 12.4 展示了正在使用中的注册表编辑器。

左侧显示项，它们按树结构排列。注意，每个项都以如下某个 HKEY 节点开头

```text
HKEY_CLASSES_ROOT
HKEY_CURRENT_USER
HKEY_LOCAL_MACHINE
. . .
```

右侧显示与特定项关联的名称/值对。例如，如果你安装了 Java 11，项

```text
HKEY_LOCAL_MACHINE\Software\JavaSoft\Java Runtime Environment
```

包含如下名称/值对

```text
CurrentVersion="11.0_10"
```

在这种情况下，值是字符串。值也可以是整数或字节数组。





![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_878_0.png)

图 12.4 注册表编辑器

### 12.10.2 用于访问注册表的 Java 平台接口

我们创建一个简单的接口，以便从 Java 代码访问注册表，然后用本机代码实现该接口。我们的接口只允许少量注册表操作；为了减小代码规模，我们省略了一些重要操作，例如添加、删除和枚举键。（添加其余的注册表 API 函数应该很容易。）

即使只提供有限的子集，你也可以

- 枚举存储在某个键中的所有名称
- 读取与某个名称一起存储的值
- 设置与某个名称一起存储的值

下面是封装注册表键的 Java 类：

```java
public class Win32RegKey
{
    public Win32RegKey(int theRoot, String thePath) { . . . }
    public Enumeration names() { . . . }
    public native Object getValue(String name);
    public native void setValue(String name, Object value);

    public static final int HKEY_CLASSES_ROOT = 0x80000000;
    public static final int HKEY_CURRENT_USER = 0x80000001;
    public static final int HKEY_LOCAL_MACHINE = 0x80000002;
    . . .
}
```

names 方法返回一个枚举，其中包含与该键一起存储的所有名称。你可以使用熟悉的 hasMoreElements/nextElement 方法获取它们。getValue 方法返回一个对象，该对象是字符串、Integer 对象或字节数组之一。setValue 方法的 value 参数也必须是这三种类型之一。

### 12.10.3 将注册表访问函数实现为本机方法

我们需要实现三种操作：

- 获取某个名称的值
- 设置某个名称的值
- 遍历某个键的名称

在本章中，你基本上已经看到了所需的全部工具，例如 Java 字符串和数组与 C 的字符串和数组之间的转换。你还看到了在出现错误时如何抛出 Java 异常。

有两个问题使这些本机方法比前面的示例更复杂。getValue 和 setValue 方法处理 Object 类型，该类型可以是 String、Integer 或 byte[] 之一。枚举对象在连续调用 hasMoreElements 和 nextElement 之间保存状态。

我们先来看 getValue 方法。该方法（如清单 12.22 所示）执行以下步骤：

1. 打开注册表键。注册表 API 要求键处于打开状态才能读取其值。
2. 查询与该名称关联的值的类型和大小。
3. 将数据读入缓冲区。
4. 如果类型是 REG_SZ（字符串），则调用 NewStringUTF 用值数据创建一个新字符串。
5. 如果类型是 REG_DWORD（32 位整数），则调用 Integer 构造函数。
6. 如果类型是 REG_BINARY，则调用 NewByteArray 创建一个新字节数组，然后调用 SetByteArrayRegion 将值数据复制到该字节数组中。
7. 如果类型不属于上述任何一种，或者调用 API 函数时发生错误，则抛出异常并释放截至当时已获取的所有资源。
8. 关闭该键并返回已创建的对象（String、Integer 或 byte[]）。

如你所见，这个示例很好地说明了如何生成不同类型的 Java 对象。

在这个本机方法中，处理通用返回类型并不困难。jstring、jobject 或 jarray 引用只需作为 jobject 返回。然而，setValue 方法接收一个 Object 的引用，并且必须确定该 Object 的确切类型，以便将该 Object 保存为字符串、整数或字节数组。我们可以通过查询值对象的类，找到 java.lang.String、java.lang.Integer 和 byte[] 的类引用，并将它们与 IsAssignableFrom 函数进行比较，从而做出这一判断。

如果 class1 和 class2 是两个类引用，那么调用

```c
(*env)->IsAssignableFrom(env, class1, class2)
```

当 class1 和 class2 是同一个类，或者 class1 是 class2 的子类时，返回 JNI_TRUE。无论哪种情况，指向 class1 对象的引用都可以转换为 class2。例如，当

```c
(*env)->IsAssignableFrom(env, (*env)->GetObjectClass(env, value),
    (*env)->FindClass(env, "[B"))
```

为真时，我们就知道 value 是一个字节数组。

下面是 setValue 方法中各步骤的概述：

1. 打开注册表键以进行写入。
2. 查找要写入的值的类型。
3. 如果类型是 String，则调用 GetStringUTFChars 获取指向字符的指针。
4. 如果类型是 Integer，则调用 intValue 方法获取存储在该包装对象中的整数。
5. 如果类型是 byte[]，则调用 GetByteArrayElements 获取指向字节的指针。
6. 将数据和长度传递给注册表。
7. 关闭该键。
8. 如果类型是 String 或 byte[]，则释放指向数据的指针。

最后，让我们转向枚举键的本机方法。这些是 Win32RegKeyNameEnumeration 类的方法（见清单 12.21）。枚举过程开始时，我们必须打开该键。在枚举期间，我们必须保留键句柄——也就是说，键句柄必须

由于注册表 API 是 Windows 特有的，因此该程序无法在其他操作系统上运行。

清单 12.23 展示了一个用于测试我们新增注册表函数的程序。我们向键

```
HKEY_CURRENT_USER\Software\JavaSoft\Java Runtime Environment
```

添加三个名称/值对：一个字符串、一个整数和一个字节数组。然后枚举该键的所有名称并检索它们的值。程序将打印

```
Default user=Harry Hacker
Lucky number=13
Small primes=2 3 5 7 11 13
```

虽然将这些名称/值对添加到该键可能不会造成损害，但在运行此程序后，你可能想使用注册表编辑器将它们删除。

#### 清单 12.21 Win32Reg/Win32RegKey.java

```java
1 import java.util.*;
2
3 /**
4  * A Win32RegKey object can be used to get and set values of a registry key in the Windows
5  * registry.
6  * @version 1.00 1997-07-01
7  * @author Cay Horstmann
8  */
9 public class Win32RegKey
10 {
11    public static final int HKEY_CLASSES_ROOT = 0x80000000;
12    public static final int HKEY_CURRENT_USER = 0x80000001;
13    public static final int HKEY_LOCAL_MACHINE = 0x80000002;
14    public static final int HKEY_USERS = 0x80000003;
15    public static final int HKEY_CURRENT_CONFIG = 0x80000005;
16    public static final int HKEY_DYN_DATA = 0x80000006;
17
18    private int root;
19    private String path;
20
21    /**
22     * Gets the value of a registry entry.
23     * @param name the entry name
24     * @return the associated value
25     */
26    public native Object getValue(String name);

/**
 * Sets the value of a registry entry.
 * @param name the entry name
 * @param value the new value
 */
public native void setValue(String name, Object value);

/**
 * Construct a registry key object.
 * @param theRoot one of HKEY_CLASSES_ROOT, HKEY_CURRENT_USER, HKEY_LOCAL_MACHINE,
 * HKEY_USERS, HKEY_CURRENT_CONFIG, HKEY_DYN_DATA
 * @param thePath the registry key path
 */
public Win32RegKey(int theRoot, String thePath)
{
    root = theRoot;
    path = thePath;
}

/**
 * Enumerates all names of registry entries under the path that this object describes.
 * @return an enumeration listing all entry names
 */
public Enumeration<String> names()
{
    return new Win32RegKeyNameEnumeration(root, path);
}

static
{
    System.loadLibrary("Win32RegKey");
}
}

class Win32RegKeyNameEnumeration implements Enumeration<String>
{
    public native String nextElement();
    public native boolean hasMoreElements();
    private int root;
    private String path;
    private int index = -1;
    private int hkey = 0;
    private int maxsize;
    private int count;

    Win32RegKeyNameEnumeration(int theRoot, String thePath)
    {
        root = theRoot;
        path = thePath;
    }
}

class Win32RegKeyException extends RuntimeException
{
   public Win32RegKeyException()
   {
   }

   public Win32RegKeyException(String why)
   {
      super(why);
   }
}
```

#### 清单 12.22 `win32reg/Win32RegKey.c`

```c
/**
 * @version 1.00 1997-07-01
 * @author Cay Horstmann
 */

#include "Win32RegKey.h"
#include "Win32RegKeyNameEnumeration.h"
#include <string.h>
#include <stdlib.h>
#include <windows.h>

JNIEXPORT jobject JNICALL Java_Win32RegKey_getValue(
               JNIEnv* env, jobject this_obj, jobject name)
{
   const char* cname;
   jstring path;
   const char* cpath;
   HKEY hkey;
   DWORD type;
   DWORD size;
   jclass this_class;
   jfieldID id_root;
   jfieldID id_path;
   HKEY root;
   jobject ret;
   char* cret;

   /* get the class */
```





#### 清单 12.22（续）

```c
const char* cvalue;
int ivalue;

/* get the class */
this_class = (*env)->GetObjectClass(env, this_obj);

/* get the field IDs */
id_root = (*env)->GetFieldID(env, this_class, "root", "I");
id_path = (*env)->GetFieldID(env, this_class, "path", "Ljava/lang/String;");

/* get the fields */
root = (*env)->GetIntField(env, this_obj, id_root);
path = (jstring)(*env)->GetObjectField(env, this_obj, id_path);
cpath = (*env)->GetStringUTFChars(env, path, NULL);

/* open the registry key */
if (RegOpenKeyEx(root, cpath, 0, KEY_WRITE, &hkey) != ERROR_SUCCESS)
{
    (*env)->ThrowNew(env, (*env)->FindClass(env, "Win32RegKeyException"),
        "Open key failed");
    (*env)->ReleaseStringUTFChars(env, path, cpath);
    return;
}

(*env)->ReleaseStringUTFChars(env, path, cpath);
cname = (*env)->GetStringUTFChars(env, name, NULL);

class_value = (*env)->GetObjectClass(env, value);
class_Integer = (*env)->FindClass(env, "java/lang/Integer");
/* determine the type of the value object */
if ((*env)->IsAssignableFrom(env, class_value, (*env)->FindClass(env, "java/lang/String")))
{
    /* it is a string--get a pointer to the characters */
    cvalue = (*env)->GetStringUTFChars(env, (jstring) value, NULL);
    type = REG_SZ;
    size = (*env)->GetStringLength(env, (jstring) value) + 1;
}
else if ((*env)->IsAssignableFrom(env, class_value, class_Integer))
{
    /* it is an integer--call intValue to get the value */
    jmethodID intValue = (*env)->GetMethodID(env, class_Integer, "intValue", "()I");
    ivalue = (*env)->CallIntMethod(env, value, intValue);
    type = REG_DWORD;
    cvalue = (char*)&ivalue;
    size = 4;
}
else if ((*env)->IsAssignableFrom(env, class_value, (*env)->FindClass(env, "B")))
{
    /* it is a byte array--get a pointer to the bytes */
    type = REG_BINARY;
    cvalue = (char*) (*env)->GetByteArrayElements(env, (jarray) value, NULL);
    size = (*env)->GetArrayLength(env, (jarray) value);
}
else
{
    /* we don't know how to handle this type */
    (*env)->ThrowNew(env, (*env)->FindClass(env, "Win32RegKeyException"),
        "Unsupported value type");
    RegCloseKey(hkey);
    (*env)->ReleaseStringUTFChars(env, name, cname);
    return;
}

/* set the value */
if (RegSetValueEx(hkey, cname, 0, type, cvalue, size) != ERROR_SUCCESS)
{
    (*env)->ThrowNew(env, (*env)->FindClass(env, "Win32RegKeyException"),
        "Set value failed");
}

RegCloseKey(hkey);
(*env)->ReleaseStringUTFChars(env, name, cname);

/* if the value was a string or byte array, release the pointer */
if (type == REG_SZ)
{
    (*env)->ReleaseStringUTFChars(env, (jstring) value, cvalue);
}
else if (type == REG_BINARY)
{
    (*env)->ReleaseByteArrayElements(env, (jarray) value, (jbyte*) cvalue, 0);
}

/* helper function to start enumeration of names */
static int startNameEnumeration(JNIEnv* env, jobject this_obj, jclass this_class)
{
    const char* cpath;
    HKEY hkey;
    DWORD maxsize = 0;
    DWORD count = 0;

    /* get the field IDs */
    jfieldID id_root = (*env)->GetFieldID(env, this_class, "root", "I");
    jfieldID id_path = (*env)->GetFieldID(env, this_class, "path", "Ljava/lang/String;");
    jfieldID id_hkey = (*env)->GetFieldID(env, this_class, "hkey", "I");
    jfieldID id_maxsize = (*env)->GetFieldID(env, this_class, "maxsize", "I");
    jfieldID id_index = (*env)->GetFieldID(env, this_class, "index", "I");
    jfieldID id_count = (*env)->GetFieldID(env, this_class, "count", "I");

    /* get the field values */
    jint root = (*env)->GetIntField(env, this_obj, id_root);
    jstring path = (jstring)(*env)->GetObjectField(env, this_obj, id_path);
    cpath = (*env)->GetStringUTFChars(env, path, NULL);

    /* open the registry key */
    if (RegOpenKeyEx(root, cpath, 0, KEY_READ, &hkey) != ERROR_SUCCESS)
    {
        (*env)->ThrowNew(env, (*env)->FindClass(env, "Win32RegKeyException"),
            "Open key failed");
        (*env)->ReleaseStringUTFChars(env, path, cpath);
        return -1;
    }
    (*env)->ReleaseStringUTFChars(env, path, cpath);

    /* query count and max length of names */
    if (RegQueryInfoKey(hkey, NULL, NULL, NULL, NULL, NULL, NULL, &count, &maxsize,
        NULL, NULL, NULL) != ERROR_SUCCESS)
    {
        (*env)->ThrowNew(env, (*env)->FindClass(env, "Win32RegKeyException"),
            "Query info key failed");
        RegCloseKey(hkey);
        return -1;
    }

    /* set the field values */
    (*env)->SetIntField(env, this_obj, id_hkey, (jint) hkey);
    (*env)->SetIntField(env, this_obj, id_maxsize, maxsize + 1);
    (*env)->SetIntField(env, this_obj, id_index, 0);
    (*env)->SetIntField(env, this_obj, id_count, count);
    return count;
}

JNIEXPORT jboolean JNICALL Java_Win32RegKeyNameEnumeration_hasMoreElements(JNIEnv* env,
    jobject thisObj)
{
    jclass this_class;
    jfieldID id_index;
    jfieldID id_count;
    int index;
    int count;
    /* get the class */
    this_class = (*env)->GetObjectClass(env, this_obj);

    /* get the field IDs */
    id_index = (*env)->GetFieldID(env, this_class, "index", "I");
    id_count = (*env)->GetFieldID(env, this_class, "count", "I");

    index = (*env)->GetIntField(env, this_obj, id_index);
    if (index == -1) /* first time */
    {
        count = startNameEnumeration(env, this_obj, this_class);
        index = 0;
    }
    else
        count = (*env)->GetIntField(env, this_obj, id_count);
    return index < count;
}

JNIEXPORT jobject JNICALL Java_Win32RegKeyNameEnumeration_nextElement(JNIEnv* env,
                                                     jobject this_obj)
{
    jclass this_class;
    jfieldID id_index;
    jfieldID id_hkey;
    jfieldID id_count;
    jfieldID id_maxsize;

    HKEY hkey;
    int index;
    int count;
    DWORD maxsize;

    char* cret;
    jstring ret;

    /* get the class */
    this_class = (*env)->GetObjectClass(env, this_obj);

    /* get the field IDs */
    id_index = (*env)->GetFieldID(env, this_class, "index", "I");
    id_count = (*env)->GetFieldID(env, this_class, "count", "I");
```

#### 清单 12.23 win32reg/Win32RegKeyTest.java

```java
import java.util.*;

/**
 * @version 1.03 2018-05-01
 * @author Cay Horstmann
 */
public class Win32RegKeyTest
{
    public static void main(String[] args)
    {
        var key = new Win32RegKey(
                Win32RegKey.HKEY_CURRENT_USER, "Software\\JavaSoft\\Java Runtime Environment");

        key.setValue("Default user", "Harry Hacker");
        key.setValue("Lucky number", new Integer(13));
        key.setValue("Small primes", new byte[] { 2, 3, 5, 7, 11 });

        Enumeration<String> e = key.names();

        while (e.hasMoreElements())
        {
            String name = e.nextElement();
            System.out.print(name + "=");

            Object value = key.getValue(name);

            if (value instanceof byte[])
                for (byte b : (byte[]) value) System.out.print((b & 0xFF) + " ");
            else
                System.out.print(value);

            System.out.println();
        }
    }
}
```

## 类型查询函数

- `jboolean IsAssignableFrom(JNIEnv *env, jclass cl1, jclass cl2)`
  
  如果第一个类的对象可以被赋值给第二个类的对象，则返回 JNI_TRUE，否则返回 JNI_FALSE。当两个类相同、cl1 是 cl2 的子类，或者 cl2 表示由 cl1 或其某个超类实现的接口时，该测试为真。




# 索引

## 数字

- `-`（减号）
  - 在权限中，558
  - 在策略文件中，557
  - 在正则表达式中，137
  - 在 URL 中，263
- `_`（下划线）
  - 在本地方法名中，811
  - 在 SQL 中，291、320
  - 在 URL 中，263
- `,`（逗号）
  - 十进制，380、387
  - 在 DTD 中，173
- `;`（分号）
  - 在类路径中，294
  - 在方法签名中，831
  - 在 SQL 中，295
  - 在注解中不需要，464
- `:`（冒号）
  - 作为文本文件中的分隔符，72
  - 在类路径中，294
  - 在权限中，558
  - 在 URL 中，252–253
- `!=` 运算符（SQL），291
- `?`（问号）
  - 在 DTD 中，173
  - 在 glob 模式中，120–141
  - 在预编译查询中，311
  - 在 URL 中，263
- `/`（斜杠）
  - 在方法签名中，832
  - 在路径中，64、109
  - 在 URL 中，252、553
- `.`（句点）
  - 十进制，380、387
  - 在方法签名中，832
  - 在正则表达式中，138、141
  - 在 URL 中，263
- `..`，在路径中，110
- `^`（脱字符），在正则表达式中，137、140–141
- `~`（波浪号），在 URL 中，263
- `. . .`，在 SQL 中，291
- `". . ."`，在 XML 中，156
- `(. . .)`
  - 在方法签名中，831
  - 在正则表达式中，139、142–144
- `[`（数组），类型代码，95、831
- `[. . .]`
  - 在 DOCTYPE 声明中，171
  - 在 glob 模式中，120
  - 在正则表达式中，137–138
  - 在 XPath 中，189
- `{. . .}`
  - 在注解中，474
  - 在 glob 模式中，120
  - 在消息格式化中，409–413
  - 在正则表达式中，140
- `@`（at 符号）
  - 在注解中，464
  - 在 URI 中，253
  - 在 XPath 中，189
- `$`（美元符号）
  - 在本地方法名中，811
  - 在正则表达式中，138、140–141、150
- `${. . .}`，在策略文件中，558
- `*`（星号）
  - 在 DTD 中，173
  - 在 glob 模式中，120
  - 在权限中，558
  - 在策略文件中，557
  - 在正则表达式中，140–141
- `\`（反斜杠）
  - 在 glob 模式中，120
  - 在路径中，64、109
  - 在权限中（Windows），558
  - 在正则表达式中，137–138、141、150
- `\\`，在正则表达式中，73
- `&`（和号）
  - 在 CDATA 段中，159
  - 在实体引用中，158
  - 解析，173
- `&&`，在正则表达式中，138
- `&amp;`、`&apos;`，在字符引用中，158
- `&amp;`，实体引用，158
- `#`（井号）
  - 在消息格式化中，412–413
  - 在 URL 中，252
- `%`（百分号）
  - 在区域设置中，387
  - 在 SQL 中，291、320
  - 在 URL 中，263
- `+`（加号）
  - 在 DTD 中，173
  - 在正则表达式中，140–141
  - 在 URL 中，263
- `<`（左尖括号）
  - 在 CDATA 段中，159
  - 在消息格式化中，413
  - 解析，173
- `<!...>`、`<...>`、`<?...>`、`<![CDATA[...]]>`，在 XML 中，159
- `< . . >`，在正则表达式中，139
- `<=` 运算符，413
- `>`（右尖括号），在 XML 中，159
- `==`、`<=>` 运算符（SQL），291
- `=>` 运算符，在枚举中，103
- `|`（竖线）
  - 作为文本文件中的分隔符，72
  - 在 DTD 中，173–174
  - 在消息格式化中，412
  - 在正则表达式中，139、141
- `\b`，在正则表达式中，138
- 1931 CIE XYZ 颜色规范，758
- 2D 图形。参见 Java 2D API

## A

- `\a`、`\A`，在正则表达式中，138、140
- abort 方法（LogiMLModule），582
- absolute 方法（ResultSet），325、328
- AbstractCellEditor 类，643–645
  - isCellEditable 方法，644
- AbstractProcessor 类，485
- AbstractTableModel 类，618
  - isCellEditable 方法，641
- accept 方法（ServerSocket），236、239–240
- acceptChanges 方法（CacheModule），332–333
- AccessController 类
  - getContext 方法，572
- 累加器函数，42
- 动作监听器
  - 添加注解，465–471
  - 安装，466
- action.properties 文件，457
- ActionListener 接口
  - actionPerformed 方法，466
- @ActionListenerFor 注解，465、482
- ActionListenerInstaller 类
  - processAnnotations 方法，466
- add 方法
  - Area 的，714–715
  - AttributeSet 的，802
  - DefaultTableModel 的，655、663
- addActionListener 方法（ButtonFrame），465–466
- addAttribute 方法（AttributesImpl），226
- addBatch 方法（Statement），346–347
- addCellEditorListener 方法（CellEditor），652
- addColumn 方法（JTable），630、636
- 加法运算符的单位元，41
- addRecipient 方法（MimeMessage），279
- addTreeModelListener 方法（TreeModel），685、693
- addTreeSelectionListener 方法（JTree），677
- addURLs 方法（URLClassLoader），532
- AES（高级加密标准），600
  - 在其中生成密钥，602–607
- aesTest.java，603
- aes/Util.java，605
- 仿射变换，730、764
- AffineTransform 类，730–732
  - 构造方法，731
  - getXxxInstance 方法，730–732
  - setToXxx 方法，730、732
- AffineTransformOp 类，764
  - 构造方法，771
  - TYPE_XXX 字段，764、771
- afterLast 方法（ResultSet），325、328
- 代理代码，496–497
- 别名，用于命名空间，179、195
- allMatch 方法（Stream），16
- allocate 方法（ByteBuffer），131、133
- AlphaComposite 类，550、556、560
- Alpha 通道，735–739
- Alpha 合成，744
- AlphaComposite 类，738
  - getInstance 方法，739、744
- 锚点矩形，726
- andFilter 方法（RowFilter），629、638
- **AnnotatedConstruct** 接口，486
- **AnnotatedElement** 接口
  - getAnnotation 方法，466、470、484、486
  - getAnnotations、isAnnotationPresent 方法，470
  - getAnnotationsByType 方法，470、484、486
  - getDeclaredAnnotations 方法，471
- **Annotation** 接口
  - 扩展，471
  - 其方法，472
- **Annotation** 接口，465、471–472
  - 预定义，478–484
- **注解处理器**，484
  - 在字节码级别，466、489
  - 在运行时，466
- **注解**，463–471
  - 适用性，481
  - 文档化，482–483
  - 元素，464、472、474
  - 用于编译，480
  - 用于局部变量，476
  - 用于管理资源，480
  - 用于包，475
  - 用其生成源代码，486–489
  - 继承的，483
  - 标记，473
  - 元，465、479–484
  - 无注解可用于，477
  - 中没有循环依赖，475
  - 处理工具，463
  - 可重复，484
  - 保留，482
  - 单值，473
  - 源代码级，484–489
  - 标准，478–484
  - 语法，471–478
  - 瞬态，482
  - 与 Javadoc 注释对比，464
- ANY 元素内容（DTD），173
- anyMatch 方法（Stream），16
- Apache，153、160
  - Commons CSV 库，515
  - Derby 数据库，293–299
    - 连接到，296
    - 驱动程序，294–296
    - 填充，306–310
    - 启动，294–295
  - Tomcat，350
- Apollo 11 的发射，358、367
- Apps，实体引用，158
- append 方法
  - **Appendable** 的，62–63
  - 形状类的，703、714
- **Appendable** 接口，59–63
- appendChild 方法（Node），207、209
- **Applet**
  - 用于 Applet 的类加载器，534
  - 代码基，547
  - 从安全内网执行，583
  - 不退出 JVM，546
- 应用服务器，350、480
- **应用程序**
  - 配置，154–155
  - 企业级，349–351
  - 无需单独的 Java 运行时即可执行，526
  - 本地化，417
  - 监控，496–497
  - 付费，537
  - 服务器端，261–270
  - 签名，597–599
- applyPattern 方法（MessageFormat），411
- apply-templates 元素（XSLT），218
- Arc2D 类，697、699–700
- Arc2D.Double 类，697–698、713
- Arc2D.Float 类，697
- Archmaker 类，704
- **弧**
  - 边界矩形，697、700
  - 闭合类型，700
  - 计算角度，701
- **Area** 类
  - add 方法，714–715
  - exclusiveOr、intersect、subtract 方法，715
- ARGB（Alpha、Red、Green、Blue），739、758
- ARRAY 数据类型（SQL），348–349
- ArrayIndexOutOfBoundsException，845
- **数组**
  - 与流之间转换，5、25、49
  - 从数据库获取，349
  - 在注解元素中，474
  - 在本地代码中，840–844
  - 基本类型数组，843



- 数组（续）
  - 字符串数组，147
  - 类型代码，95、831
  - 中的类型使用注解，476
- Array 类
  - stream 方法，5、9、43
- ArrayStoreException，845
- asCharBuffer 方法（ByteBuffer），132
- ASCII 标准，75
  - 与本地代码，820
  - 在属性文件中，419
  - 在正则表达式中，141
- ASM 库，489–498
- ASP（Active Server Pages），261
- 结合操作，41
- ATTLIST 声明（DTD），174
- attribute 元素（XML Schema），181
- Attribute 接口，799
  - getCategory 方法，801、806
  - getName 方法，806
  - 实现，801
- 属性集，801
- 属性（XML）
  - 枚举，164
  - 用于枚举类型，175
  - 在 XML Schema 中，181
  - 合法的，174
  - 名称，156
  - 命名空间，195
  - 值，156
    - 在 XPath 中访问，189
    - 使用 XSLT 复制，219
    - 默认值（DTD），175
    - 规范化，175
  - 与元素对比，157–158、175、216
- Attributes 接口
  - getXXX 方法，202
- Attributed 接口，800
  - add、get 方法，802、806
  - remove、toArray 方法，807
- AttributesInput 类
  - addAttribute 方法，226
  - clear 方法，226
- atZone 方法（LocalDateTime），367
- AudioPermission 类，556
- auth/AuthTest.java，570
- auth/AuthTest.policy，571
- auth/jaas.config，571
- auth/SysPropAction.java，570
- 认证，566–582
  - 问题，592–593
  - 基于角色的认证，573
  - 与业务逻辑分离，568
  - 通过可信中介，593–594
- AuthPermission 类，557
- 自动装箱，615
- AutoCloseable 接口
  - close 方法，61
- 自动提交模式（数据库），344–346
- 自动刷新，69
- 自动生成的键，322
- 生成的辅助文件，463
- available 方法（InputStream），57–58
- average 方法（原始类型流），44、46–47
- AWT（抽象窗口工具包），693–744
- AWTPermission 类，555

## B

- B（byte），类型代码，95、831
- `\b`、`\B`，在正则表达式中，140
- 分带，775
- Banner 类
  - getPageCount、layoutPages 方法，783
- 横幅，打印，782–792
- BASE64Encoder 类，507
- BaseStream 接口
  - iterator 方法，28
  - parallel 方法，48、53
  - unordered 方法，53
- BasicFileAttributes 接口，117
  - 方法，118
- BasicPermission 类，557
- BasicStroke 类，715–724
- 批量更新（数据库），345–348
- BCP 47 备忘录，382
- 生成的 Bean 信息类，463
- beforeFirst 方法（ResultSet），325、328
- between 方法（Duration），355、357
- 斜角连接，716–717
- 贝塞尔曲线，703
- 双三次、双线性插值，764、771
- BIG_ENDIAN 常量（ByteOrder），131
- 大端序，78、416
- 二进制数据
  - 转换为 Unicode 代码单元，68
  - 读取，79
  - 与文本对比，68
- ByteBuffer 类（续）
  - asCharBuffer 方法，132
  - get、getXxx 方法，126、131
  - order 方法，126、131
  - put、putXxx 方法，127、131
  - wrap 方法，132–133
- bytecodeAnnotations.EntryLogger.java，492
- bytecodeAnnotations.EntryLoggingAgent.java，497
- 字节码
  - 工程，489–498
    - 在加载时，495–497
  - 使用十六进制编辑器，544
  - 验证，541–545
- ByteLookupTable 类，765
  - 构造函数，771
- ByteOrder 类
  - BIG_ENDIAN、LITTLE_ENDIAN 常量，131
- 面向字节的输入/输出流，56
- 字节，读取/写入，56–59

## C

- C（char），类型代码，95、831
- C 编程语言
  - 中的数组类型，840–844
  - 中的引导类加载器，531
  - 从中调用 Java 方法，833–840
  - 中的数据库访问，284
  - 将 JVM 嵌入其中，849–854
  - 中的 FILE* 类型，59
  - 中的指针，810
  - 中的字符串，819
  - 类型，与 Java 类型对比，817
- `\c`，在正则表达式中，138
- C++ 编程语言
  - 中访问 JNI 函数，820
  - 中的数组类型，840
  - 将 JVM 嵌入其中，849–854
  - 中的异常，845
  - 用于本地方法，810、813
  - 中的指针，810、835
- 缓存行集，330–335
- CacheHost 接口，330–333
  - acceptChanges 方法，332–333
    - execute、nextPage、populate 方法，331、333
  - get/setPageSize 方法，331、333
  - get/setTableName 方法，332–333
  - previousPage 方法，333
- CachedRowSetImpl 类，507
- 凯撒密码，536–537
- Calendar 类，353
  - 格式化其对象，395
  - 中的周末，360
- call 转义（SQL），320
- call 方法（CompletionTask），454、462
- 调用栈，在权限检查期间，550
- Callable 接口，454
- Callback 接口，574
- CallbackHandler 接口
  - handle 方法，581
- CallNonvirtualXxxMethod 函数（C），836、839
- CallStaticXxxMethod 函数（C），834–835、839
- CallXxxMethod 函数（C），833、838–839
- cancelCellEditing 方法（CellEditor），644–645、652
- cancelRowUpdates 方法（ResultSet），326、329
- canInsertImage 方法（ImageWriter），748、755
- capacity 方法（Buffer），134
- 回车字符，显示，164
- 强制类型转换，中的类型使用注解，476
- Catalog 元素（XML），172
- CatalogFeatures 类
  - defaults 方法，172、179
- CatalogManager 类
  - catalogResolver 方法，172、178
- 目录，343
- CDATA 声明（DTD），174–175
- CDATA 节（XML），159
- 单元格编辑器（Swing），641–642
  - 自定义，642–652
- 单元格渲染器（Swing），639–652
  - 用于表格，622、639
  - 用于树，674–676
- CellEditor 接口
  - add/removeCellEditorListener 方法，652
  - cancelCellEditing 方法，644–645、652
  - getCellEditorValue 方法，641、644–645、652
  - isCellEditable 方法，652
  - shouldSelectCell 方法，644、652
  - stopCellEditing 方法，644–645、652
- 单元格（Swing）
  - 编辑，641–642
  - 选择，626
- 证书，566、589–592
  - 与 Java 插件，598
  - 管理，596–597
  - 发布其指纹，591
  - 根证书，599
  - 证书集，547
  - 签名，594–597
- CertificateSigner 类，595
- CGI（公共网关接口），261
- 信任链，593
- 通道，245
  - 用于文件，125
- Channels 类
  - newInputStream 方法，251
  - newOutputStream 方法，245、251
- char 类型
  - 的流，43
  - 的类型代码，95、831
  - 与 C 类型对比，817
- CharARRAY 类（DocFlavor），794
- 字符类，137
- CHARACTER 数据类型（SQL），293、348
- 字符编码，68、75–77
  - 显式指定，77
  - 部分，76
  - 平台，77、413
- 字符引用（XML），158
- CharacterData 接口
  - getData 方法，163、169
- 字符
  - 之间的差异，402
  - 转义，73、141
  - 在正则表达式中，141
  - 规范化，403
  - 轮廓，733
  - 打印，69
  - 以二进制格式写入，78
- characters 方法（ContentHandler），197、201
- CharBuffer 类，62、132
  - get、put 方法，132
- CharSequence 接口，62、142
  - charAt、length 方法，63
  - chars 方法，43
  - codePoints 方法，43、47
  - 按正则表达式拆分，6
  - subSequence、toString 方法，63
- Charset 类
  - defaultCharset 方法，77、415
  - forName 方法，77
- 复选框（Swing），639
- checked 属性（HTML、XML），156
- 受检异常，568
- Checker 框架，476
- checkError 方法（PrintWriter），69–70
- checkExit 方法（SecurityManager），546、549
- checkLogin 方法（SimpleLoginModule），573
- checkPermission 方法（SecurityManager），549–550、559–560
- checkRead 方法（SecurityManager），550
- 子元素（XML），157
  - 命名空间，194
- 子节点（Swing），652
  - 添加，655
  - 连接线，658–659
- children 方法（TreeNode），671
- choice 元素（XML Schema），181
- choice 关键字（消息格式化），412
- Church, Alonzo，358
- Cipher 类，600–601
  - doFinal 方法，601、603、606–607
  - getInstance 方法，600、606
  - getXxxSize 方法，606
  - init 方法，606
  - update 方法，601、603、606–607
  - XXX 模式，600
- CipherInputStream 类
  - read 方法，608
- CipherOutputStream 类，607
  - 构造函数，608
  - flush、write 方法，608
- 密码
  - 生成密钥，602–607
  - 中的公钥，608–612
  - 用于密码的流，607–608
  - 对称密码，600–601
- 循环依赖，在注解中，475
- Class 类
  - forName 方法，456
  - getClassLoader 方法，531、540
  - getFields 方法，687
  - getProtectionDomain 方法，551
  - getResourceAsStream 方法，514
  - 实现 AnnotatedElement，466
- .class 文件扩展名，530
- 类文件，530
  - 损坏，542–545
  - 加密，535、537
  - 格式，489



- 类文件（续）
  - 加载，530
  - 修改，490–495
  - 可移植性，416
  - 转换器，496
  - 验证，541–545

- 类加载器，457, 530–545
  - 作为命名空间，534
  - 引导类加载器，531
  - 上下文类加载器，532–534
  - 创建，546
  - 扩展类加载器，531
  - 层次结构，532–534
  - 平台类加载器，531
  - 每个网页单独使用，534
  - 指定，532
  - 系统类加载器，531
  - 编写，534–541

- 类路径，向其中添加 JAR 文件，532
- 类引用，在本机代码中，827

- 类
  - 添加验证，100
  - 注解，464, 475, 479
  - 动态编译，455
  - 描述，94
  - 封装，500
  - 可外部化，95
  - 继承树，673
  - 不可序列化，100
  - 覆盖平台类，531
  - 保护域，549
  - 解析，530
  - 每个网页单独使用，534
  - 可序列化，88–89
  - 版本控制，103–106

- 分类器函数，35
- ClassLoader 类，531
  - defineClass、findClass 方法，534, 541
  - 扩展，456, 534
  - getParent 方法，540
  - getSystemClassLoader 方法，541
  - loadClass 方法，534

- 类加载器反转，532
- classLoader/Caesar.java，540
- classLoader/ClassLoaderTest.java，537
- CLASSPATH 环境变量，531
- CLEAR 合成规则，737

- clear 方法
  - AttributesImpl 的，226
  - Buffer 的，133–134

- clearParameters 方法（PreparedStatement），317
- client/HttpClientTest.java，273
- 客户端/服务器应用程序，287

- 客户端
  - 连接到服务器，230–232
  - 服务多个客户端，239–243

- clip 方法（Graphics2D），695, 733–735, 775
- 剪贴板，访问，546

- 剪裁区域
  - 打印，775
  - 设置，695

- 剪裁形状，694, 733–735
- CLOB 数据类型（SQL），293, 348
- Clob 接口，317
  - getCharacterStream 方法，318–319
  - getSubString 方法，318–319
  - length 方法，319
  - setCharacterStream 方法，319

- CLOB（字符大对象），317
  - 创建空的，319
  - 放入数据库，318

- clone 方法，89, 106
- 克隆，106–108

- close 方法
  - AutoCloseable 的，61
  - Connection 的，301, 303, 351
  - FileLock 的，136
  - Flushable 的，59
  - InputStream 的，57–58
  - OutputStream 的，59
  - ResultSet 的，303
  - ServerSocket 的，239
  - Statement 的，302–303
  - XMLStreamWriter 的，215

- Closeable 接口，59
  - close 方法，59, 62
  - flush 方法，60

- 封闭的非本地图标，661–662, 674
- closeEntry 方法（ZipEntry），85–87
- closeOnCompletion 方法（Statement），302
- closePath 方法（Path2D），703, 714
- 闭包类型，700
- cmd shell，415
- 代码基，547, 553
- 代码生成，注解，463–471, 480
- 码点，11
- 代码源，547

- compareTo 方法（续）
  - String 的，402

- *Compilable* 接口
  - compile 方法，447

- *CompilationTask* 接口，453
  - call 方法，454, 462

- compile 方法（*Pattern*），142, 148

- *CompiledScript* 接口
  - eval 方法，447

- 编译器
  - 注解，480
  - 调用，453
  - 即时编译，850

- compiler/CompilerTest.java，458
- 复杂类型，179
- complexType 元素（XML Schema），180
- *Composite* 接口，738
- composite/CompositeComponent.java，741
- composite/CompositeTestFrame.java，740
- composite/Rule.java，743
- 合成规则，694–695, 735–744
- *计算机图形学：原理与实践*（Foley 等），703, 738, 758
- concat 方法（Stream），13
- 机密信息，传输，600
- 配置文件，135

- connect 方法
  - Socket 的，233
  - URLConnection 的，251, 256, 260

- *Connection* 接口
  - close 方法，301, 303, 351
  - commit 方法，345–347
  - createBlob、createClob 方法，318–319
  - createStatement 方法，299, 301, 323, 327, 345
  - get/setAutoCommit 方法，347
  - getMetaData 方法，334, 343
  - getWarnings 方法，306
  - prepareStatement 方法，311, 317, 323, 327
  - releaseSavepoint 方法，345, 347
  - rollback 方法，345–347
  - setSavepoint 方法，347

- 连接（数据库）
  - 关闭，303
  - 关闭后使用行集，330
  - 调试，280
  - 连接池，350
  - 启动新线程，240

- console 方法（System），415
- 构造区域几何运算，714
- Constructor 类，466
- 构造器
  - 注解，475
  - 从本机代码调用，835
  - 类型使用注解，476

- containsAll 方法（Collection），561
- 内容类型，254

- *ContentHandler* 类，197–198
  - characters 方法，197, 201
  - start/endDocument 方法，201
  - start/endElement 方法，197–201

- 上下文类加载器，532–534
- 控制点
  - 拖动，704
  - 曲线的，702–703
  - 形状的，704

- convertXxxIndexToModel 方法（JTable），626, 636
- 卷积运算，765

- *ConvolveOp* 类，764–766
  - 构造器，772

- *CookieHandler* 类
  - setDefault 方法，267

- Cookie，267
- 坐标系
  - 自定义，695
  - 平移，776

- 坐标变换，727–732

- *Copies* 类，799–802
  - getValue 方法，802

- *CopiesSupported* 类，800
- copy 方法（Files），114–115
- CORBA（公共对象请求代理体系结构），500, 531
- 核心 Swing（顶层），614, 652, 666
- count 方法（Stream），3–4, 15, 189
- counting 方法（Collectors），36, 40
- 国家/地区代码，35, 382
- CRC32 校验和，87, 125, 127

- *CRC32* 类，127

- CREATE TABLE 语句（SQL）
  - 执行，300–301, 317
  - 在批处理更新中，346

- createBindings 方法（ScriptEngine），443
- createBlob、createClob 方法（Connection），318–319
- createDirectory、createDirectories、createFile 方法（Files），113–114
- createElement 方法（Document），206–207, 209
- createElementNS 方法（Document），207, 209
- createImageXxxStream 方法（ImageIO），747, 753
- createPrintJob 方法（PrintService），793, 795
- createStatement 方法（Connection），299, 301, 323, 327, 345
- createTempXxx 方法（Files），113–114
- createTextNode 方法（Document），207, 209
- createXMLStreamReader 方法（XMLInputFactory），205
- createXMLStreamWriter 方法（XMLOutputFactory），210, 214
- createXxxSet 方法（RowSetFactory），330, 333
- creationTime 方法（BasicFileAttributes），118
- 信用卡号码，传输，600
- crypt 程序，603
- 密码学与网络安全（Stallings），584, 594
- 三次曲线，702–703
- CubicCurve2D 类，697, 699, 703
- CubicCurve2D.Double 类，697–698, 713
- CubicCurve2D.Float 类，697
- 货币，393–394
  - 可用的，394
  - 格式化，387–394
  - 标识符，393

- Currency 类，393–394
  - getAvailableCurrencies、getCurrencyCode、getDefaultFractionDigits、getNumericXxx、getSymbol 方法，394
  - getInstance 方法，393–394
  - toString 方法，394

- curveTo 方法（Path2D.Float），703, 713
- 自定义编辑器，642–652

## D

- D（double），类型代码，95, 831
- d 字面量（SQL），320
- \d、\D，在正则表达式中，139
- 虚线，717–718

- 数据
  - 指纹，583–587
  - 已签名，587–589

- 数据源（用于 JNDI 服务），350
- 数据类型
  - 类型代码，95, 831
  - 在 Java 与 C 中，817
  - 名称改编，831
  - 打印服务，792–794

- database.properties 文件，307, 349

- DatabaseMetaData 接口，334–344
  - getJDBCXxxVersion 方法，343
  - getMaxConnections 方法，343
  - getMaxStatements 方法，303, 343
  - getSQLStateType 方法，304
  - getTables 方法，334, 343
  - supportsBatchUpdates 方法，346, 348
  - supportsResultSetXxx 方法，324, 329

- 数据库
  - 用 C 语言访问，284
  - 自动提交模式，344–346
  - 自动编号键，322
  - 批处理更新，345–348
  - 缓存预编译语句，312
  - 使用 SQL 更改数据，292
  - 数据库连接，294, 296–299, 307
    - 关闭，303, 308
    - 在 Web 和企业应用程序中，349–351
  - 连接池，350
  - 驱动程序，285–286
  - 数据重复，289
  - 错误处理，346
  - 完整性，344
  - LOB，317–319
  - 元数据，334–344
  - 修改，330
  - XML 的本机存储，349
  - 列编号，300
  - 外连接，320
  - 填充，306–310
  - 将对象保存到，483
  - 标量函数，320
  - 模式，343
  - 设置参数，331
  - 启动，294–295
  - 存储过程，320
  - 结构，287, 334
  - 同步，332
  - 工具，336
  - 截断的数据，305


- 数据库 *（续）*
  - 其 URL，294
- DataFlavor 类，501
- DataInput 接口
  - readBoolean 方法，79
  - readChar 方法，79，81
  - readDouble 方法，79，89，101
  - readFloat 方法，79
  - readFully 方法，79，89，101
  - readInt 方法，79，81，89
  - readLong 方法，79
  - readShort 方法，79
  - readUTF 方法，79–80
  - skipBytes 方法，80
- DataInputStream 类，59，64
- DataIO 类
  - xxxFixedString 方法，81–82
- DataOutput 接口
  - writeBoolean 方法，78，80
  - writeByte 方法，78，80
  - writeChar 方法，78，80–81
  - writeDouble 方法，78，80，89，101
  - writeFloat 方法，78，80
  - writeInt 方法，78，80–81，89
  - writeLong 方法，78，80
  - writeShort 方法，78，80
  - writeUTF 方法，78，80
- DataOutputStream 类，59
- DataSource 接口，350
- DataTruncation 类，305
  - 其方法，306
- Date and Time API，353–377
  - 与遗留代码，376–377
- Date 类（java.sql），376
  - valueOf 方法，377
- Date 类（java.util），95，353，376
  - 格式化其对象，395
  - 其中的月份和年份，359
  - readObject、writeObject 方法，101
- DATE 数据类型（SQL），293，320，348
- dateFilter 方法（RowFilter），629，638
- DateFormat 类，373，377，396
- dateFormat/DateTimeFormatterTest.java，397
- dateFormat/EnumCombo.java，400
- 日期
  - 计算，359，364–365
  - 过滤，629
  - 格式化，371–376，380，394–401
  - 字面量，319
  - 本地日期，358–363
  - 解析，373
- datesUntil 方法（LocalDate），360，363
- DateTimeFormatter 类，371–376，394–401
  - format 方法，371，375，401
  - 与遗留类，376–377
  - ofLocalizedXxx 方法，372，375，394，401
  - ofPattern 方法，373，376
  - parse 方法，373
  - toFormat 方法，373，377
  - withLocale 方法，372，376，401
- DateTimeParseException，401
- DateTimeSyntax 类，802
- 夏令时，367–371
- DayOfWeek 枚举，360
  - getDisplayName 方法，373，395
- dayOfWeekInMonth 方法（TemporalAdjusters），365
- DBeaver 程序，336
- DDL 语句（SQL），301，317
- 调试
  - 在 JNI 中，850
  - 与 JDBC 相关的问题，297
  - 区域设置，386
  - 邮件连接，280
  - 流，14
- DECIMAL 数据类型（SQL），293，348
- 小数分隔符，380，387
- 声明注解，475–477
- decode 方法（URLDecoder），270
- 解密密钥，536
- default 语句，471
- DefaultCellEditor 类
  - 构造方法，651
  - 变体，641
- defaultCharset 方法（Charset），77，415
- DefaultHandler 类，198
- DefaultMutableTreeNode 类，654，672–673
  - add 方法，655，663
  - 构造方法，663
  - pathFromAncestorEnumeration 方法，673
  - setAllowsChildren、setAsksAllowsChildren 方法，661，663
  - xxxFirstEnumeration、xxxOrderEnumeration 方法，662，676
- defaultPage 方法（PrinterJob），781
- **DefaultRowSorter 类**
  - setComparator、setSortable 方法，628，637
  - setRowFilter 方法，629，637
- defaults 方法（catalogFeatures），172，179
- **DefaultTableCellRenderer 类**，640
- **DefaultTableModel 类**
  - isCellEditable 方法，641
- **DefaultTreeCellRenderer 类**，674–676
  - setXXIcon 方法，676
- **DefaultTreeModel 类**，664，686
  - 由其自动通知，666
  - getPathToRoot 方法，666
  - insertNodeInto 方法，665，671
  - isLeaf 方法，661
  - nodeChanged 方法，665，671
  - nodesChanged 方法，671
  - reload 方法，666，671
  - removeNodeFromParent 方法，665，671
- defaultWriteObject 方法（ObjectOutputStream），101
- defineClass 方法（ClassLoader），535，541
- DELETE 方法（HttpRequest.Builder），278
- DELETE 语句（SQL），292
  - 执行，300–301，317
  - 在批量更新中，346
  - 与 ResultSet 的方法对比，327
- delete、deleteIfExists 方法（Files），115
- deleteGlobalRef 函数（C），827
- deleteRow 方法（ResultSet），327，329
- 分隔符，在文本文件中，72
- @Deprecated 注解，479–480
- 深度优先枚举，672
- depthFirstEnumeration 方法（DefaultMutableTreeNode），672，676
- derbyclient.jar 文件，294
- DES（数据加密标准），600
- DestroyJavaVM 函数（C），850，854
- 设备坐标，727
- **Diagnostic 接口**，454
  - 其方法，462
- **DiagnosticCollector 类**，454
  - 构造方法，462
  - getDiagnostics 方法，462
- **DiagnosticListener 接口**，454
- **DialogCallbackHandler 类**，574
- digest 方法（MessageDigest），585，587
- DigiCert，591，593
- 数字指纹，94，583–587
- 数字签名，587–589
  - 验证，589–592
- 直接缓冲区，843
- **目录**
  - 创建，113–114
  - 当前目录，122
  - 层次结构，652
  - 打印其所有子目录，121
  - 遍历，118–123
  - 用户的工作目录，64
- **DirectoryStream 接口**，120
- discarding 方法（BodyHandlers），272
- distinct 方法（Stream），14–15，50
- dividedBy 方法（Duration），358
- doAs、doAsPrivileged 方法（Subject），568–569，572
- **Doc 接口**，793
- **DocAttribute 接口**，799
  - 实现，801
  - 打印其属性，803–806
- **DocAttributeSet 接口**，800–801
- **DocFlavor 类**，793–794，796
- **DocPrintJob 接口**
  - getAttributes 方法，807
  - print 方法，795
- DOCTYPE 声明（DTD），171
  - 包含在输出中，208
- **Document 接口**
  - createText 方法，206–207，209
  - getDocumentElement 方法，160，168
- 文档类型，用于打印服务，793–794
- **DocumentBuilder 类**
  - newDocument 方法，206，208，221
  - parse 方法，168
  - setEntityResolver 方法，172，177
  - setErrorHandler 方法，177
- **DocumentBuilderFactory 类**
  - isIgnoringElementContentWhitespace 方法，179
  - isNamespaceAware 方法，196
  - isValidating 方法，179
  - newDocumentBuilder 方法，160，167，207
  - newInstance 方法，160，167
  - setIgnoringElementContentWhitespace 方法，176，179
  - setNamespaceAware 方法，182，195–196，199，207
  - setValidating 方法，176，179
- @Documented 注解，479，482–483
- doFinal 方法（Cipher），601，605，606–607
- DOM（文档对象模型）解析器，159–160，196–197
  - 其命名空间感知，195，199
  - 其中的树：
    - 使用 XPath 访问，188–193
    - 分析，162–164
    - 构建，197，206–216，221
    - 写入，208–210
- dom4j/SAXConverter.java，165
- DOMResult 类，221，226
- DOMSource 类，210，220
- DOUBLE 数据类型（SQL），293，348
- double 类型
  - 打印，69
  - 其流，43
  - 其类型代码，95，831
  - 与 C 类型对比，817
  - 以二进制格式写入，78
- DoubleBuffer 类，132
- doubles 方法
  - Random 的，44，47，51
  - SplittableRandom 的，51
- DoubleStream 接口，43–48
  - 其方法，47
- DoubleSummaryStatistics 类，26，29–30，44，48
- doubleValue 方法（Number），387
- 下游收集器，36–40，50
- draw 方法（Graphics2D），695–697，715
- 绘图
  - 创建，693–744
  - 打印，772–782
- drawXxx 方法（Graphics），696
- DriverManager 类，296
  - getConnection 方法，296–297，307，351
  - setLogWriter 方法，297
- DROP TABLE 语句（SQL），297
  - 执行，300–301
  - 在批量更新中，346
- drainTo 方法（Stream），13
- DSA（数字签名算法），587–588
- DST，见合成规则，737
- DTDHandler 类，198
- DTD（文档类型定义），170–179
  - 其中的元素内容，173–174
  - 其中的实体，176
    - 外部实体，171
  - 在 XML 文档中，156，171–179
  - 定位，171–172
  - 无歧义，174
  - 其 URI，171
- Duration 类
  - between 方法，355，357
  - dividedBy 方法，358
  - getSeconds 方法，355
  - 其不可变性，355
  - isNegative、isZero 方法，358
  - minus、minusXxx 方法，358
  - multipliedBy 方法，358
  - negated 方法，358
  - ofXxx 方法，357
  - plus、plusXxx 方法，358
  - toXxx 方法，355，358
- 动态链接，850
- 动态网页，457–463

## E

- \e、\E，在正则表达式中，138
- 回显服务器，238–239
- Eclipse IDE，509
- 边缘检测，766
- 编辑器，自定义，642–652
- element 元素（XML Schema），180
- ELEMENT 元素内容（DTD），173–174
- Element 接口，485
  - getAttribute 方法，164，168
  - getSimpleName 方法，486
  - getTagName 方法，161，168，195
  - setAttribute、setAttributeNS 方法，207，209
- 元素（XML）
  - 子元素，157
  - 在 XPath 中访问，189
  - 命名空间，194
  - 构造，206
  - 在 XPath 中计数，189
  - 空元素，156
  - 合法属性，174
  - 名称，161，195
  - 根元素，157，179
  - 修剪其中的空白，163
  - 与属性对比，157–158，175，216
- Ellipse2D 类，697，699
- Ellipse2D.Double、Ellipse2D.Float 类，697




- 椭圆：边界矩形，697
- 电子邮件
  - 发送，278–281
  - 行终止，279
- employee/Employee.c, 829
- employee/Employee.java, 828
- employee/EmployeeTest.java, 828
- EMPTY 元素内容（DTD），173
- empty 方法
  - Optional 的，20–21
  - Stream 的，5, 9
- 空标签（XML），156
- 封装，500
- encode 方法（URLEncoder），270
- 加密，599–612
  - 其中的末尾块填充，601
  - 类文件的，535, 537
- end 方法
  - Matcher 的，143, 145, 149–150
  - MatchResult 的，146, 150
- 端帽样式，716–718
- 末端指针，702
- 结束标签（XML），156
- endDocument 方法（ContentHandler），201
- endElement 方法（ContentHandler），197–201
- 行尾字符。参见换行符
- 企业应用程序，349–351
- 企业 JavaBeans（EJB），287
- 实体引用（XML），158, 176
- 实体解析器，160, 172
- ENTITY、ENTITIES 属性类型（DTD），174–175
  - EntityResolver 接口，178, 198
    - resolveEntity 方法，172, 178
- entries 方法（ZipFile），88
- Entrust, 593
- Entry 类，629
  - getXxx 方法，638–639
- EntryLogger 类，496
  - 其中的 EntryLoggingAgent，496
- enum 关键字，102
- EnumCombo 类，396
- enumeration 元素（XML Schema），180
- Enumeration 接口，88
  - hasMoreElements 方法，857–859
  - nextElement 方法，672, 857–859
- 枚举
  - 树中的节点，672–673
  - 类型安全的，102–103
  - 使用属性进行，175
- EnumSyntax 类，802
- EOFException, 844
- 纪元，101, 354
- equals 方法
  - Annotation 的，472
  - Collator 的，408
  - Permission 的，559
  - Set 的，561
- 错误处理器
  - 在本地代码中，844–849
  - 安装，177
- ErrorHandler 类，198
  - 其方法，177–178
- 逃生舱机制，663
- escape 关键字（SQL），320
- 转义
  - 在正则表达式中，73, 141
  - 在 SQL 中，319–321
- Essential XML（Box 等），153, 216
- 欧元符号，393, 415
- eval 方法
  - CompiledScript 的，447
  - ScriptEngine 的，441–443
- evaluate、evaluateExpression 方法（XPath），190, 193
- 事件处理器，添加注解，465–471
- 事件监听器，464
- 事件队列（AWT），访问，546
- EventHandler 类，467
- EventListenerList 类，686
- Evins, Jim, 622
- env 指针（C），820
- 异常
  - 受检异常，568
  - 来自本地代码，844–849
  - 在 C++ 中，845
  - 在 SQL 中，304–306
  - 其中的类型使用注解，476
- ExceptionXXX 函数（C），845, 849
- 排他锁，136
- exclusiveOr 方法（Area），714–715
- exec/ExecSQL.java, 308
- ExecutableElement 接口，485
- execute 方法
  - RowSet、CachedRowSet 的，331–332
  - Statement 的，301, 307, 321–322
- executeBatch 方法（Statement），346–347
- executeLargeBatch 方法（Statement），347
- executeQuery 方法
  - PreparedStatement 的，312, 317
  - Statement 的，300–301, 324
- executeUpdate 方法
  - PreparedStatement 的，312, 317
  - Statement 的，299, 301, 322, 345
- executor 方法（HttpClientBuilder），277
- ExecutorService 接口，454
- exists 方法（Files），116–117
- exit 方法（System），546
- EXIT 语句（SQL），295
- exports 关键字，506, 508, 510, 521
- 扩展类加载器，531
- extern "C"，在本地方法（C++）中，813
- 外部实体，176
- Externalizable 接口，其方法，101–102

## F

- F（float），类型代码，95, 831
- \f，在正则表达式中，138
- 因式分解算法，588
- fatalError 方法（ErrorHandler），177–178
- Field 类
  - getName、getType 方法，687
  - 实现 AnnotatedElement，466
- 字段
  - 从以下位置访问：
    - 另一个类，546
    - 本地代码，825–830
  - 添加注解，464, 479
  - transient 字段，100
- File 类
  - separator 常量，64
  - toPath 方法，111–112
- 文件权限，557
- 文件指针，80
- POSIX 兼容的文件系统，117
- file:（URI 方案），252, 553
- file.encoding 属性，77
- File.separator 属性，558
- FileChannel 类
  - lock 方法，135–136
  - open、map 方法，125, 130
  - tryLock 方法，135–136
- FileHandler 类，415
- FileInputStream 类，63–67, 550, 559
  - 构造器，66
  - getChannel 方法，130
  - read 方法，56
- fileKey 方法（BasicFileAttributes），118
- FileLock 类
  - close 方法，136
  - isShared 方法，135
- FileNotFoundException, 266
- FileOutputStream 类
  - 构造器，67
  - getChannel 方法，130
- FilePermission 类，548, 554
- FileReader 类，550
- 文件
  - 访问，546
  - 通道，125
  - 关闭，118
  - 配置，135
  - 复制，114
  - 创建，113–114
  - 删除，115
  - 加密/解密，607
  - 过滤，120, 746
  - 自动生成，463, 484
  - 层次结构，652
  - I/O 模式，84
  - 内存映射，50, 124–134
  - 缺失，454
  - 移动，114
  - 随机访问，80–85
    - 与缓冲式对比，125
  - 读取，64, 112–113
    - 作为字符串，112
    - 一次一个字节，56–59
    - 权限，559
  - 总字节数，81
  - 遍历，120–123
  - 包含多幅图像，747–755
  - 写入，112–113
- Files 类，109, 112–123
  - copy 方法，114–115
  - createXxx 方法，113–114
  - delete、deleteIfExists 方法，115
  - exists 方法，116–117
  - find 方法，119
  - getBytes 方法，112
  - getOwner 方法，117
  - isXxx 方法，116–117
  - lines 方法，6, 10, 50
  - list 方法，118
  - move 方法，114–115
  - newDirectoryStream 方法，120, 123
  - newXxxStream、newBufferedXxx 方法，112–113
  - readAllXxx 方法，113
  - readAttributes 方法，117
  - size 方法，116–117
  - walk 方法，118
  - walkFileTree 方法，121–123
  - write 方法，113
- **FileSystem** 类
  - getPath 方法，124
- **FileSystems** 类
  - newFileSystem 方法，123–124
- **FileTime** 类
  - toInstant 方法，377
- *FileVisitor* 接口，121–122
  - 其方法，121
- fill 方法（Graphics2D），695–696, 715
- 填充形状，694–695, 724
- fillXxx 方法（Graphics），696
- filter 方法
  - *BufferedImageOp* 的，763, 771
  - *Optional* 的，18–19
  - *Stream* 的，3–11, 15
- *FilteredRowSet* 接口，330
- filtering 方法（Collectors），37, 40
- **过滤器**
  - 用于图像，763–772
  - 用于数字，629
  - 用于表格行，628–630
  - glob 模式，120
  - 实现，629
- **FilterXxxStream** 类，65
- 末尾块填充，601
- find 方法
  - Files 的，119
  - Matcher 的，145, 149
- findAll 方法（Scanner），146, 151
- findAny 方法（Stream），16
- FindClass 函数（C），826, 829, 834
- findClass 方法（ClassLoader），534, 541
- findColumn 方法（ResultSet），302
- findFirst 方法（Stream），15–16
- 指纹，94, 583–587
  - 类与其对象的指纹不同，97
- first 方法（ResultSet），325, 328
- firstDayOfXxx 方法（TemporalAdjuster），365
- firstValue 方法（HttpHeaders），273, 278
- #FIXED 属性（DTD），175
- 固定大小记录，81–82
- flatMap 方法
  - 一般概念，12
  - *Optional* 的，21–25
  - *Stream* 的，12
- flatmapping 方法（Collectors），37, 40
- flip 方法（Buffer），133–134
- FLOAT 数据类型（SQL），293, 348
- float 类型
  - 打印，69
  - 流，43
  - 类型代码，95, 831
  - 与 C 类型比较，817
  - 以二进制格式写入，78
- FloatBuffer 类，132
- 浮点数，380, 387–394
- flush 方法
  - CipherOutputStream 的，608
  - *Closeable* 的，60
  - *Flushable* 的，60, 63
  - OutputStream 的，57, 59
- *Flushable* 接口，59, 61
  - close 方法，59
  - flush 方法，60, 63
- fn 关键字（SQL），320
- 文件夹图标，661–662, 674
- followRedirects 方法（HttpClient.Builder），271, 277
- 字体渲染上下文，733
- forEach 方法（Stream），25, 28
- forEachOrdered 方法（Stream），25
- Forest（Swing），652, 660
- **ForkJoinPool** 类
  - commonPool 方法，51
- forLanguageTag 方法（Locale），386
- Format 类，376
- format 方法
  - DateTimeFormatter 的，371, 375, 401
  - Format 的，411
  - MessageFormat 的，410–411
  - NumberFormat 的，388, 392
  - String 的，385
- **格式化**
  - 日期，380, 394–401
  - 消息，409–413
  - 数字，380, 387–394
- formatting/formatting.java, 374
- 表单，处理，261–270
- forName 方法
  - Charset 的，77

- forName 方法（*续*）
  - *Class* 的，456
- ForwardingJavaFileManager 类
  - 构造函数，464
  - getFileForOutput 方法，463
- fprintf 函数（C），333
- Frame 类，457
- from 方法
  - *Instant* 的，376–377
  - *ZonedDateTime* 的，376–377
- FROM 语句（SQL），290
- FTP（文件传输协议），256
- ftp:（URI 方案），252，256
- *Function* 接口，30
- @FunctionalInterface 注解，479

## G

- \G，在正则表达式中，140
- 垃圾回收
  - 与数组，842
  - 与本机方法，821
- *GeneralPath* 类，697，699，703
  - 构造函数，713
- generate 方法（Stream），5，9，43
- @Generated 注解，479–480
- generateKey 方法（KeyGenerator），602，607
- 生成器，转换为流，49
- 泛型类型中的类型使用注解，476
- get 方法
  - *AttributeSet* 的，802，806
  - *Bindings* 的，443
  - *ByteBuffer* 的，126，131
  - *CharBuffer* 的，132
  - *Optional* 的，19–22
  - *Paths* 的，109，111
  - *ScriptingEngine* 的，443
  - *ScriptingManager* 的，443
  - *Supplier* 的，10
- GET 方法（*HttpRequest.Builder*），271，278
- GET 请求（HTML），262，264
  - 构建，271
- getActions 方法（*Permission*），559
- getAddress 方法（*InetAddress*），234–235
- getAdvance 方法（*TextLayout*），735
- getAllByName 方法（*InetAddress*），234–235
- getAllowsChildren 方法（*TreeNode*），662
- getAnnotation 方法（*AnnotatedElement*），466，470，484，486
- getAnnotations 方法（*AnnotatedElement*），470
- getAnnotationsByType 方法（*AnnotatedElement*），470，484，486
- GetArrayLength 函数（C），840，843
- getAscent 方法（*TextLayout*），735
- getAsXxx 方法（*OptionalXxx*），44，48
- getAttribute 方法（*Element*），164，168
- getAttributes 方法
  - *DocPrintJob* 的，807
  - *Node* 的，164，168
  - *PrintService* 的，807
- getAttributeXxx 方法（*XMLStreamReader*），203，206
- getAuthority 方法（*URI*），253
- getAutoCommit 方法（*Connection*），347
- getAutoCreateRowSorter 方法（*JTable*），616，618
- getAvailableCurrencies 方法（*Currency*），394
- getAvailableLocales 方法
  - *Collator* 的，408
  - *NumberFormat* 的，383，388，391
- getAvailableZoneIds 方法（*ZoneId*），367
- getAverage 方法（*XxxSummaryStatistics*），26，29，48
- getBinaryStream 方法（*Blob*），317，319
- getBlob 方法（*ResultSet*），317–318
- getBlockSize 方法（*Cipher*），606
- getBooleanArrayElements 函数（C），842–843
- getBooleanArrayRegion 函数（C），842，844
- getBooleanField 函数（C），830
- getBundle 方法（*ResourceBundle*），418–421
- getByName 方法（*InetAddress*），234–235
- getByteArrayElements 函数（C），842–843，858
- getByteArrayRegion 函数（C），842，844
- getByteField 函数（C），830
- getBytes 方法
  - *Blob* 的，317–318
  - *Files* 的，112
- getCandidateLocales 方法（*ResourceBundle.Control*），418
- getCategory 方法（*Attribute*），801，806
- getCellEditorValue 方法（*CellEditor*），641，644–645，652
- getCellSelectionEnabled 方法（*JTable*），636
- getCertificates 方法（*CodeSource*），551
- getChannel 方法（*FileXxxStream*，*RandomAccessFile*），130
- getChar 方法（*ByteBuffer*），126，131
- getCharacterStream 方法（*Clob*），318–319
- getCharArrayElements 函数（C），842–843
- getCharArrayRegion 函数（C），842，844
- getCharContent 方法（*SimpleJavaFileObject*），463
- getCharField 函数（C），830
- getChild 方法（*TreeModel*），685–687，692
- getChildAt 方法（*TreeNode*），671
- getChildCount 方法
  - *TreeModel* 的，685–687，692
  - *TreeNode* 的，671
- getChildNodes 方法（*Node*），161，168
- getClassLoader 方法（*Class*），531，540
- getClip 方法（*Graphics*），734，775
- getClob 方法（*ResultSet*），317–318
- getCodeSource 方法（*ProtectionDomain*），551
- getCollationKey 方法（*Collator*），404，408
- getColorModel 方法（*BufferedImage*），758，762
- getColumn 方法（*TableColumnModel*），636
- getColumnClass 方法（*TableModel*），622，635
- getColumnCount 方法
  - *ResultSetMetaData* 的，335
  - *TableModel* 的，618–619，622
- getColumnModel 方法（*JTable*），635
- getColumnName 方法（*TableModel*），619，622
- getColumnNumber 方法
  - *Diagnostic* 的，462
  - *SAXParseException* 的，178
- getColumnSelectionAllowed 方法（*JTable*），636
- getColumnXxx 方法（*ResultSetMetaData*），335，344
- getCommand 方法（*Runtime*），332
- getConcurrency 方法（*ResultSet*），324–325，328
- getConnection 方法（*DriverManager*），296–297，307，351
- getConnectTimeout 方法（*URLConnection*），260
- getContent 方法（*URLConnection*），261
- getContentEncoding、getContentType 方法（*URLConnection*），254，257，261，266
- getContentLength 方法（*URLConnection*），254，257，260
- getContext 方法
  - *AccessController* 的，572
  - *ScriptEngine* 的，444
- getContextClassLoader 方法（*Thread*），533，541
- getCount 方法（*XxxSummaryStatistics*），29，48
- getCountry 方法（*Locale*），35，386
- getCrc 方法（*ZipEntry*），87
- getCurrencyCode 方法（*Currency*），394
- getCurrencyInstance 方法（*NumberFormat*），387，392–393
- getData 方法（*CharacterData*），163，169
- getDataElements 方法
  - *ColorModel* 的，763
  - *Raster* 的，758，762
- getDataSize 方法（*DataTruncation*），306
- getDate 方法
  - *ResultSet* 的，300，302
  - *URLConnection* 的，254，257，261
- getDayOfXxx 方法
  - *LocalDate* 的，360，362
  - *ZonedDateTime* 的，370
- getDays 方法（*Period*），363
- getDeclaredAnnotations 方法（*AnnotatedElement*），471
- getDecomposition 方法（*Collator*），408
- getDefault 方法（*Locale*），384，386
- getDefaultEditor 方法（*JTable*），650
- getDefaultFractionDigits 方法（*Currency*），394
- getDefaultTimeZone 方法（*TimeZone*），581
- getDefaultRenderer 方法（*JTable*），641，650
- getDescent 方法（*TextLayout*），735
- getDiagnostics 方法（*DiagnosticCollector*），462
- getDirectBufferXxx 函数（C），843
- getDisplayCountry、getDisplayLanguage 方法（*Locale*），386
- getDisplayName 方法
  - *DayOfWeek* 的，373，395
  - *Locale* 的，384，386，388
- getDocumentElement 方法（*Document*），160，168
- getDoInput、getDoOutput 方法（*URLConnection*），259
- getDouble 方法
  - *ByteBuffer* 的，126，131
  - *ResultSet* 的，300，302
- getDoubleArrayElements 函数（C），842–843
- getDoubleArrayRegion 函数（C），842，844
- getDoubleField 函数（C），826，830
- getEnclosedElements 方法（*TypeElement*），486
- getEngineXxx 方法（*ScriptEngineManager*），441
- getEntry 方法（*ZipFile*），88
- getErrorCode 方法（*SQLException*），304–305
- getErrorStream 方法（*HttpURLConnection*），266，270
- getErrorWriter 方法（*ScriptContext*），444
- getExpiration 方法（*URLConnection*），254，257，261
- getExtensions 方法（*ScriptEngineFactory*），441
- GetField 函数（C），826，830
- getFields 方法（*Class*），687
- getFileForOutput 方法（*ForwardingJavaFileManager*），463
- getFileName 方法（*StackTraceElement*），111
- getFilePointer 方法（*RandomAccessFile*），81，84
- getFileSuffixes 方法（*ImageReaderWriterSpi*），755
- getFillsViewportHeight 方法（*JTable*），618
- getFirstChild 方法（*Node*），163，168
- getFloat 方法（*ByteBuffer*），126，131
- GetFloatArrayElements 函数（C），842–843
- GetFloatArrayRegion 函数（C），842，844
- GetFloatField 函数（C），830
- getFontRenderContext 方法（*Graphics2D*），733，735
- getFormatNames 方法（*ImageReaderWriterSpi*），755
- getFragment 方法（*URI*），253
- getHeaderXxx 方法（*URLConnection*），254–256，260
- getHeight 方法
  - *ImageReader* 的，748，754
  - *PageFormat* 的，775，782
- getHost 方法（*URI*），253
- getHostXxx 方法（*InetAddress*），235
- getHour 方法
  - *LocalTime* 的，366
  - *ZonedDateTime* 的，371
- getIdentifier 方法（*Entity*），638
- getIfModifiedSince 方法（*URLConnection*），260
- getImageableXxx 方法（*PageFormat*），776，782
- getImageXxxYxx 方法（*ImageIO*），746，753
- getIndex 方法（*DataTruncation*），306
- getIndexOfChild 方法（*TreeModel*），685，692
- getInputStream 方法
  - *Socket* 的，231–232，236
  - *URLConnection* 的，254，261，264，266
  - *ZipFile* 的，88
- getInstance 方法
  - *AlphaComposite* 的，739，744
  - *Cipher* 的，600，606
  - *Collator* 的，408
  - *Currency* 的，393–394
  - *KeyGenerator* 的，606
  - *Locale* 的，402
  - *MessageDigest* 的，584–586
- getInt 方法
  - *ByteBuffer* 的，126，131
  - *ResultSet* 的，300，302
- getIntArrayElements 函数（C），842–843
- GetIntArrayRegion 函数（C），842，844
- getInterface 方法（*Invocable*），446
- GetIntField 函数（C），826，830，859
- getISOCountries 方法（*Locale*），384，386
- getISOLanguages 方法（*Locale*），384
- getJavaFileObjectFromXxx 方法（*StandardJavaFileManager*），462
- getJDBCXxxVersion 方法（*DatabaseMetaData*），343
- getKeys 方法（*ResourceBundle*），421
- getKind 方法（*Diagnostic*），462
- getLanguage 方法（*Locale*），386
- getLastChild 方法（*Node*），164，168
- getLastModified 方法（*URLConnection*），254，257，261
- getLastPathComponent 方法（*TreePath*），665，671
- getLastSelectedPathComponent 方法（*JTree*），665，670
- getLeading 方法（*TextLayout*），735
- getLength 方法
  - *Attributes* 的，202
  - *NamedNodeMap* 的，169
  - *NodeList* 的，161，169
- getLineNumber 方法
  - *Diagnostic* 的，462
  - *SAXParseException* 的，178
- getLocale 方法（*MessageFormat*），411
- getLocalHost 方法（*InetAddress*），234–235
- getLocalName 方法
  - *Attributes* 的，202
  - *Node* 的，196
  - *XMLStreamReader* 的，206
- getLocation 方法（*CodeSource*），551
- getLong 方法（*ByteBuffer*），126，131
- getLongArrayElements 函数（C），842–843
- GetLongArrayRegion 函数（C），842，844
- GetLongField 函数（C），830



- getMax 方法（XxxSummaryStatistics），26、30、48
- getMaxConnections 方法（DatabaseMetaData），343
- getMaxStatements 方法（DatabaseMetaData），303、343
- getMessage 方法（Diagnostic），462
- getMetaData 方法
  - Connection 的，334、343
  - ResultSet 的，335、344
- getMethodCallsSystem 方法（ScriptEngineFactory），445
- GetMethodID 函数（C），835、838
- getMIMETypes 方法（ScriptEngineFactory），441
- getMIMEType 方法（ImageReaderWriterSpi），755
- getMin 方法（XxxSummaryStatistics），30、48
- getMinute 方法
  - LocalTime 的，366
  - ZonedDateTime 的，371
- getModel 方法（Entry），638
- getMonth、getMonthValue 方法
  - LocalDate 的，362
  - ZonedDateTime 的，370
- getMonths 方法（Period），363
- getMoreResults 方法（Statement），321–322
- getName 方法
  - Attribute 的，806
  - Field 的，687
  - NameCallback 的，581
  - Permission 的，561、566
  - Principal 的，573
  - PrintService 的，793
  - UnixPrincipal 的，567
  - XMLStreamReader 的，206
  - ZipEntry 的，87
  - ZipFile 的，88
- getNames 方法（ScriptEngineFactory），441
- getNamespaceURI 方法（Node），195–196
- getNano 方法
  - LocalTime 的，366
  - ZonedDateTime 的，371
- getNextEntry 方法（ZipInputStream），85–86
- getNextException 方法（SQLException），304–305
- getNextSibling 方法（Node），164、168
- getNextWarning 方法（SQLWarning），306
- getNodeXxx 方法（Node），164、169、195
- getNumberInstance 方法（NumberFormat），387、392
- getNumericXxx 方法（Currency），394
- getNumXxx 方法（ImageReader），747、754
- getObject 方法
  - ResourceBundle 的，420–421
  - ResultSet 的，300、302
- GetObjectArrayElement 函数（C），840、843
- GetObjectClass 函数（C），826–827
- GetObjectField 函数（C），826、830
- getOffset 方法（ZonedDateTime），371
- getOrientation 方法（PageFormat），782
- getOriginatingProvider 方法
  - ImageReader 的，746、754
  - ImageWriter 的，755
- getOutputSize 方法（Cipher），606
- getOutputStream 方法
  - Socket 的，232、236
  - URLConnection 的，254、261、264
- getOwner 方法（Files），117
- getPageCount 方法（Banner），784
- getPageSize 方法（CachedRowSet），333
- getParameter 方法（DataTruncation），306
- getParent 方法
  - ClassLoader 的，540
  - Path 的，111
  - TreeNode 的，671、673
- getParentNode 方法（Node），168
- getPassword 方法
  - PasswordCallback 的，582
  - RowSet 的，332
- getPath 方法
  - FileSystem 的，124
  - TreeSelectionEvent 的，684
  - URI 的，253
- getPaths 方法（TreeSelectionEvent），678、684
- getPathToRoot 方法（DefaultTreeModel），666
- getPercentInstance 方法（NumberFormat），387、392
- getPixel、getPixels 方法（Raster），757、762
- getPointCount 方法（ShapeMaker），704
- getPort 方法（URI），253
- getPreviousSibling 方法（Node），168
- getPrincipals 方法（Subject），572
- getPrinterJob 方法（PrinterJob），773、781
- getPrintService 方法
  - StreamPrintServiceFactory 的，796
- getPrompt 方法
  - NameCallback 的，581
  - PasswordCallback 的，582
- getProtectionDomain 方法（Class），551
- getValue 方法
  - Attributes 的，202
  - Copies 的，802
  - Entry 的，638
  - W3CRegexp 的，857
- getValueOf 方法（TableModel），618–619、622
- getValueCount 方法（Entry），639
- getVendorName、getVersion 方法（IIOServiceProvider），746、754
- getWarnings 方法（Connection、ResultSet、Statement），306
- getWidth 方法
  - ImageReader 的，748、754
  - PageFormat 的，775、782
- getWriter 方法（ScriptContext），444
- getWriterXxx 方法（ImageIO），746、753
- getYear 方法
  - LocalDate 的，362
  - ZonedDateTime 的，370
- getYears 方法（Period），363
- GIF 格式，745
  - 动画，747
  - 对图像的操作，767
  - 打印，792
- GlassFish 服务器，350
- Glob 模式，120
- GlobalSign，593
- Gmail，279–280
- GNU C 编译器，813–814
- 哥德尔定理，542
- Google Maps，263
- GradientPaint 类，725
  - 构造方法，725–726
  - cyclic 参数，725
- grant 关键字，553、568、599
- Graphic Java™（Geary），614、652
- Graphics 类，693–694
  - drawXxx、fillXxx 方法，696
  - get/setClip 方法，733–734、775
- Graphics2D 类
  - clip 方法，695、733–735、775
  - draw 方法，695–697、715
  - fill 方法，695–696、715
  - getFontRenderContext 方法，733、735
  - rotate、scale 方法，728、732
  - setComposite 方法，695、738、744
  - setPaint 方法，695、724、726
  - setRenderingHint、setRenderingHints 方法，694
  - setStroke 方法，694、715、724
  - setTransform 方法，730、732
  - shear 方法，728、732
  - transform 方法，695、730、732
  - translate 方法，728、732、784
- 格林尼治皇家天文台，354、367
- 格里高利历改革，363
- GregorianCalendar 类
  - timezone 方法，376–377
- Groovy 编程语言，440、448
- group 方法
  - Matcher 的，143、145、149–150
  - MatchResult 的，146、150
- groupCount 方法（Matcher），149
- 分组，34–35
  - 分类器函数，35
  - 归约为数字，36
- groupingBy 方法（Collectors），34–40
- groupingByConcurrent 方法（Collectors），35、50
- gzip，实体引用，158
- GUI（图形用户界面），用于 GUI 的脚本事件，447–452

## H

- 正则表达式中的 \h、\H，139
- 半关闭连接，243–244
- 《应用密码学手册》（Menezes 等），587
- handle 方法（CallbackHandler），581
- handleObject 方法（ResourceBundle），421
- 句柄（Swing），657、674
- hashDigest.java，585
- hashCode 方法
  - Annotation 的，472
  - Permission 的，559
- HashXxxAttributeSet 类，773、800
- Haskell 编程语言，440
- hasMoreElements 方法（Enumeration），857–859
- hasNext 方法（XMLStreamReader），205
- hasRemaining 方法（Buffer），130
- 来自服务器的头信息，254
- header 方法（HttpRequest.Builder），277
- 表头（Swing 表格）
  - 呈现，641
  - 滚动，615
- headers 方法（HttpResponse），272、278
- helloNative/helloNative.c，813
- helloNative/helloNative.h，812
- helloNative/HelloNative.java，811
- helloNative/HelloNativeTest.java，814
- **十六进制编辑器**
  - 在其中创建类文件，542
  - 使用其修改字节码，544
- **隐藏命令**，在 XML 注释中，159
- **主机**，234–235
- **HTML（超文本标记语言）**
  - 其中的属性，158
  - 以及其中的 `&amp;` 实体标签，156
  - 其中的表单，262
  - 从 XML 文件生成，216–219
  - 与 JSP 混用，457
  - 打印，792
  - 与 XML 对比，155
- **HTTP（超文本传输协议）**，287
  - HTTPS 与 HTTP 之间的重定向，267
  - 其中的请求头，255–256
- **http:**（URI 方案），252、553
- **HttpClient 类**，271–278
  - 为其启用日志记录，273
  - newBuilder 方法，271、273、277
  - newHttpClient 方法，271、277
  - send 方法，277
  - sendAsync 方法，273、277
- **HttpClient.Builder 类**
  - build 方法，271–272、277
  - executor 方法，277
  - followRedirects 方法，271、277
- **HttpHeaders 类**
  - firstValue 方法，273、278
  - map 方法，272、278
- **HttpRequest 类**
  - newBuilder 方法，271–273、277
- **HttpRequest.Builder 类**
  - build 方法，277
  - DELETE 方法，278
  - GET 方法，271、278
  - header 方法，277
  - POST 方法，272、278
  - PUT 方法，278
  - uri 方法，271–273、277
- **HttpResponse 类**，其方法，272、278
- **HttpResponse.BodyHandlers 类**
  - discarding 方法，272
  - ofString 方法，272–273
- **HTTPS（安全超文本传输协议）**，267
- **https:**（URI 方案），252
- **HttpURLConnection 类**
  - getErrorStream 方法，266、270
  - getResponseCode 方法，267
  - setInstanceFollowRedirects 方法，267

## I

- **I (int)**，类型代码，95、831
- **I/O 流。** 参见输入流、输出流
- **IANA（互联网号码分配局）**，367
- **IBM**，153、160
  - DB2 数据库，293
- **IBM437 编码**，415
- **ICC 配置文件**，758
- **图标**
  - 列标题中的，641
  - 表格单元格中的，639
  - 树中的，661–662、674
- **ID、IDREF、IDREFS 属性类型（DTD）**，174–175
- **恒等（不做任何操作）转换**，209
- **identity 方法（Function）**，30
- **恒等值**，41
- **ID** 的唯一性，175、183
- **IETF BCP 47**，385
- **ifPresent 方法（Optional）**，17–18、48
- **ifPresentOrElse 方法（Optional）**，18
- **IIOImage 类**，745、755
- **IIOServiceProvider 类**
  - getVendorName、getVersion 方法，746、754
- **IllegalAccessException**，687
- **IllegalArgumentException**，204、845
- **IllegalStateException**，30、747
- **可成像区域**，776
- **ImageInputStream 类**，747
- **ImageIO 类**
  - createImageXxxStream 方法，747、753
  - 确定图像类型，745
  - getImageXxxByXxx 方法，746、753
  - getReaderXxx、getWriterXxx 方法，746、753
- **ImageIO/ImageIOFrame.java**，749
- **ImageOutputStream 接口**，748
- **ImageProcessing/ImageProcessingFrame.java**，767
- **ImageReader 类**，745
  - getHeight、getWidth 方法，748、754





- getXxx 方法，747, 754
- getOriginatingProvider 方法，746, 754
- read、readThumbnail 方法，754
- setInput 方法，754
- ImageReaderWriterSpi 类
  - getXxx 方法，755
- 图像
  - 模糊处理，765
  - 颜色值，758
  - 边缘检测，766
  - 滤波，763-772
  - 读取前获取大小，748
  - 增量渲染，756
  - 操作，756-772
  - 元数据，748
  - 文件中的多幅图像，747-755
  - 打印，772-782, 792, 796
  - 栅格，744-772
    - 从像素构建，756-763
  - 图像的读取器/写入器，745-755
  - 旋转，764
  - 叠加，735-736
  - 缩略图，748
  - 矢量，693-744
- ImageWriter 类，745, 748
  - canInsertImage 方法，748, 755
  - getOriginatingProvider 方法，755
  - setOutput 方法，755
  - write、writeInsert 方法，748, 755
- implements 规范中的类型使用注解，476
- #IMPLIED 属性（DTD），175
- implies 方法
  - Permission 的，559-561, 566
  - ProtectionDomain 的，551
- import 语句，534
- INCLUDE 环境变量，854
- include 方法（RowFilter），629, 638
- 增量渲染，756
- 索引颜色模型，765
- IndexOutOfBoundsException，747
- InetAddress 类，234-235
  - getXxx 方法，234-235
- InetAddress/InetAddressTest.java，234
- InetSocketAddress 类
  - isUnresolved 方法，251
- 无限树，688
- 继承树，304
- @Inherited 注解，479, 483
- init 方法
  - Cipher 的，606
  - KeyGenerator 的，606
- 共享库的初始化块，816
- initialize 方法
  - LoginModule 的，582
  - SimpleLoginModule 的，574
- INPUT_STREAM 类（DocFlavor），794
- 输入流，56-77
  - 与 Unicode，56
  - 作为输入源，160
  - 缓冲，65-67
  - 字节处理，65
  - 面向字节，56
  - 链接，65
  - 关闭，57
  - 编码，68
  - 过滤器，63-67
  - 层次结构，59-63
  - 保持打开状态，243
  - 对象，88-108
- InputStream 类，178
- InputStream 类，56-59, 60
  - available 方法，57-58
  - close 方法，57-58
  - mark、markSupported 方法，58
  - read 方法，56-58
  - readAllBytes、readNBytes 方法，56, 58
  - reset、skip、transferTo 方法，58
- InputStreamReader 类，68
- INSERT 语句（SQL），292
  - 与自动生成的键，322
  - 执行，300-301, 317
  - 在批处理更新中，346
  - 对比 ResultSet 的方法，327
- insertNodeInto 方法（DefaultTreeModel），665, 671
- insertRow 方法（ResultSet），326, 329
- 《Inside Java™ 2 Platform Security》（Gong 等），530
- 实例字段
  - 从本地代码访问，825-829
  - 注解，475
- instanceof 关键字与类型使用注解，476
- Instant 类，354
  - from 方法，376-377
  - 不可变性，355
  - 遗留类，376-377
  - minus、minusExact 方法，357
  - now 方法，355, 357
  - plus、plusExact 方法，357
- Instrumentation API，496
- int 类型
  - 打印，69
  - 存储，78
  - 流，43
  - 类型代码，95, 831
  - 对比 C 类型，817
  - 以二进制格式写入，78
- IntBuffer 类，132
- INTEGER 数据类型（SQL），293, 348
- IntegerSyntax 类，802
- @interface 声明，465, 471
- 接口
  - 使用脚本类访问，446
  - 注解，475, 479
  - 在脚本引擎中实现，445
- 互联网工程任务组，382
- 插值，764
  - 用于渐变，725
  - 策略，764
  - 图像变换时，764
- 可中断套接字，244-251
- InterruptibleInputStreamTest.java，246
- intersect 方法（Area），714-715
- ints 方法
  - Random 的，44, 47, 51
  - SplittableRandom 的，51
- IntStream 接口，43-48
  - average、max、min、of、range、ranged、sum、summaryStatistics、toArray 方法，46
  - boxed 方法，44, 46
- IntSummaryStatistics 类，26, 29-30, 44, 48
- intValue 方法（Number），388
- 无效指针（C、C++），810
- InvalidPathException，109
- Invocable 接口，444
  - getInterface 方法，446
  - invokeExact 方法，445-446
- 调用 API，849-854
- Invocation/InvocationTest.c，851
- IOException，231
- IP 地址，229, 234-235
- IPP（互联网打印协议）1.1，806
- IPv6 地址，234
- isAfter 方法
  - LocalDate 的，363
  - LocalTime 的，366
  - ZonedDateTime 的，371
- isAfterLast 方法（ResultSet），325, 328
- isAnnotationPresent 方法（AnnotatedElement），470
- isAssignableFrom 函数（C），858, 870
- isBefore 方法
  - LocalDate 的，363
  - LocalTime 的，366
  - ZonedDateTime 的，371
- isBeforeFirst 方法（ResultSet），325, 328
- isCellEditable 方法
  - AbstractCellEditor 的，644
  - AbstractTableModel 的，641
  - CellEditor 的，652
  - DefaultTableModel 的，641
  - TableModel 的，622, 641
- isCharacters 方法（XMLStreamReader），205
- isClosed 方法
  - ResultSet 的，303
  - Socket 的，233
  - Statement 的，302
- isConnected 方法（Socket），233
- isDirectory 方法
  - BasicFileAttributes 的，118
  - ZipEntry 的，87
- isEchoOn 方法（PasswordCallback），582
- isEndElement 方法（XMLStreamReader），205
- isExecutable 方法（Files），116-117
- isFirst 方法（ResultSet），325, 328
- isGroupingUsed 方法（NumberFormat），392
- isHidden 方法（Files），116-117
- isIgnoringElementContentWhitespace 方法（DocumentBuilderFactory），179
- isInputShutdown 方法（Socket），244
- isLast 方法（ResultSet），325, 328
- isLeaf 方法
  - DefaultTreeModel 的，661
  - TreeNode 的，663, 685, 693
  - TreeModel 的，661-662
- isLeapYear 方法（LocalDate），363
- isNamespaceAware 方法
  - DocumentBuilderFactory 的，196
  - SAXParserFactory 的，201
- isNegative 方法（Duration），358
- ISO 216 标准，420
- ISO 639-1 标准，382, 386
- java 程序
  - 在其中指定区域设置，384
- Java 编程语言
  - 国际化支持，379
  - 平台无关性，78
  - 安全性，547-551
  - 对比 SQL，313
- 《Java 虚拟机规范》，489, 544
- java.activation 模块，514
- java.awt 包，501
- java.awt.AlphaComposite API，744
- java.awt.BasicStroke API，724
- java.awt.Color API，763
- java.awt.Font.TextLayout API，735
- java.awt.geom 包，100
- java.awt.geom.AffineTransform API，731-732
- java.awt.geom.Arc2D.Double API，713
- java.awt.geom.Area API，715
- java.awt.geom.CubicCurve2D.Double API，713
- java.awt.geom.GeneralPath API，713
- java.awt.geom.Path2D API，714
- java.awt.geom.Path2D.Float API，713
- java.awt.geom.QuadCurve2D.Double API，713
- java.awt.geom.RoundRectangle2D.Double API，712
- java.awt.GradientPaint API，726
- java.awt.Graphics API，734
- java.awt.Graphics2D API，696, 724, 726, 732, 735, 744
- java.awt.image.AffineTransformOp API，771
- java.awt.image.BufferedImage API，761
- java.awt.image.BufferedImageOp API，771
- java.awt.image.ColorModel API，763
- java.awt.image.ConvolveOp API，772
- java.awt.image.Kernel API，772
- java.awt.image.LookupOp API，771
- java.awt.image.Raster API，762
- java.awt.image.RescaleOp API，771
- java.awt.image.ShortLookupTable API，772
- java.awt.image.WritableRaster API，762
- java.awt.print.PageFormat API，782
- java.awt.print.Printable API，781
- java.awt.print.PrinterJob API，781-782
- java.awt.TexturePaint API，726
- java.corba 模块，514
- java.io 包，77
- java.io.BufferedInputStream API，67
- java.io.BufferedOutputStream API，67
- java.io.Closeable API，62
- java.io.DataInput API，79-80
- java.io.DataOutput API，80
- java.io.File API，112
- java.io.FileInputStream API，66, 130
- java.io.FileOutputStream API，67, 130
- java.io.Flushable API，63
- java.io.InputStream API，58
- java.io.ObjectInputStream API，93
- java.io.ObjectOutputStream API，93
- java.io.OutputStream API，59
- java.io.PrintWriter API，70
- java.io.PushbackInputStream API，67
- java.io.RandomAccessFile API，84-85, 130
- java.lang、java.lang.annotation 包，478
- java.lang.annotation.Annotation API，472
- java.lang.Appendable API，63
- java.lang.CharSequence API，47, 63
- java.lang.Class API，540, 551
- java.lang.ClassLoader API，540-541
- java.lang.Iterable API，10
- java.lang.Readable API，63
- java.lang.reflect.AnnotatedElement API，470-471
- java.lang.SecurityManager API，550
- java.lang.System API，816
- java.lang.Thread API，541
- java.logging 模块，520
- java.net 包
  - 套接字连接，232
  - 支持 IPv6 地址，234
  - 其中的 URL 与 URI，252
- java.net.http 包，271
- java.net.http.HttpClient API，277
- java.net.http.HttpClient.Builder API，277
- java.net.http.HttpHeaders API，278
- java.net.http.HttpRequest API，277
- java.net.http.HttpRequest.Builder API，277-278
- java.net.http.HttpResponse API，278
- java.net.HttpURLConnection API，270
- java.net.InetAddress API，235
- java.net.InetSocketAddress API，251
- java.net.ServerSocket API，239
- java.net.Socket API，232-233, 244
- java.net.URL API，259
- java.net.URLClassLoader API，541
- java.net.URLConnection API，259-261
- java.net.URLDecoder API，270
- java.net.URLEncoder API，270




- java.nio 包, 241, 244
  - 直接缓冲区, 843
  - 内存映射, 125
- java.nio.Buffer API, 130, 134
- java.nio.ByteBuffer API, 131–132
- java.nio.channels.Channel API, 251
- java.nio.channels.FileChannel API, 130, 136
- java.nio.channels.FileLock API, 136
- java.nio.channels.SocketChannel API, 251
- java.nio.CharBuffer API, 132
- java.nio.file.attribute.BasicFileAttributes API, 118
- java.nio.file.Files API, 10, 113–115, 117, 123
- java.nio.file.FileSystem API, 124
- java.nio.file.FileSystems API, 124
- java.nio.file.Path API, 111
- java.nio.file.Paths API, 111
- java.nio.file.SimpleFileVisitor API, 123
- java.policy 文件, 551–552
- java.se 模块, 520
- java.security 文件, 552
- java.security 包, 530, 583
- java.security.CodeSource API, 551
- java.security.MessageDigest API, 586–587
- java.security.Permission API, 566
- java.security.Principal API, 573
- java.security.PrivilegedAction API, 572
- java.security.PrivilegedExceptionAction API, 572
- java.security.ProtectionDomain API, 551
- java.sql 包, 376
- java.sql.Blob API, 318–319
- java.sql.Clob API, 319
- java.sql.Connection API, 301, 306, 317, 319, 327, 343, 347
- java.sql.DatabaseMetaData API, 329, 343, 348
- java.sql.DataTruncation API, 306
- java.sql.DriverManager API, 297
- java.sql.PreparedStatement API, 317
- java.sql.ResultSet API, 302–303, 306, 318, 328–329, 344
- java.sql.ResultSetMetaData API, 344
- java.sql.Savepoint API, 347
- java.sql.SQLXML APIs, 305
- java.sql.Statement API, 301–302, 306, 322, 347
- java.text.CollationKey API, 409
- java.text.Collator API, 408

- java.text.Format API, 411
- java.text.MessageFormat API, 410–411
- java.text.Normalizer API, 409
- java.text.NumberFormat API, 391–392
- java.time.Duration API, 357
- java.time.format.DateTimeFormatter API, 375–376, 401
- java.time.Instant API, 357
- java.time.LocalDate API, 362–363, 365, 376, 401
- java.time.LocalDateTime API, 401
- java.time.LocalTime API, 366, 401
- java.time.Period API, 363
- java.time.temporal.TemporalAdjusters API, 365
- java.time.ZonedDateTime API, 370–371, 376, 401
- java.transaction 模块, 514
- java.util.Arrays API, 9
- java.util.Collection API, 5, 53
- java.util.Currency API, 394
- java.util.DoubleSummaryStatistics API, 29, 48
- java.util.function.Supplier API, 10
- java.util.IntSummaryStatistics API, 29, 48
- java.util.Locale API, 385–386
- java.util.LongSummaryStatistics API, 29, 48
- java.util.Optional API, 17–22, 25
- java.util.OptionalXXX APIs, 48
- java.util.Random API, 47
- java.util.regex.Matcher API, 149–150
- java.util.regex.MatchResult API, 150
- java.util.regex.Pattern API, 10, 148–149
- java.util.ResourceBundle API, 421
- java.util.Scanner API, 10, 151
- java.util.Spliterators API, 9
- java.util.Stream API, 43
- java.util.stream.BaseStream API, 28, 53
- java.util.stream.Collectors API, 29, 34–35, 40
- java.util.stream.DoubleStream API, 47
- java.util.stream.IntStream API, 46
- java.util.stream.LongStream API, 46
- java.util.stream.Stream API, 4, 12–13, 15–16, 28
- java.util.stream.StreamSupport API, 10
- java.util.zip.ZipEntry API, 87
- java.util.zip.ZipFile API, 88
- java.util.zip.ZipInputStream API, 86
- java.util.zip.ZipOutputStream API, 86–87
- java.xml.bind 模块, 514
- java.xml.ws 模块, 514

- javax.xml.ws.annotation 模块, 514
- javac 程序
  - -encoding 选项, 416
  - -XprintRounds 选项, 489
- JavaCompiler 接口, 453–454
  - getStandardFileManager 方法, 461
  - getTask 方法, 461
- Javadoc, 482
- JavaFileObject 接口, 453
- JavaFX 平台, 521
- javafx 程序, 859
- JavaMail, 279
- JavaOne 大会, 286
- javap 程序, 832
- JavaScript 编程语言, 440, 447–448
- javax.annotation 包, 478
- javax.crypto.Cipher API, 606
- javax.crypto.CipherInputStream API, 606–607
- javax.crypto.spec.SecretKeySpec API, 607
- javax.imageio 包, 745
- javax.imageio.IIOMetadata API, 755
- javax.imageio.ImageIO API, 753
- javax.imageio.ImageReader API, 754
- javax.imageio.ImageWriter API, 755
- javax.imageio.spi.IIOServiceProvider API, 754
- javax.imageio.spi.ImageReaderWriterSpi API, 755
- javax.print.attribute.Attribute API, 806
- javax.print.attribute.AttributeSet API, 806–807
- javax.print.DocPrintJob API, 795, 807
- javax.print.PrintService API, 795, 807
- javax.print.PrintServiceLookup API, 795
- javax.print.SimpleDoc API, 795
- javax.print.StreamPrintServiceFactory API, 796
- javax.script.Bindings API, 443
- javax.script.Compilable API, 447
- javax.script.CompiledScript API, 447
- javax.script.Invocable API, 446
- javax.script.ScriptContext API, 444
- javax.script.ScriptEngine API, 441
- javax.script.ScriptEngineManager API, 441, 443
- javax.security.auth.callback.CallbackHandler API, 581
- javax.security.auth.callback.NameCallback API, 581
- javax.security.auth.callback.PasswordCallback API, 581–582

- javax.security.auth.login.LoginContext API, 571–572
- javax.security.auth.spi.LoginModule API, 582
- javax.security.auth.Subject API, 572
- javax.sql 包, 350
- javax.sql.rowset 包, 330
- javax.sql.RowSet API, 332
- javax.sql.rowset.CachedRowSet API, 333
- javax.sql.rowset.RowSetFactory API, 333
- javax.sql.rowset.RowSetProvider API, 333
- javax.swing.CellEditor API, 652
- javax.swing.DefaultCellEditor API, 651
- javax.swing.DefaultRowSorter API, 637
- javax.swing.event.TreeModelEvent API, 693
- javax.swing.event.TreeModelListener API, 693
- javax.swing.event.TreeSelectionEvent API, 684
- javax.swing.event.TreeSelectionListener API, 684
- javax.swing.JComponent API, 663
- javax.swing.JTable API, 618, 635–636, 650
- javax.swing.JTree API, 662, 670, 683
- javax.swing.ListSelectionModel API, 637
- javax.swing.RowFilter API, 638
- javax.swing.RowFilter.Entry API, 638–639
- javax.swing.table.TableCellEditor API, 651
- javax.swing.table.TableCellRenderer API, 651
- javax.swing.table.TableColumn API, 637
- javax.swing.table.TableColumnModel API, 636
- javax.swing.table.TableModel API, 622, 635
- javax.swing.table.TableRowSorter API, 637
- javax.swing.table.TableStringConverter API, 637
- javax.swing.tree.DefaultMutableTreeNode API, 663, 676
- javax.swing.tree.DefaultTreeCellRenderer API, 676
- javax.swing.tree.DefaultTreeModel API, 663, 671
- javax.swing.tree.MutableTreeNode API, 662
- javax.swing.tree.TreeCellRenderer API, 676
- javax.swing.tree.TreeModel API, 663, 692–693
- javax.swing.tree.TreeNode API, 662, 671
- javax.swing.tree.TreePath API, 671
- javax.tools.Diagnostic API, 462
- javax.tools.DiagnosticCollector API, 462
- javax.tools.ForwardingJavaFileManager API, 463
- javax.tools.JavaCompiler API, 461
- javax.tools.JavaCompiler.CompilationTask API, 462
- javax.tools.SimpleJavaFileObject API, 463
- javax.tools.StandardJavaFileManager API, 462
- javax.tools.Tool API, 461
- javax.xml.catalog.CatalogFeatures API, 179
- javax.xml.catalog.CatalogManager API, 178

- javax.xml.catalog.files 系统属性, 172
- javax.xml.parsers.DocumentBuilder API, 168, 177, 208
- javax.xml.parsers.DocumentBuilderFactory API, 167, 179, 196
- javax.xml.parsers.SAXParser API, 201
- javax.xml.parsers.SAXParserFactory API, 201
- javax.xml.stream.XMLInputFactory API, 204–205
- javax.xml.stream.XMLOutputFactory API, 214–215
- javax.xml.stream.XMLStreamReader API, 205–206
- javax.xml.stream.XMLStreamWriter API, 214–215
- javax.xml.transform.dom.DOMResult API, 226
- javax.xml.transform.dom.DOMSource API, 210
- javax.xml.transform.sax.SAXSource API, 225
- javax.xml.transform.stream.StreamResult API, 210
- javax.xml.transform.stream.StreamSource API, 225
- javax.xml.transform.Transformer API, 209
- javax.xml.transform.TransformerFactory API, 209, 225
- javax.xml.xpath.XPath API, 193
- javax.xml.xpath.XPathEvaluationResult API, 193
- javax.xml.xpath.XPathFactory API, 193
- JAXB（Java XML 绑定架构）, 512
- JAXP（Java XML 处理 API）
  - 库, 160
- jboolean 类型（C）, 817
- jbooleanArray 类型（C）, 840
- jbyte 类型（C）, 817
- jbyteArray 类型（C）, 840
- jchar 类型（C）, 817, 819
- jcharArray 类型（C）, 840
- JCheckBox 类, 641
- jclass 类型（C）, 835
- JComboBox 类, 641
- JCommander 框架, 465
- JComponent 类
  - paint 方法, 639, 694
  - paintComponent 方法, 694
  - paintImmediately 方法, 658, 663
- JDBC API, 285
  - 配置, 293–299
  - 调试, 297
  - 设计, 284–287
  - 跟踪, 297
  - 用途, 286–287
  - 版本, 283
- JDBC API 教程与参考（Fisher 等）, 327, 349
- JDBC 驱动程序
  - 转义语法, 319–321
  - JAR 文件, 294
  - 注册类, 295–296
  - 可滚动/可更新结果集, 324
  - 类型, 285–286
- JDBC/ODBC 桥接器, 在 Java 8 中不可用, 285
- JdbcRowSet 接口, 330
- jdeprscan 程序, 480
- jdeps 程序, 524–525
- JDK（Java 开发工具包）
  - DOM 解析器, 160
  - keytool 程序, 589
  - 过时特性, 500
  - serialver 程序, 104
  - src.jar 文件, 850
  - SunJCE 密码算法, 600
- jdk.incubator.http 包, 271
- jdouble 类型（C）, 817
- jdoubleArray 类型（C）, 840
- jfloat 类型（C）, 817
- jfloatArray 类型（C）, 840
- jint 类型（C）, 817
- jintArray 类型（C）, 840
- JLabel 类, 674–675
- jlink 程序, 526
- jlong 类型（C）, 817
- jlongArray 类型（C）, 840
- JMOD 文件, 526, 531
- jmod 程序, 526
- JNDI 服务, 350
  - 类加载器, 532
- JndiLoginModule 类, 568
- JNI（Java 本地接口）, 810–871
  - 访问：
    - 数组元素, 840–844
    - C++ 中的函数, 820
  - 调用约定, 820
  - 调试模式, 850
  - 错误处理, 844–849
  - 调用 Java 方法, 833–840
  - 在线文档, 821
- JNI_CreateJavaVM 函数（C）, 850, 854
- JNI_OnLoad、JNI_OnUnload 方法（C）, 816
- jni.h 文件, 817
- JNICALL、JNIEXPORT 宏, 812
- JobAttributes 类（已过时）, 806
- jobject 类型（C）, 835, 840, 858




- jobjectArray 类型（C），840
- 连接样式，716-717
- joining 方法（Collectors），26, 29
- JoinRowSet 接口，330
- JPanel 类，777
- JPEG 格式，745
    - 对图像的操作，767
    - 打印，792
    - 读取，746
- jrt: 语法，527
- js.properties 文件，447
- JScrollPane 类，615
- JSF（JavaServer Faces），261
- JShell，将模块加载到其中，511
- jshort 类型（C），817
- jshortArray 类型（C），840
- JSON-B（JSON Binding），512, 514
- JSP（JavaServer Pages），457-463
- jstring 类型（C），820, 835, 858
- JTable 类，613-652
    - addColumn 方法，630, 636
    - 非对称，622
    - 单元格编辑器，自动安装，641
    - 构造方法，618
    - convertXxxIndexToModel 方法，626, 636
    - 默认渲染操作，622
    - getAutoCreateRowSorter 方法，616, 618
    - getCellSelectionEnabled 方法，636
    - getColumnModel 方法，635
    - getColumnSelectionAllowed 方法，636
    - getDefaultEditor 方法，650
    - getDefaultRenderer 方法，641, 650
    - getFillsViewportHeight 方法，618
    - getRowHeight、getRowMargin 方法，635
    - getRowSelectionAllowed 方法，636
    - getSelectionModel 方法，636
    - moveColumn、removeColumn 方法，630, 636
    - print 方法，616, 618
    - 调整大小模式，625
    - setAutoCreateRowSorter 方法，616, 618, 627
    - setAutoResizeMode 方法，625, 635
    - setCellSelectionEnabled 方法，626, 636
    - setColumnSelectionAllowed 方法，626, 636
    - setDefaultRenderer 方法，640
    - setFillsViewportHeight 方法，618
    - setRowHeight、setRowMargin 方法，625, 635
    - setRowSelectionAllowed 方法，626, 636
    - setRowSorter 方法，627, 636
- JTextArea 类，560
- JTextField 类，641
- JTree 类，652-693
    - addTreeSelectionListener 方法，677
    - 构造方法，654, 662
    - getLastSelectedPathComponent 方法，665, 670
    - getSelectionPath 方法，665, 670, 678, 683
    - getSelectionPaths 方法，678, 683
    - 标识节点，663
    - makeVisible 方法，666, 670
    - scrollPathToVisible 方法，666, 670
    - setRootVisible 方法，660, 662
    - setShowsRootHandles 方法，659, 662
- JUnit 工具，464
- 即时编译器，850
- JVM（Java 虚拟机）
    - 其中的引导类加载器，531
    - 其中的类文件，530
    - 创建，850
    - 嵌入原生代码，849-854
    - 规范，489, 544
    - 终止，546-566, 850
- jvm 指针（C），850

## K

- \x，在正则表达式中，139
- Kerberos 协议，566
- Kernel 类，766, 772
- 卷积核，766
- 键值对。参见 Properties
- 键盘，读取，56, 68
- KeyGenerator 类，602
    - generateKey 方法，602, 607
    - getInstance 方法，606
    - init 方法，606
- KeyPairGenerator 类，609
- 密钥
    - 自动生成，322
    - 生成，602-607
    - 主键，322
- keystore 关键字，599
- KeyStoreLoginModule 类，568
- 密钥库，589-592, 598
    - 在策略文件中引用，599
- keytool 程序，589-592
- krb5LoginModule 类，568

## L

- L（对象），类型代码，95, 831
- Lambda 表达式，与流一起使用，11
- 横向方向，730
- 语言代码，35, 382
- 语言模型 API，485–486
- 语言标签，385
- last 方法（ResultSet），325, 328
- lastXxx 方法（TemporalAccessor），365
- lastXxxTime 方法（BasicFileAttributes），118
- 布局算法，783
- layoutPages 方法（Banner），783
- 惰性操作，3, 7, 14, 147
- LCD 显示器，758
- LD_LIBRARY_PATH 环境变量，816, 854
- 闰秒，354
- 闰年，359, 363
- 《Learn SQL The Hard Way》（Shaw），287
- 《Learning SQL》（Beaulieu），287
- 叶子节点（Swing），652, 660, 685
    - 用于叶子节点的图标，661–662, 674
- 遗留数据，转换为 XML，221
- length 方法
    - Blob 的，318
    - CharSequence 的，63
    - Clob 的，319
    - RandomAccessFile 的，81, 85
- LIB 环境变量，854
- lib/ext 目录，531
- LIKE 语句（SQL），291, 320
- limit 方法（Stream），12, 50, 130
- 换行符，69, 414
    - 在电子邮件中，279
    - 在正则表达式中，140
- Line2D 类，697, 699
- Line2D.Double、Line2D.Float 类，697
- lines 方法（Files），6, 10, 50
- lineTo 方法（Path2D.Float），703, 713
- Linux 操作系统
    - 编译调用 API，854
    - 库路径，816
    - 其中的 OpenSSL，596
    - 使用 GNU C 编译器，813
- list 方法（Files），118
- ListResourceBundle 类，420
- 列表，转换为流，49
- ListSelectionModel 接口
    - setSelectionMode 方法，626, 637
- LITTLE_ENDIAN 常量（ByteOrder），131
- 小端顺序，78, 126, 416
- 加载时间，495
- loadClass 方法
    - ClassLoader 的，534
    - URLClassLoader 的，532
- loadLibrary 方法（System），814, 816
- LOB（大对象），317–319
    - 创建空 LOB，319
    - 放入数据库，318
    - 读取，317
- 本地主机，234
- 本地名称，196
- 局部变量，注解，475
- LocalDate 类，360, 363
    - getDayOfXxx 方法，360, 362
    - getMonth、getMonthValue 方法，362
    - getYear 方法，362
    - isAfter、isBefore、isLeapYear 方法，363
    - 与遗留类，377
    - minus、minusXxx 方法，360, 362
    - now 方法，359, 362
    - of 方法，359, 362
    - parse 方法，376, 395, 401
    - plus、plusXxx 方法，359–360, 362
    - toLocalDate 方法，377
    - until 方法，359, 362
    - 其中的周末，360
    - with 方法，364–365
    - withXxx 方法，362
- LocalDates/LocalDates.java，361
- LocalDateTime 类，366
    - atZone 方法，367
    - 与遗留类，377
    - parse 方法，395, 401
    - toLocalDateTime 方法，377
- Locale 类，31, 381–386
    - 构造方法，385
    - 调试，386
    - forLanguageTag 方法，386
    - getCountry 方法，35, 386
    - getDefault 方法，384, 386
    - getDisplayCountry、getDisplayLanguage 方法，386
    - getDisplayName 方法，384, 386, 388
    - getInstance 方法，402
    - getISOCountries 方法，384, 386
    - getISOLanguages 方法，384
    - getLanguage 方法，386
    - setDefault 方法，384, 386
    - toLanguageTag 方法，383, 386
    - toString 方法，386
- 区域设置，30, 380-386
    - 与资源包，417-418
    - 当前，410
    - 默认，372, 384
    - 显示名称，384
    - 格式化样式，373, 395-396
    - 其中的数字，388
    - 预定义，383
    - 其中的变体，381, 418
- LocalTime 类，365-366
    - getXxx 方法，366
    - isAfter、isBefore 方法，366
    - 与遗留类，377
    - minus、minusXxx 方法，365-366
    - now 方法，365-366
    - of 方法，365-366
    - parse 方法，395, 401
    - plus、plusXxx 方法，365-366
    - toLocalTime 方法，377
    - toXxxOfDay 方法，366
    - withXxx 方法，366
- lock 方法（FileChannel），135-136
- 锁
    - 文件尾部，135
    - 共享，135
    - 解锁，135
- 日志文件，415
- 日志消息，添加到类，490-495
- @LogEntry 注解，490
- 日志记录，代码生成，463
- Logging.properties 文件，273
- LoggingPermission 类，557
- LoginContext 类，567
    - 构造方法，571
    - getSubject 方法，572
    - login、logout 方法，567, 572
- LoginException，572
- LoginModule 接口
    - 开发者指南，575
    - 方法，582
- 登录
    - 已提交，575
    - 模块，568
        - 自定义，573-582
    - 与操作代码分离，575
- Long 类
    - MAX_VALUE 常量，135
- LONG NVARCHAR 数据类型（SQL），348
- long 类型
    - 打印，69
    - 流，43
    - 类型代码，95, 831
    - 与 C 类型，817
    - 以二进制格式写入，78
- LONG VARCHAR 数据类型（SQL），348
- LongBuffer 类，132
- longs 方法
    - Random 的，44, 47, 51
    - SplittableRandom 的，51
- LongStream 接口，43-48
    - 方法，46
- LongSummaryStatistics 类，26, 29-30, 44, 48
- 外观
    - 在其中显示树，658
    - 其中子树的手柄，674
    - 在其中选择多个节点，678
- lookup 方法（Matcher），149
- lookup 方法（MethodHandles），514
- 查找表，420
- LookupOp 类，764-765
    - 构造方法，771
- lookupPrintServices 方法（PrintServiceLookup），793, 795
- lookupStreamPrintServiceFactories 方法（StreamPrintServiceFactory），796
- LookupTable 类，765
- LSB（最低有效字节），78
- LSOutput 接口，208
- LSSerializer 接口，208
- <，实体引用，158

## M

- Mac OS X
    - 其中的字符编码，413
    - 其中的 OpenSSL，596
    - 其中的资源，417
- 邮件消息/邮件头，278-281
- mail/MailTest.java，280
- main 方法
    - 执行，530
    - 在其中设置安全管理器，553
- makeShape 方法（ShapeMaker），704
- makeVisible 方法（JTree），666, 670




- 曼德博集合，759
- 名称改编，813, 831
- 清单文件，86
- map 方法
  - FileChannel 的，125, 130
  - HttpHeaders 的，272, 278
  - Optional 的，18–19
  - Stream 的，11
- mapping 方法（Collectors），37, 40
- 映射
  - 并发映射，31
  - 流元素的映射，30–34, 50
- mapToInt 方法（Stream），42
- mapToXxx 方法（XxxStream），44
- mark 方法
  - Buffer 的，133–134
  - InputStream 的，58
- 标记注解，473
- markSupported 方法（InputStream），58
- 《精通正则表达式》（Friedl），142
- match 属性（XSLT），218
- match/notMatch.java，146
- Matcher 类
  - end 方法，143, 145, 149–150
  - find 方法，145, 149
  - group 方法，143, 145, 149–150
  - groupCount 方法，149
  - lookingAt 方法，149
  - matches 方法，142, 149
  - quoteReplacement 方法，150
  - replaceXxx 方法，148, 150
  - results 方法，146, 150
  - start 方法，143, 145, 149–150
- matcher 方法（Pattern），142, 149
- matches 方法（Matcher），142, 149
- MatchResult 接口，146
  - 其方法，146, 150
- 矩阵变换，729–730
- max 方法
  - 原始类型流的，44, 46–47
  - Stream 的，15–16
- MAX_VALUE 常量（Long），135
- maxBy 方法（Collectors），36, 40
- maxOccurs 属性（XML Schema），181
- MD5 算法，584
- 内存地址与序列号，92
- 内存映射，124–134
- memoryMap/MemoryMapTest.java，127
- MessageDigest 类
  - digest 方法，585, 587
  - 扩展，584
  - getInstance 方法，584–586
  - reset 方法，587
  - update 方法，585–586
- MessageFormat 类，409–413, 422
  - applyPattern 方法，411
  - 构造器，410
  - format 方法，410–411
  - get/setLocale 方法，411
  - 忽略第一个限制，413
- 元注解，465, 481–484
- 元数据（数据库），334–344
- Metal 外观
  - 在其中选择多个节点，678
  - 其中的树，657–658
- Method 类，466
- 方法引用中的类型使用注解，476
- 方法验证错误，545
- MethodHandle 类
  - lookup 方法，514
- 方法
  - 向其中添加日志消息，490–495
  - 注解，464, 475, 479
  - 从本机代码调用，833–840
  - getter/setter 自动生成，489
  - 实例方法，833–834
  - 名称改编，813, 831
  - 注解接口的，472
  - 重写，480
  - 受保护的，532
  - 签名，831–832
  - 静态方法，834–835
- Microsoft
  - 编译器，813–814
  - 其中的调用 API，854
  - 记事本，76
  - ODBC API，284
  - SQL Server，293
- MIME（多用途互联网邮件扩展），745
  - 用于打印服务的，794
- Mime 类的方法，279
- min 方法
  - 原始类型流的，44, 46–47
  - Stream 的，15–16
- minBy 方法（Collectors），36, 40
- minOccurs 属性（XML Schema），181
- minus、minusX 方法
  - Duration 的，358
  - Instant 的，357
  - LocalDate 的，360, 362
  - LocalTime 的，365–366
  - Period 的，363
  - ZonedDateTime 的，370
- MissingResourceException，418
- 斜接连接，716–717
- 斜接限制，717
- 混合内容（XML），157
  - 解析，174
- 现代绘画示例，215
- 修改过的 UTF-8，78–80, 416
  - 与本机代码，819–822
- Module 类
  - getResourceAsStream 方法，514
- module 关键字，503
- module-info.class 文件，510, 515
- module-info.java 文件，503, 515
- 模块，499–527
  - 访问，511–514, 518
  - 自动模块，515–518
  - 声明，503–504
  - 显式模块，517
  - 导出包，506–510
  - 加载到 JShell，511
  - 迁移到模块，515–519
  - 命名，501–502, 515
  - 不传递访问权限，506
  - 开放模块，513
  - 在其中打开包，513
  - 其中同名包，510
  - 限定导出，521
  - 依赖，504–506
  - 服务实现与模块，522
  - 工具，524–527
  - 未命名模块，517–518
  - 版本管理，501
- 单子，12
- Month 枚举，359
  - getDisplayName 方法，373, 395
- MonthDay 类，360
- move 方法（Files），114–115
- moveColumn 方法（JTable），630, 636
- moveTo 方法（Path2D.Float），703, 713
- moveToCurrentRow 方法（ResultSet），326, 329
- moveToInsertRow 方法（ResultSet），326, 328
- MSB（最高有效字节），78
- 多页打印，782–784
- multiplyBy 方法（Duration），358
- MutableTreeNode 接口
  - 实现，654
  - setUserObject 方法，654, 662
- MySQL 数据库，293

## N

- \n
  - 作为换行符，69, 164, 279, 414
  - 在正则表达式中，138–139
- NameCallback 类，574
  - 构造器，581
  - 其方法，581
- NamedNodeMap 接口
  - getLength、item 方法，169
- names 方法（Win32Key），857
- 命名空间，193–196
  - 激活其处理，182
  - 其别名（前缀），179, 195
  - 属性的，195
  - 子元素的，194
  - 将类加载器用作，534
- Nashorn 引擎，440–441
- 国家字符字符串，349
- 美国国家标准与技术研究院，228, 584
- native 关键字，810
- 本机方法
  - 与垃圾回收，821
  - 其中的数组元素，840–844
  - 其中的类引用，827
  - 编译，813
  - 用其枚举键，858
  - 其中的错误处理，844–849
  - 其中的异常，845
  - 其中的实例字段，825–829
  - 在其中调用 Java 构造器，835
  - 链接到 Java，816
  - 命名，811–812
  - 重载，811
  - 使用原因，810
  - 其中的注册表访问函数，857–871
  - 静态本机方法，811
  - 其中的静态字段，829–830
  - 其中的字符串，819
- native2ascii 程序，419
- NCHAR、NCLOB 数据类型（SQL），348–349
- negated 方法（Duration），358
- Nervous text 小应用程序，582
- net.properties 文件，273
- NetPermission 类，556
- newBufferedXxx 方法（Files），112–113
- newBuilder 方法（HttpClient、HttpRequest），271–273, 277
- NewDirectByteBuffer 函数（C），843
- newDirectoryStream 方法（Files），120, 123
- newDocument 方法（DocumentBuilder），206, 208, 221
- newDocumentBuilder 方法
  - （DocumentBuilderFactory），160, 167, 207
- newFactory 方法（RowSetProvider），330, 333
- newFileSystem 方法（FileSystems），123–124
- NewGlobalRef 函数（C），827
- newHttpClient 方法（HttpClient），271, 277
- newInputStream 方法
  - Channels 的，251
  - Files 的，112–113
- newInstance 方法
  - DocumentBuilderFactory 的，160, 167
  - SAXParserFactory 的，198, 201
  - TransformerFactory 的，209
  - XMLInputFactory 的，204
  - XMLOutputFactory 的，210, 214
  - XPathFactory 的，190, 193
- NewObject 函数（C），835, 840, 844
- newOutputStream 方法
  - Channels 的，245, 251
  - Files 的，112–113
- newSAXParser 方法（SAXParserFactory），198, 201
- NewString 函数（C），822
- NewStringUTF 函数（C），820, 822, 824, 857
- newTransformer 方法（TransformerFactory），209, 225
- newXPath 方法（XPathFactory），193
- NewXxxArray 函数（C），843, 857
- next 方法
  - ResultSet 的，300, 302, 322
  - TemporalAdjusters 的，365
  - XMLStreamReader 的，205
- nextElement 方法（Enumeration），672, 857–859
- nextOrSame 方法（TemporalAdjusters），365
- nextPage 方法（CachedRowSet），331, 333
- NMTOKEN、NMTOKENS 属性类型（DTD），174–175
- Node 接口
  - appendChild 方法，207, 209
  - getAttributes 方法，164, 168
  - getChildNodes 方法，161, 168
  - getFirstChild 方法，163, 168
  - getLastChild 方法，164, 168
  - getLocalName 方法，196
  - getNamespaceURI 方法，195–196
  - getNextSibling 方法，164, 168
  - getNodeXxx 方法，164, 169, 195
  - getParentNode 方法，168
  - getPreviousSibling 方法，168
  - 其子接口，161
- 节点渲染器，661
- nodeChanged 方法（DefaultTreeModel），665, 671
- NodeList 接口，161
  - getLength 方法，161, 169
  - item 方法，161, 169, 177
- 节点（Swing），652
  - 添加/移除，665
  - 子节点，652, 655
  - 折叠的，668
  - 连接线，658–659
  - 当前选中的，663
  - 编辑，667, 668
  - 枚举，672–673
  - 展开，666, 668
  - 句柄，657, 659, 674
  - 高亮，674
  - 通过树路径标识，663
  - 使其可见，666
  - 父节点，652, 655
  - 渲染，674–676
  - 根节点，652–660
  - 行位置，665
  - 搜索给定用户对象，673, 678
  - 选择，677
  - 用户对象，654, 665
- nodesChanged 方法（DefaultTreeModel），671
- 非确定性解析，174
- noneMatch 方法（Stream），16
- 流操作的非干扰性，7
- @Nonnull 注解，476–477
- normalize 方法（Path），110–111
- 归一化颜色值，757




- Normalizer 类，404
  - normalize 方法，409
- NoSuchAlgorithmException，586、606
- NoSuchElementException，19–20、859
- notifier 方法（RowFilter），629、638
- NotSerializableException，100
- now 方法
  - Instant 的 of，355、357
  - LocalDate 的 of，359、362
  - LocalTime 的 of，365–366
  - ZonedDateTime 的 of，370
- NTLoginModule 类，568–569
- NTUserPrincipal 类，569
- NullPointerException，845
  - 与 Optional 比较，15
- Number 类
  - doubleValue 方法，387
  - intValue 方法，388
- numberFilter 方法（RowFilter），629、638
- NumberFormat 类，387–394
  - format 方法，388、392
  - getMaximumIntegerDigits 和 getMinimumIntegerDigits 方法，392
  - getAvailableLocales 方法，383、388、391
  - getCurrencyInstance 方法，387、392–393
  - getInstance 方法，387、392
  - getPercentInstance 方法，387、392
  - isGroupingUsed 方法，392
  - isParseIntegerOnly 方法，392
  - parse 方法，387–388、392
  - setCurrency 方法，393
- numberFormat/NumberFormatTest.java，389
- 数字
  - 过滤，629
  - 浮点数，380、387–394
  - 格式化，380、387–394
    - 支持的区域设置，388
    - 使用 C，817
  - 由分组元素生成，36
  - 在正则表达式中，139、141
  - 打印，69
  - 随机数，5、12、44
  - 读取：
    - 从文件读取，64
    - 从 ZIP 归档读取，66
  - 使用区域设置，387
  - 真随机，602
  - 以二进制格式写入，78
- NUMERIC 数据类型（SQL），293、348
- NVARCHAR 数据类型（SQL），348

## O

- Object 类
  - clone 方法，89、106
- 对象检查树，684–693
- 对象序列化，88–108
  - 使用其克隆，106–108
  - 文件格式，93–100
  - 修改默认行为，100–102
  - 单例的序列化，102–103
  - 序列号，90–91
- ObjectInputStream 类，89
  - 构造器，93
  - readObject 方法，89、93、101
- ObjectOutputStream 类，88
  - 构造器，93
  - defaultWriteObject 方法，101
  - writeObject 方法，88、93、100
- 对象关系映射器，512
- 对象
  - 克隆，106–108
  - 转换为流，6、23
  - 指纹，95
  - 生命周期，480
  - 打印，69
  - 从输入流读取，89
  - 保存：
    - 在数据库中，483
    - 在输出流中，88、90
    - 以文本格式，72–75
  - 可序列化，88–93
  - 通过网络传输，92
  - 类型代码，95、831
  - 版本管理，103–106
- objectStream/ObjectStreamTest.java，92
- ODBC API，284、286
- of 方法
  - DoubleStream 的 of，47
  - IntStream 的 of，43、46
  - LocalDate 的 of，359、362
  - LocalTime 的 of，365–366
  - LongStream 的 of，46
  - Optional 的 of，20–21
  - Period 的 of，363
  - Stream 的 of，5、9
  - ZonedDateTime 的 of，367、370
  - ZoneId 的 of，367
- ofDateAdjuster 方法（TemporalAdjusters），364
- ofDays 方法
  - Duration 的 ofDays，357
  - Period 的 ofDays，359、363、368
- ofFile、ofFileDownload 方法（BodyHandlers），272
- OffsetDateTime 类，368
- ofHours 方法（Duration），357
- ofInstant 方法（ZonedDateTime），370
- ofLocalizedXxx 方法（DateTimeFormatter），372、375、394、401
- ofMillis、ofMinutes 方法（Duration），357
- ofMonths 方法（Period），360、363
- ofNanos、ofSeconds 方法（Duration），357
- ofNullable 方法
  - Optional 的 ofNullable，20–21
  - Stream 的 ofNullable，6、9、23
- ofPattern 方法（DateTimeFormatter），373、376
- ofString 方法（BodyHandlers、BodyPublishers），272–273
- ofWeeks、ofYears 方法（Period），363
- of() 字面量（SQL），320
- open 关键字，513
- open 方法
  - FileChannel 的 open，125、130
  - SocketChannel 的 open，244、251
- openConnection 方法（URL），254、259
- 展开的非叶节点图标，661–662、674
- openOutputStream 方法（SimpleJavaFileObject），463
- opens 关键字，513、521
- OpenSSL 工具包，596–597
- openStream 方法（URL），251、259
- 操作系统
  - 字符编码，77、413
  - 路径，64、109
  - 资源，417
- 操作
  - 结合操作，41
  - 惰性操作，3、7、14、147
  - 无状态操作，49
- Optional 类，15–22
  - 创建其值，20
  - empty 方法，20–21
  - filter 方法，18–19
  - flatMap 方法，21–25
  - 用于空流，41
  - get 方法，19–22
  - ifPresent 方法，17–18、48
  - ifPresentOrElse 方法，18
  - isPresent 方法，19–22
  - map 方法，18–19
  - of、ofNullable 方法，20–21
  - or 方法，19
  - orElse 方法，15、17、48
  - orElseGet 方法，17、48
  - orElseThrow 方法，17、20
    - stream 方法，22–25
- optional 关键字，568
- optional/OptionalTest.java，23
- OptionalXxx 类，44、48
- Oracle JVM 实现，842
- ORDER BY 语句（SQL），300
- order 方法（ByteBuffer），126、131
- orFilter 方法（RowFilter），629、638
- org.omg.CORBA 包，500
- org.w3c.dom 包，160
- org.w3c.dom.CharacterData API，169
- org.w3c.dom.Document API，168、209
- org.w3c.dom.Element API，168、209
- org.w3c.dom.NamedNodeMap API，169
- org.w3c.dom.Node API，168–169、196、209
- org.w3c.dom.NodeList API，169
- org.xml.sax.Attributes API，202
- org.xml.sax.ContentHandler API，201
- org.xml.sax.EntityResolver API，178
- org.xml.sax.ErrorHandler API，178
- org.xml.sax.helpers.AttributesImpl API，226
- org.xml.sax.InputSource API，178
- org.xml.sax.SAXParseException API，178
- org.xml.sax.XMLReader API，226
- Orientation 类，102–103
- 外连接，320
- OutOfMemoryError，845
- output 元素（XSLT），218
- 输出流，56–77
  - 与 Unicode，56
  - 缓冲的，65–67
  - 字节处理，65
  - 面向字节的，56
  - 关闭，57、243
  - 过滤器，63–67
  - 层次结构，59–63
  - 对象，88–108
- OutputStream 类，56、60–61、210
  - close 方法，59
  - flush、write 方法，57、59
- OutputStreamWriter 类，68
- OverlappingFileLockException，136
- 重载，811
- @Override 注解，479–480

## P

- 正则表达式中的 \p、\P，138
- Package 类，实现 AnnotatedElement，466
- package-info.java 文件，475
- 包，500
  - 标注，475、479
  - 避免名称冲突，193、534
  - 导出，506–510
  - 隐藏，510
  - 打开，513
  - 拆分，510
- 数据包，232
- 填充方案，601
- 页面设置对话框，777–778
- Pageable 接口
  - 实现，782
  - 对象打印，792
- PageAttributes 类（已过时），806
- pageDialog 方法（PrinterJob），776、778、781
- PageFormat 类
  - getHeight、getWidth 方法，775、782
  - getImageableX/Y 方法，776、782
  - getOrientation 方法，782
- 页面
  - 尺寸，776
  - 多页打印，782–792
  - 方向，730、776、782
- Paint 接口，724–726
- paint 方法（JComponent），639、694
- paintComponent 方法
  - JComponent 的，694
  - StrokePanel 的，719
- 纸张边距，775
- 纸张大小，420、775
- parallel 方法（BaseStream），48、53
- parallel/ParallelStreams.java，51
- parallelStream 方法（Collection），2–3、5、48
- 参数变量标注，475
- 父节点（Swing），652、655
- parse 方法
  - DateTimeFormatter 的 parse，373
  - DocumentBuilder 的 parse，168
  - Locale 的 parse，376、395、401
  - LocalDateTime 的 parse，395、401
  - NumberFormat 的 parse，387–388、392
  - SAXParser 的 parse，198、201
  - XMLReader 的 parse，226
  - ZonedDateTime 的 parse，376、395、401
- 解析后的字符数据，173
- ParseException，388、391
- 解析器，159–169
  - 检查 ID 唯一性，175、183
  - 拉式，202
  - 验证，170
- 解析（XML），159–169
  - 非确定性，174
  - 使用 XML Schema，182
- partitionBy 方法（Collectors），35、37
- PasswordCallback 类，574
  - 构造器，581
  - 其方法，582
- 受密码保护的资源，256
- Path 接口，109–112
  - getXxx 方法，111
  - normalize、relativize、resolve、resolveSibling、toXxx 方法，110–111
- Path2D 类，699
  - append、closePath 方法，703、714
- Path2D.Double 类，697
- Path2D.Float 类，697
  - 其方法，703、713
- pathFromAncestorEnumeration 方法（DefaultMutableTreeNode），673
- 路径（文件系统），109–112
  - 绝对路径与相对路径，64、109–110
  - 检查其属性，116–118
  - 过滤，119
  - 相对化，110
  - 解析，66、110
  - 根组件，109
  - 分隔符，64、109
- 路径（图形），703–704
- Paths 类，123
  - get 方法，109、111
- Pattern 类，142
  - compile 方法，142、148
  - matcher 方法，142、149
  - split 方法，147、149
  - splitAsStream 方法，6、10、147
- 模式，137–151
- #PCDATA 元素内容（DTD），173
- PDF 格式打印，792
- peek 方法（Stream），14–15
- PEM（Privacy Enhanced Mail），596
- Pentium 处理器中的小端序，78
- 百分比格式化，387–394



- 性能
  - 加密算法的，608
  - 文件操作的，125–132
- Period 类
  - `getXxx`、`minus`、`minusXxx`、`plus`、`plusXxx`、`withXxx` 方法，363
  - `Xxx` 方法的，359–360，363，368
  - 用于夏令时，368
- Perl 编程语言中的正则表达式，142
- Permission 类
  - 构造函数，566
  - equals 方法，559
  - 扩展，559
  - `getActions` 方法，559
  - `getName` 方法，561，566
  - `hashCode` 方法，559
  - implies 方法，559–561，566
- 权限文件，548
- permission 关键字，554，558
- 权限，547–551
  - 调用栈，550
  - 类层次结构，549
  - 常用类，554–557
  - 用于文件，557
  - 用于用户，567
  - 实现，559–566
  - 蕴含其他权限，561
  - 在策略文件中，551–559
  - 将代码源映射到，547
  - 顺序，559
  - 属性，558
  - 限制为特定用户，569
  - 套接字，558
  - 目标，557–558
- `permissions/PermissionTest.java`，564
- `permissions/WordCheckPermission.java`，562
- `@Persistent` 注解，483
- 个人数据，传输，600
- Picocli 框架，465
- 像素
  - 上的仿射变换，764
  - 的平均值，766
  - 合成，735–744
  - 插值，725，764
  - 读取，756
  - 设置单个像素，756–763
- 占位符，在消息格式化中，409–413

- 平台类加载器，531
- 插件，加载，532
- plus、plusXxx 方法
  - Duration 的，358
  - Instant 的，357
  - LocalDate 的，359–360，362
  - LocalTime 的，365–366
  - Period 的，363
  - ZonedDateTime 的，370
- PNG 格式，745
  - 打印，792
- `Point2D` 类，698–699
- `Point2D.Double`、`Point2D.Float` 类，697
- 点，在排版中，775
- `Policy` 类，548，552
- 策略文件，551–559
  - 与 Java 插件，598
  - 构建，598
  - 位置，551
  - 解析，561
  - 平台无关，558
  - 在其中引用密钥库，599
  - 中的系统属性，558
  - 中的用户角色，556–582
  - 可见性，562
- 策略管理器，551–559
- 多边形，697，703
- 池，用于并行流，51
- `populate` 方法（`CachedRowSet`），331，333
- Porter–Duff 规则，736–739
- 纵向方向，776
- 端口，229
  - 阻塞，228
  - 在 URI 中，253
- `position` 函数（XPath），220
- `position` 方法（`Buffer`），134
- 符合 POSIX 的文件系统，117
- `PosixFileAttributes` 接口，117
- POST 方法（`HttpRequest.Builder`），272，278
- POST 请求（HTML），262，264–266
  - 构建，272
- `post/PostTest.java`，268
- `@PostConstruct` 注解，479–480
- PostgreSQL 数据库，293
  - 连接到，297
  - 驱动程序，294
- 后序遍历，672
- `postOrderEnumeration` 方法（`DefaultMutableTreeNode`），672，676

- PostScript 格式
  - 打印，792，796
  - 写入，796
- `postVisitDirectory` 方法
  - `FileVisitor` 的，121
  - `SimpleFileVisitor` 的，123
- 预定义字符类，138–141
- `@Deprecated` 注解，479–480
- 谓词函数，35
- `premain` 方法（Instrumentation API），496
- `preorderEnumeration` 方法
  - （`DefaultMutableTreeNode`），672，676
- 预编译语句，311–317
  - 缓存，312
  - 执行，311
- `PreparedStatement` 接口
  - `clearParameters` 方法，317
  - `executeXxx`、`setXxx` 方法，311，317
- `prepareStatement` 方法（`Connection`），311，317，323，327
- `previous` 方法（`ResultSet`），324，328
- `previous`、`previousOrSame` 方法
  - （`TemporalAdjusters`），365
- `previousPage` 方法（`CachedRowSet`），333
- `preVisitDirectory` 方法
  - `FileVisitor` 的，121
  - `SimpleFileVisitor` 的，123
- 主键，322
- 基本类型
  - 的数组，843
  - 中二进制格式的 I/O，59
  - 的流，42–44
- `Principal` 接口
  - `getName` 方法，573
- 主体（登录），568
- `print` 方法
  - `DocPrintJob` 的，795
  - `JTable` 的，616，618
  - `PrintWriter` 的，69–70，833–834
- 打印对话框，773
  - 中显示页码范围，774，783
  - 本机，774，778
- 打印服务，792–795
  - 文档类型，793–794
  - 用于图像，795
  - 流，796–799
- `print(PrintComponent.java)`，779
- `print(PrintTestFrame.java)`，778

- `Printable` 接口
  - 实现，772，777
  - 对象，打印，792
- `print` 方法，773，781，783
- 打印机图形上下文，784
- `PrinterException`，773
- `PrinterJob` 类
  - `defaultPage` 方法，781
  - `getPrinterJob` 方法，773，781
  - `pageDialog` 方法，776，778，781
  - `print` 方法，773–774，782
  - `printDialog` 方法，773–774，781
  - `setPageable` 方法，783
  - `setPrintable` 方法，782
- `print` 函数（C），817
- `print` 方法（`PrintWriter`），69–70，385
- `printf/Printf.c`，818
- `printf/Printf.java`，818
- `printf/PrintfTest.java`，819
- `printf2/Printf2.c`，824
- `printf2/Printf2.java`，823
- `printf2/Printf2Test.java`，823
- `printf3/Printf3.c`，837
- `printf3/Printf3.java`，836
- `printf3/Printf3Test.java`，836
- `printf4/Printf4.c`，846
- `printf4/Printf4.java`，848
- `printf4/Printf4Test.java`，848
- 打印
  - 裁剪区域，775
  - 期间计数页数，775
  - 图像，772–782
  - 布局，783
  - 多页文档，782–784
  - 份数，799
  - 页面方向，730，776
  - 纸张大小，775
  - 质量，802
  - 选择设置，773
  - 开始，546，773
  - 文本，772–782
  - 使用：
    - 分带，775
    - 变换，784
- 打印属性，799–807
  - 添加/获取，802
  - 类别，801–802
  - 检查值，802
  - 层次结构，800

- `PrintJob` 类（已过时），773
- `PrintJobAttribute` 接口，799
  - 打印属性，803–806
- `PrintJobAttributeSet` 接口，800
- `println` 方法
  - `PrintWriter` 的，69–70
  - `System.out` 的，414–415
- `PrintQuality` 类，802
- `PrintRequestAttribute` 接口，799
  - 打印属性，803–806
- `PrintRequestAttributeSet` 接口，773，800
- `PrintService` 接口
  - `createPrintJob` 方法，793，795
  - `getAttributes` 方法，807
  - `getName` 方法，793
- `printService/PrintServiceTest.java`，797
- `PrintServiceAttribute` 接口，799
  - 打印属性，803–806
- `PrintServiceAttributeSet` 接口，800
- `PrintServiceLookup` 类
  - `lookupPrintServices` 方法，793，795
- `PrintStream` 类，69
- `PrintWriter` 类，64，68–70
  - `checkError` 方法，69–70
  - 构造函数，70
  - `print` 方法，69–70，833–834
  - `printf` 方法，69–70
  - `println` 方法，69–70，385
- 私钥，587–599，608
- `PrivilegedAction` 接口，575
  - 实现，568
  - `run` 方法，568，572
- `PrivilegedExceptionAction` 接口，568
  - `run` 方法，572
- `processAnnotations` 方法
  - （`ActionListenerInstaller`），466
- 处理指令（XML），159
- 处理工具，463
- `Processor` 接口，485
- 程序员节，359
- 程序。参见应用程序
- `Properties` 类，154
- 属性，自动生成，489
- 属性文件，154
  - 字符编码，419
  - 事件处理器，447
  - 用于资源包，417–418
  - 用于字符串资源，417
  - 用于字符串，418–419
  - 中无密码，279
- 属性权限，558
- `@Property` 注解，489
- `PropertyPermission` 类，554
- 保护域，549
- `ProtectionDomain` 类
  - 构造函数，551
  - `getCodeSource`、`implies` 方法，551
  - `provides` 关键字，524
- 代理对象，466
- 公共证书的密钥库，599
- `PUBLIC` 标识符（DTD），208
- 公钥密码，587–594，608–612
  - 性能，608
- 公钥密码学标准 (PKCS) #5，601
- 拉式解析器，202
- `PushbackInputStream` 类，65
  - 构造函数，67
  - `unread` 方法，67
- `put` 方法
  - `Bindings` 的，443
  - `ByteBuffer` 的，131
  - `CharBuffer` 的，132
  - `ScriptEngine` 的，443
  - `ScriptEngineManager` 的，443
- PUT 方法（`HttpRequest.Builder`），278
- `putClientProperty` 方法（`JComponent`），658，663
- `putNextEntry` 方法（`ZipOutputStream`），85–86
- `putXXX` 方法（`ByteBuffer`），127，131

## Q

- `\0`，在正则表达式中，138
- QBE（按例查询）工具，289
- `QuadCurve2D` 类，697，699，703
- `QuadCurve2D.Double` 类，697–698，713
- `QuadCurve2D.Float` 类，697
- 二次曲线，702–703
- `quadTo` 方法（`Path2D.Float`），703，713
- 限定导出，521
- 限定名称，195
- 量词，141
- 查询（数据库），290–292
  - 按例，289
  - 执行，300，310–322
  - 多个，303
  - 用其结果填充行集，331
  - 准备，311–317
  - 返回多个结果，321–322




- query/QueryTest.java, 313
  - 实体引用，158
- quoteReplacement 方法 (Matcher)，150

## R

- R 编程语言，440, 448
  - \r 在字段字符中，69, 164, 414
    - 在电子邮件中，279
  - \r、\n，在正则表达式中，138, 140
- 竞态条件，49
- Random 类，602
  - 其方法，44, 47, 51
- 随机数流，5, 12, 44, 51
- 随机访问文件，80–85
- randomAccess/RandomAccessTest.java, 83
- RandomAccessFile 类，80–85
  - 构造器，84
  - getChannel 方法，130
  - getFilePointer 方法，81, 84
  - length 方法，81, 85
  - seek 方法，80, 85
- 随机性，602
- range、rangeClosed 方法 (XxxStream)，43, 46
- 范围，转换为流，49
- Raster 类
  - getDataElements 方法，758, 762
  - getPixel、getPixels 方法，757, 762
- 光栅图像，744–772
  - 从像素构造，756–763
  - 过滤，763–772
  - 读取器/写入器，745–755
- rasterImage/RasterImageFrame.java, 760
- read 方法
  - CipherInputStream 的，608
  - FileInputStream 的，56
  - ImageIO 的，745, 753
  - ImageReader 的，754
  - InputStream 的，56–58
  - ZipInputStream 的，85
- read/config.dtd, 187
- read/config.xml, 187
- read/config.xsd, 187
- read/XMLReadTest.java, 183
- Readable 接口，59
  - read 方法，61, 63
- ReadableByteChannel 接口，245
- readAllBytes 方法 (InputStream)，56, 58
- readAllXxx 方法 (Files)，113
- readAttributes 方法 (Files)，117
- readBoolean 方法 (DataInput)，79
- readChar 方法 (DataInput)，79, 81
- readDouble 方法 (DataInput)，79, 89, 101
- Reader 类，56, 60
  - read 方法，59
- READER 类 (DocFlavor)，794
- readExternal 方法 (Externalizable)，101–102
- readFixedString 方法 (DataIO)，81–82
- readFloat 方法 (DataInput)，79
- readInt 方法 (DataInput)，79, 81, 89
- readLine 方法 (Console)，71
- readLong 方法 (DataInput)，79
- readNBytes 方法 (InputStream)，56, 58
- readObject 方法
  - Date 的，101
  - ObjectInputStream 的，89, 93, 101
- ReadOnlyBufferException
- readResolve 方法 (Serializable)，103
- readShort 方法 (DataInput)，79
- readThumbnail 方法 (ImageReader)，754
- readUTF 方法 (DataInput)，79–80
- REAL 数据类型 (SQL)，293, 348
- 接收器参数，478
- Rectangle2D 类，697, 699
- Rectangle2D.Double、Rectangle2D.Float 类，697
- RectangularShape 类，697
- URL 的重定向，266–267
- reduce 方法 (Stream)，41–43
- reducing 方法 (Collectors)，37
- 归约，15, 41–43
- ref 属性 (XML Schema)，181
- 反射
  - 访问：
    - 私有成员，511–514, 546
    - 受保护方法，532
  - 构造：
    - 类树，678
    - 静态字段名，396
  - 从变量枚举字段，687
- ReflectPermission 类，556
- regex/RegexTest.java, 144
- regexFilter 方法 (RowFilter)，629, 638
- 注册表编辑器，855, 860
- 注册表项，856–858
- 正则表达式，137–151
  - 其中的转义，73, 141
  - 过滤，629

- *ResultSet 接口（续）*
  - close 方法，303
  - 并发值，323, 325, 327, 329
  - deleteRow 方法，327, 329
  - findColumn 方法，302
  - first、last 方法，325, 328
  - getBlob、getClob 方法，317–318
  - getConcurrency 方法，324–325, 328
  - getDate、getDouble、getInt、getObject、getString 方法，300, 302
  - getMetaData 方法，335, 344
  - getRow 方法，325, 328
  - getType 方法，324, 328
  - getWarnings 方法，306
  - insertRow 方法，326, 329
  - isClosed 方法，303
  - isFirst、isLast、isBeforeFirst、isAfterLast 方法，325, 328
  - 迭代协议，300
  - moveToCurrentRow 方法，326, 329
  - moveToInsertRow 方法，326, 328
  - next 方法，300, 302, 322
  - previous 方法，324, 328
  - relative 方法，324, 328
  - 类型值，323, 325, 327, 329
  - updateObject 方法，302
  - updateXXX 方法，326, 329
- *ResultSetMetaData 接口*，335
  - getColumnXXX 方法，335, 344
- 保留策略，482
- @Retention 注解，465, 479, 482
- retire/Retire.java, 424
- retire/RetireResources_de.java, 435
- retire/RetireResources_zh.java, 436
- retire/RetireResources.java, 435
- retire/RetireStrings_de.properties, 436
- retire/RetireStrings_zh.properties, 437
- retire/RetireStrings.properties, 436
- 退休计算器示例，421–437
- RETURN_GENERATED_KEYS 字段 (Statement)，322
- 返回值，缺失，15
- rewind 方法 (Buffer)，133–134
- RFC 821 标准，279
- RFC 822 标准，372
- RFC 1123 标准，372
- RFC 2396 标准，253
- RFC 2616 标准，255
- RFC 2911 标准，806
- RGB 颜色模型，735, 758
- 罗纳德·李维斯特，584
- 基于角色的认证，573
- rollback 方法 (Connection)，345–347
- 根证书，599
- 根组件（文件系统），109
- 根元素 (XML)，157
  - 在其中引用模式，179
- 根节点 (Swing)，652–660
  - 其句柄，659–660
  - 分离其子节点，659
- rotate 方法 (Graphics2D)，728, 732
- 旋转，727–728
  - 与插值像素，764
  - 以中心点，729
- 圆端帽，716
- 圆角连接，716–717
- 圆角矩形，699–700
- RoundEnvironment 接口，486
- RoundRectangle2D 类，697, 699–700
- RoundRectangle2D.Double 类，697–698, 712
- RoundRectangle2D.Float 类，697
- 行集（数据库），329–333
  - 缓存的，330–335
  - 构造，330
  - 修改，330
  - 其页大小，331
- RowFilter 类，628–630
  - 其方法，629, 638
- RowFilter.Entry 类，629
- ROWID 数据类型 (SQL)，348–349
- RowId 接口，349
- 行（数据库），287
  - 删除/插入，327
  - 遍历，325
  - 在结果集中的顺序，300
  - 检索，349
  - 选择，290
  - 更新，326
- 行 (Swing)
  - 过滤，628–630
  - 其高度，625
  - 隐藏，630
  - 其边距，625
  - 位置，在节点中，665
  - 调整大小，625
  - 选择，615, 626
  - 排序，616, 627–628
- RowSet 接口，329–332
  - 其方法，331–332

- SecureRandom 类
  - setSeed 方法，602
- *Securing Java*（McGraw/Felten），550
- 安全性
  - 字节码验证，541–545
  - 类加载器，530–545
  - 代码签名，597–599
  - 不同级别，583
  - 数字签名，582–599
  - 加密，599–612
  - 用户认证，566–582
- 安全管理器，546–566
- 安全策略，547
- SecurityException，547, 549
- SecurityManager 类
  - checkExit 方法，546, 549
  - checkPermission 方法，549–550, 559–560
  - checkRead 方法，550
- SecurityPermission 类，556
- “仅向前查找”模式 (ImageInputStream)，747
- seek 方法 (RandomAccessFile)，80, 85
- select 属性 (XSLT)，219
- SELECT 语句 (SQL)，290–291
  - 执行，300
  - 用于 LOB，317
  - 查询中的多个，321
  - 批更新中不支持，346
- 选择模型，626
- send 方法 (HttpClient)，277
- sendAsync 方法 (HttpClient)，273, 277
- separator 常量 (File)，64
- 分隔符（文件系统），64, 109
- sequence 元素 (XML Schema)，181
- 序列，生成，5
- 序列号，90–91
  - 与内存地址，92
- serialClone/SerialCloneTest.java, 106
- Serializable 类，106
- Serializable 接口，89, 95, 483
  - readResolve 方法，103
- @Serializable 注解，483
- SerializablePermission 类，556
- 序列化，88–108
  - 使用其克隆，106–108
  - 其文件格式，93–100
  - 修改默认，100–102
  - 单例的，102–103
  - 用于其的序列号，90–91
- serialver 程序，104
- serialVersionUID 常量，104
- server/EchoServer.java, 237
- 服务器
  - 访问，251–270
  - 将客户端连接到，230–232
  - 实现，236–251
  - 调用程序，261
- 服务器端代理，261–270
  - 在其中重定向 URL，266–267
- ServerSocket 类，236–251
  - accept 方法，236, 239–240
  - close 方法，239
  - 构造器，239
- 服务加载，522–524
- 服务提供者接口，746
- SERVICE_FORMATTED 类 (DocFlavor)，794
- ServiceLoader 类，522
- Servlet，457–463
- Session 类
  - setDebug 方法，280
- Set 接口
  - containsAll、equals 方法，561
- set/Item.java, 494
- set/SetTest.java, 495
- setAllowsChildren、setAsksAllowsChildren 方法 (DefaultMutableTreeNode)，661, 663
- setAllowUserInteraction 方法 (URLConnection)，254
- setAttribute、setAttributes 方法 (Element)，207, 209
- setAutoCommit 方法 (Connection)，347
- setAutoCreateRowSorter 方法 (JTable)，616, 618, 627
- setAutoResizeMode 方法 (JTable)，625, 635
- setBinaryStream 方法 (Blob)，319
- SetBooleanArrayRegion 函数 (C)，842
- SetBooleanField 函数 (C)，830
- SetByteArrayRegion 函数 (C)，842, 844, 857
- SetByteField 函数 (C)，830
- setClip 方法 (Graphics)，733–734, 775




- setClosedIcon 方法（DefaultTreeCellRenderer），676
- setColumnSelectionAllowed 方法（JTable），626, 636
- setCommand 方法（RowSet），331–332
- setComparator 方法（DefaultRowSorter），628, 637
- setComposite 方法（Graphics2D），695, 738, 744
- setConnectTimeout 方法（URLConnection），254, 260
- setContentHandler 方法（XMLReader），226
- setContextClassLoader 方法（Thread），533, 541
- setCrc 方法（ZipEntry），87
- setCurrency 方法（NumberFormat），393
- setDataElements 方法（WritableRaster），759, 762
- setDate 方法（PreparedStatement），311, 317
- setDebug 方法（Session），280
- setDecomposition 方法（Collator），408
- setDefault 方法
  - CookieHandler 的，267
  - Locale 的，384, 386
- setDefaultNamespace 方法（XMLStreamWriter），214
- setDefaultRenderer 方法（JTable），640
- setDoInput 方法（URLConnection），254–255, 259
- setDoOutput 方法（URLConnection），254–255, 259, 264, 266
- setDouble 方法（PreparedStatement），311, 317
- setDoubleArrayRegion 函数（C），842, 844
- setDoubleField 函数（C），826, 830
- setEntityResolver 方法（DocumentBuilder），172, 177
- setErrorHandler 方法（DocumentBuilder），177
- setErrorWriter 方法（ScriptContext），444
- setFeature 方法（SAXParserFactory），199
- setFillsViewportHeight 方法（JTable），618
- setFloatArrayRegion 函数（C），842, 844
- setFloatField 函数（C），830
- setFrom 方法（MimeMessage），279
- setGroupingUsed 方法（NumberFormat），392
- setHeaderXxx 方法（TableColumn），641, 651
- setIfModifiedSince 方法（URLConnection），254–255, 260
- setIgnoringElementContentWhitespace 方法（DocumentBuilderFactory），176, 179
- setInput 方法（ImageReader），754
- setInstanceFollowRedirects 方法（HttpURLConnection），267
- setInt 方法（PreparedStatement），311, 317
- setIntArrayRegion 函数（C），842, 844
- setIntField 函数（C），826, 830, 859
- setLeafIcon 方法（DefaultTreeCellRenderer），676
- setLevel 方法（ZipOutputStream），87
- setLocale 方法（MessageFormat），411
- setLogWriter 方法（DriverManager），297
- setLongArrayRegion 函数（C），842, 844
- setLongField 函数（C），830
- setMaximumXxxDigits、setMinimumXxxDigits 方法（NumberFormat），392
- setMaxWidth 方法（TableColumn），624, 637
- setMethod 方法（ZipEntry, ZipOutputStream），87
- setMinWidth 方法（TableColumn），624, 637
- setName 方法（NameCallback），581
- setNamespaceAware 方法
  - DocumentBuilderFactory 的，182, 195–196, 199, 207
  - SAXParserFactory 的，201
- setObjectArrayElement 函数（C），840, 843, 845
- setObjectField 函数（C），826, 830
- setOpenIcon 方法（DefaultTreeCellRenderer），676
- setOutput 方法（ImageWriter），755
- setOutputProperty 方法（Transformer），209
- setPageable 方法（PrinterJob），783
- setPageSize 方法（CachedRowSet），331, 333
- setPaint 方法（Graphics2D），695, 724, 726
- setParseIntegerOnly 方法（NumberFormat），392
- setPassword 方法
  - PasswordCallback 的，582
  - RowSet 的，331–332
- setPixel、setPixels 方法（WritableRaster），756, 762
- setPreferredWidth 方法（TableColumn），624, 637
- setPrefix 方法（XMLStreamWriter），214
- setPrintable 方法（PrinterJob），782
- setProperty 方法（XMLInputFactory），203–204
- setReader 方法（ScriptContext），444
- setReadTimeout 方法（URLConnection），254, 260
- Files 的，116–117
- skip 方法
  - InputStream 的，58
  - Stream 的，12
- skipBytes 方法（DataInput），80
- SMALLINT 数据类型（SQL），293, 348
- SMTP（Simple Mail Transport Protocol），278–281
- SOAP（Simple Object Access Protocol），501
- Socket 类
  - connect 方法，233
  - 构造函数，232–233
  - getInputStream 方法，231–232, 236
  - getOutputStream 方法，232, 236
  - isClosed、isConnected 方法，233
  - isXxxShutdown、shutdownXxx 方法，244
  - setSoTimeout 方法，232–233
- Socket 权限，558
- socket/socketTest.java，231
- SocketChannel 类，244
  - open 方法，244, 251
- SocketPermission 类，554
- Sockets
  - 半关闭，243–244
  - 中断，244–251
  - 打开，231, 246
  - 超时，232–233
- SocketTimeoutException，232, 260
- sort 方法（Collections），402
- sorted 方法（Stream），14–15
- 源文件
  - 其字符编码，416
  - 从内存读取，454
- Source 接口，220, 349
- 源码级注解，484–489
- 空格。参见空白字符
- SPARC 处理器，其中的大端序，78
- split 方法
  - Pattern 的，147, 149
  - String 的，72, 147
- 拆分包，510
- splitAsStream 方法（Pattern），6, 10, 147
- spliterator 方法（Iterable），10
- Spliterators 类
  - spliteratorUnknownSize 方法，6, 9
- SplittableRandom 类，其方法，51
- sprintf、snprintf 函数（C），823
- SQL（结构化查询语言），287–293
  - 更改数据库内的数据，292
  - 其中的命令，295
  - 其中的数据类型，293, 348–349
  - 其中的相等性测试，291
  - 其中的转义，319–321
  - 其中的异常，304–306
  - 其中执行语句，299–303
  - 其中的关键字，290
  - 从文件读取指令，306
  - 其中的字符串，291
  - 与 Java 对比，313
  - 其中的警告，304
  - 其中的通配符，291
- SQLException 类，304–306, 324
  - 与回滚，345
  - 与保存点，347
  - getXxx、iterator 方法，304–305
- SQLPermission 类，557
- SQLWarning 类，304, 324
  - getNextWarning 方法，306
- SQLXML 数据类型（SQL），348–349
- 方形端帽，716
- 平方根，计算，21
- SquirtLE 程序，336
- SRC，src Xxx 组合规则，737–739
- src.jar 文件，850
- sRGB 标准，758
- 标准扩展，531
- StandardCharsets 类，77
- StandardJavaFileManager 接口，453–455
  - getJavaFileObjectsFromXxx 方法，462
- start 方法
  - Matcher 的，143, 145, 149–150
  - MatchResult 的，146, 150
- startDocument 方法（ContentHandler），201
- startElement 方法（ContentHandler），197–201
- 无状态操作，49
- Statement 接口，299–303
  - addBatch 方法，346–347
  - close、closeOnCompletion 方法，302–303
  - execute 方法，301, 307, 321–322
  - executeBatch 方法，346–347
  - executeLargeBatch 方法，347
  - executeQuery 方法，300–301, 324
  - executeUpdate 方法，299, 301, 322, 345
  - getMoreResults 方法，321–322
  - getResultSet 方法，302
  - getUpdateCount 方法，302, 321
  - getWarnings 方法，306
  - isClosed 方法，302
  - RETURN_GENERATED_KEYS 字段，322
  - 用于多个查询，303
- 语句（数据库）
  - 关闭，303
  - 复杂，313
  - 并发打开，303
  - 执行，299–303
  - 分组为事务，344–349
  - 在批量更新中，346
  - 多个，303
  - 预编译，311–317
  - 其中的截断，305
- 静态字段，在本地代码中，829–830
- 静态初始化块，814
- 静态方法，从本地代码调用，834–835
- statusCode 方法（HttpResponse），272, 278
- StAX 解析器，202–206
  - 其中的命名空间处理，203
  - 其中无缩进输出，211
- stax/StAXTest.java，203
- StAXSource 类，220
- stopCellEditing 方法（CellEditor），644–645, 652
- 存储过程，319–320
- *Stream 接口*
  - allMatch、anyMatch 方法，16
  - collect 方法，25–30, 42–43
  - concat 方法，13
  - count 方法，3–4, 15
  - distinct 方法，14–15, 50
  - dropWhile 方法，13
  - empty 方法，5, 9
  - filter 方法，3–11, 15
  - findAny 方法，16
  - findFirst 方法，15–16
  - flatMap 方法，12
  - forEach 方法，25, 28
  - forEachOrdered 方法，25
  - generate 方法，5, 9, 43
  - iterate 方法，5, 9, 14, 43
  - iterator 方法，25
  - limit 方法，12, 50
  - map 方法，11
  - mapToInt 方法，42
  - max、min 方法，15–16
  - noneMatch 方法，16
  - of 方法，5, 9
  - ofNullable 方法，6, 9, 23
  - peek 方法，14–15
  - reduce 方法，41–43
  - skip 方法，12
  - sorted 方法，14–15
  - takeWhile 方法，13
  - toArray 方法，25, 28
  - unordered 方法，50
- stream 方法
  - Arrays 的，5, 9, 43
  - Collection 的，2–3, 5
  - Optional 的，22–25
  - StreamSupport 的，6, 10
- 流式解析器，159, 196–206
- StreamPrintService 类，796
- StreamPrintServiceFactory 类，796
  - getPrintService 方法，796
  - lookupStreamPrintServiceFactory 方法，796
- StreamResult 类，210, 221
- 流，1–7
  - 收集其元素，25–31
  - 从中计算值，41–43
  - 与数组相互转换，5, 25, 49
  - 创建，5–10
  - 调试，14
  - 空，5, 15, 41
  - 加密，607–608
  - 过滤，22
  - 有限，6
  - 展平，12, 22
  - 用于打印服务，796–799
  - 无限，3, 5, 12, 14
  - 输入，160
  - 的中间操作，3
  - 的非干扰性，7
  - 基本类型值的，42–44
  - 随机数的，44
  - 并行，2, 16, 25, 31, 35, 41, 48–53
  - 惰性处理，3, 7, 14
  - 的归约，15
  - 从中移除重复项，14
  - 由 Files.lines 返回，50
  - 排序，14, 49
  - 拆分/合并，12–13
  - 汇总，26, 44
  - 的终止操作，3, 15



- 转换，11-12, 44
- 与集合对比，3
- streams/CountingWords.java, 4
- streams/CreatingStreams.java, 7
- streams/PrimitiveTypeStreams.java, 44
- StreamSource 类，220
  - 构造函数，225
  - transform 方法，221
- StreamSupport 类
  - stream 方法，6, 10
- String 类，62
  - compareTo 方法，402
  - format 方法，385
  - split 方法，72, 147
  - toLowerCase 方法，11
  - trim 方法，163, 388
- STRING 类（Oracle），794
- String 参数，819-825
- StringBuffer 类，62, 132
- StringBuilder 类，62, 82
- 字符串
  - 转换为码点，11
  - 编码，379, 416
  - 固定大小，I/O，81-82
  - 在本机代码中，819-825
  - 在 SQL 中，291
  - 国际化，417-418
  - 排序，402
  - 模式，137-151
  - 打印，69
  - 排序，402
  - 拆分，6
  - 转换为小写/大写，11
  - 以二进制格式写入，78
- StringSource 类，454
- Stroke 接口，715
- stroke/StrokeTest.java, 719
- StrokePanel 类，719
- 描边，694, 715-724
  - 虚线模式，717-718
  - 端点样式，716-718
  - 连接样式，716-717
  - 设置，694
  - 粗细，716
- 样式表（XSLT），216-226
- Subject 类
  - doAs、doAsPrivileged 方法，568-569, 572
  - getPrincipals 方法，572
- 主体（登录），568
- subSequence 方法（CharSequence），63
- subtract 方法（Area），714-715
- 减法运算符，不满足结合律，41
- 子树（Swing），657, 674
  - 向其添加节点，666
  - 折叠和展开，658
- 苏埃托尼乌斯，盖乌斯·特兰奎卢斯，536
- sufficient 关键字，568
- sum、summaryStatistics 方法（原始类型流），46, 46-47
- summarizingXxx 方法（收集器），26, 29, 37
- summingXxx 方法（收集器），36, 40
- SunJCE 密码算法，600
- 超类，其中的类型使用注解，476
- Supplier 接口
  - get 方法，10
- @SupportedAnnotationTypes 注解，485
- @SupportedValuesAttribute 接口，799
- supportsBatchUpdates 方法（DatabaseMetaData），346, 348
- supportsResultSetXxx 方法（DatabaseMetaData），324, 329
- @SuppressWarnings 注解，479-480
- SVG（可缩放矢量图形），215-216
- Swing，613-693
  - 为其生成动态代码，457
  - 表格，613-652
  - 树，652-693
- 对称密码算法，600-601
  - 性能，608
- SyncProviderException 接口，332-333
- System 类
  - console 方法，415
  - loadLibrary 方法，814, 816
  - setSecurityManager 方法，553
- 系统类加载器，531
- SYSTEM 标识符（DTD），171, 208
- 系统属性，在策略文件中，558
- System.err 类，69, 453
- System.in 类，69
  - 与字符编码，415
- System.out 类，69, 453
  - 与字符编码，415
  - println 方法，414-415

## T
- t 字面量（SQL），320
- \t，在正则表达式中，138
- **文本**，68
  - 编码，75–77
  - 从 XML 文件生成，219–221
  - 输出，68–70
  - 打印，772–782, 792
  - 读取，70–72
  - 在其中保存对象，72–75
  - 通过套接字传输，236–251
  - 与二进制数据对比，68
- **文本字段**
  - 编辑，641
  - 验证其中的输入，560–566
- **文本文件的编码**，414–415
- **文本节点（XML）**
  - 构造，207
  - 从 XML 检索，163
- **TextCallbackHandler 类**，574
- **textFile/textFileTest.java**，73
- **TextLayout 类**
  - getXxxx 方法，373
- **TextStyle 枚举**，396
- **TextSyntax 类**，802
- **TexturePaint 类**，725–726
- this 关键字，826
  - 添加注解，477–478
- **Thread 类**
  - get/setContextClassLoader 方法，533, 541
- **threaded/ThreadEchoServer.java**，241
- **ThreadedEchoHandler 类**，239–243
- **线程**
  - 阻塞，57, 244–251
  - 在其中执行脚本，442
  - 使用线程的 Internet 连接，239–243
  - 竞争条件，49
  - 在其中引用类加载器，533–534
- **三层模型**，286–287
- **Throw、ThrowNew 函数（C）**，844–845, 849
- **Throwable 类**，844
- **缩略图**，748
- **时间**
  - 当前，354
  - 格式化，371–376, 394–401
  - 实例，365
  - 字面量，319
  - 本地时间，365–366
  - 测量，355
  - 解析，373
  - 带时区的时间，367–371, 394
- **Time 类**，376
  - valueOf 方法，377
- **当日时间服务**，228
- **TIME、TIMESTAMP 数据类型（SQL）**，293, 320, 348
- **timeline/Line.java**，356
- **超时**，232–233
- **Timestamp 类**，376
  - toInstant、valueOf 方法，377
- **时间戳**，371
  - 将时刻用作时间戳，355
- **TimeZone 类**
  - getTimeZone、toZoneId 方法，377
- **toAbsolutePath 方法（Path）**，110–111
- **toArray 方法**
  - AttributeSet 的，807
  - 原始类型流的，44, 46–47
  - Stream 的，25
  - 流的，28
- **toCollection 方法（Collectors）**，25, 29
- **toConcurrentMap 方法（Collectors）**，31, 34
- **toDays 方法（Duration）**，355, 358
- **toFile 方法（Path）**，111
- **toFormat 方法（DateTimeFormatter）**，373, 377
- **toHours 方法（Duration）**，355, 358
- **toInstant 方法**
  - Date 的，376–377
  - FileTime 的，377
  - Timestamp 的，377
- **toLocalDateTime**，367, 371
- **tokens 方法（Scanner）**，6, 10
- **toLanguageTag 方法（Locale）**，383, 386
- **toList 方法（Collectors）**，25, 29
- **toLocalXxx 方法**
  - LocalXxx 的，377
  - ZonedDateTime 的，371
- **toLowerCase 方法（String）**，11
- **toMap 方法（Collectors）**，30–34
- **toMillis、toMinutes、toNanos 方法（Duration）**，355, 358
- **toNanoOfDay 方法（LocalTime）**，366
- **Tool 接口**
  - run 方法，461
- **TopLevel 工具类**
  - getSystemJavaCompiler 方法，453
- **tools.jar 文件**，527
- **toPath 方法（File）**，111–112
- **顶层窗口，打开**，546
- **toSecondOfDay 方法（LocalTime）**，366
- toSeconds 方法（Duration），355, 358
- toSet 方法（Collectors），25, 29, 36
- toString 方法
  - 使用注解实现，486–489
  - Annotation 的，472
  - CharSequence 的，63
  - Currency 的，394
  - Locale 的，386
  - TableStringConverter 的，628, 637
  - Variable 的，687
- toUnmodifiableList 方法（Collectors），29
- toUnmodifiableMap 方法（Collectors），34
- toUnmodifiableSet 方法（Collectors），29
- toZonedDateTime 方法（GregorianCalendar），376–377
- toZoneId 方法（TimeZone），377
- 事务，344–349
  - 提交，344
  - 错误处理，346
  - 回滚，344
- transferTo 方法（InputStream），58
- transform 方法
  - Graphics2D 的，695, 730, 732
  - StreamSource 的，221
  - Transformer 的，209, 220
- transform/makentl.xsl, 221
- transform/makeprop.xsl, 222
- transform/TransformerTest.java, 223
- 变换，694, 727–732
  - 仿射，730, 764
  - 组合，728–729
  - 基本类型，727–728
  - 矩阵，729–730
  - 顺序，728
  - 设置，695
  - 用于打印，784
- Transformer 类
  - setOutputProperty 方法，209
  - transform 方法，209, 220
- TransformerFactory 类
  - newInstance 方法，209
  - newTransformer 方法，209, 225
- transient 关键字，100
- transitive 关键字，519–521
- translate 方法（Graphics2D），728, 732, 784
- 平移，727–728
- 透明度，735–744
- 遍历顺序，672
- 树事件，677–684
- 树模型
  - 构造，654, 685
  - 自定义，684–693
  - 默认，654
- 树解析器，159
- 树路径，663–671
  - 构造，666, 673
- 树选择监听器，677
- tree/SimpleTreeFrame.java, 656
- TreeCellRenderer 接口，674–676
  - getTreeCellRendererComponent 方法，675–676
  - 实现，674
- treeEdit/TreeEditFrame.java, 668
- TreeMap 类，31
- TreeModel 接口，654, 664
  - add/removeTreeModelListener 方法，685, 693
  - getChild、getChildCount、getRoot 方法，685–687, 692
  - getIndexOfChild 方法，685, 692
  - 实现，654
  - isLeaf 方法，663, 685, 693
  - valueForPathChanged 方法，686, 693
- treeModel/ObjectInspector.java, 688
- treeModel/ObjectTreeModel.java, 689
- treeModel/Variable.java, 691
- TreeModelEvent 类，693
- TreeModelListener 接口，685
  - treeNodesInserted、treeStructureChanged 方法，685, 693
- TreeNode 接口，654, 664
  - children、getChildXx 方法，671
  - getAllowsChildren 方法，662
  - getParent 方法，671, 673
  - isLeaf 方法，661–662
- TreePath 类，665
  - getLastPathComponent 方法，665, 671
- treeRenderer/ClassNameTreeCellRenderer.java, 683
- treeRender/ClassTreeFrame.java, 679
- 树（Swing），652–693
  - 向其添加监听器，677
  - 背景色，674
  - 连接线，658–659
  - 显示，654–671
  - 编辑，663–671, 686
  - 手柄，657, 659, 674
  - 类的层次结构，655
  - 索引，665
  - 无限，688




- 叶子，652, 660–662, 674, 685
- 节点，652, 662, 674, 685
- 与其他组件配对，677
- 渲染，674–676
- 滚动到新添加的节点，666, 668
- 结构，652
- 子树，657–658
- 遍历，672–673
- 更新与重新加载，666
- 用户对象，654, 665
- 视图，665–666
- 使用水平线，659
- *TreeSelectionEvent* 类
  - getPath 方法，684
  - getPaths 方法，678, 684
- *TreeSelectionListener* 接口
  - 实现，677–684
  - valueChanged 方法，677, 679, 684
- *TreeSelectionModel* 接口，677
- trim 方法（String），163, 388
- 疑难解答。参见调试
- *真实几率：风险如何影响你的日常生活*（Walsh），583
- tryLock 方法（FileChannel），135–136
- try-with-resources 语句，61, 120
  - 关闭文件，118
  - 用于数据库连接，303
  - 用于锁，135
- ts 字面量（SQL），320
- 类型边界，95, 831
- 类型定义，179
  - 匿名，181
  - 嵌套，181
- 类型参数，标注，475
- 类型使用注解，476
- TYPE_BICUBIC、TYPE_BILINEAR 字段（AffineTransformOp），764, 771
- TYPE_BYTE_GRAY 字段（BufferedImage），760–761
- TYPE_BYTE_INDEXED 字段（BufferedImage），761
- TYPE_INT_ARGB 字段（BufferedImage），756–757, 761
- TYPE_NEAREST_NEIGHBOR 字段（AffineTransformOp），764, 771
- *TypeElement* 接口，485–486
- 类型。参见数据类型
- 类型安全枚举，102–103

## U

- \\u，在正则表达式中，138
- UDP（用户数据报协议），232
- UIManager 类，640
- Unicode 标准，43
  - 与输入/输出流，56
  - 与本地代码，820
  - 字符顺序，402
  - 转换为二进制数据，68
  - 在属性文件中，419
  - 在正则表达式中，141
  - 规范化形式，403
  - 用于所有字符串，379
- 度量单位，158
- UNIX 操作系统
  - 身份验证，566–567
  - 以句点开头的文件名，552
  - 换行符，69, 414
  - 路径，109
  - 指定区域设置，384
- UnixLoginModule 类，568
- UnixNumericGroupPrincipal 类，568
- UnixPrincipal 类，567–568
  - getName 方法，567
- UnknownHostException，231
- unordered 方法（BaseStream），50, 53
- 未解析的外部实体，176
- unread 方法（PushbackInputStream），67
- UnsatisfiedLinkError，811
- until 方法（LocalDate），359, 362
- update 方法
  - Cipher 的，601, 603, 606–607
  - MessageDigest 的，585–586
- UPDATE 语句（SQL），292, 312, 325
  - 执行，300–301, 317
  - 在批量更新中，346
  - 截断，305
  - 与 ResultSet 的方法对比，327
- updateObject 方法（ResultSet），302
- updateXxx 方法（ResultSet），326, 329
- URI 类，271
  - getXxx 方法，253
  - 不可用于访问资源，252
- uri 方法（HttpRequest.Builder），271–273, 277
- URI（统一资源标识符），252
  - 绝对与相对，252–253
  - 基础，253
  - 层次结构，252
  - 命名空间，193–196
  - 不透明与非不透明，252
  - 协议（scheme），252
  - 与 HTTP，271
- URISyntax 类，802
- URL 类（java.lang.Object），251–253, 271, 794
  - 接受的协议，252
  - openConnection 方法，254, 259
  - openStream 方法，251, 259
- URLClassLoader 类
  - addURL、getURLs 方法，532
  - 构造器，541
  - loadClass 方法，532
- URLConnection 类，251, 254–261, 271
  - connect 方法，254, 256, 260
  - getConnectTimeout 方法，260
  - getContent 方法，261
  - getContentEncoding、getContentType 方法，254, 257, 261, 266
  - getContentLength 方法，254, 257, 260
  - getDate、getExpiration、getLastModified 方法，254, 257, 261
  - getDoInput、getDoOutput 方法，259
  - getHeaderField、getHeaderFields 方法，254–256, 260
  - getIfModifiedSince 方法，260
  - getInputStream 方法，254, 261, 264, 266
  - getOutputStream 方法，254, 261, 264
  - getReadTimeout 方法，260
  - getRequestProperty 方法，260
  - setAllowUserInteraction 方法，254
  - setConnectTimeout 方法，254, 260
  - setDoInput 方法，254–255, 259
  - setDoOutput 方法，254–255, 259, 264, 266
  - setIfModifiedSince 方法，254–255, 260
  - setReadTimeout 方法，254, 260
  - setRequestProperty 方法，254–255, 260
  - setUseCaches 方法，254
- URLConnection/URLConnectionTest.java，257
- URLDecoder 类
  - decode 方法，270
- URLEncoder 类
  - encode 方法，270
- URL（统一资源定位符），252
  - 附加参数，263
  - 连接，251
  - 编码，263
  - 用于数据库，294
  - 用于本地文件，553
  - 用于命名空间标识符，194
  - 重定向，266–267
  - 相对与绝对，599
  - 用于 DTD，171
- URN（统一资源名称），252
- 美国信纸，775
- useLocale 方法（Scanner），385, 389
- 用户坐标，727
- 用户对象，654, 665
- User-Agent 请求参数，267
- 用户
  - 身份验证，566–582
  - 权限，569
  - 偏好，135
- uses 关键字，523–524
- UTC（协调世界时），367
- UTF-8 标准，75–77, 78
  - 用于文本文件，414–415
  - 修改版，78–80, 416, 819–822
- UTF-16 标准，43, 68, 76, 78
  - 与本地代码，819
  - 在正则表达式中，138

## V

- V（void）类型，代码，831
- \\v、\\w，在正则表达式中，139
- 验证，169–188
  - 激活，176
  - 添加到类，100
- value 方法（MathEvaluationResult），191, 193
- valueChanged 方法（TreeSelectionListener），677, 679, 684
- valueForPathChanged 方法（TreeModel），686, 693
- value-of 元素（XSLT），219
- valueOf 方法（旧版日期/时间类），377
- VARCHAR 数据类型（SQL），293, 348
- Variable 类，514, 686
  - toString 方法，687
- 变量句柄，514
- VariableElement 接口，485
- 变量
  - 标注，464, 476
  - 绑定，442
  - 字段，687
  - 初始化，542
  - 作用域，443
- 变体，在区域设置中，381, 418
- 供应商名称，读取器，746
- verifier/VerifierTest.java，545
- 验证器，541–545
- 版本号，读取器，746
- 版本控制，103–106
- view/ViewDB.java，336
- visitFile、visitFileFailed 方法
  - FileVisitor 的，121
  - SimpleFileVisitor 的，121, 123
- 可视化表示，286

## W

- \\w、W，在正则表达式中，139
- walk 方法（Files），118
- walkFileTree 方法（Files），121–123
- warning 方法（ErrorHandler），177–178
- 警告
  - 在 SQL 中，304
  - 抑制，480
- WBMP 格式，745
- WeakReference 对象，688
- Web 应用程序，连接管理，349–351
- Web 容器，480
- 网络爬虫，198
  - 使用 SAX 解析器，199
  - 使用 STAX 解析器，203
- 网页
  - 动态，457–463
  - 为小程序分离类加载器，534
- WebRowSet 接口，330
- 周末，360
- WHERE 语句（SQL），291
- 空白
  - 解析时忽略，163
  - 在电子邮件 URI 中，263
  - 在正则表达式中，139, 141
- 通配符，类型使用注解，476
- 王尔德，奥斯卡，380
- win32reg/Win32RegKey.c，862
- win32reg/Win32RegKey.java，860
- win32reg/Win32RegKeyTest.java，870
- Win32RegKey 类，856, 859
  - get/setValue 方法，857–858
  - names 方法，857
- Win32RegKeyNameEnumeration 类，858–859
- Windows 操作系统
  - 启用 telnet，228
  - 身份验证，566, 569
  - 字符编码，413
  - 类路径，294
  - 编译调用 API，854
  - 动态链接，850
  - glob 语法，121
  - 换行符，69, 414
  - 路径，64, 109
  - 权限，558
  - 注册表，从本地代码访问，855–871
  - 资源，417
  - 使用 Microsoft 编译器，813–814
- Windows 外观，树，658
- with 方法（Temporal），364–365
- withLocale 方法（DateTimeFormatter），372, 376, 401
- withXxx 方法
  - LocalDate 的，362
  - LocalTime 的，366
  - Period 的，363
  - ZonedDateTime 的，370
- WordCheckPermission 类，560–566
- 单词，在正则表达式中，139
- 工作目录，64
- wrap 方法（ByteBuffer），132–133
- WritableByteChannel 接口，245
- WritableRaster 类，756
  - setDataElements 方法，759, 762
  - setPixel、setPixels 方法，756, 762
- write 方法
  - CipherOutputStream 的，608
  - Files 的，113
  - ImageIO 的，745, 753
  - ImageWriter 的，748, 755
  - OutputStream 的，57, 59
- write/XMLWriteTest.java，211
- writeAttribute 方法（XMLStreamWriter），210, 214
- writeBoolean 方法（DataOutput），78, 80
- writeByte 方法（DataOutput），78, 80
- writeDTD 方法（XMLStreamWriter），215
- writeChar 方法（DataOutput），78–80
- writeCharacters 方法（XMLStreamWriter），210, 215





- writeChars 方法（DataOutput），78, 80
- writeComment 方法（XMLStreamWriter），215
- writeDouble 方法（DataOutput），78, 80, 89, 101
- writeDTD 方法（XMLStreamWriter），215
- writeEmptyElement 方法（XMLStreamWriter），211, 214
- writeEndXxx 方法（XMLStreamWriter），210, 214
- writeExternal 方法（Externalizable），101–102
- writeFixedString 方法（DataOutput），81–82
- writeFloat 方法（DataOutput），78, 80
- writeInsert 方法（ImageWriter），748, 755
- writeInt 方法（DataOutput），78, 80–81, 89
- writeLong 方法（DataOutput），78, 80
- writeObject 方法
  - Date 的，101
  - ObjectOutputStream 的，88, 93, 100
- Writer 类，56, 60–61
  - write 方法，59
- writeShort 方法（DataOutput），78, 80
- writeStartXxx 方法（XMLStreamWriter），210, 214
- writeUTF 方法（DataOutput），78, 80

## X

- X.509 格式，590
- X，正则表达式中，138
- XHTML（可扩展超文本标记语言），156, 198
- XML（可扩展标记语言）
  - 该标准的注释版，155
  - 大小写敏感性，156
  - 其中的结束标签和空标签，156
  - 其中的层次结构，154–155
  - 在数据库中，349
  - 其中的命名空间，193–196
  - 与 HTML 的比较，155
- XML 绑定，513–514
- XML 目录，172
- XML 文档
  - 其中的 DTD，156, 171–179
  - 格式，155
  - 生成，206–216
    - 从非 XML 遗留数据生成，221
    - 从中生成 HTML 文件，216–219
    - 从中生成纯文本，219–221
    - 使用 StAX，210–215
  - 在其中定位信息，188–193
  - 格式错误，211
  - 解析，159–169
  - 结构，156–160, 170
  - 验证，169–188
  - 带/不带命名空间，206–207
- XML Schema，170, 179–182, 194
  - 其中的属性，181
  - 使用其解析，182
  - 在 XML 文档中引用，179
  - 其中的重复元素，181
  - 其中的类型定义，179, 181
- XMLInputFactory 类
  - createXMLStreamReader 方法，205
  - newInstance 方法，204
  - setProperty 方法，203–204
- xmlns 属性（XSLT），195
- XMLOutputFactory 类
  - createXMLStreamWriter 方法，210, 214
  - newInstance 方法，210, 214
- XMLReader 接口
  - 实现，220
  - parse 方法，226
  - setContentHandler 方法，226
- XMLStreamReader 接口
  - getAttributeXxx 方法，203, 206
  - getName、getLocalName 方法，206
  - getText 方法，206
  - hasNext、next 方法，205
  - isXxx 方法，205
- XMLStreamWriter 接口
  - close 方法，215
  - 不是 AutoCloseable，211
  - setDefaultNamespace、setPrefix 方法，214
  - writeAttribute 方法，210, 214
  - writeCData 方法，210, 215
  - writeCharacters 方法，210, 215
  - writeComment 方法，215
  - writeDTD 方法，215
  - writeEmptyElement 方法，211, 214
  - writeEndXxx 方法，210, 214
  - writeStartXxx 方法，210, 214
- XOR 组合规则，737
- XPath（XML 路径语言），188–193
  - 其中的元素/属性，189
  - 在其中求值表达式，190–193
- XPath 接口
  - evaluate、evaluateExpression 方法，190, 193
- xpath/XPathTest.java，191
- XPathEvaluationResult 接口
  - type 方法，193
  - value 方法，191, 193
- XPathFactory 类
  - newInstance 方法，190, 193
  - newXPath 方法，193
- XPathNodes 类，190
- xs:、xsd: 前缀（XML Schema），180
- xsd:attribute 元素（XML Schema），181
- xsd:choice 元素（XML Schema），181
- xsd:complexType 元素（XML Schema），180
- xsd:element 元素（XML Schema），180
- xsd:enumeration 元素（XML Schema），180
- xsd:schema 元素（XML Schema），182
- xsd:sequence 元素（XML Schema），181
- xsd:simpleType 元素（XML Schema），180
- xsl:apply-templates 元素（XSLT），218
- xsl:output 元素（XSLT），218
- xsl:template 元素（XSLT），218
- xsl:value-of 元素（XSLT），219
- XSLT（可扩展样式表语言转换），208, 216–226
  - 在其中复制属性值，219
  - 其中的模板，218
- XSLT 处理器，216

## Y

- Year、YearMonth 类，360

## Z

- Z（boolean），类型代码，95, 831
- \Z，正则表达式中的 Z，140
- ZIP 归档，85–88
  - 用于 JMOD 文件，52
  - 读取，85
  - 数量，66
  - 写入，85
- Zip code 查询，264
- ZipEntry 类的方法，87
- ZipFile 类的方法，88
- ZipInputStream 类，59, 85
  - closeEntry、getNextEntry 方法，85–86
  - 构造函数，86
  - read 方法，85
- ZipOutputStream 类，59, 85
  - closeEntry 方法，85, 87
  - 构造函数，86
  - putNextEntry 方法，85–86
  - setLevel、setMethod 方法，87
- ZonedDateTime 类，367–371
  - from 方法，376–377
  - getXxx 方法，370–371
  - isAfter、isBefore 方法，371
  - 遗留类及，376–377
  - minus、minusXxx 方法，370
  - now 方法，370
  - of、ofInstant 方法，367, 370
  - parse 方法，376, 395, 401
  - plus、plusXxx 方法，370
  - toInstant 方法，367, 371
  - toLocalXxx 方法，371
  - withXxx 方法，370
- zonetimes/ZonedTimes.java，369
- ZoneId 类，377
  - getAvailableZoneIds、of 方法，367

# 致谢

- 封面图片：Chromakey/Shutterstock
- 第 3 章：“可扩展标记语言（XML）已经取代 Java、设计模式和对象技术，成为软件行业解决世界饥饿问题的方案。” Box, D., Skonnard, A., & Lam, J. (2000). Essential XML: Beyond Markup. Boston, Mass: Addison-Wesley.
- 第 3 章，图 3.3：Mozilla Firefox 的屏幕截图 © Mozilla Foundation
- 第 4 章，图 4.1、4.3、4.4、4.5：Microsoft Windows 的屏幕截图 © Microsoft 2018
- 第 4 章，图 4.6：Java 的屏幕截图 © Oracle
- 第 4 章，图 4.7：HTML 表单的屏幕截图 © 2018 USPS
- 第 4 章，图 4.9：Mozilla Firefox 的屏幕截图 © Mozilla Foundation
- 第 5 章，图 5.3、5.4：Ubuntu 的屏幕截图 © 2018 Canonical Ltd. Ubuntu 和 Canonical 是 Canonical Ltd. 的注册商标。
- 第 5 章，图 5.6：Java 的屏幕截图 © Oracle
- 第 7 章：“我们确实拥有一切……当然，除了语言。”奥斯卡·王尔德
- 第 7 章，图 7.1、7.2、7.3、7.4、7.5、7.6：Java 的屏幕截图 © Oracle
- 第 8 章，图 8.2：Mozilla Firefox 的屏幕截图 © Mozilla Foundation
- 第 9 章，图 9.2：Eclipse 的屏幕截图 © Eclipse Foundation, Inc.
- 第 10 章，图 10.3、10.7、10.8、10.12：Java 的屏幕截图 © Oracle
- 第 10 章，图 10.4：十六进制编辑器的屏幕截图 © Jaka Mocnik 和 Chema Celorio
- 第 11 章，图 11.1、11.2、11.3、11.4、11.5、11.7、11.8、11.9、11.10、11.14、11.15、11.16、11.17、11.18、11.19、11.20、11.21、11.22、11.23、11.24、11.25、11.26、11.28、11.29、11.30、11.39、11.44、11.54、11.55、11.56、11.60、11.62：Java 的屏幕截图 © Oracle
- 第 11 章，图 11.51：Shao-Chun Wang/123RF
- 第 11 章，图 11.57：Luca Trovato/The Image Bank/Getty Images
- 第 11 章：各种行星的图像由 Jim Evins 提供
- 第 12 章，图 12.4：注册表编辑器的屏幕截图 © Microsoft 2018

*本页有意留空*

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_958_0.png)

# 在 informit.com/register **注册您的产品**

获取额外权益，并在下次购买时**节省 35%**

- 自动获得一张下次购买可享 35% 折扣的优惠券，有效期为 30 天。请在您的 InformIT 购物车或账户页面的“管理代码”部分查找您的代码。
- 下载可用的产品更新。
- 访问可用的附加材料。*
- 勾选该复选框，以便接收我们的消息，并获取关于新版本和相关产品的专属优惠。

*注册权益因产品而异。权益将列在您账户页面的“已注册产品”下。

# InformIT.com——值得信赖的技术学习资源

InformIT 是培生（Pearson）旗下信息技术品牌的在线家园，培生是全球领先的教育公司。在 InformIT.com，您可以：

- 选购我们的图书、电子书、软件和视频培训
- 享受我们的特别优惠和促销活动（informit.com/promotions）
- 订阅特别优惠和内容简报（informit.com/newsletters）
- 访问数千个免费章节和视频课程


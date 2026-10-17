
`import java.lang._`

`import scala._`

`import Predef._`

第一个是将 Java 的所有标准类引入作用域。它导入了基础的 `scala` 包，然后是 `scala.Predef` 对象的所有内容。你可以通过查看 API 来查看 Scala 包的完整结构。

# 使用 Scala 进行编程和问题解决简介

## 9.3 从文件读取

现在是时候实际使用 `scala.io.Source` 来帮助我们从标准输入以外的源读取信息了。使用 Java 库还有其他方法从硬盘读取文件，但目前我们将使用 `Source`，因为它为我们提供了足够的能力，并与我们已经讨论过的 Scala 集合相匹配。本节中的任何代码都假设你已经导入了 `scala.io.Source`，这样我们可以直接引用为 `Source`。

有一个 `Source` 对象，它拥有我们可以调用的方法来获取 `Source` 类型实例，我们将使用这些实例进行读取。读取文件简单的方法是使用 `Source` 对象的 `fromFile` 方法。

```scala
val fileSource = Source.fromFile("sampleFile.txt")
fileSource: scala.io.BufferedSource = non-empty iterator
```

`BufferedSource` 只是一个迭代器的原因并不难理解。记住，读取文件是非常缓慢的。你应该只读取一次，并在那时获取你需要的信息。反复读取是低效的。为了迫自己提高效率，你必须显式地重置文件或重新打开它进行迭代。此外，文件可能非常大。迭代器的优势在于，它只需要在内存中保留当前内容，而不是整个文件。相比之下，`Array` 和 `List` 需要为它们存储的所有内容使用内存。

对于 `List` 和 `Array` 类型，你是参数化的。你可以创建一个 `List[Int]` 或 `List[String]`。`Iterator` 也是如此。`Source` 和 `BufferedSource` 类型通常是 `Iterator[Char]`。这意味着它们对单个字符操作。上面的对 `next` 的调用说明了这一点。此外，如果你调用 `map` 或 `filter` 等函数，或者将 `Iterator` 转换为 `List` 或 `Array`，结果将是一组字符。我们在这里可以显式地看到这一点。

```scala
scala val newSource = fileSource.reset
newSource: scala.io.Source = non-empty iterator
```

```scala
scala newSource.next
res3: Char = T
```

```scala
scala newSource.toList
res4: List[Char]
```

```scala
List(h, i, s, i, a, s, a, m, p, l, e, t, t, e, x, t, f, i, l, e, t, h, r, a, l, h, a, v, e, r, i, t, e, n, t, o, u, s, e, f, o, r, t, h, r, e, f, i, l, s, r, e, a, l, y, i, s, n, o, t, a, 1, l, 1, c, a, p, t, e, r, t, h, a, t, h, m, u, c, h, o, t, h, i, s, f, i, l, e, a, l, 1, r, a, t, e, h, o, w, w, e, c, a, 1, y, s, u, p, p, o, s, e, d, t, o, b, e, u, e, d, t, o, i, l, l, s, t, r, a, a, n, d, r, o, m, f, i, i, l, e, s)
```

注意字符 'T' 是[在那儿]（there）的，因为它已经被对 `next` 的调用消耗了。将 `Iterator` 转换为 `Array` 或 `List` 只会获取尚未迭代过的元素。在此过程中它也会消耗该 `Iterator`。

```scala
scala newSource
res5: scala.io.Source = empty iterator
```

虽然你想要的所有数据都是字符形式，但用这种格式完成你真正想做的事情可能有点困难。由于原因，有一个 `getLines[String]` 方法会给你一个不同的迭代器。这个新迭代器的类型是 `Iterator[String]`，每个元素都是文件中的完整行，且末尾没有换行符。

```scala
scala val lines = fileSource.reset.getLines
lines: Iterator[String] = non-empty iterator
```

```scala
scala lines.next
res6: String = This is a sample file that I have written to use for the files chapter.
```

### 9.3.2 String split 方法

行并不总是有用到你可以将字符串拆分成每行的不同部分。因此，对于大多数用途，这些方法中最简单是 `split` 方法，它在 6.7.1 节中引入。`split` 方法接受单个参数，即一个 `String`，它应该是你拆分部分之间的分隔符。它将返回一个 `Array[String]`，包含所有被分隔符隔开的内容。这是一个简单的示例。

```scala
scala="This is a test.".split(" ")
res7: Array[String] = Array(This, is, a, test.)
```

字符串 "This is a test," 使用单个空格作为分隔符进行拆分。结果将字符串中的每个单词作为单独的元素。

从技术上讲，`split` 的参数是一个**正则表达式**（REGULAR EXPRESSION）。我们不会在书中详细介绍正则表达式的细节。它们在《面向对象、抽象与数据结构 Scala》中会有介绍。此时这里有几点值得提到。正则表达式可以包含多个字符。字符 `*` 和 `+` 有特殊含义。`+` 表示它前面的字符可以出现一次或多次。在这里提到这一点是值得的，因为输入内容在单词之间可能存在多个空格这并不罕见。为了处理这种情况，你经常会在调用 `split` 时使用 `"+"` 而不仅仅是空格。

现在我们想让 `split` 方法采取行动，并具备逐行读取的能力。我们想做的是从二维结构中创建数值数据。在这种情况下，我们将创建一个二维 `Array`，其直接访问能力对于我们想要在此使用的大多数应用程序都是很有用的。我们将通过两种方式来实现。我们将此拆分为两个函数。第一个函数将处理任何 `Iterator[String]` 并返回我们需要的 `Array[Double]`。`Iterator[String]` 很有帮助，因为 `getLines` 很有用。

```scala
def dataGrid(lines: Iterator[String], delim: String): Array[Double] = {
  for (l <- lines; if !l.trim.isEmpty) yield {
    for (n <- l.split(delim); if !n.trim.isEmpty) yield n.trim.toDouble
  }
}.toArray
```

### 9.3.3 从其他内容读取

`scala.io.Source` 对象的一个特点是，它不仅仅有用于我们读取文件的 `fromFile` 方法。事实上，有许多以 `scala.io.Source` 开头的不同方法。我们只考虑其中一个，尽管你完全可以查看 API 获取其他的。你可能会发现最有趣的是 `fromURL(s:String)` 方法。URL 代表统一资源定位符（Uniform Resource Locator），它们是你输入到网络浏览器地址栏中的内容。你调用此方法时传递一个 URL 作为 `String`，非常就像你在浏览器中输入的内容一样。

这使得程序从网络上读取信息变得异常简单。例如，执行以下行将把你的网页内容作为一个 `String` 给你。

```scala
Source.fromURL("http://cs.trinity.edu/mlewis/").mkString
```

你可以对这个 `Source` 做任何你对文件 `Source` 所做的事。和文件一样，这个 `Source` 是一个迭代器，你只能通过调用来读取它

重置。这也有道理，因为在现代计算机上，没有比从硬盘读取更慢了，那就是从网络读取信息。

### 9.3.4 其他选项（基于 Java）

使用 `scala.io.Source` 的优势在于你可以获得一个 Scala 迭代器（Iterator），它拥有你习惯用于 `List` 和 `Array` 类型时的所有方法。然而，这并不意味着 `Source` 是你的最佳选择。在某些情况下，可能会发现 `java.util.Scanner` 类更好。

`java.util.Scanner` 有读取特定类型数据的方法，以及检查是否有特定类型数据可用。以下是 `java.util.Scanner` 中可用方法的示例：

- `hasNextNext():Boolean` - 检查是否有另一个“单词”。
- `hasNextDouble():Boolean` - 检查是否有 `Double` 类型可以读取。
- `hasNextInt():Boolean` - 检查是否有 `Int` 类型可以读取。
- `hasNextLine():Boolean` - 检查是否有一行文本可以读取。
- `next():String` - 读取下一个“单词”。
- `nextDouble():Double` - 读取下一个 `Double`。
- `nextInt():Int` - 读取下一个 `Int`。
- `nextLine():String` - 读取下一行文本。
- `useDelimiter(pattern:String)` - 更改用于分隔符的模式。

这个列表非常自显其意。人们可能唯一疑惑的是为什么“单词”要加引号。这个原因反映在列出的最后一个方法中。当你用 `Scanner` 读取一个“单词”时，它将读取到下一个分隔符，无论是什么。默认情况下，它是任何空白字符组合。

为了使用 `Scanner`，你必须先创建一个。为了做到，你可能需要导入 `java.util.Scanner` 并使用以下表达式：

```scala
new Scanner(file)
```

文件需要是一个类型为 `java.io.File` 的表达式，我们将通过另一个 `new` 表达式创建它。将这些结合在一起，如果你有一个用空格分隔的整数文件，可以在程序中放入这样的代码来读取并打印一组 `Int`。请注意，这在我们名为 "numbers.txt" 的文件上不起作用，因为有逗号，而且该文件中的值是 `Double`。

```scala
import java.util.Scanner
import java.io.File
```

```scala
val sc = new Scanner(new File("numbers.txt"))
while (sc.hasNextInt()) {
  println(sc.nextInt())
}
sc.close()
```

在这里选择打印的原因是 `Scanner` 无法很好地产生 Scala 集合。你可以将值放入集合中，但通常需要更多精力，例如你可以将它们放入一个 `Var List`。当你完成 `Scanner` 使用后，也应该关闭它们。如果它们链接到文件，它们正持有宝贵的资源。

## 9.4 写入文件

Scala 自己的库没有提供任何写入文件的功能。这是 Java 已经支持的功能，添加 Scala 库并没有认为是一个显著优势。在 Java 中有很多方法设置写入文件。最简单的方法（我们将使用的方法）是 `java.io.PrintWriter`。我们可以通过 `new` 创建一个新的 `PrintWriter` 并告诉它我们想要写入的文件名。这样我们就可以通过这段代码获取一个用于输出的 `PrintWriter`。

```scala
import java.io.PrintWriter
val pw = new PrintWriter("output.txt")
```

现在我们可以调用 `pw`，这将导致内容写入该文件。你可以使用 `print` 和 `println` 方法打印，就像你在 Scala 中使用这些函数打印标准输出一样。

使用这种方法，我们可以编写代码打印 100 个 x 和 y 值在 0 到 1 之间的随机点。

```scala
for (i <- 1 to 100) {
  pw.println(math.random() + " " + math.random())
}
pw.close()
```

最后一行是至关重要的，因为 `PrintWriter` 像 `BufferedSource` 一样在内存中持有内容。如果你不关闭文件，内容就不会写入磁盘。如果你不想立即关闭文件，可以使用 `flush` 方法。

`flush`

当你调用此方法时，缓冲区中的内容就会被写入。

### 9.4.1 追加到文件

创建 `PrintWriter` 的如上述方法有一个副作用，它会创建一个新文件或删除现有文件并覆盖。如果你有一个现有文件并想在末尾追加内容，还需要多一个步骤。与其简单地告诉 `PrintWriter` 文件名，不如告诉它一个 `FileWriter` 和一个布尔值。如果该值为 `true`，现有文件内容将留在原地，任何写入的内容将到文件末尾。如果是 `false`，它的行为就像我们之前一样。所以如果你想追加到 `output.txt` 文件，可以这样做：

```scala
import java.io.FileWriter,PrintWriter
var pw = new PrintWriter(new FileWriter("output.txt",true));
```

## printf 和 format

如果你有一个对输出格式有要求的应用程序，有一些你应该了解的额外函数/方法。这些是用于打印屏幕的 `printf` 函数和 `String` 上的 `format` 方法。这两个方法为你提供了一种编码你想要打印内容的方式，使用 C 编程语言默认的格式样式。

关于格式的完整描述超出了本书的范围，可以在 Java API 的 `java.util.Formatter` 中找到。你可以通过网络搜索或访问 java.oracle.com 网站找到 Java API。在本书期间，Java 8 是当前版本。你可能需要查看 Java 8 版本的 API 或任何可用的新版本。这里提供一个简要介绍。

让我们从创建几个变量并使用我们习惯的 API 打印它们开始。

```scala
scala val g = 6.67e-11
```

```scala
scala val name = "Mark"
```

```scala
scala val classSize = 20
```

```scala
scala println(g+" "+classSize)
```

# 文件

其类型为 `Array[String]`。我们可以像处理任何其他数组一样获取该数组的值。你可以引用 `args(0)` 来获取文件名后的第一个参数，通过 `args(1)` 获取第二个参数，依此类推。一个说明参数用法的简单示例是一个将两个参数转换为 `Double` 并将它们相加的脚本。

```scala
```

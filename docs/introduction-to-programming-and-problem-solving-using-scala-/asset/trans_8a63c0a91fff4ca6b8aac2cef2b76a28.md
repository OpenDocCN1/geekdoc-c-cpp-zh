
重置。这也有道理，因为在现代计算机上，没有比从硬盘读取更慢了，那就是从网络读取信息。

## 9.3.4 其他选项（基于 Java）

使用 `scala.io.Source` 的优势在于你可以获得一个 Scala 迭代器（Iterator），它拥有你习惯用于 `List` 和 `Array` 类型时的所有方法。然而，这并不意味着 `Source` 是你的最佳选择。在某些情况下，可能会发现 `java.util.Scanner` 类更好。

`java.util.Scanner` 有读取特定类型数据的方法，以及检查是否有特定类型数据可用。以下是 `java.util.Scanner` 中可用方法的示例：

- *hasNextNext():Boolean* - 检查是否有另一个“单词”。
- *hasNextDouble():Boolean* - 检查是否有 `Double` 类型可以读取。
- *hasNextInt():Boolean* - 检查是否有 `Int` 类型可以读取。
 * *hasNextLine():Boolean* - 检查是否有一行文本可以读取。
- *next():String* - 读取下一个“单词”。
- *nextDouble():Double* - 读取下一个 `Double`。
- *nextInt():Int* - 读取下一个 `Int`。
- *nextLine():String* - 读取下一行文本。
- *useDelimiter(pattern:String)* - 更改用于分隔符的模式。

这个列表非常自显其意。人们可能唯一疑惑的是为什么“单词”要加引号。这个原因反映在列出的最后一个方法中。当你用 `Scanner` 读取一个“单词”时，它将读取到下一个分隔符，无论是什么。默认情况下，它是任何空白字符组合。

为了使用 `Scanner`，你必须先创建一个。为了做到，你可能需要导入 `java.util.Scanner` 并使用以下表达式：

```
new Scanner(file)
```

文件需要是一个类型为 `java.io.File` 的表达式，我们将通过另一个 `new` 表达式创建它。将这些结合在一起，如果你有一个用空格分隔的整数文件，可以在程序中放入这样的代码来读取并打印一组 `Int`。请注意，这在我们名为 "numbers.txt" 的文件上不起作用，因为有逗号，而且该文件中的值是 `Double`。

```
import java.util.Scanner
import java.io.File
```

```
val sc = new Scanner(new File("numbers.txt"))
while (sc.hasNextInt()) {
  println(sc.nextInt())
}
sc.close()
```

# 使用 Scala 进行编程和解决问题的简介

在这里选择打印的原因是 `Scanner` 无法很好地产生 Scala 集合。你可以将值放入集合中，但通常需要更多精力，例如你可以将它们放入一个 `Var List`。当你完成 `Scanner` 使用后，也应该关闭它们。如果它们链接到文件，它们正持有宝贵的资源。

## 9.4 写入文件

Scala 自己的库没有提供任何写入文件的功能。这是 Java 已经支持的功能，添加 Scala 库并没有认为是一个显著优势。在 Java 中有很多方法设置写入文件。最简单的方法（我们将使用的方法）是 `java.io.PrintWriter`。我们可以通过 `new` 创建一个新的 `PrintWriter` 并告诉它我们想要写入的文件名。这样我们就可以通过这段代码获取一个用于输出的 `PrintWriter`。

```
import java.io.PrintWriter
val pw = new PrintWriter("output.txt")
```

现在我们可以调用 `pw`，这将导致内容写入该文件。你可以使用 `print` 和 `println` 方法打印，就像你在 Scala 中使用这些函数打印标准输出一样。

使用这种方法，我们可以编写代码打印 100 个 x 和 y 值在 0 到 1 之间的随机点。

```
for (i <- 1 to 100) {
  pw.println(math.random() + " " + math.random())
}
pw.close()
```

最后一行是至关重要的，因为 `PrintWriter` 像 `BufferedSource` 一样在内存中持有内容。如果你不关闭文件，内容就不会写入磁盘。如果你不想立即关闭文件，可以使用 `flush` 方法。

flush

当你调用此方法时，缓冲区中的内容就会被写入。

## 9.4.1 追加到文件

创建 `PrintWriter` 的如上述方法有一个副作用，它会创建一个新文件或删除现有文件并覆盖。如果你有一个现有文件并想在末尾追加内容，还需要多一个步骤。与其简单地告诉 `PrintWriter` 文件名，不如告诉它一个 `FileWriter` 和一个布尔值。如果该值为 `true`，现有文件内容将留在原地，任何写入的内容将到文件末尾。如果是 `false`，它的行为就像我们之前一样。所以如果你想追加到 `output.txt` 文件，可以这样做：

```
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

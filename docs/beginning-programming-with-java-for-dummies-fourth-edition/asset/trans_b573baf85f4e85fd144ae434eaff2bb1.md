
Listing 13-3 中的内容并不是一个完整的程序。相反，它是一个代码模板——一段半成品的代码，留有空格供你填写。

使用 Listing 13-3 中的模板，你可以从磁盘文件输入数据。使用类似的模板，你可以向文件写入输出。该模板在 Listing 13-4 中。

## Listing 13-4：写入磁盘文件的数据模板

```
/*
 * Before Eclipse can compile this code,
 * you must fill in the blanks.
 */
import java.io.File;
import java.io.FileNotFoundException;
import java.io.PrintStream;

class ________ {
    public static void main(String args[])
        throws FileNotFoundException {
        PrintStream diskWriter =
            new PrintStream("________");
        diskWriter.print(_____);
        diskWriter.println(_____);
        // Etc.
        diskWriter.close();
    }
}
```

要使用 Listing 13-4，请将你的类名插入到第一个空白处。在引号之间的空格中输入输出文件的名称。然后，要将一行的部分内容写入输出文件，请调用 diskWriter.print。要将一行的剩余部分写入输出文件，请调用 diskWriter.println。

![](img/6d9dcff12e52b997f3ad31445b712549_274_0.png)

Eclipse 具有内置的功能来创建和插入代码模板。要开始使用 Eclipse 模板，请选择 Window→Preferences（在 Windows 中）或 Eclipse→Preferences（在 Mac 上）。在 resulting 的 Preferences 对话框中，选择 Java→Editor→Templates。创建新模板并不简单。但如果你稍微探索一下，就能完成很多工作。

如果你的程序从一个磁盘文件获取输入并向另一个文件写入输出，请将 Listings 13-3 和 13-4 的内容结合起来。这样做时，你会得到一个像 Listing 13-2 那样的程序。

## 快速浏览 Java 的磁盘访问设施

Listings 13-3 和 13-4 中的模板非常不错。但了解模板的工作原理会更好。以下是描述 Java 磁盘访问代码内部工作原理的几个要点。

在 Listing 13-2 中，添加的单词 `throws FileNotFoundException` 构成了一个 throws 子句。throws 子句是一种免责声明。在代码中放置 throws 子句就像在说，“我意识到这段代码可能会遇到麻烦。”

**PrintStream 是可用于写入输出的东西。**

`PrintStream` 类似于 `Scanner`。两者最大的区别是 `Scanner` 用于读取输入，而 `PrintStream` 用于写入输出。要了解我的意思，请查看 Listing 13-2。注意使用 `Scanner` 的语句与使用 `PrintStream` 的语句之间的相似性。

单词 `PrintStream` 在 Java API 中定义。

**在 Listing 13-2 中，表达式 `new File("rawData.txt")` 扮演的角色与许多其他程序中 `System.in` 扮演的角色相同。**

正如 `System.in` 代表计算机的键盘，表达式 `new File("rawData.txt")` 代表你计算机硬盘上的一个文件。当计算机调用 `new File("rawData.txt")` 时，计算机创建了类似 `System.in` 的东西——你可以将其塞进 `new Scanner()` 括号中的东西。

单词 `File` 在 Java API 中定义。

当然，在法律领域，你通常别无选择，只能签署免责声明。“如果你不签署此免责声明，外科医生就不会为你手术。”好吧，那我就签它。Java throws 子句也是如此。如果你将诸如 `new PrintStream("cookedData.txt")` 之类的内容放入代码中，并且没有添加类似 `throws FileNotFoundException` 的内容，那么 Java 编译器就会拒绝编译你的代码。

那么在什么时候需要这个 `throws FileNotFoundException` 子句，什么时候不需要它呢？嗯，代码中存在某些内容——例如 `new PrintStream("cookedData.txt")`——会强制你创建一个 throws 子句。你可以花一些时间学习所有需要 throws 子句的类型。但在这一点上，最好集中精力于其他编程问题。作为一名初学 Java 程序员，最安全的做法是遵循 Listings 13-3 和 13-4 中的模板。

单词 `FileNotFoundException` 是……你猜对了……在 Java API 中定义。

**为了创建本章的代码，我编造了名称 `diskScanner` 和 `diskWriter`。**

单词 `diskScanner` 和 `diskWriter` 不来自 Java API。代替 `diskScanner` 和 diskWriter，你可以使用任何你想要的名称。你所要做的就是在每个 Java 程序中一致地使用这些名称。

**对 close 方法的调用结束了你的程序与文件之间的连接。**

在本书的许多示例中，你通过调用 `keyboard.close()` 来切断程序与计算机键盘之间的连接。当你为磁盘文件的 scanner 或磁盘文件的 `PrintStream` 实例调用 `close` 方法时也是如此。调用 `close` 方法提醒 Java 完成所有待处理的读或写操作，并切断程序与磁盘文件、键盘或为程序保存数据的任何其他内容的连接。

本书的示例相当简单。如果你省略了其中一个示例中的 `close` 方法调用，你可能会收到 Eclipse 的警告信息，但世界并没有结束。（也就是说，你的程序仍然能正确运行。）然而，在一个成败攸关的严肃应用程序中，`close` 调用的正确放置很重要。这些 `close` 调用可确保程序的输入和输出操作正确完成，并有助于释放磁盘资源供其他正在运行的程序使用。

## 运行示例程序

测试 Listing 13-2 中的代码是一个三步过程。以下是三个步骤的概述：

- 1. 创建 `rawData.txt` 文件。
- 2. 运行 Listing 13-2 中的代码。
- 3. 查看 `cookedData.txt` 文件的内容。

接下来的几节将详细介绍每一步。

## 创建输入文件

你可以使用任何普通的文本编辑器为 Listing 13-2 中的代码创建输入文件。在本节中，我将向你展示如何使用 Eclipse 的内置编辑器。

要创建输入文件：

- 1. 在 Eclipse 的 Package Explorer 中选择一个项目。
- 在此示例中，选择 13-02 项目（包含 Listing 13-2 代码的项目）。
- 在 Package Explorer 中，选择标签为项目名称的分支。（选择 13-02 分支以运行 Listing 13-2 中的代码。）不要选择项目内的项目。（例如，不要选择 src 分支或 (default package) 分支。）

![](img/6d9dcff12e52b997f3ad31445b712549_276_0.png)

### 2. 在 Eclipse 的主菜单中，选择 File→New→File。

Eclipse 的 New File 对话框打开。

### 3. 在 File Name 字段中，输入你的新数据文件的名称。

你可以输入计算机认为有效的任何文件名。对于本节的示例，我使用了名称 `rawData.txt`，但其他名称，例如 `rawData.dat`、`rawData` 或 `raw123.01.dataFile` 也是可以的。我尽量避免麻烦的名称（包括简短、无信息量的名称和包含空白的名称），但你选择的名称完全由你决定（以及你的计算机操作系统、老板的喜好以及客户的规格）。

### 4. 单击 Finish。

文件名称出现在 Eclipse 的 Package Explorer 中。Eclipse 的编辑器区域中会出现一个空编辑器（其选项卡上显示新文件的名称）。

### 5. 在编辑器中输入文本。

为了创建本节的示例，我输入了文本 `19.95 5`，如 Figure 13-4 所示。要创建你自己的示例，请在程序运行期间输入程序所需的任何文本。

![](img/6d9dcff12e52b997f3ad31445b712549_277_0.png)

### 图 13-4：编辑输入文件。

![](img/6d9dcff12e52b997f3ad31445b712549_277_1.png)

本节的步骤适用于你使用 Eclipse 创建输入文件的情况。你也可以使用其他程序创建输入文件，例如 Windows Notepad 或 Macintosh TextEdit。但如果你这样做，就必须注意文件格式和文件名扩展名。例如，要使用 Windows Notepad 创建名为 `raw123.01.dataFile` 的文件，请在“另存为”对话框的 File Name 字段中输入 "`raw123.01.dataFile`"（带引号）。如果你没有用引号括住名称，Notepad 可能会在文件名后添加 `.txt`（将 `raw123.01.dataFile` 变为 `raw123.01.dataFile.txt`）。类似的问题也适用于 Macintosh 的 TextEdit 程序。默认情况下，TextEdit 会为每个新文件添加 `.rtf` 扩展名。要为特定文件覆盖 `.rtf` 默认设置，请在保存文件前选择 Format→Make Plain Text。然后，当你保存文件时，TextEdit 会提供在文件名后添加 `.txt` 扩展名的选项。在“另存为”对话框中，如果你不希望文件名以 `.txt` 结尾，请取消选中标记为 If no extension is provided, use ".txt" 的复选框。

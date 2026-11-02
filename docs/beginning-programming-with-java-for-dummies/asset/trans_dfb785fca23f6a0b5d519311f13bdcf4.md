
> **对 close 方法的调用结束了程序与文件之间的连接。**
> 
> `diskWriter`，你可以使用任何你想要的名称。唯一需要做的就是在每个 Java 程序中一致地使用这些名称。本书的示例相当简单。如果你在这些示例中的一个中省略了 `close` 方法调用，你可能会从 Eclipse 得到一个警告信息，但世界并不会因此终结。（也就是说，你的程序仍然能正确运行。）然而，在一个成败攸关的严肃应用中，`close` 调用的正确放置很重要。这些 close 调用确保程序的输入和输出操作得到妥善完成，并有助于释放磁盘资源供其他正在运行的程序使用。
> 
> 在本书的许多示例中，你通过调用 `keyboard.close()` 来切断程序与计算机键盘之间的连接。当你为磁盘文件的文件扫描器或磁盘文件的 `PrintStream` 实例调用 `close` 方法时也是如此。调用 `close` 方法提醒 Java 完成所有待处理的读写操作，并切断程序与磁盘文件、键盘或程序数据的其他来源之间的连接。

## 运行示例程序

测试《清单 13-2》中的代码是一个三步过程。以下是这三步的概述：

- 1. **创建** `rawData.txt` 文件。
- 2. **运行**《清单 13-2》中的代码。
- 3. **查看** `cookedData.txt` 文件的内容。

接下来的几节将详细介绍每一步。

## 创建输入文件

你可以使用任何普通的文本编辑器为《清单 13-2》中的代码创建输入文件。在本节中，我将向你展示如何使用 Eclipse 的内置编辑器。

创建输入文件：

- 1. **在 Eclipse 的 Package Explorer 中选择一个项目。**
  
  在此示例中，选择 13-02 项目（包含《清单 13-2》代码的项目）。
  
  在 Package Explorer 中，选择标签为项目名称的分支。（选择 13-02 分支以运行《清单 13-2》中的代码。）不要选择项目内的条目。（例如，不要选择 `src` 分支或 `(default package)` 分支。）

![](img/f938eba5f15e231d828a6255e7ec5523_276_0.png)

- 2. 在 Eclipse 的主菜单中，选择 File→New→File。

Eclipse 的 New File 对话框打开。

- 3. 在 File Name 字段中，输入你的新数据文件的名称。

你可以输入计算机认为有效的任何文件名。对于本节的示例，我使用了 rawData.txt 名称，但其他名称，如 rawData.dat、rawData 或 raw123.01.dataFile 也是可以的。我尽量避免使用麻烦的名称（包括简短、无信息性的名称和包含空格的名称），但你选择的名称完全由你决定（以及你的计算机操作系统、老板的喜好以及客户的规范）。

- 4. 单击 Finish。

文件名称出现在 Eclipse 的 Package Explorer 中。Eclipse 的编辑器区域中会出现一个空编辑器（其选项卡上显示新文件的名称）。

- 5. 在编辑器中输入文本。

为了创建本节的示例，我输入了文本 19.95 5，如图 13-4 所示。要创建你自己的示例，在运行期间输入程序所需的任何文本。

### 图 13-4：编辑输入文件。

![](img/f938eba5f15e231d828a6255e7ec5523_277_0.png)

![](img/f938eba5f15e231d828a6255e7ec5523_277_1.png)

本节的步骤适用于你使用 Eclipse 创建输入文件的情况。你也可以使用其他程序创建输入文件，例如 Windows Notepad 或 Macintosh TextEdit。但如果你这样做，就必须注意文件格式和文件扩展名。例如，要使用 Windows Notepad 创建名为 raw123.01.dataFile 的文件，在 Save As 对话框的 File Name 字段中输入 "raw123.01.dataFile"（带引号）。如果你没有用引号包围名称，Notepad 可能会在文件名称后添加 .txt（将 raw123.01.dataFile 变为 raw123.01.dataFile.txt）。类似的问题也适用于 Macintosh 的 TextEdit 程序。默认情况下，TextEdit 会为每个新文件添加 .rtf 扩展名。要为特定文件覆盖 .rtf 默认设置，请在保存文件前选择 Format→Make Plain Text。然后，当你保存文件时，TextEdit 会提供在文件名称后添加 .txt 扩展名的选项。在 Save As 对话框中，如果你不希望文件名称以 .txt 结尾，请取消选中标签为 If no extension is provided, use ".txt" 的复选框。

## 运行代码

要让 Eclipse 运行代码，就像运行任何其他 Java 程序一样。选择你要运行的项目（本示例中为项目 13-02）。然后选择 Run→Run As→Java Application。

当你运行《清单 13-2》中的程序时，Eclipse 的 Console 视图中不会出现任何文本。这种完全缺乏明显输出的情况会让一些人感到不安。事实是，像《清单 13-2》中的程序这样的工作都在幕后完成。程序没有任何从键盘读取的语句，也没有任何向屏幕打印的语句。因此，如果你有一台非常吵的硬盘，在你选择 Run→Run As→Java Application 时，你可能会听到一点啁啾声，但你不会输入任何程序输入，也不会看到任何程序输出。

程序将所有输出发送到硬盘上的一个文件。那么，你如何查看文件的内容呢？

## 查看输出文件

要查看《清单 13-2》程序的输出，请按照以下步骤操作：

- 1. **在 Project Explorer 中选择 `13-02` 项目分支。**
- 2. **在主菜单中选择 File→Refresh。**
- 3. **在 Project Explorer 中展开 `13-02` 项目分支。**
  
  Package Explorer 树中（在 13-02 项目中）会出现一个名为 `cookedData.txt` 的新文件。
  
- 4. **在 Project Explorer 树中双击 `cookedData.txt` 分支。**
  
  `cookedData.txt` 的内容会出现在 Eclipse 编辑器中。（参见图 13-5。）

![](img/f938eba5f15e231d828a6255e7ec5523_278_0.png)

## 磁盘文件问题的故障排除

当你运行《清单 13-2》中的代码时，计算机执行 new Scanner(new File("rawData.txt"))。如果 Java 虚拟机找不到 rawData.txt 文件，你会看到如图 13-6 所示的消息。此错误信息可能非常令人沮丧。在许多情况下，你确信硬盘上存在 rawData.txt 文件。愚蠢的计算机就是找不到它。

### 图 13-6：计算机找不到你的文件。

![](img/f938eba5f15e231d828a6255e7ec5523_279_0.png)

没有快速、万无一失的方法来修复此问题。但你应该首先检查以下事项：

![](img/f938eba5f15e231d828a6255e7ec5523_279_1.png)

- **再次检查是否存在名为 rawData.txt 的文件。**
  打开 My Computer（Windows）或 Finder（Mac）并查找该名称的文件。
  My Computer 和 Finder 中显示的文件名可能具有误导性。你可能会看到名称 rawData，即使文件的实际名称是 rawData.txt。要永久修复此问题，请参阅第 2 章。
- **检查文件名称的拼写。**
  确保程序中的名称与硬盘上的文件名完全相同。只要有一个字母放错位置，计算机就可能找不到文件。
- **如果你使用 Linux（或除 Mac OS X 之外的其他 UNIX 变体），请检查文件名称的大小写。**
  在 Linux 和许多版本的 UNIX 中，大写和小写的区别会让计算机困惑。
- **检查文件是否在正确的目录中。**
  当然，你有一个名为 rawData.txt 的文件。但不要指望你的 Java 程序会在硬盘上的每个文件夹中查找文件。你怎么知道 rawData.txt 之类的文件应该放在哪个文件夹？

其工作原理如下。每个 Eclipse 项目在计算机硬盘上都有自己的文件夹。你在图 13-5 中看到 13-02 项目文件夹及其 src 子文件夹。但在图 13-7 中，Windows Explorer 显示了 13-02 文件夹、其 src 子文件夹以及名为 .settings 和 bin 的其他子文件夹。（Mac 用户可以在 Finder 窗口中看到相同的子文件夹。）

src、bin 和 .settings 文件夹包含自己的文件。但在图 13-7 中，rawData.txt 和 cookedData.txt 文件直接位于 13-02 项目文件夹内部。换句话说，rawData.txt 和 cookedData.txt 文件位于 13-02 项目文件夹的根目录中。

![](img/f938eba5f15e231d828a6255e7ec5523_280_0.png)

当你运行本节的示例时，rawData.txt 文件应位于硬盘上 13-02 项目文件夹的根目录中。这就是为什么在“创建输入文件”部分的步骤 1 中，我提醒你选择 13-02 项目文件夹而不是项目的 src 子文件夹。

图 13-7 显示了输入和输出文件位于其 Eclipse 项目的根目录中。但通常情况下，文件位置可能很棘手，尤其是在你从 Eclipse 切换到不熟悉的 IDE 时。关于将输入和输出文件直接放在项目目录内的通用规则可能不适用于其他编程环境。

所以这里有一个技巧：无论你使用什么 IDE（甚至如果你不使用 IDE 创建 Java 程序），请运行《清单 13-2》中代码的这个精简版本：

```java
import java.io.File;
import java.io.FileNotFoundException;
import java.io.PrintStream;

class JustWrite {

    public static void main(String args[])
        throws FileNotFoundException {

        PrintStream diskWriter =
            new PrintStream("cookedData.txt");
        diskWriter.println(99.75);

        diskWriter.close();
    }
}
```

此程序不需要讨厌的 rawData.txt 文件。如果你运行此代码且没有错误信息，请在硬盘上搜索此程序的输出（cookedData.txt 文件）。记下包含 cookedData.txt 文件的文件夹名称。当你将 rawData.txt 放在同一文件夹中时，你在运行《清单 13-2》代码时遇到的任何问题都应该消失。


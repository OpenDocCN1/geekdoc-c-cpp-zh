
然而，这仍然是一项必不可少的技能。当你第一次安装 Java 时，你会希望在安装开发环境之前先排查安装问题。此外，通过自己执行这些基本步骤，你能更好地理解开发环境在幕后为你做了什么。

不过，在你掌握了编译和运行 Java 程序的基本步骤之后，就会希望使用专业的开发环境。你将在下一节看到如何做到这一点。

让我们从困难的方式开始：从命令行编译并启动一个 Java 程序。

1. 打开终端窗口。
2. 转到 `corejava/v1ch02/Welcome` 目录。（`corejava` 目录是你安装本书示例源代码的位置，如第 22 页 2.1.3 节“安装源文件和文档”所述。）
3. 输入以下命令：

```bash
javac Welcome.java
java Welcome
```

你应该会在终端窗口中看到图 2.3 所示的输出。

![](img/127bccebb2cfadea3f02579edaad63c3_50_0.png)

图 2.3 编译并运行 Welcome.java

## AI芯片的竞争：从云端到边缘

随着人工智能技术的快速发展，AI芯片已成为科技巨头竞争的新焦点。从云端数据中心到终端设备，AI芯片正在重塑整个计算产业的格局。

在云端，英伟达凭借其GPU在AI训练领域占据主导地位，而谷歌的TPU（张量处理单元）则展示了专用芯片在特定任务上的巨大优势。AMD也在积极追赶，其MI系列加速器在性能上不断逼近竞争对手。

在边缘侧，华为的昇腾系列、地平线的征程系列等国产AI芯片正在加速落地。苹果的A系列仿生芯片和华为的麒麟芯片将AI算力集成到移动处理器中，推动了端侧智能的发展。

AI芯片的性能评估通常从算力、功耗、生态三个维度进行。下表对比了当前主流AI芯片的关键参数：

| 芯片型号 | 算力 (TOPS) | 功耗 (W) | 制程 (nm) | 应用场景 |
|---|---|---|---|---|
| NVIDIA A100 | 312 | 400 | 7 | 云端训练 |
| Google TPU v4 | 275 | 300 | 7 | 云端推理 |
| Huawei Ascend 910 | 320 | 310 | 7 | 云端推理 |
| Horizon Journey 5 | 128 | 30 | 16 | 车载边缘 |

尽管专用AI芯片在某些任务上表现出色，但通用GPU仍拥有更成熟的软件生态。“软件才是关键的区别因素。”正如一位行业分析师所言，芯片硬件只是在编舞，软件生态才是真正的舞台。

- 算力密度：指单颗芯片在单位面积上提供的计算能力。
- 能效比：指每瓦特功耗带来的AI性能，对边缘设备尤为重要。
- 生态成熟度：包括开发框架支持、算子库丰富度及社区活跃度。

未来，AI芯片的竞争将不仅仅是硬件的较量，更是架构创新、软件生态和制造供应链的综合竞争。中国的AI芯片企业需要在开放生态中寻求突破，才能在全球市场中赢得一席之地。

3. 输入以下内容：

```bash
javac ImageViewer.java
java ImageViewer
```

会弹出一个新的程序窗口，其中运行 ImageViewer 应用程序。现在，选择“文件”→“打开”，查找要打开的图像文件。（同一目录中有几个示例文件。）图像会显示出来（见图 2.4）。要关闭程序，请单击标题栏中的关闭框，或从菜单中选择“文件”→“退出”。

![](img/127bccebb2cfadea3f02579edaad63c3_53_0.png)

**图 2.4** 运行 ImageViewer 应用程序

快速浏览一下源代码（程序清单 2.2）。这个程序比第一个程序长得多，但如果你考虑用 C 或 C++ 编写类似应用程序需要多少代码，它并不太复杂。你将在第 10 章学习如何编写这样的图形用户界面。

### 程序清单 2.2 ImageViewer/ImageViewer.java

```java
1 import java.awt.*;
2 import java.io.*;
3 import javax.swing.*;
4
5 /**
6  * A program for viewing images.
7  * @version 1.31 2018-04-10
 * @author Cay Horstmann
 */
public class ImageViewer
{
   public static void main(String[] args)
   {
      EventQueue.invokeLater(() -> {
         var frame = new ImageViewerFrame();
         frame.setTitle("ImageViewer");
         frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
         frame.setVisible(true);
      });
   }
}

/**
 * A frame with a label to show an image.
 */
class ImageViewerFrame extends JFrame
{
   private static final int DEFAULT_WIDTH = 300;
   private static final int DEFAULT_HEIGHT = 400;

   public ImageViewerFrame()
   {
      setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);

      // use a label to display the images
      var label = new JLabel();
      add(label);

      // set up the file chooser
      var chooser = new JFileChooser();
      chooser.setCurrentDirectory(new File("."));

      // set up the menu bar
      var menuBar = new JMenuBar();
      setJMenuBar(menuBar);

      var menu = new JMenu("File");
      menuBar.add(menu);

      var openItem = new JMenuItem("Open");
      menu.add(openItem);
      openItem.addActionListener(event -> {
          // show file chooser dialog
          int result = chooser.showOpenDialog(null);

          // if file selected, set it as icon of the label
          if (result == JFileChooser.APPROVE_OPTION)
          {
              String name = chooser.getSelectedFile().getPath();
              label.setIcon(new ImageIcon(name));
          }
      });

      var exitItem = new JMenuItem("Exit");
      menu.add(exitItem);
      exitItem.addActionListener(event -> System.exit(0));
   }
}
```

### 2.3 使用集成开发环境

在上一节中，你了解了如何从命令行编译和运行 Java 程序。这是排查问题的有用技能，但大多数日常工作都应使用集成开发环境。这些环境功能强大且方便，不用它们费力工作实在没多大意义。优秀的选择有免费可用的 Eclipse、IntelliJ IDEA 和 NetBeans。本章你将学习如何开始使用 Eclipse。当然，如果你更喜欢其他开发环境，也完全可以配合本书使用。

从 http://eclipse.org/downloads 下载 Eclipse 开始。有适用于 Linux、Mac OS X 和 Windows 的版本。运行安装程序并选择名为“Eclipse IDE for Java Developers”的安装集。

以下是用 Eclipse 编写程序的步骤。

1. 启动 Eclipse 后，从菜单选择“文件”→“新建”→“项目”。
2. 在向导对话框中选择“Java 项目”（见图 2.5）。
3. 单击“下一步”。*取消选中*“使用默认位置”复选框。单击“浏览”并导航到 `corejava/v1ch02/Welcome` 目录（图 2.6）。

![](img/127bccebb2cfadea3f02579edaad63c3_56_0.png)

图 2.5 Eclipse 中的“新建项目”对话框

![](img/127bccebb2cfadea3f02579edaad63c3_56_1.png)

图 2.6 在 Eclipse 中配置项目

4. 单击“完成”。项目现已创建。
5. 单击左窗格中项目旁的三角形，直到找到文件 `Welcome.java`，然后双击它。现在应看到显示程序代码的窗格（见图 2.7）。

![](img/127bccebb2cfadea3f02579edaad63c3_57_0.png)

图 2.7 使用 Eclipse 编辑源文件

6. 用鼠标右键单击左窗格中的项目名（Welcome）。选择“运行”→“运行方式”→“Java 应用程序”。程序输出显示在控制台窗格中。

大概这个程序没有拼写错误或缺陷。（毕竟它只有几行代码。）为讨论方便，假设你的代码偶尔包含拼写错误（甚至可能是语法错误）。试一试——例如通过如下改变 `String` 的大小写来运行文件：

```java
string greeting = "Welcome to Core Java!";
```

注意 `string` 下方的波浪线。在源代码下方的选项卡中，单击“问题”并展开三角形，直到看到抱怨未知字符串类型的错误消息（见图 2.8）。单击错误消息。光标移到编辑窗格中匹配的行，你可以在那里更正错误。这可以让你快速修正错误。

![](img/127bccebb2cfadea3f02579edaad63c3_58_0.png)

图 2.8 Eclipse 中的错误消息

> **提示：** Eclipse 错误报告通常伴有灯泡图标。单击灯泡可获取建议修复列表。

### 2.4 JShell

在上一节中，你了解了如何编译和运行 Java 程序。Java 9 引入了另一种使用 Java 的方式。JShell 程序提供“读取-求值-打印循环”，即 REPL。你输入一个 Java 表达式；JShell 会求值你的输入，打印结果，并等待下一个输入。要启动 JShell，只需在终端窗口中输入 `jshell`（见图 2.9）。

![](img/127bccebb2cfadea3f02579edaad63c3_59_0.png)

**图 2.9** 运行 JShell

JShell 以问候语开始，随后是提示符：

```text
Welcome to JShell -- Version 11.0.1
For an introduction type: /help intro
```

```text
jshell>
```

现在输入一个表达式，例如

```java
"Core Java".length()
```

JShell 用结果回应——在这个例子中，是字符串“Core Java”的字符数。

```text
$1 ==> 9
```

注意你*不要*输入 `System.out.println`。JShell 会自动打印你输入的每个表达式的值。

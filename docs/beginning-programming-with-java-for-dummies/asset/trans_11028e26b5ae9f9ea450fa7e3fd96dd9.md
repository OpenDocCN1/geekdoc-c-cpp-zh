
## 下一步？

如果你正在阅读这一段，你可能已经按照本章中的一些说明操作了——这些说明用于在你的计算机上安装 Java 和 Eclipse IDE。那么迫切的问题是：你是否正确完成了安装？ 这个问题的答案在第 3 章，因为在该章中，你将使用这些工具来运行一个全新的 Java 程序。

## 第 3 章
## 运行程序

### 本章内容

- 编译并运行程序
- 使用工作区
- 编辑自己的 Java 代码

如果你是编程新手，对你来说，运行程序可能意味着点击鼠标。你想运行 Internet Explorer，于是你双击 Internet Explorer 图标。就这么简单。

当你创建自己的程序时，情况就有点不同了。对于一个新程序，程序员（或程序员公司的人）会创建程序的图标。在此之前，一个完全正常的程序可能根本没有图标。那么你该如何处理一个全新的 Java 程序呢？如何让程序运行？本章会告诉你需要知道的内容。

### 运行现成的 Java 程序

了解 Java 的最好方法就是实践 Java。当你在实践 Java 时，你就是在编写、测试和运行自己的 Java 程序。本节通过描述如何运行和测试程序来为你做准备。不要自己编写程序，而是运行我已经为你写好的程序。该程序计算你房屋抵押贷款的月付款额。

抵押贷款计算程序不会打开自己的窗口。相反，程序在 Eclipse 的 Console 视图中运行。Console 视图是 Eclipse 工作台右下部分的一个标签页（见图 3-1）。完全在此 Console 视图中运行的程序称为基于文本的程序。

图 3-1：本章基于文本的抵押贷款程序的运行。

![](img/f938eba5f15e231d828a6255e7ec5523_69_0.png)

![](img/f938eba5f15e231d828a6255e7ec5523_69_1.png)

你可能在 Eclipse 工作台的右下部分看不到 Console 标签。要让 Console 视图显示出来，请选择 Window→Show View→Other。在出现的 Show View 对话框中，展开 General 分支。最后，在该 General 分支中，双击 Console 项目。

有关 Console 视图（以及 Eclipse 工作台的总体情况）的更多信息，请参阅本章后面的“Views, editors, and other stuff”部分。

![](img/f938eba5f15e231d828a6255e7ec5523_69_2.png)

你可以通过访问本书网站（allmycode.com/BeginProg）查看图 3-1 中程序的 GUI 版本，以及本书中许多其他示例的 GUI 版本。

实际上，当你运行抵押贷款程序时，你会在 Eclipse 的 Console 视图中看到两件事：

> 抵押贷款程序发送给你的消息和结果：消息包括诸如 How much are you borrowing? 之类的内容。结果包括诸如 Your monthly payment is $552.20 之类的行。

> 你在程序运行时给抵押贷款程序的响应：如果你在回答程序关于你借款金额的问题时输入 100000.00，你会看到该数字在 Eclipse 的 Console 视图中回显。

以下是运行抵押贷款程序的方法：

1. 确保你已按照第 2 章中的说明操作——安装 Java、安装和配置 Eclipse 以及获取本书示例程序的说明。
   太好了！你不必多次遵循这些说明。
2. 启动 Eclipse。
   Eclipse Workspace Launcher 对话框出现（见图 3-2）。

![](img/f938eba5f15e231d828a6255e7ec5523_70_0.png)

图 3-2：Eclipse Workspace Launcher。

工作区是你计算机硬盘上的一个文件夹。Eclipse 将你的 Java 程序存储在一个或多个工作区文件夹中。除了这些 Java 程序之外，每个工作区文件夹还包含一些 Eclipse 设置。这些设置存储诸如你使用的 Java 版本、你在编辑器中偏好的单词颜色、拖动编辑器区域边缘时编辑器区域的大小等信息，以及其他内容。你可以拥有多个工作区，每个工作区包含不同的程序和不同的设置。

默认情况下，Workspace Launcher 会提供打开上次运行 Eclipse 时打开的工作区。你想打开第 2 章中使用的那个工作区，所以不要修改 Launcher 的 Workspace 字段中的内容。

3. 在 Workspace Launcher 对话框中，点击 OK。
   大的 Eclipse 工作台出现在你的计算机屏幕上（见图 3-3）。

在图 3-3 中，工作台最左侧的部分是 Eclipse 的 Package Explorer，其中包含像 03-01、04-01 等这样的数字。每个数字实际上都是一个 Eclipse 项目的名称。正式地说，项目是工作区内的一组文件和文件夹。直观地说，项目是一个基本工作单元。例如，用于管理你的 CD 收藏（连同包含数据的）的一组自包含的 Java 程序文件可能构成一个单一的 Eclipse 项目。

再次查看图 3-3 中的 Package Explorer，你会看到名为 03-01、04-01 等的项目。我的项目 03-01 包含第 3 章（本章）的第一个也是唯一一个示例。项目 06-02 包含《本书第 6 章的第二个代码清单》中的 Java 程序 Listing 6-2。项目名称可以包含字母、数字、空白字符和其他字符，但对于本书示例的名称，我只使用数字和连字符。

要了解有关 Eclipse 的 Package Explorer 等内容的更多信息，请参阅即将到来的“What's All That Stuff in Eclipse's Window?”部分。

![](img/f938eba5f15e231d828a6255e7ec5523_71_0.png)

图 3-3：Eclipse 工作台。

![](img/f938eba5f15e231d828a6255e7ec5523_71_1.png)

当你启动 Eclipse 时，你可能会看到与图 3-3 中的内容不同的东西。你可能会看到只有几个图标的 Eclipse 欢迎屏幕，窗口其余部分空空如也。你也可能会看到像图 3-3 那样的一个工作台，但在 Package Explorer 中没有 03-01、04-01 等数字的列表。如果是这样，你可能错过了第 2 章中有关配置 Eclipse 的一些说明。或者，你可能在该节说明的第 2 步中修改了 Launcher 的 Workspace 字段中的内容。

无论如何，请确保你在 Package Explorer 中看到像 03-01 和 04-01 这样的数字。看到这些数字可确保 Eclipse 已准备好运行本书的示例程序。

4. 在 Package Explorer 中，点击 03-01 分支。
   本章的 Java 项目——03-01 项目——出现高亮。

![](img/f938eba5f15e231d828a6255e7ec5523_71_2.png)

你可能想先预览一些 Java 代码。要查看你在项目 03-01 中运行的 Java 程序，请在 Package Explorer 中展开 03-01 分支。在 03-01 分支内部，你会找到一个 src 分支，其中又包含一个（default package）分支。在（default package）分支内部，你会找到 Mortgage.java 分支。该 Mortgage.java 分支代表我的 Java 程序。双击 Mortgage.java 分支会使我的代码出现在 Eclipse 的编辑器中。

5. 从主菜单中选择 Run→Run As→Java Application，如图 3-4 所示。
   当你选择 Run As→Java Application 时，计算机运行项目的代码。（在此示例中，计算机运行我编写的 Java 程序。）作为运行的一部分，消息 How much are you borrowing? 出现在 Eclipse 的 Console 视图中。（Console 视图与 Problems 视图、Javadoc 视图、Declaration 视图以及可能的其他视图共享 Eclipse 工作台的右下区域。参考图 3-1。）

图 3-4：运行项目 03-01 中代码的一种方式。

![](img/f938eba5f15e231d828a6255e7ec5523_72_0.png)

6. 在 Eclipse 的 Console 视图中单击任意位置，然后输入一个数字，如 100000.00，并按 Enter。

![](img/f938eba5f15e231d828a6255e7ec5523_72_1.png)

   当你在第 6 步输入数字时，不要包含你所在国家/地区的货币符号，也不要对数字进行分组。（美国居民，不要输入美元符号，也不要使用任何逗号。）诸如 $100000.00 和 1,000,000.00 之类的内容会导致程序崩溃。你会在 Console 视图中看到 NumberFormatException 消息。

分组分隔符因国家/地区而异。图 3-1 中显示的运行是针对配置为美国的计算机，其中 100000.00（带点）表示十万。但在配置为我所说的逗号国家/地区的计算机上，运行可能看起来不同——在该国家/地区，100000,00（带逗号）表示十万。如果你生活在逗号国家/地区，并且像图 3-1 中所示那样输入 100000.00，你可能会收到错误消息（InputMismatchException）。如果是这样，请将文件中的数字金额更改为与你所在国家/地区的数字格式相匹配。完成后，你应该没问题。

按 Enter 后，Java 程序会在 Console 视图中显示另一条消息（What's the interest rate?）。（再次参考图 3-1。）

7. 针对利率问题，输入一个数字，如 5.25，并按 Enter。
   按 Enter 后，Java 程序会在 Console 视图中显示另一条消息（How many years . . . ?）。

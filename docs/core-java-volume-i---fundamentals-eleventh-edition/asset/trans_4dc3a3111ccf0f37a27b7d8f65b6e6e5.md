
你已经见过 JDK 这个缩写，它代表 Java Development Kit（Java 开发工具包）。有点令人困惑的是，该工具包的 1.2 到 1.4 版本被称为 Java SDK（Software Development Kit，软件开发工具包）。你仍会偶尔看到对这个旧称的引用。直到 Java 10，还存在一个只包含虚拟机的 Java Runtime Environment（JRE，Java 运行时环境）。作为开发者，这不是你想要的。它面向不需要编译器的最终用户。

接下来，你会到处看到 Java SE 这个术语。它指的是 Java Standard Edition（Java 标准版），与 Java EE（Enterprise Edition，企业版）和 Java ME（Micro Edition，微型版）相对。

你可能会遇到 Java 2 这个术语，它诞生于 1998 年，当时 Sun 的市场营销人员觉得，小数版本号的递增无法恰当传达 JDK 1.2 的重大进步。然而，由于他们是在发布之后才意识到这一点，他们决定让 *开发工具包* 继续使用版本号 1.2。后续版本编号为 1.3、1.4 和 5.0。然而，*平台* 从 Java 更名为 Java 2。因此，就有了 Java 2 Standard Edition Software Development Kit Version 5.0，简称 J2SE SDK 5.0。

幸运的是，2006 年版本编号被简化了。Java 标准版的下一个版本被称为 Java SE 6，随后是 Java SE 7 和 Java SE 8。

然而，“内部”版本号是 1.6.0、1.7.0 和 1.8.0。这种小小的疯狂终于在 Java SE 9 时结束，当时版本号变成了 9，然后是 9.0.1。（为什么初始版本不是 9.0.0？为了保留一点点兴奋感，版本号规范要求在主版本发布与其首个安全更新之间的短暂间隔内去掉末尾的零。）

> **注意：** 在本书余下部分，我们将省略“SE”这一缩写。当你看到“Java 9”时，它指的是“Java SE 9”。

在 Java 9 之前，Java Development Kit 有 32 位和 64 位版本。Oracle 不再开发 32 位版本。要使用 Oracle JDK，你需要有 64 位操作系统。

在 Linux 上，你可以在 RPM 文件和 .tar.gz 文件之间选择。我们推荐后者——你可以直接将其解压缩到你喜欢的任何位置。

现在你知道如何选择正确的 JDK 了。总结如下：

- 你需要的是 JDK（Java SE Development Kit），而不是 JRE。
- Linux：选择 `.tar.gz` 版本。

接受许可协议并下载该文件。

> **注意：** 取决于行星的排列，Oracle 可能会提供一个同时包含 Java Development Kit 和 NetBeans 集成开发环境的捆绑包。我建议你远离所有捆绑包，此时只安装 Java Development Kit。如果你以后决定使用 NetBeans，只需从 http://netbeans.org 下载它。

### 2.1.2 设置 JDK

下载 JDK 后，你需要安装它，并弄清楚它安装到了哪里——稍后你会需要这个信息。

- 在 Windows 上，启动安装程序。系统会询问你要将 JDK 安装到哪里。最好不要接受路径名中包含空格的默认位置，例如 `c:\Program Files\Java\jdk-11.0.x`。只需从路径名中去掉 Program Files 部分。
- 在 Mac 上，运行安装程序。它会将软件安装到 `/Library/Java/JavaVirtualMachines/jdk-11.0.x.jdk/Contents/Home`。用 Finder 找到它。
- 在 Linux 上，只需将 `.tar.gz` 文件解压缩到你选择的位置，例如你的主目录或 `/opt`。或者，如果你是从 RPM 文件安装的，请再次确认它安装在 `/usr/java/jdk-11.0.x`。

在本书中，安装目录记为 `jdk`。例如，当提到 `jdk/bin` 目录时，我指的是名称为 `/opt/jdk-11.0.4/bin` 或 `c:\Java\jdk-11.0.4\bin` 的目录。

在 Windows 或 Linux 上安装 JDK 时，你需要执行一个额外步骤：将 `jdk/bin` 目录添加到可执行文件路径中——也就是操作系统用来查找可执行文件的目录列表。

- 在 Linux 上，将类似下面的一行添加到 `~/.bashrc` 或 `~/.bash_profile` 文件的末尾：

  ```bash
  export PATH=jdk/bin:$PATH
  ```

  请务必使用 JDK 的正确路径，例如 `/opt/jdk-11.0.4`。
- 在 Windows 10 上，在 Windows 设置的搜索栏中输入“environment”，然后选择“编辑账户的环境变量”（见图 2.1）。应该会出现“环境变量”对话框。（它可能隐藏在 Windows 设置对话框后面。如果到处都找不到它，可以尝试从“运行”对话框中运行 `sysdm.cpl`——同时按住 Windows 和 R 键即可打开该对话框——然后选择“高级”选项卡并单击“环境变量”按钮。）在“用户变量”列表中找到并选择名为 Path 的变量。单击“编辑”按钮，再单击“新建”按钮，并添加一个指向 `jdk\bin` 目录的条目（见图 2.2）。

![](img/127bccebb2cfadea3f02579edaad63c3_47_0.png)

图 2.1  在 Windows 10 中设置系统属性

保存设置。你新启动的任何“命令提示符”窗口都将具有正确的路径。

下面说明如何测试你是否做对了：启动一个终端窗口。输入以下行

```text
javac --version
```

然后按 Enter 键。你应该会看到类似下面的显示：

```text
javac 11.0.1
```

## BIO 1113

## 第 18 章：基因表达

基因表达是利用基因中的信息合成功能性基因产物（通常是蛋白质）的过程。该过程包括两个主要步骤：转录和翻译。

**转录**是以 DNA 为模板合成 RNA 的过程。RNA 聚合酶读取模板链并生成互补的 RNA 链。转录的产物是信使 RNA（mRNA）。

- **起始**：RNA 聚合酶结合到启动子区域并解开 DNA。
- **延伸**：RNA 聚合酶沿模板链移动，添加 RNA 核苷酸。
- **终止**：RNA 聚合酶到达终止子序列，释放 mRNA。

**翻译**是以 mRNA 为模板合成多肽链的过程。核糖体通过读取 mRNA 上的密码子，并将它们与携带氨基酸的适当 tRNA 分子相匹配，来促进这一过程。

| 密码子 | 氨基酸 |
|-------|------------|
| AUG   | 甲硫氨酸（起始） |
| UAA   | 终止密码子 |
| UAG   | 终止密码子 |
| UGA   | 终止密码子 |

遗传密码具有简并性，这意味着多个密码子可以编码同一种氨基酸。阅读框由起始密码子 AUG 决定，从而确保蛋白质的正确翻译。

翻译后修饰，如磷酸化、糖基化和泛素化，可以改变蛋白质的功能和定位。这些修饰对于调节蛋白质活性至关重要。

- 2. 在主目录中创建目录 `javasrc`。如果愿意，你可以在终端窗口中执行此操作。

  ```bash
  mkdir javasrc
  ```

- 3. 在 `jdk/lib` 目录中，找到文件 `src.zip`。
- 4. 将 `src.zip` 文件解压到 `javasrc` 目录中。在终端窗口中，你可以执行以下命令

  ```bash
  cd javasrc
  jar xvf jdk/lib/src.zip
  cd ..
  ```

> **提示：** `src.zip` 文件包含所有公共库的源代码。要获取更多源代码（用于编译器、虚拟机、原生方法和私有辅助类），请访问 http://openjdk.java.net。

文档包含在一个与 JDK 分离的压缩文件中。你可以从 `www.oracle.com/technetwork/java/javase/downloads` 下载文档。请按照以下步骤操作：

- 1. 下载文档 zip 文件。它的名称为 `jdk-11.0.x_doc-all.zip`。
- 2. 解压该文件，并将 doc 目录重命名为更具描述性的名称，例如 javadoc。如果愿意，你可以在命令行中执行此操作：

  ```bash
  jar xvf Downloads/jdk-11.0.x_doc-all.zip
  mv docs jdk-11-docs
  ```

- 3. 在浏览器中，导航到 `jdk-11-docs/index.html`，并将此页面添加到书签。

你还应该安装 Core Java 程序示例。你可以从 `http://horstmann.com/corejava` 下载它们。这些程序打包在一个 zip 文件 `corejava.zip` 中。只需将它们解压到你的主目录中。它们将位于 `corejava` 目录中。如果愿意，你可以在命令行中执行此操作：

```bash
jar xvf Downloads/corejava.zip
```

### 2.2 使用命令行工具

如果你的编程经验来自 Microsoft Visual Studio 之类的开发环境，那么你习惯于一个带有内置文本编辑器、用于编译和启动程序的菜单以及调试器的系统。JDK 中没有任何哪怕稍微类似的东西。你需要通过在终端窗口中键入命令来完成所有操作。这听起来很繁琐，但它是

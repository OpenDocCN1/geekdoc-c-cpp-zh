
有关 `.zip` 文件的更多信息，请参阅本章中的“压缩归档文件”侧边栏。

我最喜欢把 eclipse 文件夹直接拖到 C: 盘。于是我的 C: 盘上有名为 `Program Files`、Windows、eclipse 等文件夹。我避免将 eclipse 文件夹设为 Program Files 的子文件夹，因为有时我会遇到处理名称中包含空格的 `Program Files` 的问题。

## 如果你使用 Mac OS X：

下载 Eclipse 时，你会得到一个 `.tar.gz` 文件或一个 `.dmg` 文件。

- 一个 `.tar.gz` 文件是一个压缩归档文件。下载文件时，你的网页浏览器可能会自动为你解压一部分。如果是这样，你在下载文件夹中找不到 `.tar.gz` 文件。相反，你会找到一个 `.tar` 文件（因为浏览器解压了 `.gz` 部分），或一个 eclipse 文件夹（因为浏览器解压了 `.tar` 和 `.gz` 两部分）。

如果你在下载文件夹中找到新的 `.tar` 文件或 `.tar.gz` 文件，双击该文件直到看到 eclipse 文件夹。将这个新的 eclipse 文件夹拖到你的应用程序文件夹中，就大功告成了。

- 如果你下载的是 `.dmg` 文件，你的网页浏览器可能会为你打开该文件。如果没有，请在下载文件夹中找到 `.dmg` 文件并双击它。按照双击后出现的任何说明操作。如果需要将 Eclipse 拖入你的应用程序文件夹，请执行此操作。

## 如果你使用 Linux：

你可能会得到一个 `.tar.gz` 文件，但也有可能得到一个自解压的 `.bin` 文件。将 `.tar.gz` 文件解压到你喜欢的目录，或执行自解压的 `.bin` 文件。

## 首次运行 Eclipse

第一次启动 Eclipse 时，你需要执行几个额外步骤。要运行 Eclipse，请执行以下操作：

- 1. **启动 Eclipse。**

  在 Windows 中，开始菜单可能没有 Eclipse 图标。这种情况下，请在 Windows 资源管理器（又名文件资源管理器）中查找包含已解压 Eclipse 文件的文件夹。双击代表 `eclipse.exe` 文件的图标。（如果看到 eclipse 文件但没有 `eclipse.exe` 文件，请查阅本章的“那些讨厌的文件名扩展名”侧边栏。）

![](img/bf4858233d2b2a32ff4e3991860526b3_58_0.png)

**图 2-11：** Eclipse 的欢迎屏幕。

![](img/bf4858233d2b2a32ff4e3991860526b3_58_1.png)

**图 2-12：** 带有全新工作区的 Eclipse 工作台。

## 在 Eclipse 中配置 Java

Eclipse 通常会在你的计算机上查找 Java 安装并选择一个已安装的 Java 版本来运行你的 Java 程序。你的计算机可能安装了多个 Java 版本，因此你可能需要再次检查 Eclipse 对 Java 版本的选择。以下步骤会告诉你如何操作：

- 1. 在 Windows 或 Linux 上：在 Eclipse 的主菜单中选择 Window▸ Preferences。在 Mac 上：在 Eclipse 的主菜单中选择 Eclipse▸ Preferences。

结果，Eclipse 的首选项对话框会出现。（你可以对照图 2-13 进行操作。）

![](img/bf4858233d2b2a32ff4e3991860526b3_59_0.png)

**图 2-13：** Eclipse 的首选项对话框。

- 2. 在首选项对话框左侧的树中，展开 Java 分支。
- 3. 在 Java 分支中，选择 Installed JREs 子分支。
- 4. 查看首选项对话框主体中的 Java 版本列表（Installed JREs）。

在列表中，每个 Java 版本都有一个复选框。Eclipse 使用已勾选的版本。如果已勾选的版本不是你偏好的版本（例如，已勾选的版本不是 8 或更高版本），你可以进行一些更改。

- 5. **如果你的首选 Java 版本出现在 Installed JREs 列表中，请在该版本的复选框中打勾。**

- 6. **如果你的首选 Java 版本未出现在 Installed JREs 列表中，请单击 Add 按钮。**

单击 Add 按钮后，会出现 JRE Type 对话框（见图 2-14）。

![](img/bf4858233d2b2a32ff4e3991860526b3_60_0.png)

**图 2-14：** JRE Type 对话框。

- 7. **在 JRE Type 对话框中，双击 Standard VM。**

结果，JRE Definition 对话框会出现（见图 2-15）。接下来要做什么取决于一些不同的因素。

- 8. **填写对话框的 JRE Home 字段。**

  如何操作取决于你的操作系统。

  - 在 Windows 上，浏览到你安装首选 Java 版本的目录。在我的许多 Windows 计算机上，该目录是 `C:\Program Files\Java\jre8`、`C:\Program Files\Java\jdk1.8.0_8`、`C:\Program Files (x86)\Java\jre8` 或类似路径。

  - 在 Mac 上，使用 Finder 浏览到你安装首选 Java 版本的目录。在对话框的 JRE Home 字段中输入该目录的名称。

  我的 Mac 上有一个名为 `/System/Library/Java/JavaVirtualMachines/1.6.0.jdk/Contents/Home` 的 Java 目录，另一个名为 `/Library/Java/JavaVirtualMachines/jdk1.8.0.jdk/Contents/Home` 的 Java 目录。（前者是 Apple 的旧版 Java；后者是 Oracle 的新版 Java。）你也可能在 `/Library/Internet Plug-Ins/JavaAppletPlugin.plugin/Contents/Home` 目录中找到 Oracle 的 Java。

  /System 和 /Library 等目录通常不会出现在 Finder 窗口中。要浏览到其中一个目录（例如 /Library 目录），请在 Finder 的菜单栏中选择 Go→Go to Folder。在弹出的对话框中，输入 /Library 然后按 Go。

  当你导航到包含首选 Java 版本的目录时，你可能会遇到 JDK 1.8.0.jdk 图标或其他扩展名为 .jdk 的项目。要查看此项目的内容，请按住 control 键单击该项目的图标，然后选择显示包内容。

  - 在 Linux 上，浏览到你安装首选 Java 版本的目录。如有疑问，请搜索名称以 jre 或 jdk 开头的目录。

![](img/bf4858233d2b2a32ff4e3991860526b3_61_0.png)

**图 2-15：** JRE Definition 对话框（在执行步骤 8 和 9 之后）。

![](img/bf4858233d2b2a32ff4e3991860526b3_61_1.png)

![](img/bf4858233d2b2a32ff4e3991860526b3_61_2.png)

你可能还需要在 JRE Definition 对话框中做一件事。

- 9. 查看 JRE Definition 对话框的 JRE Name 字段；如果 Eclipse 没有自动填写名称，请在 JRE Name 字段中输入一个名称（几乎任何文本均可）。

- 10. 通过单击 Finish 关闭 JRE Definition 对话框。

Eclipse 的首选项对话框重新回到前台。Installed JREs 列表中包含你刚刚添加的 Java 版本。

- 11. 在你刚刚添加的 Java 版本旁边的复选框中打勾。

你几乎完成了。（还有几个步骤需要跟进。）

- 12. 在首选项对话框左侧的 Java 分支中，选择 Compiler 子分支。

在首选项对话框的主体中，你会看到一个 Compiler Compliance Level 下拉列表（见图 2-16）。

![](img/bf4858233d2b2a32ff4e3991860526b3_62_0.png)

**图 2-16：** 设置编译器兼容级别。

- 13. 在 Compiler Compliance Level 下拉列表中，选择一个与你首选 Java 版本相匹配的数字。

对于 Java 7，我选择兼容级别 1.7。对于 Java 8，我选择兼容级别 1.8。

- 14. 呼！单击首选项对话框的 OK 按钮返回 Eclipse 工作台。

## 导入本书的示例程序

这个导入过程可能有点棘手。随着你从一个对话框移动到下一个对话框，许多选项的名称相似。这是因为 Eclipse 提供了许多不同的方式来导入许多不同类型的内容。总之，如果你按照这些说明操作，就没问题。

- 1. 按照本章前面“获取本书示例程序”部分中的步骤操作。
- 2. 在 Eclipse 的主菜单中选择 File→Import（见图 2-17）。

结果，Eclipse 显示一个 Import 对话框。

![](img/bf4858233d2b2a32ff4e3991860526b3_63_0.png)

- 3. 在 Import 对话框的树中，展开 General 分支。
- 4. 在 General 分支中，双击 Existing Projects into Workspace 子分支（见图 2-18）。

结果，出现一个 Import Projects 对话框。

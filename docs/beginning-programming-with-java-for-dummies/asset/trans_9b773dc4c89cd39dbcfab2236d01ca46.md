
- 8. 输入一个数字，例如 30，然后按 Enter。

输入的数字对应的，Java 程序会显示一个月度付款金额。再次参考图 3-1。

免责声明：您当地的抵押贷款公司收取各种费用。现实生活中获得抵押贷款，您支付的金额会比我的 Java 程序计算的金额多。（多得多。）

在第 8 步输入数字时，不要包含小数点。像 30.0 这样的数字会导致程序崩溃。您会在 Console 视图中看到 NumberFormatException 消息。

有时，在程序运行过程中，您可能会决定自己犯了某种错误。您想立即停止程序的运行。只需单击 Console 视图上方的那个小红色矩形（参见图 3-5）。

![](img/f938eba5f15e231d828a6255e7ec5523_73_0.png)

![](img/f938eba5f15e231d828a6255e7ec5523_73_1.png)

图 3-5：如何提前终止程序的运行。

![](img/f938eba5f15e231d828a6255e7ec5523_73_2.png)

如果您按照本节的说明操作但没有得到我描述的结果，您可以尝试三件事。我按从最好到最差的顺序列出它们：

- 检查所有步骤，确保您已正确完成所有操作。
- 发送电子邮件至 BeginProg@allmycode.com，或在我的 Facebook 墙上发布（/allmycode），或向 Burd（@allmycode）发推。如果您描述发生了什么，我很可能能找出问题所在并告诉您如何纠正。
- 恐慌。

## 自己输入和运行代码

前一节内容是关于运行别人的 Java 代码（从本书网站下载的代码）。但最终，您将自己编写代码。本节向您展示如何使用 Eclipse IDE 创建代码。

### 将您的程序与我的程序分开

在第 2 章中，您从我的网站下载本书的示例。然后您创建一个 Eclipse 工作区并将本书的示例导入到工作区中。

您可以在同一工作区中创建自己的项目。但如果您想将自己的代码与我的代码分开，可以创建一个第二个工作区。以下是创建新工作区的两种方法：

- **启动 Eclipse 时，在 Eclipse 工作区启动器对话框的 Workspace 字段中输入一个新文件夹名称。**

  如果该文件夹尚不存在，Eclipse 会创建该文件夹。如果该文件夹已存在，Eclipse 的 Package Explorer 会列出该文件夹包含的任何项目。

- **在 Eclipse 工作台的主菜单中，选择 File > Switch Workspace（参见图 3-6）。**

  当您选择 File > Switch Workspace 时，Eclipse 会为您提供之前打开的一些工作区文件夹。如果您选择的文件夹不在列表中，请选择 Other 选项。响应后，Eclipse 会重新打开其 Workspace Launcher 对话框。

![](img/f938eba5f15e231d828a6255e7ec5523_74_0.png)

### 编写和运行您的程序

以下是创建新 Java 项目的方法：

- 1. 启动 Eclipse。
- 2. 从 Eclipse 的菜单栏中选择 File→New→Java Project。

  一个 New Java Project 对话框出现。

- 3. 在 New Java Project 对话框中，为您的项目输入一个名称，然后单击 Finish。

在图 3-7 中，我输入的名称为 `MyFirstProject`。

如果您单击 Next 而不是 Finish，您会看到一些现在不需要的其他选项。因此，为了避免任何混淆，只需单击 Finish 即可。

单击 Finish 会带您返回 Eclipse 的工作台，其中 `MyFirstProject` 显示在 Package Explorer 中，如图 3-8 所示。

下一步是创建一个新的 Java 源代码文件。

![](img/f938eba5f15e231d828a6255e7ec5523_75_0.png)

![](img/f938eba5f15e231d828a6255e7ec5523_75_1.png)

图 3-7：让 Eclipse 创建新项目。

图 3-8：您的项目出现在 Eclipse 的 Package Explorer 中。

![](img/f938eba5f15e231d828a6255e7ec5523_76_0.png)

- 4. 在 Package Explorer 中选择您新创建的项目。

要创建图 3-8，我选择了 MyFirstProject 而不是 SomeOtherProject。

- 5. 在 Eclipse 的主菜单中选择 File→New→Class。

Eclipse 的 New Java Class 对话框出现（参见图 3-9）。

Java 程序员通常将代码划分为一个或多个包。典型的包名称类似于 java.util 或 org.allyourcode.images。在图 3-9 中，Eclipse 警告我没有为项目的代码命名一个包。因此代码进入一个名为 Java 默认包的不起眼的东西。Java 默认包是一个没有名称的包——代码未被其他方式打包时的一个总括位置。包对于管理大型编程项目非常有用，但本书不包含大型编程项目。因此，在本示例（以及本书所有示例中），我选择忽略该警告。有关 Java 包的更多信息，请参阅第 18 章。

**技术细节**

与其他所有窗口化环境一样，Eclipse 提供了多种完成同一任务的方法。除了选择 File→New→Class，您还可以在 Windows 中右键单击 Package Explorer 中的 MyFirstProject（或在 Mac 上 control-单击 Package Explorer 中的 MyFirstProject）。在 resulting 上下文菜单中，选择 New→Class。您也可以先按 Windows 上的 Alt+Shift+N（或 Mac 上的 Option+⌘+N）。点击和按键的选择由您决定。

**提示**

- 6. 在 New Java Class 对话框的 Name 字段中，输入新类的名称。

在本示例中，我使用名称 MyFirstJavaClass，名称中各词之间没有空白。（参见图 3-9。）

![](img/f938eba5f15e231d828a6255e7ec5523_77_0.png)

图 3-9：让 Eclipse 创建新的 Java 类。

![](img/f938eba5f15e231d828a6255e7ec5523_77_1.png)

New Java Class 对话框中的名称不得包含空白。唯一允许的标点符号是下划线字符（_）。您可以将类命名为 MyFirstJavaClass 或 My_First_Java_Class，但不能将其命名为 My First Java Class 或 Java Class, MyFirst。

- 7. 在 public static void main(String[] args) 复选框中打勾。

您的勾选告诉 Eclipse 创建一些样板 Java 代码。

- 8. 接受 New Java Class 对话框中所有其他内容的默认值（换句话说，单击 Finish）。

您甚至可以忽略对话框顶部附近的“Default Package Is Discouraged”警告。

单击 Finish 会带您返回 Eclipse 的工作台。现在 MyFirstProject 包含一个名为 MyFirstJavaClass.java 的文件。为了方便您，MyFirstJavaClass.java 文件中已有一些代码。Eclipse 的编辑器显示 Java 代码（参见图 3-10）。

![](img/f938eba5f15e231d828a6255e7ec5523_78_0.png)

图 3-10：Eclipse 在编辑器中编写一些代码。

- 9. 替换您新 Java 程序中已有的代码行。

在 Eclipse 的 Editor 中输入一行代码。将以下行替换

```
// TODO Auto-generated method stub
```

为以下行

```
System.out.println("Chocolate, royalties, sleep");
```

完全按照 Listing 3-1 中的显示复制新代码行。

- 拼写每个单词的方式必须与 Listing 3-1 中的拼写完全相同。
- 大小写每个单词的方式必须与我在 Listing 3-1 中的做法完全相同。
- 包含所有标点符号——点号、引号、分号、所有内容。
- 区分小写字母 l 和数字 1。单词 println 告诉计算机打印整行。单词 println 中的每个字符都是小写字母。该单词不包含数字。

**Listing 3-1: 显示我喜欢的东西的程序**

```java
public class MyFirstJavaClass {

    /**
     * @param args
     */
    public static void main(String[] args) {
        System.out.println("Chocolate, royalties, sleep");
    }
}
```

### 我在 Java 程序中看到格式了吗？

当您使用 Eclipse 的编辑器编写 Java 程序时，您会看到各种颜色的单词。某些单词始终为蓝色。其他单词始终为黑色。您甚至会看到一些粗体和斜体短语。您可能认为您看到了格式，但实际上没有。您看到的被称为语法着色或语法高亮。

这种格式不是程序文件的一部分。相反，编辑器以便于阅读 Java 程序的方式显示每个单词。

例如，在 Java 程序中，某些单词（例如 class、public 和 void）具有其自身的特殊含义。因此 Eclipse 的编辑器以粗体、红色的字母显示 class、public 和 void。当我保存 Java 程序文件时，计算机不会在我的 Java 程序文件中存储有关粗体、彩色字母的任何信息。但编辑器会自行决定用红色着色突出显示特殊单词。

无论您如何称呼它，问题如下：

- 使用 Microsoft Word，诸如粗体格式之类的内容在文档内部标记。当您保存 myPersonalDiary.docx 时，使单词“love”和“hate”加粗的指令会记录在 MyPersonalDiary.docx 文件内部。
- 使用 Java 程序编辑器，诸如粗体和着色之类的内容不会在 Java 程序文件内部标记。相反，编辑器以便于阅读 Java 程序的方式显示每个单词。

其他一些编辑器可能会以蓝色字体显示相同的单词。另一个编辑器（如 Windows Notepad）以普通的黑色显示所有单词。

![](img/f938eba5f15e231d828a6255e7ec5523_79_0.png)

Java 是区分大小写的，这意味着 system.out.println 与 System.out.println 不同。如果您输入 system.out.println，您的程序将无法工作。请确保代码的大小写与 Listing 3-1 中的完全一致。

如果您从电子书中复制并粘贴代码，请检查代码中的引号是否为直引号 (" )，而不是弯引号（“ ”）。在 Java 程序中，直引号是好的；弯引号会带来麻烦。

如果您正确输入了所有内容，您会看到图 3-11 中的内容。

图 3-11：Eclipse 编辑器中的 Java 程序。

![](img/f938eba5f15e231d828a6255e7ec5523_79_1.png)

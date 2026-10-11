
| 成员 | 描述 |
| :--- | :--- |
| Bold | 粗体文本 |
| Italic | 斜体文本 |
| Regular | 普通文本 |
| Strikeout | 带删除线的文本 |
| Underline | 下划线文本 |

# 第 12 章 使用控件

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_574_0.png)

与其实例化 `Font`，你可以编写类似下面的代码语句：

```csharp
this.label1.Font = bigFont;
this.okButton.Font = bigFont;
```

- 1. 通过使用表单设计器和属性窗口，你可以节省时间并减少错误机会。
- 2. 当你使用表单设计器将 `Label` 拖到表单上时，不需要为 `Label` 调用构造函数。
- 3. 你可以使用属性窗口为 `Label` 设置属性，如 `Font`、`Location`、`Size` 和 `Text`。

> 谎言语句是 #2。当你使用表单设计器将 `Label` 拖到表单上时，你不需要编写构造函数调用，但系统会为你生成一个。

## 第 12 章 使用控件

如果你在 IDE 中双击 `LinkLabel`，系统将为你为你创建一个格式为 `xxx_LinkClicked()` 的方法外壳，其中 `xxx` 是属于 `LinkLabel` 的属性名称。（这对应于你在 IDE 中双击 `Button` 时的操作）。例如，双击会生成一个 `linkLabel1_LinkClicked()` 方法外壳。像 `Button` 的 `Click()` 方法一样，你通常希望重命名 `Clicked()` 方法，使其按照习惯以大写字母开头。图 12-7 显示了当图 12-7 中 `Form` 的自动创建方法被修改为大写字母开头时，所生成的两个方法。

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_576_0.png)

图 12-6 一个带有两个 `LinkLabel` 的表单。在图 12-7 中，两个阴影语句是代码中唯一自动生成的部分。程序员添加了这些行，以指示当用户在运行应用程序中点击相应的 `LinkLabel` 时应该发生哪些操作。

```csharp
public partial class Form1 : Form
{
    public Form1()
    {
        InitializeComponent();
    }
    private void LinkLabel1_LinkClicked(object sender,
        LinkLabelClickedEventArgs e)
    {
        System.Diagnostics.Process.Start("IEExplore",
        "http://www.cengage.com");
    }
    private void LinkLabel2_LinkClicked(object sender,
        LinkLabelClickedEventArgs e)
    {
        System.Diagnostics.Process.Start(
        (@"C:\CSharp\Chapter12\Policy.txt");
    }
}
```

图 12-7 两个 `Clicked()` 方法

如果你在文件顶部使用了 `System.Diagnostics;`，你可以消除图 12-7 中的引用，并直接将进程称为 `Process.Start`。

当你在 IDE 中查看时，换行符不会像在本章代码插图中看到那么多。插入换行符是为了让行能够更好地适应书的页面。

## 使用 LinkLabel

在图 12-7 的每个 `Clicked()` 方法中，程序员都添加了对 `System.Diagnostics.Process.Start()` 的调用。该方法允许你在应用程序内运行其他程序。`Start()` 方法有两个重载版本：

- 当你使用一个字符串参数时，你提供了要打开的文件名。
- 当你使用两个参数时，你提供了应用程序名称及其所需的参数。

在 `LinkLabel1_LinkClicked()` 方法中，两个参数打开了 Internet Explorer (`"IEExplore"`) 并传递了 Cengage 网站的地址。如果 Internet 连接活动，控制将转移到该网站。

在 `LinkLabel2_LinkClicked()` 方法中，只提供了一个参数。它打开了存储在本地磁盘上的文件。默认应用程序根据文件的扩展名打开。例如，记事本是 `.txt` 扩展名文件的默认应用程序。或者，你可以复制以下内容，它显式地命名了：

```csharp
System.Diagnostics.Process.Start("Notepad",@"C:\CSharp\Chapter12\Policy.txt");
```

> 在 `LinkLabel2_LinkClicked()` 方法中，要打开的文件名前出现了一个符号 (`@`)。该符号表示字符串中的所有字符都被字面解释。因此，路径中的反斜杠不会被解释为转义序列字符。

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_577_0.png)

当用户点击链接时，可以将 `LinkVisited` 属性设置为 `true`，如图 12-8 中的阴影语句所示。此设置表示链接应以不同的颜色显示，以便用户可以看到链接已被访问。默认情况下，访问过的链接颜色是紫色，但你可以在 `LinkLabel` 的属性列表中更改此设置。

```csharp
private void LinkLabel1_LinkClicked(object sender,
LinkLabel1LinkClickedEventArgs e)
{
    System.Diagnostics.Process.Start("IEExplore",
"http://www.cengage.com");
    linkLabel1.LinkVisited = true;
}
```

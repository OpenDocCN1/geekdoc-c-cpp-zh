
```csharp
try
(
    // 用于存储从文件中读取的数字；
    // 以及它们的总和
    int number1, number2, number3, total;

    // 一个 StreamReader 变量。
    StreamReader inputFile;

    // 打开文件并获取 StreamReader 对象。
    inputFile = File.OpenText("NumericData.txt");

    // 从文件中读取三个数字。
    number1 = int.Parse(inputFile.ReadLine());
    number2 = int.Parse(inputFile.ReadLine());
    number3 = int.Parse(inputFile.ReadLine());
    // 计算数字的总和。
    total = number1 + number2 + number3;
    // 显示总和。
    MessageBox.Show("The total is " + total);
    // 关闭文件。
    inputFile.Close();
}
catch (Exception ex)
{
// 显示错误消息。
MessageBox.Show(ex.Message);
}
```

让我们仔细观察代码。

第 1 行：这是 `try-catch` 语句的开始。`try` 块中的代码可能会抛出各种异常，导致程序跳转到第 27 行的 `catch` 句。

第 5 行：该语句声明了 `int` 变量 `number1`、`number2`、`number3` 和 `total`。这些变量保存了从文件中读取的三个值及其总和。

第 8–11 行：执行这些语句后，`NumericData.txt` 文件被打开用于读取，`inputFile` 变量引用一个与文件相关的 `StreamReader` 对象。

第 14 行：该语句执行了以下操作：

- 它调用 `inputFile.ReadLine` 方法从文件中读取一行文本。
- `inputFile.ReadLine` (string) 返回的值作为参数传递给 `int.Parse` 方法。
- `int.Parse` 方法返回的值赋值给 `number1` 变量。

在执行该语句后，`number1` 变量被赋值为从文件中读取的第一个值，并转换为 `int`。（`number1` 变量被赋值为值 10）。

**第 15 行**：该语句从文件中读取下一个值，将其转换为 `int`，并将结果赋值给 `number2` 变量。（`number2` 变量被赋值为值 20）。

**第 16 行**：该语句从文件中读取下一个值，将其转换为 `int`，并将结果赋值给 `number3` 变量。（`number3` 变量被赋值为值 30）。

**第 19 行**：该语句计算 `number1`、`number2` 和 `number3` 的和，并将结果赋值给 `total`。

**第 22 行**：该语句在消息框中显示数字之和。

**第 25 行**：该语句关闭文件。

## 使用循环读取文件并检测文件末尾

很多时候，程序必须在不知道文件中存储了多少项目的情况下读取文件内容。例如，假设你需要编写一个程序显示文件中的所有项目，但你不知道文件中包含多少个项目。你可以打开文件，然后使用循环反复从文件中读取一个项目并显示它。然而，如果程序尝试读取文件末尾之后的内容，将抛出异常。程序需要某种方法来判断何时到达文件末尾，这样它就不会尝试读取末尾之后的内容。下面的伪代码显示了该逻辑：

```
打开文件
当未到达文件末尾时：
    从文件中读取一个项目
    显示项目
结束循环
关闭文件
```

`StreamReader` 对象具有一个布尔属性 `EndOfStream`，用于指示已到达文件末尾。如果文件的位置位于文件末尾（且没有更多可读数据），`EndOfStream` 属性设置为 `true`。否则，它设置为 `false`。当你需要在不知道文件包含多少项目的情况下读取文件中所有项目时，你可以写一个只要 `EndOfStream` 属性为 `false` 就一直迭代的循环。

假设 `inputFile` 引用一个与已文件相关的 `StreamReader` 对象。你可以如下所示编写循环：

```csharp
while (inputFile.EndOfStream == false)
{
  // 从文件中读取一个项目。
  // 处理该项目。
}
```

然而，大多数程序员更倾向于使用 `!` 运算符的以下逻辑：

```csharp
while (!inputFile.EndOfStream)
{
  // 从文件中读取一个项目。
  // 处理该项目。
}
```

记住 `!` 运算符是逻辑非运算符。当你读取此循环的第一行时，你自然会想到“*当未到达流末尾时*”。在教程 5-6 中，你将完成一个使用此技术显示文件中所有项目的应用程序。

## 教程 5-6：使用循环读取到文件末尾

> 教程 5-6：使用循环读取到文件末尾

在本教程中，你将完成位于书籍示例程序 `Chap05` 文件夹下的 *South America* 应用程序。应用程序的表单已经创建，如图 36 所示。应用程序还有一个名为 `Countries.txt` 的辅助文件，存储在项目文件夹下的 `bin\Debug` 中。`Countries.txt` 文件包含了南美的国家名称。图 37 显示了文件在记事本中的外观。

# 图 36 南美洲应用程序的表单

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_704_0.png)

# 图 37 Countries.txt 文件

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_701_0.png)

# 南美应用中 Form1 的完整代码

```csharp
1 using System;
2 using System.Collections.Generic;
3 using System.ComponentModel;
4 using System.Data;
5 using System.Drawing;
6 using System.Linq;
7 using System.Text;
8 using System.Threading.Tasks;
9 using System.Windows.Forms;
10 using System.IO;
11
12 namespace South_America
13 {
14     public partial class Form1 : Form
15     {
16         public Form1()
17         {
18             InitializeComponent();
19         }
20
    private void getCountriesButton_Click(object sender, EventArgs e)
    {
        try
        {
            // 定义一个变量来存储国家名称。
            string countryName;

            // 声明一个 StreamReader 变量。
            StreamReader inputFile;

            // 打开文件并获取 StreamReader 对象。
            inputFile = File.OpenText("Countries.txt");

            // 清空 ListBox 中当前的所有项。
            countriesListBox.Items.Clear();

            // 读取文件内容。
            while (!inputFile.EndOfOfStream)
            {
                // 获取国家名称。
                countryName = inputFile.ReadLine();

                // 将国家名称添加到 ListBox。
                countriesListBox.Items.Add(countryName);
            }

            // 关闭文件。
            inputFile.Close();
        }
        catch (Exception ex)
        {
            // 显示错误消息。
            MessageBox.Show(ex.Message);
        }

    private void exitButton_Click(object sender, EventArgs e)
    {
        // 关闭表单。
        this.Close();
    }
}
```

```csharp
exitButton_Click(object sender, EventArgs e) 
{
    // 关闭表单。
    this.Close();
}
```

### 检查点

- 5.18 什么是输出文件？
- 5.19 什么是输入文件？
- 5.20 程序在使用文件时，必须采取哪三个步骤？
- 5.21 文本文件和二进制文件之间的区别是什么？
- 5.22 文件访问的两种类型是什么？这两种之间的区别是什么？
- 5.23 如果你想向文本文件写入，你会创建什么类型的对象？
- 5.24 如果你想从文本文件中读取，你会创建什么类型的对象？
- 5.25 如果你调用 File.CreateText 方法且指定的文件已存在，现有文件会发生什么？
- 5.26 如果你调用 File.AppendText 方法且指定的文件已存在，现有文件会发生什么？
- 5.27 本章讨论的 WriteLine 和 Write 方法之间的区别是什么？
- 5.28 你调用哪个方法来打开文本文件并从中读取数据？
- 5.29 文件的读取位置是什么？当打开输入文件时，读取位置最初在哪里？
- 5.30 如何从文本文件中读取一行文本？
- 5.31 如何关闭文件？
- 5.32 假设 inputFile 引用一个与打开文件关联的 StreamReader 对象。以下哪个循环的通用格式编写是正确的，可以读取文件中的所有项？

循环 A：

```csharp
while (inputFile.EndOfStream)
{
    // 从文件中读取一个项。
}
```

循环 B：

```csharp
while (!inputFile.EndOfStream)
{
    // 从文件中读取一个项。
}
```

## 5.7 OpenFileDialog 和 SaveFileDialog 控件

> 概念

> OpenFileDialog 和 SaveFileDialog 控件允许你的应用程序显示标准的 Windows 对话框，用于打开和保存文件。这些对话框允许用户轻松地指定文件名和位置。

到目前为止，本章中打开文件的应用程序都是将文件名指定为字符串字面量。然而，大多数 Windows 用户习惯于使用对话框来浏览磁盘以查找要打开的文件或保存文件的位置。你可以使用 OpenFileDialog 和 SaveFileDialog 控件为应用程序配备用于这些目的的标准 Windows 对话框。

### OpenFileDialog 控件

OpenFileDialog 控件显示一个标准的 Windows 打开对话框，如图 5-43 所示。打开对话框对于必须打开现有文件的应用程序来说是非常很有用的，因为它允许用户浏览系统并选择文件。

图 5-43 Windows 打开对话框

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_724_0.png)

#向项目中添加 OpenFileDialog 控件

要在表单上添加 OpenFileDialog 控件，请双击工具箱窗口中对话框（Dialogs）组下的 OpenFileDialog 工具。当控件被创建时，它不会显示在表单上，而是显示在设计器底部的组件托盘（component tray）区域。图 5-44 显示了 OpenFileDialog 控件在组件托盘中显示的示例。控件的默认名称为 OpenFileDialog1。与其他控件一样，你可以更改控件的 Name 属性来更改它的名称。

**图 5-44** 组件托盘中的 OpenFileDialog 控件。

# 显示打开对话框

在代码中，你可以通过调用 OpenFileDialog 控件的 ShowDialog 方法来显示打开对话框。例如，假设我们已经创建了一个 OpenFileDialog 控件并将其名称更改为 openFile。以下语句调用了 ShowDialog 方法：

```csharp
openFile.ShowDialog();
```

在大多数情况下，你需要知道用户是点击了打开按钮还是取消按钮来关闭对话框。ShowDialog 方法返回一个值，指示用户点击了哪个按钮。如果用户点击了打开按钮，返回 DialogResult.OK。如果用户点击了取消按钮，返回 DialogResult.Cancel。假设 openFile 是控件名称，以下是判断用户点击了打开按钮还是取消按钮的 if-else 语句示例：

```csharp
if (openFile.ShowDialog() == DialogResult.OK)
{
    // 用户点击了打开按钮。
}
else
{
    // 用户取消了操作。
}
```

# Filename 属性

当用户通过打开对话框选择文件时，路径和文件名存储在控件的 Filename 属性中。假设 openFile 是 OpenFileDialog 控件。以下代码显示了如何显示对话框并选择文件：

```csharp
StreamReader inputFile;
if (openFile.ShowDialog() == DialogResult.OK)
{
    // 打开了文件。
    inputFile = new StreamReader(openFile.FileName);
}
else
{
    // 操作已取消。
}
```

# InitialDirectory 属性

默认情况下，打开对话框显示 Documents 文件夹。可以通过 InitialDirectory 属性指定另一个目录。例如，以下代码显示 C:\Data：

```csharp
openFile.InitialDirectory = "C:\Data";
if (openFile.ShowDialog() == DialogResult.OK)
{
    // 打开了文件。
}
```

# Title 属性

默认情况下，打开对话框标题栏中显示“打开”。你可以通过控件的 Title 属性更改标题栏中显示的文本。

### SaveFileDialog 控件

SaveFileDialog 控件显示标准的 Windows 保存对话框，如图 5-45 所示。保存对话框允许用户浏览系统并为保存的文件选择位置和名称。

图 5-45 Windows 保存对话框

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_729_0.png)

#向项目中添加 SaveFileDialog 控件

SaveFileDialog 控件与 OpenFileDialog 控件有许多共同点。要在表单上添加 SaveFileDialog 控件，请双击工具箱窗口中对话框（Dialogs）组下的 SaveFileDialog 工具。当控件被创建时，它出现在设计器底部的组件托盘中。控件将被赋予一个默认名称，如 saveFileDialog1，但你可以通过 Name 属性更改名称。

# 显示保存为对话框

在代码中，你可以通过调用 SaveFileDialog 控件的 ShowDialog 方法来显示另存为对话框。例如，假设我们已经创建了一个 SaveFileDialog 控件并将其名称更改为 saveFile。以下语句调用了 ShowDialog 方法：

```csharp
saveFile.ShowDialog();
```

方法返回一个值，指示用户点击了保存按钮还是取消按钮以关闭另存为对话框。如果用户点击了保存按钮，返回 DialogResult.OK。如果用户点击了取消按钮，返回 DialogResult.Cancel。假设 saveFile 是控件名称，以下是判断用户点击了保存按钮还是取消按钮的 if-else 语句示例：

```csharp
if (saveFile.ShowDialog() == DialogResult.OK)
{
    // 用户点击了保存按钮。
}
else
{
    // 用户点击了取消按钮。
}
```

# Filename 属性

当用户在“另存为”对话框中指定位置和文件名时，文件的路径和文件名将存储在控件的 `Filename` 属性中。假设 `saveFile` 是一个 `SaveFileDialog` 控件的名称。

以下代码演示了如何显示“另存为”对话框，以及如果用户点击“保存”按钮关闭对话框，则打开所选的文件：

```csharp
StreamWriter outputFile;

if (saveFile.ShowDialog() == DialogResult.OK)
{
    // 创建所选文件。
    outputFile = File.CreateText(saveFile.Filename);

    // 向文件写入数据...
}
else
{
    MessageBox.Show("操作取消.");
}
```

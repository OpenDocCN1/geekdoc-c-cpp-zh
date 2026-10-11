
```cs
using System;
using System.Console;
using System.IO;
using System.Runtime.Serialization.Formatters.Binary;
using System.Runtime.Serialization;
class SerializableDemonstration
{
    static void Main()
    {
        const int END = 999;
        const string FILENAME = "Data.ser";
        Employee emp = new Employee();
        FileStream outfile = new FileStream(FILENAME,
            FileMode.Create, FileAccess.Write);
        BinaryFormatter formatter = new BinaryFormatter();
        Write("Enter employee number or " + END +
            " to quit >> ");
        emp.EmpNum = Convert.ToInt32(ReadLine());
        while (emp.EmpNum != END)
        {
            Write("Enter last name >> ");
            emp.Name = ReadLine();
            Write("Enter salary >> ");
            emp.Salary = Convert.ToDouble(ReadLine());
            formatter.Serialize(outfile, emp);
            Write("Enter employee number or " + END +
                " to quit >> ");
            emp.EmpNum = Convert.ToInt32(ReadLine());
        }
    }
}
```

**图 14-22** `SerializableDemonstration` 程序（继续）

# 第 14 章 文件与流

（续）

```cs
outFile.Close();
FileStream inFile = new FileStream(FILENAME,
FileMode.Open, FileAccess.Read);
WriteLine("\n{0,-5}{1,-12}{2}\n",
  "Num", "Name", "Salary");
while (inFile.Position < inFile.Length)
{
    emp = (Employee)formatter.Deserialize(inFile);
    WriteLine("{0,-5}{1,-12}{2}",
      emp.Num, emp.Name, emp.Salary.ToString("C"));
}
inFile.Close();
```

**图 14-22** `SerializableDemonstration` 程序

在图 14-22 中的 `SerializableDemonstration` 程序生成输出文件后，这些文件被重新打开用于读取。当输入文件的 `Position` 属性小于其 `Length` 时，将执行一个循环。换句话说，当文件中还有更多数据时，循环就会执行。图中最后一条阴影语句从文件中反序列化数据并将其强制转换为 `Employee` 对象，从而可以访问其各个字段。图 14-23 显示了程序的典型执行情况。

```
Enter employee number or 999 to quit >> 189
Enter last name >> West
Enter salary >> $45500
Enter employee number or 999 to quit >> 272
Enter last name >> Palmer
Enter salary >> $51200
Enter employee number or 999 to quit >> 387
Enter last name >> Wong
Enter salary >> $55000
Enter employee number or 999 to quit >> 426
Enter last name >> Lopez
Enter salary >> $61250
Enter employee number or 999 to quit >> 999

Num  Name       Salary

189 West       $45,500.00
272 Palmer     $51,200.00
387 Wong       $55,000.00
426 Lopez       $61,250.00
```

**图 14-23** `SerializableDemonstration` 程序的典型执行

Copyright 2018 Cengage Learning. All Rights Reserved. May not be copied, scanned, duplicated, in whole or in part. WCN-02-200-202

# 理解序列化与反序列化

`SerializableDemonstration` 程序创建的文件不像本章之前讨论的 `WriteSequentialFile` 程序创建的文本文件（图 14-11）那样容易读取。图 14-24 显示了在记事本中显示的文件内容（插入了一些换行符，以便输出能够适应本页）。如果你仔细检查该文件，可以识别出字符串名称和一些 `Employee` 类信息，但其余部分并不容易读取。

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_703_0.png)

图 14-24 使用 `SerializableDemonstration` 程序创建的数据文件

观看视频《理解序列化与反序列化》。

## 两个真理一个谎言

理解序列化与反序列化

- 1. 将数据写入文本文件的一个优点是可以在 Notepad 等文本编辑器中轻松读取数据。
- 2. 序列化是将对象转换为字节流的过程。反序列化是相反的过程；它将字节流转换为对象。
- 3. 默认情况下，所有的 C# 类都是可序列化的。

> 错误的陈述是 #3。默认情况下，所有的 C# 简单数据类型都是可序列化的，包括字符串。然而，如果你的类包含更复杂的字段，你必须检查这些类的声明以确保它们是可序列化的。默认情况下，并不是所有的 C# 类都是可序列化的。

## 你来做

### 在 GUI 环境中创建文本文件

本章中的文件读写示例使用了控制台应用程序，以便你能够在最简单的环境中专注于文件的特性。然而，你也可以在 GUI 环境中读写文件。在接下来的步骤中，你将创建两个应用程序。第一个允许用户使用 Form 表单输入发票记录并将其存储在文件中。第二个允许用户使用 Form 查看存储的记录。

- 1. 打开 Visual Studio IDE，并启动名为 **EnterInvoices** 的新 Windows Forms 项目。
- 2. 通过以下更改创建一个类似于图 14-25 所示的 Form：
    - 将 Form 的 `Text` 属性更改为 **Invoice Data**。
    - 向 Form 上拖入一个 Label，并将其 `Text` 属性更改为 **Enter data**。将 Label 的字体增大到 12。
    - 向 Form 上拖入三个 Label，并分别将它们的 `Text` 属性更改为 **Invoice number、Last name 和 Amount**。
    - 在描述性 Label 旁边向 Form 上拖入三个 TextBox。将这三个 TextBox 的 `Name` 属性分别更改为 **invoiceBox、nameBox 和 amountBox**。
    - 向 Form 上拖入一个 Button，将它的 `Name` 更改为 **enterButton**，并将它的 `Text` 更改为 **Enter record**。如有必要，调整 **enterButton** 的大小以便所有文本均可见。

| Invoice Data |

| --- |

| Enter data |

| Invoice number |

| Last name |

| Amount |

| Enter record |

**图 14-25** 设计 `EnterInvoices` Form

- 3. 查看 Form 的代码。在类的开始处，在 `Form1()` 构造函数之前，添加图 14-26 所示的阴影代码。新代码包含了执行以下操作的语句：
    - 声明一个用于分隔输出文件中记录的分隔符。
    - 声明一个路径和文件名。如果你想将文件存储在不同位置，可以更改路径。

```cs
namespace EnterInvoices
{
    public partial class Form1 : Form
    {
        const string DELIM = "@";
```

记住在字符串前放置符号 (@) 表示其字符应被视为字面量。@ 符号被用于文件名，以便路径中的反斜杠被解释为转义符。

- 4. 在文件顶部，在 `using` 语句处添加以便可以使用 `FileStream` 的声明：

`using System.IO;`

- 5. 保存并返回设计视图，如图 14-27 所示，双击 **Enter record** 按钮。在 `writer` 和 `outFile` 语句处添加在 `EnterButton_Click` 方法中。

```cs
private void EnterButton_Click(object sender, EventArgs e)
{
    num = Convert.ToInt32(invoiceBox.Text);
    name = nameBox.Text;
    amount = Convert.ToDouble(amountBox.Text);
    writer.WriteLine(num + DELIM + name + DELIM + amount);
    invoiceBox.Clear();
    nameBox.Clear();
    amountBox.Clear();
}
```

**图 14-27** `EnterInvoices` 程序的 `EnterButton_Click` 方法

- 6. 定位 `Dispose()` 方法，当用户点击关闭按钮时执行它。在 Visual Studio IDE 中定位该方法的方法是选择主菜单中的 **查找并替换**，并在对话框中输入 **Dispose**。（查找范围设置可以是整个解决方案或当前项目）。在图 14-28 所示的阴影语句处添加关闭 `writer` 和 `outFile` 的语句。

```cs
protected void Dispose(bool disposing)
{
    writer.Close();
    outFile.Close();
    if (disposing && (components != null))
    {
        components.Dispose();
    }
    base.Dispose(disposing);
}
```

**图 14-28** `EnterInvoices` 程序中的 `Dispose` 方法

- 7. 点击 **保存全部**。执行程序。当 Form 出现时，在每个 TextBox 中输入数据，然后点击 **Enter record** 按钮完成。TextBox 会清空，以便你输入另一条记录。在关闭 Form 前输入至少三条记录。表 14-29 显示正在输入数据。

## 从文件读取数据到 Form

在接下来的步骤中，你将创建一个可以文件中读取记录的 Form。

- 在 Visual Studio 中打开一个新的 Windows 项目并命名为 `ViewInvoices`。

通过以下更改创建一个类似于图 14-30 所示的 Form：

- 将 Form1 的文本更改为 Invoice Data。
- 根据图 14-30 所示的文本、大小和大致位置添加 Label1。（你可以点击组件 Text 属性旁边的向下箭头，以获得一个可以输入多行文本的框。）
- 添加一个文本为 View records 的按钮。如有必要，调整按钮的大小。将按钮命名为 `viewButton`。
- 添加三个 TextBox。分别将它们命名为 `invoiceBox、nameBox` 和 `amountBox`。

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_707_0.png)

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_707_1.png)

在 IDE 中，双击 View records 按钮查看代码。将 Click() 方法重命名为以大字母开头。

图 14-29 在 `EnterInvoices` 应用程序中输入数据

图 14-30 `ViewInvoices` Form

# 第 14 章 文件与流

（续）

4. 添加图 14-31 所示的阴影语句。它们包括：
   - `using System.IO` 语句
   - 文件分隔符字符和文件名的常量（如有必要，请更改文件路径）
   - 用于在记录拆分为字段之前读取记录的字符串
   - 用于存储已输入字符串中拆分后的独立字段的字符串数组
   - 一个用于处理输入文件的 `FileStream` 和 `StreamReader`
   - 在 `ViewButton_Click()` 方法中，用于从文件中读取一行并拆分为三个组件的语句

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
using System.IO;
namespace ViewInvoices{
    public partial class Form1 : Form {
        const char DELIM = ';';
        const string FILENAME = @"C:\CSharp\Chapter14\Invoices.txt";
        string recordin;
        string[] fields;
        static FileStream file = new FileStream(FILENAME, FileMode.Open, FileAccess.Read);
        StreamReader reader = new StreamReader(file);
        public Form1() {
            InitializeComponent();
        }
    }
```

图 14-31 `ViewInvoices` 程序的部分代码（续）

（续）

# 理解序列化与反序列化

（续）

```csharp
private void Button_Click(object sender, EventArgs e) {
    recordIn = reader.ReadLine();
    fields = recordIn.Split(DELIM);
    invoiceBox.Text = fields[0];
    nameBox.Text = fields[1];
    amountBox.Text = fields[2];
}
```

图 14-31 `ViewInvoices` 程序的部分代码

+   5. 在 `Form1Designer` 的 `Dispose()` 方法中添加两个 `Close()` 语句，如图 14-32 所示。

```csharp
protected override void Dispose(bool disposing) {
    reader.Close();
    file.Close();
    if (disposing && components != null) {
        components.Dispose();
    }
    base.Dispose(disposing);
}
```

图 14-32 `ViewInvoices` 程序的 `Dispose()` 方法

+   6. 保存项目并执行它。当表单出现时，点击按钮查看记录。查看你在运行 `EnterInvoices` 时输入的数据；你的表单应该像图 14-33 所示。点击按钮显示下一条记录。

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_709_0.png)

图 14-33 `ViewInvoices` 程序的典型执行

（续）

# 第 14 章 文件与流

（续）

7. 继续点击按钮查看每条记录。在查看完输入的最后一条记录后，再次点击按钮。这将产生一个未处理的异常，如图 14-34 所示，因为你尝试读取输入文件末尾之后的数据。

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_710_0.png)

图 14-34 用户尝试读取文件末尾后显示的错误消息窗口

取决于你正在使用的 Visual Studio 版本，你的错误消息可能与图 14-34 所示的不同。

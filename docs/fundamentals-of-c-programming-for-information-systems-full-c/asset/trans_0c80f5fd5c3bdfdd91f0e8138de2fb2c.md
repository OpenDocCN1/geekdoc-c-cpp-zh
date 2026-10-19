

Gina Rodriguez, 77, 88

你可以在文本编辑器中或使用程序创建这样一个文件。在任何一种情况下，在每一行的末尾都会自动插入一个不可见的新行字符。

让我们看看如何从名为 Exams.txt 的文本文件中读取上述数据。你使用 .txt 扩展名，这通常用来表示文件包含文本数据。

框架类库的 System.IO 命名空间中提供了多种类来处理文件和目录。你使用 StreamReader 类从文件中读取数据。文本文件中的数据被视为数据流——因此得名 StreamReader。

要从文本文件读取数据，你使用 StreamReader 类创建一个 StreamReader 对象。创建 StreamReader 对象的语句语法如下：

```
StreamReader VariableName = new StreamReader(@"Path and FileName");
```

new 关键字创建用于读取指定文件的 StreamReader 对象，并返回对该对象的引用。对象的引用（地址）存储在左侧指定的变量中。

## 为文件指定路径

如果未指定路径，则假定默认路径为 ProjectDirectory\Bin\DeBug。如果未指定路径，则无需使用前缀 @。如果找不到文件，将抛出异常。

例如，创建用于从 E:\Csharp\Exams.txt 读取的 StreamReader 对象如下：

```
StreamReader examsReader = new StreamReader(@"E:\Csharp\Exams.txt");
```

如果文件位于默认目录 Bin\Debug，则跳过路径：

```
StreamReader examsReader = new StreamReader("Exams.txt");
```

如果文件存储在默认文件夹 Bin\Debug 上方的某个文件夹中，你可以使用每个层级的 "..\"。以下是示例：
- "..\Exams.txt"——文件 Exams.txt 位于默认文件夹 Debug 上一级的 Bin 文件夹中。
- "..\..\Exams.txt"——文件位于默认文件夹 Debug 上两级的项目文件夹中。

## System.IO 的 using 指令

由于 StreamReader 类位于 System.IO 命名空间中，你必须在窗体中添加以下 using 指令：

```
using System.IO;
```

## ReadLine 方法

StreamReader 提供了一个名为 ReadLine 的方法，用于读取当前读取位置处的行，然后将位置推进到下一行。此方法在循环内使用，以顺序读取数据的每一行。这就是你如何使用循环读取每一行并在名为 lstDisplay 的 ListBox 中显示该行：

```
string currentLine;
while (examsReader.EndOfStream == false) // or. !examsReader.EndOfStream
{
    // Read current line and store it in a string variable
    currentLine = examsReader.ReadLine();
    lstDisplay.Items.Add(currentLine);    // Display the line
}
examsReader.Close();
```

## EndOfStream 属性

当当前读取位置位于文件末尾时，StreamReader 的 EndOfStream 属性的值为 true。上述代码中 while 循环的头部 while (examsReader.EndOfStream == false) 使用 EndOfStream 属性在 EndOfStream 为 true 时终止循环。也就是说，只要 EndOfStream 为 false，循环就会继续。

语句
    currentLine = examsReader.ReadLine();
读取当前行并将整行作为单个字符串存储在字符串变量 currentLine 中。在循环的第一次迭代结束时，字符串变量 currentLine 的值将为："Mike Burns, 75, 92"

因此，循环读取每一行，将其存储在字符串变量 currentLine 中，然后显示它以给出图 8-1 所示的输出。

## 图 8-1：Exams.txt 文件中的数据

```
Mike Burns, 75, 92
Cathy Arnold, 86, 95
Wesley Mathews, 82, 90
Jerry Luke, 70, 89
Gina Rodriguez, 77, 88
```

## 教程 1：读取文本文件

本教程读取并处理来自文件 Exams.txt 的姓名和考试成绩。

步骤 1-1：打开 Projects_Starts 文件夹中的项目 Ch8_FilesAndArrays。打开窗体 ReadTextFiles。图 8.2 显示了该窗体。

图 8-2：ReadTextFiles 窗体

![](img/143bad48262566137acc9c41f668a88f_248_0.png)

步骤 1-2：打开 Ch8_FilesAndArrays 项目目录的 Bin\Debug 文件夹中的文件 Exams.txt，并查看记录。关闭文件。

步骤 1-3：确保已添加 System.IO 命名空间，如图 8-3 所示。

图 8-3：带有 System.IO 命名空间的 using 指令

```
1 using System;
2 using System.Collections.Generic;
3 using System.ComponentModel;
4 using System.Data;
5 using System.Drawing;
6 using System.Linq;
7 using System.Text;
8 using System.Threading.Tasks;
9 using System.Windows.Forms;
10 using System.IO; //Add this statement
11 namespace Ch8_FilesAndArrays
```

步骤 1-4：将图 8-4 中的代码添加到 btnDisplayRecords 的 Click 事件处理程序中。请注意，在第 32 行，ListBox 的名称 lstDisplay 以字母“l”开头，而不是数字 1，尽管字体使其看起来像数字 1。

## 图 8-7：获取单个数据项的代码

```
private void btnComputPercent_Click(object sender, EventArgs e)
{
    float percentScore;
    string[] fields;
    string fmtStr, currentLine;
    // Create StreamReader object to read Exams.txt
    StreamReader examsReader = new StreamReader("Exams.txt");

    lstDisplay.Items.Clear();        //Clear ListBox
    // Print heading in the listbox
    fmtStr = "{0,-15}{1,8}{2,8}{3,8:N1}";
    lstDisplay.Items.Add(string.Format(fmtStr, "Name", "Exam1", "Exam2", "Percent"));

    while (examsReader.EndOfStream == false)
    {
        currentLine = examsReader.ReadLine();
        // Split currentLine to three string data items and store in a string array.
        fields = currentLine.Split(',');

        percentScore = (float.Parse(fields[1]) + float.Parse(fields[2]))/2;

        //display the three data items and student total in the List box
        lstDisplay.Items.Add(string.Format(fmtStr, fields[0], fields[1], fields[2],
                                            percentScore));
    }
    examsReader.Close();
}
```

让我们看一些关键语句：

## 第 52 行：currentLine = examsReader.ReadLine();

与之前的代码一样，此行读取当前行，并将整行作为单个字符串存储在字符串变量 currentLine 中。在循环的第一次迭代结束时，字符串变量 currentLine 的值将为：

![](img/143bad48262566137acc9c41f668a88f_251_0.png)

## 第 54 行：fields = currentLine.Split(',')

这是关键语句。由于 Split 方法返回一个字符串数组，因此在第 40 行变量 fields 被声明为对字符串数组的引用。在第一次迭代结束时，数组 fields 将如下所示：

![](img/143bad48262566137acc9c41f668a88f_251_1.png)

## 第 56 行：percentScore = (float.Parse(fields[1]) + float.Parse(fields[2]))/2;

来自元素 fields[1] 和 fields[2] 的两个成绩被转换为 float 类型并取平均值以计算百分比。百分比存储在 float 变量 percentScore 中。

## 第 59 行：lstDisplay.Items.Add(string.Format(fmtStr, fields[0], fields[1], fields[2], percentScore));

元素 fields[0] 给出姓名；fields[1] 和 fields[2] 分别给出 score1 和 score2。三个项目使用在第 47 行定义为 "{0,-15}{1,8}{2,8}{3,8:N1}." 的格式字符串 fmtStr 在 ListBox 中显示。名称使用格式代码 {0,-15} 中的 "-" 符号左对齐，并且百分比使用 {3,8:N1} 中的代码 N1 显示一位小数。

## 步骤 1-6：打开窗体 ReadTextFiles。打开 btnComputePercent 的 Click 事件处理程序。

- 添加图 8-7 中第 51–61 行的缺失代码。
- 在第 61 行的循环末尾设置一个断点。

确保 ListBox 的字体类型为等宽类型，如 Courier New。否则，列可能无法与正确格式化的代码均匀对齐。

## 步骤 1-7：运行项目。单击 Compute Percent 按钮。当程序中断时，查看 currentLine、fields 数组和 percentScore 的值。查看前几次迭代的数据。

## 注意文本文件末尾的隐藏空行！

如果你不小心按 Enter 键在文本文件末尾插入了一个空行，你将在第 56 行（percentScore = float.Parse(fields[1]) + float.Parse(fields[2]))/2;）处收到错误。这是因为当空行被拆分时，结果数组不具有像 fields[1] 和 fields[2] 这样的元素。

## 自己试试！

## 步骤 1-8：在 Exams.txt 末尾插入一个空行，如下所示，并保存文件。现在运行项目并单击 ComputePercent 按钮。你将收到“index was outside the bounds of the array.”的错误消息。重新打开 Exams.txt，删除空行并保存它。

![](img/143bad48262566137acc9c41f668a88f_252_0.png)

是时候练习了！做练习 8-1。

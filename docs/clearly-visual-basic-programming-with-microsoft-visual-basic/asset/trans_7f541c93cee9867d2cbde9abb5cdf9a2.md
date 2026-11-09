
```vb
' assign IDs and prices to the array
gifts(0).strId = "BX35"
gifts(0).intPrice = 13
gifts(1).strId = "CR20"
gifts(1).intPrice = 10
gifts(2).strId = "FE15"
gifts(2).intPrice = 12
gifts(3).strId = "KW10"
gifts(3).intPrice = 24
gifts(4).strId = "MM67"
gifts(4).intPrice = 4

' assign the product ID to a variable
strSearchFor = txtId.Text.ToUpper

' search the array for the product ID
' continue searching until there are
' no more array elements to search or
' the product ID is found
strFound = "N"
Do Until intSubscript = gifts.Length _
    OrElse strFound = "Y"
    If gifts(intSubscript).strId = strSearchFor Then
        strFound = "Y"
    Else
        intSubscript = intSubscript + 1
    End If
Loop

' determine whether the product ID
' was found in the array
If strFound = "Y" Then
    lblPrice.Text = gifts(intSubscript).intPrice.ToString("C0")
Else
    MessageBox.Show("Invalid product ID", _
        "Treasures Gift Shop", MessageBoxButtons.OK, _
        MessageBoxIcon.Information)
End If
End Sub
```

**图 22-18** *（接上页）*

## 顺序访问文件

除了从键盘获取数据并将数据发送到计算机屏幕之外，应用程序还可以从磁盘上的文件获取数据，并将数据发送到磁盘上的文件。从文件获取数据称为“从文件读取”，将数据发送到文件称为“写入文件”。

写入数据的文件称为**输出文件**，因为这些文件存储应用程序产生的输出。由计算机读取的文件称为**输入文件**，因为应用程序将文件中的数据用作输入。

大多数输入和输出文件由文本行组成，这些文本行按顺序读写——换句话说，按连续顺序，一次一行，从文件的第一行开始，到文件的最后一行结束。由于访问文本行的方式，这类文件称为**顺序访问文件**。

存储在顺序访问文件中的文本示例包括员工列表、备忘录或销售报告。你将在 Game Show Contestants 应用程序中使用顺序访问文件，该应用程序将在本章剩余部分中编写。

图 23-1 显示了该应用程序的用户界面。该界面提供了一个文本框，用于输入参赛者姓名。Write to File 按钮会将姓名写入顺序访问文件。Read from File 按钮会从顺序访问文件中读取每个姓名，并将其显示在 Contestants 框中。（txtContestants 控件的 Multiline 和 ReadOnly 属性设置为 True，其 ScrollBars 属性设置为 Vertical。）你将首先编写 Write to File 按钮的代码。

![](img/cf88270932e011575089da06b940a1d9_531_0.png)

图 23-1：Game Show Contestants 应用程序的用户界面

### 写入这些文本行

一条数据——例如字符串“Yolanda”——在人和计算机看来是不同的。对人来说，该字符串表示一个人的姓名；对计算机来说，它只是一个字符序列。程序员将字符序列称为**字符流**。在 Visual Basic 中，你使用 **StreamWriter 对象**将字符流写入顺序访问文件。在创建 StreamWriter 对象之前，首先要声明一个变量，用于在计算机内部存储器中存储该对象。图 23-2 显示了声明 StreamWriter 变量的语法和示例。语法中的 IO 代表“输入/输出”。

### 声明 StreamWriter 变量

```
Syntax
{Dim | Private} streamWriterVariableName As IO.StreamWriter

Example
Dim outFile As IO.StreamWriter
declares a StreamWriter variable named outFile
```

**图 23-2：** 声明 StreamWriter 变量的语法和示例

**要打开 Game Show Contestants 应用程序，然后开始编写该应用程序的代码：**

- 1. 启动 Visual Studio 2008（或 Visual Basic 2008 Express Edition）。打开 **Contestant Solution（Contestant Solution.sln）** 文件，该文件位于 ClearlyVB\Chap23\Contestant Solution 文件夹中。如有必要，打开设计器窗口。
- 2. 打开代码编辑器窗口，然后找到 btnWrite 控件的 Click 事件过程的代码模板。单击 ' declare a StreamWriter variable 注释下方的**空白行**。键入 **dim outFile as io.streamwriter**，然后按 **Enter**。

声明 StreamWriter 变量后，可以使用图 23-3 所示的语法创建 StreamWriter 对象。如图所示，创建 StreamWriter 对象涉及使用两种方法之一打开顺序访问文件：CreateText 或 AppendText。使用 **CreateText 方法**打开顺序访问文件以进行输出。当打开文件进行输出时，计算机会创建一个新的空文件，可将数据写入其中。如果文件已存在，计算机在向其中写入任何数据之前会先清除文件内容。使用 **AppendText 方法**打开顺序访问文件以进行追加。当文件以追加方式打开时，新数据会写入文件中任何现有数据之后。如果文件不存在，计算机会为你创建该文件。除了打开文件外，这两种方法都会自动创建一个 StreamWriter 对象，以在应用程序中表示该文件。将 StreamWriter 对象赋给一个 StreamWriter 变量，然后在代码中使用该变量引用文件。图 23-3 还包含使用 CreateText 和 AppendText 方法的示例。处理示例 1 中的语句时，计算机会在 C 盘的 ClearlyVB\Chap23 文件夹中搜索 pay.txt 文件。如果文件存在，则清除其内容并打开文件进行输出；否则，创建一个新的空文件并打开进行输出。该语句创建一个 StreamWriter 对象并将其赋给 outFile 变量。与示例 1 中的 *fileName* 参数不同，示例 2 中的 *fileName* 参数不包含文件夹路径。因此，计算机会在默认文件夹中搜索该文件，即当前项目的 bin\Debug 文件夹。在这种情况下，如果计算机在默认文件夹中找到 report.txt 文件，就会打开该文件进行追加。如果找不到该文件，则创建一个新的空文件，然后打开该文件进行追加。与示例 1 中的语句一样，示例 2 中的语句创建一个 StreamWriter 对象并将其赋给 outFile 变量。

**通过打开顺序访问文件创建 StreamWriter 对象**

```
Syntax
IO.File.method(fileName)
```

| 方法 | 说明 |
| --- | --- |
| CreateText | 打开顺序访问文件以进行输出 |
| AppendText | 打开顺序访问文件以进行追加 |

```
Example 1
outFile = IO.File.CreateText("C:\ClearlyVB\Chap23\pay.txt")
opens the pay.txt file for output; creates a StreamWriter object and assigns it to the outFile variable

Example 2
outFile = IO.File.AppendText("report.txt")
opens the report.txt file for append; creates a StreamWriter object and assigns it to the outFile variable
```

**图 23-3：** 通过打开文件创建 StreamWriter 对象的语法和示例

当用户单击 Game Show Contestants 应用程序中的 Write to File 按钮时，在 Name 框中输入的姓名应添加到文件中现有姓名的末尾；因此，你需要打开顺序访问文件以进行追加。用于存储参赛者姓名的文件，其描述性名称是 contestants.txt。虽然这不是硬性要求，但在命名顺序访问文件时通常使用“txt”（“text”的缩写）文件扩展名；这是因为这些文件包含文本。

**要继续编写 btnWrite 控件的 Click 事件过程：**

- 1. 单击 ' open the file for append 注释下方的**空白行**。
- 2. 键入 **outFile = io.file.appendtext("contestants.txt")**，然后按 **Enter**。

打开文件进行输出或追加后，就可以开始向其中写入数据。可以使用 **Write 方法**或 **WriteLine 方法**来完成；不过，在大多数情况下你会使用 WriteLine 方法。两种方法的区别在于，WriteLine 方法会在数据之后写入一个换行符。图 23-4 显示了这两种方法的语法和示例。如图所示，使用 Write 方法时，写入文件的下一个字符将紧跟在字符串“Hello”中的字母 o 之后出现。然而，使用 WriteLine 方法时，写入文件的下一个字符将出现在该字符串下一行。请注意，两种方法的语法中都不需要包含文件名。这是因为数据将写入与 StreamWriter 变量关联的文件。

### 将数据写入顺序访问文件

```
Syntax

streamWriterVariableName.Write(data)
streamWriterVariableName.WriteLine(data)

Example 1

outFile.Write("Hello")

Result

Hello|
the next character will appear immediately after the letter o

Example 2

outFile.WriteLine("Hello")

Result

Hello
|
the next character will appear on the next line
```

**图 23-4：** 将数据写入顺序访问文件的语法和示例


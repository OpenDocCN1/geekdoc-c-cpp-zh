
当你调用 `File.CreateText` 方法打开文件，且参数指定的文件已存在时，它会被擦除并创建一个同名的新空文件。例如，当你运行在教程 5-4 中完成的 `Friend` 应用时，每次点击 `Write` Name 按钮，`Friend.txt` 文件都会被擦除并创建一个新文件。

有时你希望保留现有文件并向其当前内容追加新数据。要向现有文件追加数据，请使用 `File.AppendText` 方法打开它。它的工作原理与 `File.CreateText` 方法类似，但如果文件已存在，则不会被擦除。写入文件的任何数据都会追加到现有文件的内容之后。

例如，文件 `Names.txt` 并包含图 5-26 所示的数据：

### 图 5-26 Names.txt 文件

![](img/8a88e1d8c69a687988c05f162ce32cac_317_0.png)

以下代码打开文件并追加了数据：

```csharp
1 StreamWriter outputFile;
2 outputFile = File.AppendText("Names.txt");
3 outputFile.WriteLine("Lynn");
4 outputFile.WriteLine("Steve");
5 outputFile.WriteLine("Bill");
6 outputFile.Close();
```

执行此代码后，`Names.txt` 文件包含图 5-26 所示的数据。

## 指定输出文件的位置

当你调用 `File.CreateText` 或 `File.AppendText` 方法来打开文件时，你将文件名作为字符串参数传递。如果你传递的文件名不包含文件路径，则该文件的位置将将是位于应用程序项目文件夹下的 `bin\Debug` 文件夹。你在教程 5-4 和 5-5 中在 Visual Studio 中打开 `Friend.txt` 文件时已经看到过这一点。

如果你想在不同的位置打开文件，可以在传递给 `File.CreateText` 或 `File.AppendText` 方法的参数中同时指定路径和文件名。如果你在字符串字面量中指定路径，请务必在路径前加上字符 `@` 字符。以下是一个示例：

```
StreamWriter outputFile;
outputFile = File.CreateText("C:\Users\Chris\Documents\Names.txt");
```

> 提示：你还可以让用户指定文件位置。有关 `SaveFileDialog` 控件的更多信息请参见第 5.7 节。

## 使用 StreamReader 对象从文件中读取数据

要从文本文件中读取数据，你需要创建一个 `StreamReader` 对象。然后你可以使用 `StreamReader` 类的 `ReadLine` 方法从文件中读取一行文本。例如，假设存在名为 `Students.txt` 的文件，其中包含图 5-29 所示的四个名称。

### 图 5-29 Students.txt 文件的内容

![](img/8a88e1d8c69a687988c05f162ce32cac_320_0.png)

假设你想编写一个程序，从 `Students.txt` 文件中读取这四个名称并在消息框中显示它们。你可以做到这一点。以下代码示例取自本书第 `Chap05` 文件夹下的 `Student Names` 项目。

```
1 try
2 (
3
4
5 // 声明一个变量来存储从文件中读取的项目。
6 string studentName;
7
8 // 声明一个 StreamReader 变量。
9 StreamReader inputFile;
10
11 // 打开文件并获取 StreamReader 对象。
12 inputFile = File.OpenText("Students.txt");
13 * *
// 读取并显示第一个名字。
13 studentName = inputFile.ReadLine();
14 MessageBox.Show(studentName);
16 // 读取并显示第二个名字。
17 studentName = inputFile.ReadLine();
18 MessageBox.Show(studentName);
20 // 读取并显示第三个名字。
21 studentName = inputFile.ReadLine();
22 MessageBox.Show(studentName);
24 // 读取并显示第四个名字。
25 studentName = inputFile.ReadLine();
26 MessageBox.Show(studentName);
28 // 关闭文件。
29 inputFile.Close();
30 }
31 catch (Exception ex)
32 {
33 // 显示错误消息。
34 MessageBox.Show(ex.Message);
35 }
```

让我们来看这段代码。

- **第 1 行：** 这是 `try-catch` 语句的描述。如果在打开文件或从文件中读取项目时发生问题，`try` 块将抛出异常。如果发生了这种情况，程序将跳转到第 31 行的 `catch` 子句。

- **第 4 行：** 该语句声明了一个名为 `studentName` 的字符串变量。每当我们从文件中读取一行文本时，都会将其赋值给该变量。

- **第 7 行：** 该语句声明了一个名为 `inputFile` 的变量，可用于引用一个 `StreamReader` 对象。

- **第 10 行：** 该语句打开我们正在读取的文件。它是通过调用 `File.OpenText` 方法并传递字符串 `"Students.txt"` 作为参数来实现的。`File.OpenText` 方法执行以下操作：

    - 打开一个由参数指定的现有文本文件。如果文件不存在，则会抛出异常。
    - 在内存中创建一个与文件关联的 `StreamReader` 对象。
    - 返回该 `StreamReader` 对象的引用。

注意，赋值运算符将 `File.OpenText` 返回的值分配给 `inputFile` 变量。这导致 `inputFile` 变量引用由该方法创建的 `StreamReader` 对象。

- **第 13 行：** 该语句调用 `inputFile.ReadLine` 方法，该方法读取文件的一行。该行文本作为字符串返回并赋值给 `studentName` 变量。此语句读取文件的第一行文本，`studentName` 变量被赋值为字符串 `"Joe Merrell"`。

- **第 14 行：** 该语句在消息框中显示 `studentName` 变量。

- **第 17 行和 18 行：** 第 17 行的语句从文件中读取下一行文本并将其赋值给 `studentName` 变量。在该行执行后，`studentName` 被赋值为字符串 `"Chris Rich"`。第 18 行的语句在消息框中显示 `studentName` 变量的内容。

- **第 21 行和 22 行：** 第 21 行的语句从文件中读取下一行文本并将其赋值给 `studentName` 变量。在该行执行后，`studentName` 变量被赋值为字符串 `"Kathryn Stevens"`。第 22 行的语句显示 `studentName` 变量的内容。

- **第 25 行和 26 行：** 第 25 行的语句从文件中读取下一行文本并将其赋值给 `studentName` 变量。在该行执行后，`studentName` 被赋值为字符串 `"Carly Colombo"`。第 26 行的语句在消息框中显示 `studentName` 变量的内容。

- **第 29 行：** 关闭文件。

### 5.6 使用文件存储数据

## 循环、文件与随机数

### 读取位置

当程序与输入文件工作时，内部会维护一个名为读取位置（read position）的特殊值。当打开输入文件时，该位置最初设置为开头。随着项目的读取，读取位置会向前移动。让我们通过之前的代码示例查看这种工作方式。

第 13 行的 `ReadLine` 调用读取文件的当前读取位置并赋值给 `studentName` 变量。在该行执行后，`studentName` 被赋值为字符串 `"Joe Merrell"`。

### 图 30 读取位置

![](img/8a88e1d8c69a687988c05f162ce32cac_322.png)

第 17 行的 `ReadLine` 方法读取文件的当前读取位置并将其赋值给 `studentName` 变量。在该行执行后，`studentName` 被赋值为字符串 `"Chris Rich"`。

### 图 31 读取位置

![](img/8a88e1d8c69a687988c05f162ce32cac_322.png)

第 21 行的 `ReadLine` 调用读取文件的当前读取位置并将其赋值给 `studentName` 变量。在该行执行后，`studentName` 变量被赋值为字符串 `"Kathryn Stevens"`。

### 图 32 读取位置

![](img/8a88e1d8c69a687988c05f162ce32cac_322.png)

第 25 行的 `ReadLine` 方法读取文件的当前读取位置并赋值给 `studentName` 变量。在该行执行后，`studentName` 被赋值为字符串 `"Carly Colombo"`。

### 图 33 读取位置

![](img/8a88e1d8c69a687988c05f162ce32cac_322.png)

> 注意：你是否注意到之前的代码示例是顺序从 `students.txt` 文件的开头到结束读取项目的？回顾一下我们在本节开始时讨论过的，这就是顺序访问文件的本质。

## 从文件中读取数值数据

记住当数据存储在文本文件中时，它是以文本编码的，使用如 Unicode 等方案。即使文件包含数字，这些数字在文件中也是作为一系列存储的。此外，当你使用 `StreamReader` 类的 `ReadLine` 从文本文件中读取项目时，它返回的是字符串。

假设一个文本文件包含数值数据，如图 5-35 所示。当我们使用 `ReadLine` 方法从文件中读取项目时，得到字符串 `"10"`、`20"` 和 `"30"`。如果我们需要对这些值进行数学运算，则必须将每个值从字符串转换为数值类型。可以使用你已经熟悉的 `Parse` 或 `TryParse` 系列方法来执行此转换。

### 图 35 包含数值数据的文本文件

![](img/8a88e1d8c69a687988c05f162ce32cac_323_0.png)

假设你想编写一个程序，从图 5-35 中的 `NumericData.txt` 文件读取三个数字，并在消息框中显示它们的总和。下面的代码示例演示了这一点。（该代码示例取自本书 `Chap05` 文件夹下学生示例程序中的 `Numeric Data` 项目。）

```c
try
{
    // 变量用于存储从文件中读取的数字
    // 以及它们的总和
    int number1,number2,number3, total;

    // StreamReader 变量。
    StreamReader inputFile;

    // 打开文件并获取一个 StreamReader 对象。
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
catch (Exception ex) {
    // 显示错误消息。
    MessageBox.Show(ex.Message);
}
```

让我们仔细观察这段代码：

- 第 1 行：这是 `try-catch` 语句的开始。`try` 块可能会抛出各种异常，导致程序跳转到第 27 行的语句块。

- 第 5 行：该语句声明了 `int` 变量 `number1`,`number2`,`number3` 和 `total`。这些变量保存了从文件中读取的三个值以及它们的总总和。

- 第 8–11 行：执行完这些语句后，`NumericData.txt` 文件被打开用于读取，`inputFile` 变量引用了一个与文件关联的 `StreamReader` 对象。

- 第 14 行：该语句调用 `inputFile.ReadLine` 方法从文件中读取一行文本。

- `inputFile.ReadLine` 方法返回的值（一个字符串）作为参数传递给 `int.Parse` 方法。

- `int.Parse` 方法返回的值被赋值给 `number1` 变量。

在该语句执行后，`number1` 变量被赋值从文件中读取的第一个值，并转换为 `int`。（`number1` 变量被赋值为 10。）

### 5.6 使用文件进行数据存储

- 第 15 行：该语句从文件中读取下一个值，将其转换为 `int`，并将结果赋值给 `number2` 变量。（`number2` 变量被赋值为 20。）

- 第 16 行：该语句从文件中读取下一个值，将其转换为 `int`，并将结果赋值给 `number3` 变量。（`number3` 变量被赋值为 30。）

- 第 19 行：该语句计算 `number1`、`number2` 和 `number3` 的和，并将结果赋值给 `total`。

- 第 22 行：该语句在消息框中显示数字之和。

- 第 25 行：该语句关闭文件。

### 使用循环读取文件并检测文件末尾

通常，程序必须在不知道文件中存储了多少项目的情况下读取文件内容。例如，假设你需要编写一个程序显示文件中的所有项目，但你并不知道文件中包含多少项目。你可以打开文件并使用循环反复读取项目。伪代码如下：

```
打开文件
当不在文件末尾时
  读取项目
  显示项目
关闭文件
```

`StreamReader` 对象有一个名为 `EOFStream` 的布尔属性，指示是否已到达文件末尾。如果文件已到末（没有更多数据），该属性被设置为 `true`；否则，它设置为 `false`。当你需要在不知道文件中包含多少项目的情况下读取所有项目时，可以使用该属性配合循环使用：

```csharp
while (inputFile.EOFStream == false)
{
    // 读取项目
    // 显示项目
}
```

然而，大多数程序员更喜欢使用以下逻辑：

```csharp
while (!inputFile.EOFStream)
{
    // 读取项目
    // 显示项目
}
```

记住 `!` 运算符是逻辑非运算符。当你读取文件的第一行时，自然会认为不在文件末尾。

## 教程 5-6：

### 使用循环读取到文件末尾

在本教程中，你将完成位于书中 `Chap05` 文件夹中的南美应用程序。该应用程序已经创建，并如图 5-36 所示。该应用程序还有一个名为 `Countries.txt` 的配套文件，存储在项目的 `bin\Debug` 文件夹下。文本文件包含了南美国家的名称。

[img/8a88e1d8c69a887988c05f162ce3cac_327_0]

当完成的应用程序运行时，用户点击 Get 按钮时，`ListBox` 应该会显示来自 `Countries.txt` 文件的国家名称。

第 1 步：切换回设计视图。在第 10 行插入 `using System.IO;` 指令。

第 2 步：打开 `Form1` 并双击 `getButton` 控件。在代码编辑器中，你会看到一个名为 `getCountriesButton_click` 的事件处理程序。

第 3 步：切换回设计视图并双击 `exitButton` 控件。在代码编辑器中，你会看到一个空的名为 `exitButton_click` 事件处理程序。

第 4 步：保存项目，然后按键盘上的 `F5` 或点击工具栏上的“启动调试”按钮来编译并运行应用程序。应用程序运行时，点击 Get Countries 按钮。`ListBox` 应该显示来自 `Countries.txt` 文件的国家名称，如图 5-38 所示。点击 Exit 按钮退出应用程序。

**图 5-38** 显示国家列表的南美应用程序

# 程序 5-6 South America 应用中 Form1 的完成代码

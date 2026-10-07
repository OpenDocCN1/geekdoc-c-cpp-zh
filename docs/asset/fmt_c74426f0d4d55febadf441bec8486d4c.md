
注意在此示例中，更新表达式是 `count += 10`。这意味着每次迭代结束时，`count` 增加了 10。

### 通过递减计数器反向计数

虽然计数器在计数控制循环中通常是递增，但你也可以递减计数器。例如，查看以下代码：

```cs
for (int count = 10; count >= 0; count--)
{
    MessageBox.Show(count);
}
```

在这个循环中，`count` 被初始化为 10。只要 `count` 大于等于 0，循环就会迭代。在每次迭代结束时，`count` 递减 1。第一次迭代期间 `count` 为 10，第二次迭代期间 `count` 为 9，依此类推。

### 避免在循环体中修改计数变量

不要在循环体中放置修改计数变量的语句。控制变量的所有修改都应该在更新表达式中进行，该表达式在每次迭代结束时自动执行。如果循环体语句也修改了计数变量，循环可能不会在你预期的时刻终止。例如，以下循环每次迭代增加两次 `count`：

```cs
for (int count = 1; count <= 10; count++)
{
    MessageBox.Show(count);
    count++; // 错误！
}
```

循环中你将使用计数变量来计算每小时英里的速度。

该项目名为“速度转换器”（Speed Converter），已经为你准备好了。它位于本书学生示例程序的 `Chap05` 文件夹中。应用程序的表单在运行时如图 5-14 所示。图中左侧的显示了控件的名称。右侧的显示了用户点击“显示速度”（Display Speeds）按钮后的表单。

### 图 5-14 速度转换器界面

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_661_0.png)

- **步骤 1:** 启动 Visual Studio。在本书学生示例程序的 `Chap05` 文件夹中打开名为 Speed Converter 的项目。
- **步骤 2:** 在设计器（Designer）中打开 `Form1` 表单。
- **步骤 3:** 在设计器中，双击 `displayButton` 控件。打开代码编辑器，你将看到一个名为 `displayButton_Click` 的空事件处理程序。通过输入程序 5-3（本教程末尾）中第 22-41 行的代码，完成 `displayButton_Click` 事件处理程序。

让我们仔细查看代码：

**第 23-26 行:** 这些语句声明了以下命名常量：
- `START_SPEED`，一个 `int` 类型常量，设置为 60。它是转换列表的起始速度，也是循环计数变量初始化的值。
- `END_SPEED`，一个 `int` 类型常量，设置为 130。它是转换列表的结束速度。当计数变量超过此值时，循环停止。
- `INTERVAL`，一个 `int` 类型常量，设置为 10。这是每次迭代后加到循环计数变量的数值。
- `CONVERSION_FACTOR`，一个 `double` 类型常量，设置为 0.6214。这是你在公式中用于将每小时公里（KPH）转换为每小时英里（MPH）的转换因子。

**第 29-30 行:** 这些语句声明了以下变量：
- `kph`，一个 `int` 类型变量，用于存储每小时公里的速度。
- `mph`，一个 `double` 类型变量，用于存储每小时英里的速度。

**第 33 行:** 这是 `for` 循环的开始，其工作方式如下：
**初始化:** `kph` 变量被初始化为 `START_SPEED` 的值，即 60。
**测试:** 在每次迭代开始时测试表达式 `kph <= END_SPEED`。
**更新:** 在每次迭代结束时执行表达式 `kph += INTERVAL`。这会将 `INTERVAL` 的值（即 10）加到 `kph` 变量上。

随着循环迭代，`kph` 变量被赋值为 60、70、80 等值，直直到 130。

**第 36 行:** 该语句将 `kph` 变量的值转换为每小时英里，并将结果赋值给 `mph` 变量。

**第 39-40 行:** 该语句向 `outputListBox` 控件添加一行，显示 `kph` 变量的当前值以及对应的每小时英里值。

- **步骤 4:** 将视图切换回设计器并双击 `exitButton` 控件。在代码编辑器中，你将看到一个名为 `exitButton_Click` 的空事件处理程序。通过输入程序 5-3 中第 46–47 行的代码，完成 `exitButton_Click` 事件处理程序。
- **步骤 5:** 保存项目。然后，按下键盘上的 F5 或点击工具栏上的“启动调试”按钮 (*) 来编译并运行应用程序。点击“显示速度”按钮，你应该能看到右图所示的输出。

图 5-14. 点击退出按钮关闭表单。

### 程序 5-3 速度转换器完整的 Form1 代码

```cs
1 using System;
2 using System.Collections.Generic;
```
```cs
3 using System.ComponentModel;
4 using System.Data;
5 using System.Drawing;
6 using System.Linq;
7 using System.Text;
8 using System.Threading.Tasks;
9 using System.Windows.Forms;
10
11 namespace Speed_Converter
12 {
13 partial class Form1 : Form
14 {
15 public Form1()
16 {
17 InitializeComponent();
18 }
19
20 private void displayButton_Click(object sender, EventArgs e)
21 {
22 // Constants
23 const int START_SPEED = 60;
24 const int END_SPEED = 130;
25 const int INTERVAL = 10;
26 const double CONVERSION_FACTOR = 0.6214;
27
28 // Variables
29 int kph; // Kilometers per hour
30 double mph; // Miles per hour
31
32 // Display the table of speeds.
33 for (kph = START_SPEED; kph <= END_SPEED; kph += INTERVAL)
34
{
35 // Calculate miles per hour.
36 mph = kph * CONVERSION_FACTOR;
37
38 // Display the conversion.
39 outputListBox.Items.Add(kph + " KPH = " + mph + " MPH");
40 }
41
42 private void exitButton_Click(object sender, EventArgs e)
43 {
44 this.Close();
45 }
46 //
47 
48 
49 }
50 }
```

## 5.6 使用文件进行数据存储

### 概念

当程序需要保存数据以备后后用时，它会将数据写入文件。稍后可以从文件中读取这些数据。

你到目前为止编写的程序每次运行时都需要要求用户重新输入数据，因为存储在变量和控制属性中的数据存储在 RAM（随机内存）中，一旦程序停止运行就会消失。如果程序要在多次运行之间保留数据，它就必须有一种保存数据的方法。数据保存在文件中，文件通常存储在计算机的磁盘上。一旦数据保存到文件中，在程序停止运行后它仍将留在那里。存储在文件中数据可以在以后被检索和使用。

你每天使用的大多数商业软件都将数据存储在文件中。以下是一些例子：
- **文字处理器**：文字处理程序用于写信、备忘录、报告和其他文档。这些文档随后保存在文件中，以便进行编辑和打印。
- **图像编辑器**：图像编辑程序用于绘制图形和编辑图像，例如你用数码相机拍摄的照片。你用图像编辑器创建或编辑的图像保存在文件中。
- **电子表格**：电子表格程序用于处理数值数据。数字和数学公式可以插入到电子表格的行和列中。电子表格随后可以保存到文件中供以后使用。
- **游戏**：许多电脑游戏将数据存储在文件中。例如，某些游戏会将玩家名称及其得分的列表保存在文件中。这些游戏通常按得分从高到低的顺序显示玩家名称。某些游戏允许你将当前的游戏状态保存到文件中，这样你就可以退出游戏，并在稍后恢复游戏，而无需从头开始。
- **网络浏览器**：有时当你访问 Web 页面时，浏览器会在你的计算机上存储一个名为 cookie 的小文件。Cookie 通常包含有关浏览会话的信息，例如购物篮的内容。

用于日常业务操作的程序高度依赖文件。薪资程序将员工数据保存在文件中，库存程序将公司产品数据保存在文件中，会计系统将公司财务运营数据保存在文件中，以此此类推。

程序员通常将将数据保存到文件的过程称为向文件写入数据。当一段数据被写入文件时，它从 RAM 中的一个变量复制到文件中。这如图 5-16 所示。“输出文件”（output file）一词用于描述向其中写入数据的文件。它被称为输出文件是因为程序将输出存储在其中。

### 图 5-16 向文件写入数据

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_673_0.png)

从文件中检索数据的过程被称为从文件中读取数据。当一段数据从文件中读取时，它会从文件复制到 RAM 中的一个变量中。图 5-17 阐明了这一点。“输入文件”（input file）一词用于描述从其中读取数据的文件。它被称为输入文件是因为程序从文件中获取输入。

### 图 5-17 从文件中读取数据

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_674_0.png)

在本节中，我们讨论了创建文件数据的方法。在使用文件时，总是要采取三个步骤：
- **打开文件**（OPEN）：打开文件会建立程序与文件之间的连接。如果你想向文件中写入数据，它是输出文件。
- **处理文件**（PROCESS）：当你从文件中读取数据时，它是输入文件。如果你想向文件中写入数据，它是输出文件。
- **关闭文件**（CLOSE）：当你完成使用文件后，必须关闭文件。这会断开程序与文件。

### 文件类型

通常，文件有两种类型：**文本文件**（text file）和**二进制文件**（binary file）。文本文件包含以文本编码的数据，你可以使用文本编辑器查看它。二进制文件包含未转换为文本的数据，它是文件。

### 访问方法

大多数编程语言提供了两种访问文件中存储数据的方式：**顺序访问**（sequential access）和**直接访问**（direct access）。当你使用顺序访问文件时，你从文件开始读取数据。如果你想直接跳转到文件中的任何数据，你可以使用直接访问（也称为随机访问），这类似于 CD 播放器的方式。

## 文件名和文件对象

磁盘上的文件由文件名标识。例如，当你使用 Windows 资源管理器查看文件内容时，你会看到名为 cat.jpg、notes.txt 和 resume.docx 的文件，如图 5-18 所示。

### 图 5-18 三个文件

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_676_0.png)

每个操作系统对命名都有自己的规则。许多系统（包括 Windows）支持扩展名，它是文件名末尾的短字符序列，前面有一个点（被称为“点”）。例如，图 5-18 中的文件具有 .jpg、txt 和 .docx 扩展。扩展通常指示文件中数据的类型。

为了让程序处理磁盘上的文件，程序必须创建一个对象。**文件对象**是一个与特定文件关联的对象，并为程序提供工作的方法。在程序中，变量与对象关联。我们说变量引用该对象。该变量用于对文件执行任何操作。这一概念如图 5-19 所示。

## 图 5-19 引用文件对象的变量

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_677_0.png)

你将使用 .NET Framework 中的两个类创建文件对象。当你想向文本文件写入数据时，使用 `StreamWriter` 类；当你想从文本文件读取数据时，使用 `StreamReader` 类。这些类位于 .NET Framework 中的 System.IO 命名空间中，因此你需要在程序的顶部编写以下指令：

```
using System.IO;
```

> 注意
> 在编程术语中，文件被视为数据流。在 C# 中，你使用 `StreamWriter` 对象打开流（如文件）并向写入数据。你使用 `StreamReader` 对象打开流（如文件）并从中读取数据。

## 使用 StreamWriter 对象向文件写入数据

你可以使用 `StreamWriter` 类的 `WriteLine` 方法向文件写入一行文本。假设你想编写一个创建一个名为 courses.txt 文件的程序，并将你正在修的课程名称写入文件中。以下代码示例显示了如何这样做：

```cs
1 StreamWriter outputFile;
2 outputFile = File.CreateText("courses.txt");
3
4 outputFile.WriteLine("Intro to Computer Science");
5 outputFile.WriteLine("English Composition");
```
```cs
6 outputFile.WriteLine("Calculus I");
7 outputFile.WriteLine("Music Appreciation");
9 outputFile.Close();
```

让我们来看每一行代码。

**第 1 行：** （注）该语句声明了一个名为 `outputFile` 的变量，它可以用于引用 `StreamWriter` 对象。

**第 2 行：** 简而言之，该语句打开了你要写入数据的文件。它是通过调用 `File.CreateText` 方法实现的，并将字符串 "courses.txt" 作为参数传递。`File.CreateText` 方法执行了以下操作：
- 它创建一个以参数指定的命的文件。如果文件已存在，其内容将被擦除。
- 它在内存中创建一个与文件关联的 `StreamWriter` 对象。
- 它返回 `StreamWriter` 对象的引用。

注意，赋值运算符将 `File.CreateText` 方法返回的值赋值给 `outputFile` 变量。这使得 `outputFile` 变量引用了由方法创建的 `StreamWriter` 对象。

在执行第 2 行语句后，磁盘上创建了 courses.txt 文件，内存中存在一个与该文件关联的 `StreamWriter` 对象，且 `outputFile` 变量引用了对象。

**第 4 行：** 该语句将字符串 "Intro to Computer Science" 写入 courses.txt 文件。它是通过调用 `StreamWriter` 类的 `WriteLine` 方法实现的，并将要写入文件的字符串作为参数传递的。当 `WriteLine` 方法向文件写入数据时，它会在数据后立即写入一个换行符。换行符是一个指定文本行结束的不可见字符。

**第 5 行：** 该语句将字符串 "English Composition" 写入 courses.txt 文件。

**第 6 行：** 该语句将字符串 "Calculus I" 写入 courses.txt 文件。

**第 7 行：** 该语句将字符串 "Music Appreciation" 写入 courses.txt 文件。

**第 9 行：** 该语句关闭了 courses.txt 文件。它是通过调用 `StreamWriter` 类的 `Close` 方法实现的。

在执行此代码后，我们可以使用文本编辑器打开 courses.txt 文件并查看其内容。图 5-20 显示了文件内容在记事本中的外观。

图 5-20 记事本显示的 courses.txt 文件内容

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_680_0.png)

## 使用 Write 方法写入数据

早些时候你读过 `StreamWriter` 类的 `WriteLine` 方法向文件写入项目数据并写入一个换行符。换行符指定文本行的结束。例如，下面的代码示例打开了一个名为 Example.txt 的文件，然后使用 `WriteLine` 方法将字符串 "One"、Two" 和 "Three" 写入文件。由于每个字符串后都写入了换行符，当在文本编辑器中查看时，字符串显示在不同的行上。图 5-21 左侧所示显示了文件在记事本中的外观。

## 图 5-21 使用 WriteLine 和 Write 方法写入的项目

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_681_0.png)

```cs
1 StreamWriter outputFile;
2 outputFile = File.CreateText("Example.txt");
3
4 outputFile.WriteLine("One");
5 outputFile.WriteLine("Two");
6 outputFile.WriteLine("Three");
7
8 outputFile.Close();
```

在某些情况下，你可能想向文件写入一个项目而不在其后立即紧跟换行符。`StreamWriter` 类提供了 `Write` 方法来实现此目的。它向文本文件写入项目数据而不写入换行符。图 5-21 右侧所示了生成的文件在记事本中的显示。

```cs
```

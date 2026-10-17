
```csharp
{
  try {
    // 声明一个变量存储国家名称。
    string countryName = "";
    // 声明一个 StreamReader 变量。
    StreamReader StreamReader = new StreamReader(inputFile);
    // 打开文件并获取 StreamReader 对象。
    inputFile = File.OpenText("Countries.txt");
    // 读取文件内容。
    string contents = "";
    while (!inputFile.EndOfStream) {
      // 获取一个国家名称
      countryName = inputFile.ReadLine();
      // 将名称添加到 ListBox 中。
      countriesListBox.Items.Add(countryName);
    }
    // 关闭文件。
    inputFile.Close();
  } catch (Exception ex) {
    // 显示错误消息。
    MessageBox.Show(ex.Message);
  }
}
private void exitButton_Click(object sender,
```

```csharp
EventArgs e)
55     {
56         // 关闭表单。
57         this.Close();
58     }
59  }
60 }
```

### 检查点

**5.41** Load 事件何时发生？

**5.42** 如何为 Load 事件创建事件处理程序？

### 关键术语

- 累加器 (accumulator)
- 二进制文件 (binary file)
- 主体 (body)
- 组件托盘 (component tray)
- 计数变量 (counter variable)
- 递减 (decrement)
- 直接访问文件 (direct access file)
- 文件对象 (file object)
- 文件名 (filename)
- 文件扩展名 (filename extensions)
- Name 属性 (Filename property)
- 递增 (increment)
- 初始目录属性 (InitialDirectory property)
- 初始化表达式 (initialization expression)
- 输入文件 (input file)
- `Items.Add` 方法
- `Items.Clear` 方法
- `Items.Count` 属性
- 迭代 (iteration)
- Load 事件 (Load event)
- 新行符 (newline character)
- Next 方法
- 打开对话框 (Open dialog box)
- OpenFileDialog 控件
- 输出文件 (output file)
- 后置模式 (postfix mode)
- 后测试循环 (posttest loop)
- 前置模式 (prefix mode)
- 前测试循环 (pretest loop)
- 伪随机数 (pseudorandom numbers)
- 随机访问文件 (random access file)
- 读取位置 (read position)
- ReadLine 方法
- 运行总计 (running total)
- 另存为对话框 (Save As dialog box)
- SaveFileDialog 控件
- 种子值 (seed value)
- 顺序访问文件 (sequential access file)
- StreamReader 类
- StreamWriter 类
- 测试 表达式 (test expression)
- 文本文件 (text file)
- Title 属性 (Title property)
- 更新表达式 (update expression)
- while 子句 (while clause)
- Write 方法
- WriteLine 方法

# 复习习题

### 单选题

- 1. ListBox 控件有一个方法可以擦除 Items 属性中的所有项。
  a. Items.Erase
  b. Items.Remove
  c. Items.Clear
  d. Items.Empty
- 2. ____ 通常用于控制循环迭代的次数。
  a. 计数变量
  b. 测试表达式
  c. while 子句
  d. 受控变量
- 3. ____ 循环在执行迭代之前测试其条件。
  a. 抢占式 (preemptive)
  b. 前测试 (pretest)
  c. 无限 (infinite)
  d. 逻辑 (logical)
- 4. ____ 术语用于描述被写入的文件。
  a. 输入文件
  b. 输出文件
  c. 保存的文件
  d. 用户文件
- 5. ____ 术语用于描述被读取的文件。
  a. 数据
  b. 写入
  c. 读取
  d. 输入
- 6. ____ 包含被编码的 ____。在 ____ 循环中。
  a. 文本
  b. 字符
  c. Unicode
  d. 顺序
- 7. 当你访问 ____ 文件时，从开始访问。
  a. 直接访问
  b. 随机访问
  c. 顺序访问
  d. 二进制访问
- 8. 磁盘上的文件通过 ____ 识别。
  a. 唯一标识符
  b. 文件名
  c. 序列
  d. 扩展
- 9. ____ 用于标记 ____。
  a. 累加器
  b. 目录
  c. 流
  d. 文件
- 10. ____ 术语用于描述从 ____ 读取。
  a. 输入
  b. 读取位置
  c. 读取
  d. 顺序
- 11. 当用户选择文件时，显示 ____ ____。
  a. 文件名
  b. 路径
  c. 名称
  d. 文本
- 12. ____ 对话框。
  a. SaveDialog
  b. FileDialog
  c. SaveFileDialog
  d. 标准
- 13. 一旦创建了 Random 对象，就可以调用它的 ____ 方法获取随机数。
  a. Generate
  b. Rand
  c. Next
  d. NextInteger
- 14. 在生成随机数时，____ 值用于序列。
  a. Start
  b. 种子
  c. Next
  d. 顺序
- 15. 当运行应用程序时，____ 事件发生。
  a. Startup
  b. Begin
  c. Load
  d. Initialize

# 判断题

1. 如果 ListBox 是空的，Items.Count 属性等于 -1。
2. while 循环被称为前测试循环，这意味着它在执行迭代之前会测试条件。
3. 递增变量意味着增加其值，递减变量意味着减少其值。
4. 当变量在 for 循环的初始化表达式中声明时，其作用域仅限于循环。
5. 即使布尔表达式为假，while 循环也会执行一次迭代。
6. 读取文件 术语用于描述被读取的文件。
7. 要向现有文件追加数据，你使用 AppendText 方法。
8. 当从文件中读取项时，位置会向前移动。
9. Random 类生成的数字是真正的随机的。
10. Load 事件在表单显示后发生。

# 简答题

1. 循环体中包含什么？
2. 写一条使用后置模式递增变量 `count` 的语句。
3. 如果 for 循环的测试表达式为假，会发生多少次迭代？
4. 什么是文件扩展名？它们指示了什么？
5. 当打开输入文件时，读取位置最初设置在哪里？
6. 在不知道文件中包含多少项的情况下，如何读取文件中所有的项？
7. 用于累加总数的变量称为？
8. 默认情况下，Open 对话框显示用户的文档目录。如何指定另一个要显示的目录？
9. 为什么系统时间是 Random 对象的优选种子值？
10. 什么样的代码应该放在 Load 事件中？

# 算法工作

1. 写一个循环显示10次你的名字。
2. 写一个循环显示 1 到 49 之间所有的奇数。
3. 写一个循环显示 0 到 100 之间每隔五个数字。
4. 写一个代码示例，使用循环将从10开始的数字写入文件。
5. 假设名为 People.txt 的文件包含姓名列表。写一个代码示例，使用 while 循环读取文件并在 ListBox 控件中显示其内容。

## 编程问题

### 1. 距离计算器

如果你知道车辆的速度和行驶的时间，就可以按照以下公式计算它行驶的距离：

距离 = 速度 × 时间

例如，如果一列火车以每小时 40 英里的速度行驶了 3 小时，则行驶距离为 120 英里。创建一个与图 5-51 所示表单类似的应用程序。用户在文本框中输入车辆的速度和行驶的小时。当用户点击“计算”（Calculate）按钮时，应用程序应使用循环在列表框中显示在该时间段每小时行驶的距离。

图 5-51 距离计算器应用程序

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_761_0.png)

### 2. 距离文件

修改你为编程问题 1 编写距离计算器程序，使其输出到文件，而不是在 ListBox 控件中显示。使用记事本或 Visual Studio 打开文件以确认输出结果。

### 3. 摄氏度转华氏度表

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_762_0.png)

假设 $C$ 是摄氏度温度，使用以下公式将温度转换为华氏温度（$F$）：

$F = \frac{9}{5}C + 32$

创建一个应用程序，显示 0–20 摄氏度及其对应的华氏度的表格。该应用程序应使用循环在列表框中显示温度。

### 4. 人口数量

创建一个预测生物群口近似数量的应用程序。该应用程序应使用文本框允许用户输入初始生物数量、平均每日人口增长率（百分比）以及生物留给繁殖的天数。例如，假设用户输入了以下值：
- 初始生物数量：2
- 平均每日增长率：30%
- 繁殖天数：10

应用程序应在 ListBox 控件中显示以下数据表：

| 天数 | 大似人口 |
|---|---|
| 1 | 2 |
| 2 | 2.6 |
| 3 | 3.38 |
| 4 | 4.394 |
| 5 | 5.7122 |
| 6 | 7.42586 |
| 7 | 9.653619 |
| 8 | 12.5497 |
| 9 | 16.31462 |
| 10 | 21.209 |

### 5. 分分工资

Susan 被聘佣了一份工作，她的雇主同意每天支付工资。雇主还同意 Susan 的工资第一天为 1 分钱，第二天为 2 分钱，第三天为 4 分钱，之后每天翻倍。创建一个应用程序，允许用户输入 Susan 工作的天数，并计算她在该期间将收到的总金额。

### 6. 海洋水位

假设海平面目前每年上升约 1.5 毫米，创建一个应用程序，显示未来 10 年海平面每年上升的毫米数。在 ListBox 控件中显示输出结果。

### 7. 消耗的热路里

在特定的跑步机上跑步，你每分钟消耗 3.9 卡路里。创建一个应用程序，使用循环显示在 10、15、20、25 和 30 分钟后消耗的卡路里数。在 ListBox 控件中显示输出。

### 8. 学费上涨

某大学全日制学生的每期学费为 6,000 美元。据宣布，学费将在未来五年内每年增长 2%。创建一个带有循环的应用程序，在 ListBox 控件中显示未来 5 年的预计每期学费。

### 9. 骰子模拟器

创建一个模拟掷两个骰子的应用程序。当用户点击按钮时，应用程序应生成两个在 1 到 6 之间的随机数来代表骰子的值。使用 PictureBox 控件显示骰子。（在学生示例程序的 Chap05 文件夹中，你会找到名为 Die1.bmp、Die2.bmp、Die3.bmp、Die4.bmp、Die5.bmp 和 Die6.bmp 的图像，你可以在 PictureBoxes 中使用它们）。

### 10. 加法教程

创建一个应用程序，生成两个随机整数，每个范围在 100 到 500 之间。这些数字应以加法题的形式显示在应用程序的表单上。表单应有一个文本框供用户输入问题的答案。当点击按钮时，应用程序应执行以下操作：
- 检查用户的输入并显示消息指示是否为正确答案。
- 生成两个新的随机数，并在表单上的新问题中显示它们。

### 12. 随机数猜游戏

创建一个在 1-100 范围内生成随机数的应用程序，并让用户猜是多少。如果用户的猜测大于随机数，程序应显示“太大了，再试一次”（Too high, try again）。如果用户的猜测小于随机数，程序应显示“太小了，再试一次”（Too low, try again）。如果用户猜对了数字，应用程序应该祝贺用户并生成一个新的随机数。可选增强：增强游戏记录猜测次数。

### 13. 计算数字阶乘

在数学中，符号 $n!$ 表示 $n$ 的阶乘。$n$ 的阶乘是从 1 到 $n$ 的所有非负整数的乘积。例如，
$7! = 1 \times 2 \times 3 \times 4 \times 5 \times 6 \times 7 = 5,040$
以及
$4! = 1 \times 2 \times 3 \times 4 = 24$
创建一个应用程序，让用户输入一个非负整数，然后循环计算该数字的阶乘。在标签或消息框中显示阶乘。

### 14. 随机文件写入器

创建一个应用程序，将一系列随机数写入文件。每个随机数应在 1-100 范围内。应用程序应允许用户指定文件包含多少个随机数，并使用 SaveFileDialog 控件让用户指定文件名和位置。

### 15. 随机文件读取器

此练习假设你已完成问题 14 随机文件写入器。创建一个应用程序，使用 OpenFileDialog 控件让用户选择上一个应用程序创建的文件。该应用程序应从文件中读取数字，在 ListBox 控件中显示这些数字，然后显示以下数据：
- 数字的总和
- 从文件中读取的随机数数量

图 6-1 和 6-2 通过比较两个程序来阐释这一思想：一个是使用一个长且复杂的事件处理程序，其中包含了解决问题所需的所有语句；另一个是将问题划分为多个较小的问题，每个问题都由一个独立的方法处理。

# 图 6-1 使用一个长语句序列来执行任务

# 图 6-2 使用方法分而治之解决问题

```csharp
namespace Example
{
    public partial class Form1 : Form
  {
```

```csharp
private void myButton_Click(object sender, EventArgs e)
{
    Method2();
    Method3();
    Method4();
    // Event Handler
}
```

```csharp
private void Method2()
{
    statement;
    statement; // Method 2
    statement;
}
```

在程序程序中，任务被分成了更小的任务，每个任务都由一个独立的方法执行。

```csharp
private void Method3()
{
    statement;
    statement; // Method 3
    statement;
}
```

```csharp
private void Method4()
{
    statement;
    statement; // Method 4
    statement;
}
```

```csharp
}

}
```

通俗地说，将程序分成较小的代码单元（如方法）的程序被称为模块化程序。模块化倾向于简化代码。如果某个特定任务在程序的多个地方被执行，可以只写一次方法来执行该任务，然后在需要时随时执行。使用方法的这种优势被称为**代码重用**，因为你只需要编写一次执行任务的代码，然后在每次需要执行该任务时重用它。

# void 方法和有返回值的方法

在本章中，你将学习编写两种类型的方法：void 方法和有返回值的方法。当你调用 void 方法时，它仅仅是执行其包含的语句然后终止。当你调用一个有返回值的方法时，它会执行其包含的语句，然后将一个值返回给调用它的语句。

Parse 方法是有返回值方法的良好示例。

你将学习编写的第一类方法是 void 方法。

## 6.2 void 方法

> **概念**
> void 方法执行一个任务，然后终止。它不会向调用它的语句返回值。

要创建一个方法，你需要编写它的定义。方法定义包含两个部分：头部和方法体。**方法头部**出现在方法定义的开头，它列出了关于方法的几个重要信息，包括方法的名称。**方法体**是执行方法时执行的一系列语句。这些语句被封装在一组大括号内。这里是一个方法定义的示例：

```csharp
private void DisplayMessage()
{
    MessageBox.Show("This is the DisplayMessage method.");
}
```

# 方法头部

使用之前显示的方法定义，图 6-3 指出了方法头部的不同部分，头部是第一行。

图 6-3 方法头部的部分

| 访问修饰符 | 返回类型 | 方法名 | 括号 |
| --- | --- | --- | --- |
| private | void | DisplayMessage | () |

```csharp
private void DisplayMessage() {
    MessageBox.Show("This is the DisplayMessage method.");
}
```

让我们仔细观察图中识别出的部分：

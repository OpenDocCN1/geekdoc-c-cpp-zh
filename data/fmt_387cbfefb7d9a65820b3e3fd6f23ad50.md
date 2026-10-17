
```csharp
public partial class Form1 : Form
{
    // 存储 PhoneBookEntry 对象列表的字段。
    private List<PhoneBookEntry> phoneList =
        new List<PhoneBookEntry>();

    public Form1()
    {
        InitializeComponent();
    }

    // Read 方法读取 Phone.txt 文件的内容
    // 并将其作为 PhoneBookEntry 对象
    // 存储在 phoneList 中。
    private void Read()
    {
        try {
            StreamReader inputFile; // 用于读取文件
            string line; // 用于存储文件中的一行

            // 为了读取文件
            StreamReader inputFile; // To read the file
            string line; // To hold a line from the file

            // 读取 Phone.txt 文件的内容
            // 并将其作为 PhoneBookEntry 对象
            // 存储在 phoneList 中。
            // The Read method reads the contents of the
            // Phone.txt file and stores it as PhoneBookEntry
            // objects in the phoneList.

            // 创建 PhoneBookEntry 结构的一个实例。
            // Create an instance of the PhoneBookEntry structure.
            PhoneBookEntry entry = new PhoneBookEntry();

            // 创建分隔符。
            // Create a delimiter.
            char[] delim = { ',' };

            // 打开 PhoneBook.txt。
            // Open the file.
            inputFile = File.OpenText("PhoneBook.txt");

            // 读取文件中的行。
            // Read the lines from the file.
            while (!inputFile.EndOfStream) {
                // 读取文件中的一行。
                // Read a line from the file.
                line = inputFile.ReadLine();

                // 对行进行分词。
                // Tokenize the line
                string[] tokens = line.Split(delim);

                // 将标记赋值给 entry 的 name。
                // Assign the tokens to the entry.
                entry.name = tokens[0];

                // 将标记赋值给 entry 的 phone。
                // Assign the tokens to the entry.
                entry.phone = tokens[1];

                // 将 entry 添加到 phoneList。
                // Add the entry to phoneList.
                phoneList.Add(entry);
            }
        } catch (Exception ex) {
            // 显示错误消息。
            // Show an error message.
            MessageBox.Show(ex.Message);
        }
    }

    // DisplayNames 方法显示 listBox 中的名称。
    // The DisplayNames method displays the names in listBox.
    private void DisplayNames()
    {
        foreach (PhoneBookEntry entry in phoneList)
        {
            // 将名称添加到 listBox。
            // Add the name to listBox.
            listBox.Items.Add(entry.name);
        }
    }
}
```

## 8.4 枚举类型

**概念：** 枚举类型是一种用户定义的类型，它由被称为枚举符的常量组成。

有时，在程序中，你需要表示某些值。例如，假设你有星期几（星期日、星期一等），你需要一种方法来表示它们，尽管这种方法有缺点。处理这类数据的更好方案是创建一个枚举类型。这是一个枚举类型的示例：

```csharp
enum Day { Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday }
```

必须使用枚举成员的全限定名称，因为在多个枚举类型中可能存在相同的枚举名称。这里是另一个示例：

```cs
Day weekendDay = Day.Saturday;
```

此语句声明了一个名为 `weekendDay` 的变量，并将其初始化为 `Day.Saturday`。

下面的代码显示了另一个示例。（假设应用程序表单有一个名为 `mondayRadioButton` 的单选按钮控件。）

```cs
1 Day selectedDay;
2 if (mondayRadioButton.Checked)
3 {
4 selectedDay = Day.Monday;
5 }
```

在这段代码中，`Day` 声明了一个名为 `selectedDay` 的变量。第 2 行的语句判断 `mondayRadioButton` 控件是否选中。如果是，第 4 行的语句将 `Day.Monday` 赋值给 `selectedDay` 变量。下面的代码显示了如何与枚举值和枚举成员进行比较。

你可以查看一个示例。（假设 `selectedDay` 是一个 `Day` 类型的变量。）

```cs
1 if (selectedDay == Day.Wednesday)
2 {
3 Message.Show("Halfway through the week!");
4 }
```

第 1 行的语句判断 `selectedDay` 变量是否等于 `Day.Wednesday`。如果是，第 3 行将显示一个消息框。

下面的代码显示了如何在 `switch` 语句测试枚举变量。（假设 `selectedDay` 是一个 `Day` 类型的变量。）

```cs
1 switch (selectedDay)
2 {
3 case Day.Sunday:
4 Message.Show("Rest.");
5
6 break;
7 case Day.Monday:
8 Message.Show("Back to work.");
9 break;
10 case Day.Tuesday:
11 Message.Show("Just a regular work day.");
12 break;
13 case Day.Wednesday:
14 Message.Show("Halfway through the week.");
15 break;
16 case Day.Thursday:
17 Message.Show("Almost there.");
18 break;
19 case Day.Friday:
20 Message.Show("Last day!");
21 break;
22 case Day.Saturday:
23 Message.Show("Sleep late today.");
24 break;
25 }
```

在第 1 行中，`switch` 语句测试 `selectedDay` 变量。根据变量的值，程序将跳转到相应的 `case` 语句。

### 使用枚举成员或枚举变量的 ToString 方法

枚举成员和枚举变量都有一个 `ToString` 方法。当你调用枚举成员的 `ToString` 方法时，它会以字符串的形式返回枚举的名称。例如，下面的代码将在消息框中显示字符串 "Sunday"：

```cs
MessageBox.Show(Day.Sunday.ToString());
```

当你调用枚举变量的 `ToString` 方法时，它会将变量所包含的值名称以字符串的形式返回。例如，下面的代码将在消息框中显示字符串 "Thursday"：

```cs
Day today = Day.Thursday;
MessageBox.Show(today.ToString());
```

当你使用 `+` 运算符连接字符串和枚举变量时，会隐式调用该变量的 `ToString` 方法。当你对 `int` 变量使用 `+` 运算符也会发生相同的情况。`int` 变量的 `ToString` 方法会被隐式调用。这是一个示例：

```cs
Day today = Day.Thursday;
MessageBox.Show("Today is " + today);
```

此代码将在消息框中显示字符串 "Today is Thursday"。

在教程 8-6 中，你完成了一个使用枚举类型来表示光谱颜色的应用程序。

![](img/8a88e1d8c69a687988c05f162ce32cac_533_0.png)

# 教程 8-6：完成色彩光谱应用程序

助记法 ROY G BIV 通常用于帮助记忆可见光谱的以下颜色序列：红、橙、黄、绿、蓝、靛和紫。在本教程中，你将完成显示这些颜色的色彩光谱（Color Spectrum）应用程序。如果你点击颜色，应用程序将显示该颜色的名称。

已经为你创建好的应用程序表单如图 8-17 所示。颜色实际上是一组 `Label` 控件，通过它们的 `BackColor` 属性来设置合适的颜色。

图 8-17 色谱应用程序的表单

| orangeLabel | yellowLabel | greenLabel | blueLabel | indigoLabel |

| --- | --- | --- | --- | --- |

![](img/8a88e1d8c69a687988c05f162ce32cac_533_1.png)

# 第 8 章 更多数据处理

**步骤 1：** 启动 Visual Studio（或 Visual Studio Express）。打开 Student Programs 中 Chap08 文件夹下名为 `Color Spectrum` 的项目。

**步骤 2：** 在代码编辑器中打开 `Form1` 的代码。编写 `Spectrum` 枚举类型的声明，如程序 8-7 的第 13–17 行所示。确保将声明写在 `Color_Spectrum` 命名空间内，完全如图所示。

**步骤 3：** 编写 `DisplayColor` 方法的注释和代码，位于程序 8-7 的第 26–31 行。注意程序 8-7 的第 28 行，该方法有一个 `Spectrum` 类型参数。当你调用此方法时，传递一个枚举成员作为参数。

**步骤 4：** 接下来为 `Label` 控件创建 `Click` 事件。回到设计器并双击 `redlabel` 以创建一个名为 `redlabel_Click` 的事件程序。通过编写程序 8-7 第 35 行所示的语句来完成事件。

**步骤 5：** 对剩余的 `Label` 控件重复此过程，编写程序 8-7 中所示的剩余 `Click` 事件。

**步骤 6：** 保存项目。然后，按下键盘上的 F5 或点击启动调试来编译并运行应用程序。当应用程序运行时，点击表单上的颜色以确认应用程序运行正常。完成后，点击退出应用程序。

# 程序 8-7 色彩光谱应用程序的 Form1 完成代码

```cs
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace Color_Spectrum
{
    enum Spectrum
    {
        Red, Orange, Yellow, Green,
        Blue, Indigo, Violet
    }

    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
    }
}
```

# 8.4 枚举类型

```cs
// DisplayColor 方法显示
// 颜色的名称。
private void DisplayColor(Spectrum color)
{
    colorLabel.Text = color.ToString();
}
private void redLabel_Click(object sender, EventArgs e)
{
    DisplayColor(Spectrum.Red);
}
private void orangeLabel_Click(object sender, EventArgs e)
{
    DisplayColor(Spectrum.Orange);
}
private void yellowLabel_Click(object sender, EventArgs e)
{
    DisplayColor(Spectrum.Yellow);
}
private void greenLabel_Click(object sender, EventArgs e)
{
    DisplayColor(Spectrum.Green);
}
private void blueLabel_Click(object sender, EventArgs e)
{
    DisplayColor(Spectrum.Blue);
}
private void indigoLabel_Click(object sender, EventArgs e)
{
    DisplayColor(Spectrum.Indigo);
}
private void violetLabel_Click(object sender, EventArgs e)
{
    DisplayColor(Spectrum.Violet);
}
```

## 8.4 枚举类型

枚举器和枚举变量可以直接与整数值进行比较。例如，以下代码显示了“星期日等于零”的消息。

```csharp
if (Day.Sunday == 0)
{
    MessageBox.Show("Sunday is equal to zero.");
}
```

### 使用枚举变量遍历数组元素

由于枚举器表示整数值，因此它们可以用于循环遍历数组中的元素。例如，查看以下代码：

```csharp
decimal[] sales = {
    1000, 2000, 3000, 4000,
    5000, 6000, 7000
};
for (Day dayCount = Day.Sunday; dayCount <= Day.Saturday; dayCount++)
{
    MessageBox.Show("Sales for " + dayCount + " were " +
    sales[(int)dayCount].ToString(""));
}
```

第 1 行和第 2 行创建了一个名为 `sales` 的 `decimal` 数组。`for` 循环从第 4 行开始，使用名为 `dayCount` 的变量作为其计数变量。注意关于循环的以下几点：

- `DayCount` 初始化为 `Day.Sunday`。

- 只要 `Day` 小于等于 `Day.Saturday`，循环就会继续。

- 在每次迭代结束时，`dayCount` 都会加增。

在第 7 行中，`(int)dayCount` 被用数组下标。随着循环的执行，它将显示以下消息：

- Sales for Sunday were $1,000.00

- Sales for Monday were $2,000.00

- Sales for Tuesday were $3,000.00

- Sales for Wednesday were $4,000.00

- Sales for Thursday were $5,000.00

- Sales for Friday were $6,000.00

- Sales for Saturday were $7,000.00

## 检查点

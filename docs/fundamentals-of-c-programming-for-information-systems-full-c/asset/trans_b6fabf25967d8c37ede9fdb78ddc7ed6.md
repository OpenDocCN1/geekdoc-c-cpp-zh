

将其中一个整数强制转换为 float 类型会得到正确的结果：

```
float average = 25f/10;
```

25f/10 的结果为 float 类型，即两种类型中较大的那一种，从而得到正确的结果。2.5。

因此，当你用一个整数除以另一个整数时，至少其中一个必须强制转换为实数类型，才能得到带小数部分（如果有）的结果。

步骤 1-9：将以下语句添加到 Compute Total 按钮的单击事件处理程序中，运行程序并观察 average 的值：

```
float average = 25 / 10;    //yields 2
```

将表达式改为 25f/10f，并查看值的差异（2.5）。

将表达式改为 25f/10，结果为 2.5。

删除该语句。

## 使用大整数的乘法

使用大整数进行乘法可能会产生意想不到的后果：

```
int price = 3000;
int quantity = 1000000;
long cost = price * quantity;
```

乘积 3000 * 1000000 为 30 亿。然而，由于两个 int 类型（price * quantity）的乘积表示为 int，其限制约为 21.5 亿，结果超出限制并产生错误结果。

步骤 1-10：添加以下语句，运行程序并注意 cost 的值。

```
int price = 3000;
int quantity = 1000000;
long cost = price * quantity;
```

删除语句。

cost 的值不正确，因为结果为 int 类型，其限制约为 21.5 亿，对于 3000,000,000（30 亿）的结果来说太小了。

## C# 中的一个奇特现象

当操作涉及 short 或 sbyte 类型时，这些类型在执行操作之前会自动转换为 int 类型。因此，结果将为 int 类型。

```
short exam1 = 80;
sbyte exam2 = 90;
short total = exam1 + exam2; // Error! The result is int type (odd!), whereas total is short type
```

你可以将结果强制转换为 short，如

```
short total = (short) (exam1 + exam2);
```

由于使用 sbyte 和 short 时存在这种奇怪的行为，通常你可以使用 int 类型来表示所有在 int 范围内的整数，除非在内存使用是关注点时。

是时候练习了！做练习 2-1。

## 复习问题

2.1 哪种实数数据类型最适合在需要精确表示数字的财务计算中使用？

2.2 与 decimal 相比，float 和 double 类型的优势是什么？

2.3 哪种数据类型具有最大的范围？

2.4 哪种数据类型具有最大的大小（内存）？

更正以下语句中的错误，如有：

2.5 double sales = 2560.50;

2.6 float cost = 2.50;

2.7 float units = 45000;

2.8 sbyte quantity = 200;

2.9 decimal price = 300;
float currentPrice = price;

2.10 short units = 2500;
int quantity = units;

2.11 int qty1 = 1000000000;
int qty2 = 2000000000;
long total = qty1 + qty2;

2.12 float total = 255.50 + 500;

2.13 以下代码旨在计算平均值：
int totalScore = 25;
int count = 4;
float average = total/count;

2.14 decimal price = 100;
float quantity = 5.5;
decimal netCost = price*quantity - 10;

## 2.3 使用字符串和字符

在本节中，你将学习如何使用 string 类型和字符类型的数据和变量。C# 中的 string 类型表示零个或多个字符的组合。“John Adams”和“P410-2023-3180-05”是 string 类型数据的示例。请注意，字符串用引号括起来。

## 值类型和引用类型

我们在第 1 章中讨论的整数和实数类型称为值类型，因为这些类型的每个变量都持有该变量内存位置中的实际值 t。

相比之下，字符串（以及其他对象如数组）称为引用类型，因为这些类型的每个变量只保存对数据的引用——即数据的内存位置或地址，而不是实际数据。引用类型将在第 7 章后面讨论。

为了理解如何使用字符串，让我们看一个通过组合以下三个字符串类型数据来创建用户名的应用程序：

- 1. 姓氏的前 5 个字符
- 2. 名字的第一个字符
- 3. id 的最后两位数字

图 2-4 显示了名为 UserNameString 的用户界面窗体。

## 图 2-4：UserNameString 窗体

![](img/143bad48262566137acc9c41f668a88f_83_0.png)

## 教程 2：字符串操作

本教程创建了图 2-4 中所示的 UserNameString 窗体。主要目标是学习字符串操作。

步骤 2-1：打开 Tutorial_Starts 文件夹中的项目 Ch2_DataTypes。打开窗体 UserNameString。为了便于理解代码，代码中使用的控件名称在表 2-3 中显示。

## 表 2-3：窗体 UserNameString 上的控件

| 用途 | 控件类型 | 属性 | 设置 |
| 输入姓氏 | TextBox | Name | txtLname |
| 输入名字 | TextBox | Name | txtFname |
| 输入 id | TextBox | Name | txtId |
| 创建用户名 | Button | Name | btnUserName |
| 显示用户名 | Label | Name | lblUserName |

图 2-5 显示了创建用户名的代码。

## 图 2-5：创建用户名的代码

```
20  private void btnUserName_Click(object sender, EventArgs e)
21  {
22      string lName = txtLname.Text;  // Get input data
23      string fName = txtFname.Text.Trim();
24      string id = txtId.Text.Trim();
25      string userName;
26      // Combine three strings to get the user name
27      userName = lName.Substring(0, 5).ToLower() + fName.Substring(0, 1).ToLower() +
                  id.Substring((id.Length - 2), 2);
29      // Alternate way using the Concat method;
30      userName = string.Concat(lName.Substring(0, 5).ToLower(), fName.Substring(0, 1).ToLower(),
                  id.Substring((id.Length - 2), 2));
32      lblUserName.Text = userName;
33  }
```

让我们看看这些语句的作用。

第 22-24 行从 TextBoxes 获取输入数据并将数据保存到变量中。

第 27 行从姓氏、名字和 id 中提取所需的子字符串；将其转换为小写；并组合起来形成用户名。

string 类型有大量的方法和属性来帮助处理字符串。我们首先查看上述程序中使用的这些方法和属性。

lName.Substring(0, 5).ToLower() 将姓氏的前五个字符转换为小写。同样，ToUpper() 转换为大写。

## 连接字符串

两个或多个字符串可以使用“+”运算符连接，如

```
String fullName = "G " + "C " + "Philip"
```

fullName 的值将为“G C Philip”。这是第 27 行计算用户名时使用的方法：

```
userName = lName.Substring(0, 5).ToLower() +
    fName.Substring(0, 1).ToLower() + id.Substring((id.Length - 2), 2);
```

## 步骤 2-3：在第 27 & 28 行添加计算用户名的语句。运行窗体进行测试。

将 fName 的 Substring 方法的参数改为 3 和 1，如

```
fName.Substring(3, 1).
```

观察用户名的变化。

输入大写姓氏以及带前导和尾随空格的姓氏，并观察输出。输入不同长度的 id。

连接字符串的另一种选择是使用 string 的 Concat() 方法，如

```
String fullName = String.Concat("G ", "C ", "Philip");
```

结果为“G C Philip”。

第 30 行使用 Concat 方法组合字符串：

```
30  userName = string.Concat(lName.Substring(0, 5).ToLower(),
    fName.Substring(0, 1).ToLower(),id.Substring((id.Length - 2), 2));
```

## 步骤 2-4：添加图 2-5 中的第 30 到 32 行以完成程序，并测试代码。

进行以下每项更改，运行程序，并描述它对输出的影响以及原因。

将 lName.Substring(0, 5) 中的参数 (0, 5) 改为 (0,4)。

将上述同一组参数改为 (2, 3)。

将参数 ((id.Length - 2), 2)) 改为 ((id.Length - 1), 1))。

## String() 方法的附加方法

## Replace (string, string) 方法：将第一个字符串（如果有）替换为第二个字符串。

示例：lName = lName.Replace(" ", null);


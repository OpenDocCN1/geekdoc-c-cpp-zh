

使用有意义的名称为变量命名以使程序易于阅读。你应避免使用未被广泛认可的缩写或首字母缩写。例如，使用 totalQuantitySold 而不是 tqs。

## 用于保存其他类型数据的变量

我们正在查看的图 1-18 中的代码示例不包括用于保存其他类型数据的变量，如字符和字符串数据。每种类型的变量都使用相同的语法声明。以下是创建字符和字符串变量的语句示例：

```
char middleInitial;
string lastName;
```

## 为变量赋值

创建变量后，你可以使用以下形式的语句为其赋值

```
variable name = value (or an expression that computes a value)
```

例如，程序中声明为类型 int 的变量 scoops 可以使用语句将其赋值为 3

```
scoops = 3
```

也就是说，值 3 将存储在名为 scoops 的内存位置中，如下所示表示：

![](img/143bad48262566137acc9c41f668a88f_45_0.png)

同样，语句

```
scoops = (10/5) + 1
```

会将值 3 赋给 scoops。

## 变量的生命周期

你不能使用不存在的变量！这意味着你不能在变量声明之前使用它，因为变量仅在创建声明语句后才存在。

同样，变量在声明它的方法的执行完成后就不再存在。因此，在方法内声明的变量的生命周期是其在方法执行期间在内存中创建的时间到方法执行完成的时间之间的时间段。一般来说，生命周期表示变量在内存中创建到销毁之间的时间段。

一个相关的术语是变量的作用域，即可以在程序中访问该变量的部分。变量的作用域是从变量声明到下一个右大括号之间的语句块。变量的作用域将在第 1.10 节中进一步讨论。

## 表示数字

## 科学计数法

你可以使用科学计数法表示非常大的数字：

```
3.95e8
```

e8 表示 10 的 8 次方。因此，3.95e8 等于 3.95 乘以 10⁸——即 395,000,000。

同样，3.95e-8 表示 3.95 乘以 10 的 -8 次方——即 0.0000000395。

数字只能包含数字、十进制点、减号和加号，以及使用科学计数法时的字母“e”或“E”。逗号和美元符号 ($) 在数字中无效。因此，以下语句无效：

```
double unitPrice = $1.50;    //Invalid; dollar sign is not allowed in a number
double cost = 3,520.00;      //Invalid; comma is not allowed in a number
double amount = "15.45";   //Invalid; "15.45" is a string
```

注意！一般来说，当你将错误类型的值赋给变量时，编译器不喜欢这样。以下语句会导致错误，因为 scoops 声明为类型 int，即整数类型，但 1.5 是实数。

```
int scoops = 1.5    //Invalid; 1.5 is not an integer
```

我们将在第 2 章中查看混合不同类型的整数和实数类型的具体规则。

## 将一个变量的值赋给另一个变量

你可以将一个变量的值赋给另一个变量，如以下示例所示：

```
int scoops = 3;
int temp;
temp = scoops;
```

语句“temp = scoops”将 scoops 的值复制到变量 temp 中。执行此语句后，两个变量的存储位置都将包含相同的值 3：

![](img/143bad48262566137acc9c41f668a88f_47_0.png)

如果在上述代码之后添加以下语句更改 scoops 的值会怎样？

```
scoops = 5;
```

它会改变 temp 的值吗？答案是否定的，因为每个变量都有自己的存储位置。执行语句“scoops = 5”后，两个变量将具有以下值：

![](img/143bad48262566137acc9c41f668a88f_47_1.png)

## 1.10 在标签中格式化和显示输出

你在标签中看到的内容是其 Text 属性的值。早在步骤 1-10 中，你已在设计器窗口中使用其 Text 属性在标签中显示文本。现在我们来看如何使用代码在运行时在标签中显示文本。为此，你将文本赋给标签的 Text 属性。

第 36 行的语句，

```
lblCost.Text = cost.ToString("C");
```

通过将其赋给 lblCost 的 Text 属性，将 cost 的值显示在标签 lblCost 中。

cost 的值是 double 类型，使用变量的 ToString() 方法将其转换为字符串，接下来将描述该方法。

## 使用 ToString() 方法格式化数字

每种数值数据类型都有一个名为 ToString() 的方法（程序单元），它将数字转换为字符串并格式化。例如，

```
cost.ToString()
```

会将 cost 的值转换为字符串，以便在标签中显示。

ToString() 方法还允许指定格式代码（字符串），例如

```
cost.ToString("C")
```

其中“C”指定货币格式。

使用其他 ToString() 格式代码的示例在表 1-7 中给出。

## 表 1-7：ToString() 格式代码

| Number | Format string | ToString() would format the number as |
| 1145.857 | null | 1145.857 |
| 1145.857 | "C" | $1,145.86 |
| 1145.857 | "N" | 1,145.86 |
| 1145.857 | "F" | 1145.86 |
| 0.156 | "P" | 15.60% |
| Optionally, you may specify the number of decimal places. Here are some examples: |
| 1145.857 | "C0" | $1,146 |
| -1145.857 | "C1" | ($1,145.9) |
| -1145.857 | "N1" | -1,145.9 |
| 1145 | "N3" | 1,145.000 |
| Format code for integers only |
| 157 | "D5" | 00157 |
| 157 | "D" | 157 |
| 157 | "D1" | 157 |

如果格式代码未指定小数位数，如 cost.ToString("C") 中，默认的小数位数为两位。

## 步骤 2-5：添加显示 cost 的语句：

```
lblCost.Text = cost.ToString("C");
```

btnComputeCost_Click 事件处理程序应如下图 1-21 所示。

## 图 1-21：btnComputeCost 按钮的单击事件处理程序

```
20    private void btnComputeCost_Click(object sender, EventArgs e)
21    {
22        /*Compute the total cost for an order of icecream
23            using the formula: cost = unitPrice * NumberOfScoops:
24            Declare variables to hold input data and computed results*/
25        int scoops;
26        double unitPrice, cost;
27
28        //Get input data from Text Boxes:
29        scoops = int.Parse(txtScoops.Text);
30        unitPrice = double.Parse(txtUnitPrice.Text);
31
32        // Compute result
33        cost = unitPrice * scoops;
34
35        // Display Result
36        lblCost.Text = cost.ToString("C");
```

## 步骤 2-6：运行表单：

双击 program.cs 打开代码编辑器窗口。
指定 IceCreamCost 为要运行的表单的名称，如下所示：

    Application.Run(new IceCreamCost());

单击工具栏上的开始按钮运行表单。
输入 3 作为 scoops，3.95 作为 unitPrice。单击计算成本按钮查看结果。
关闭窗口。

通过单击 IceCreamCost.cs 选项卡返回到代码编辑器窗口。
将格式字符串“C”更改为“C0”，运行程序并观察格式差异。

重复使用格式字符串“C1”、“N”和“F”，并观察每种情况下的格式。

在未输入单价数据的情况下运行表单。程序在第 30 行中断，并显示如下错误消息，因为 txtUnitPrice.Text 是一个空字符串。

```
unitPrice = double.Parse(txtUnitPrice.Text);
```

// Compute result
cost = unitPrice * scoops;

// Display Result

FormatException was unhandled
An unhandled exception of type 'System.FormatException' occurred in mscorlib.dll
Additional information: Input string was not in a correct format.


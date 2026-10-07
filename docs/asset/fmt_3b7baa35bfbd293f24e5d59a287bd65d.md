
```csharp
30  bool inputGood = false;
31  // Try to convert both
32  inputs to decimal.
33  if
34  decimal.TryParse(grossPay.Text, out pay)
35  {
36      if
37  decimal.TryParse(bonus.Text, out bonus)
38      {
39          // Both inputs
40          are good;
41          inputGood = true;
42      }
43      else
44      {
45          // Display error for bonus.
46          MessageBox.Show("Bonus is
47          invalid.");
48      }
49  }
50  else
51  {
52      // Display error for pay.
53      MessageBox.Show("Gross is
54      invalid.");
55  }
56  // Return the result.
57  return inputGood;
58  }
59  private void
60  calculateButton_Click
61  {
62      // Variables for gross
63      pay, bonus, and contributions
64      decimal grossPay = 0m,
65      bonus = 0m, contributions = 0m;
67      if (InputIsValid(ref grossPay, ref bonus)
68  {
69          // Calculate the
70          amount of contribution.
71      contributions = (grossPay + bonus) *
72      CONTRIB_RATE;
73  }
74      // Display the contribution.
75      contributionLabel.Text = contributions.ToString("c");
76  }
77  
78  private void
79  exitButton_Click(object sender,
80  e)
81  {
82      // Close the form.
83      this.Close();
84  }
85 }
```

# 从方法返回字符串

到此为止，你已经看到了返回数字和布尔值的方法的示例。你可以编写返回任何类型数据的方法。让我们来看一个返回字符串的示例。`Chap06` 文件夹包含一个名为 `Full Name` 的项目。图 6-26 显示了应用程序的表单，Program 6-10 显示了代码。当你运行应用程序时，在 `TextBox` 控件中输入你的名、中间和姓。当你点击 `Name` 按钮时，你的姓名将显示在 `fullNameLabel` 控件中。

# 图 6-26 Full Name 应用程序的表单

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_852_0.png)

`showFullNameButton` `exitButton`

# Program 6-10 Name 应用程序中 Form1 表的代码

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
10
11 namespace Full_Name
12 {
13     public partial class Form1 : Form
14     {
15         public Form1()
16         {
17             InitializeComponent();
18         }
19
20         // The FullName method accepts
21         arguments for a first
22         // name, a middle name, and a last
23         name. It returns
24         // the full name.
25         private string FullName(string
26         first, middle, last)
27         {
28             return first + " " + middle + " "
29             " " + last;
30         }
31
32         private void
33         showFullNameButton_Click(object sender,
34         EventArgs e)
35         {
36             // Variables to hold the first,
37             middle, last, and full names
38             string first, middle, last,
39             full;
40             // Get the first, middle, and
41             last names;
42             first = firstNameTextBox.Text;
43             middle = middleNameTextBox.Text;
44             last = lastNameTextBox.Text;
45             // Get the full name.
46             full = FullName(first, middle,
47             last);
48             // Display the full name.
49             fullNameLabel.Text = full;
50         }
51     }
52 }
```

```csharp
4445 private void exitButton_Click(object
46 sender, EventArgs e)
47 {
48 // Close the form.
49 this.Close();
50 }
51
```

第 23–26 行定义了一个名为 `FullName` 的方法。注意关于该方法的几点：

- 它的返回类型是 `string`。
- 它有三个 `string` 参数：名、中间名姓。当我们调用方法时，我们将名、中间名和姓作为参数传递。
- 第 25 行返回一个字符串，该字符串是名、中间名和姓参数拼接的结果，它们之间插入了空格。

图 6-27 显示了用户在每个 `TextBox` 中输入名称并点击“Show Full Name”按钮后的应用程序表单示例。

# 图 6-27 Full Name 应用程序示例输出

### 检查点

**6.15** 什么是返回值的方法？它是如何使用的？

**6.16** 布尔方法返回什么内容？

**6.17** 方法可以写成返回任何类型的数据吗？

# 6.6 调试方法

### 概念

`Visual Studio` 调试命令允许你逐方法单步执行应用程序。“逐入”`Step Into`命令允许你单步执行被调用的方法。“逐过”`Step Over`命令允许你执行方法调用而不逐行执行其内部代码。“逐出”`Step Out`命令允许你执行正在调试的方法的所有剩余行，而无需逐行执行。

在[第 3 章](#)中，你学习了如何在应用程序代码中设置断点并单步执行代码。让我们来看看如何步入方法、跳过方法以及从方法中跳。

当应用程序处于中断模式`break mode`时，“逐入”命令会执行当前高亮的行`执行点`。如果该行包含对方法的调用，则下一行高亮将是该方法的第一行。换句话说，“逐入”命令允许你在方法被调用时对其单步执行。使用以下程序之一激活“逐入”命令：

- 按 `F11` 键
- 从菜单栏中选择“调试”`Debug`，并在“调试”菜单中选择“逐入”`Step Into`
- 如果工具栏可见，点击调试工具栏上的“逐入”按钮 ` `

与“逐入”命令一样，“*逐过命令*也会执行当前高亮的行。然而，如果该行包含方法调用，方法将执行完毕而不逐行执行其语句。使用以下程序之一激活*逐过*命令：

- 按 `[F10]` 键。
- 从菜单栏中选择*调试*，然后在*调试*菜单中选择*逐过*。
- 如果*工具栏*可见，点击*调试工具栏*上的*逐过*按钮 `?`。

在对方法进行单步执行时，如果你希望方法的剩余部分完成执行而不逐步执行，请使用*逐出命令*。方法完成后，方法调用之后的行将会被高亮，你可以继续单步执行。使用以下程序之一激活*逐出*命令：

- 按 `[Shift] + [F11]` 键。
- 从菜单栏中选择*调试*，然后在*调试*菜单中选择*逐出*。
- 如果*工具栏*可见，点击*调试工具栏*上的*逐出*按钮 `?`。

> 提示
>
> `Visual Studio` 可以以不同的方式配置。在某些配置下，“逐入”命令可能通过 `[F8]` 功能键激活。同样，在某些配置下，“逐过”命令可能通过 `[Shift] + [F8]` 键激活。同样，“逐出”命令可能通过 `Control + Shift + F8` 键激活。要找出使用了哪些键，请在点击“调试”菜单时仔细查看这些命令。

在教程 6-6、6-7 和 6-8 中，你将练习使用这些命令中的每一个。

# 教程 6-6：练习“逐入”命令

在本教程中，你将使用教程 6-5 中的 `Pay and Bonus` 项目来练习单步执行方法。

> 视频笔记 教程 6-6：练习“逐入”命令

- **步骤 1：** 打开教程 6-5 中的 `Pay and Bonus` 项目。
- **步骤 2：** 打开代码编辑器，并在图 6-28 所示的 `calculateButton_Click` 事件程序中的某行设置断点。

图 6-28 断点位置

```csharp
private void calculateButton_Click(object sender, EventArgs e)
{
    // 用于总薪、奖金和缴款的变量
    decimal grossPay = 0, bonus = 0, contributions = 0;

    if (IsValid(ref grossPay, ref bonus))
    {
        // 计算缴款金额。
        contributions = (grossPay + bonus) * CONTRIB_RATE;

        // 显示缴款。
        contributionLabel.Text = contributions.ToString("c");
    }
}
```

> > 提示
>
> 当鼠标指针位于代码行左侧边隙时点击即可设置断点。

你也可以将光标移动到想要设置断点的行，然后按 `F9`。

- **步骤 3：** 按 `F5` 键运行应用程序。
- **步骤 4：** 点击“逐过”命令。
- **步骤 5：** 点击“逐入”命令。
- **步骤 6：** 按“逐入”命令。
- **步骤 7：** 点击“逐过”命令。

执行这些程序之一后，应用程序将退出中断模式并恢复执行。

# 教程 6-7：练习“逐过”命令

# 图 6-29 断点位置

```csharp
Form1.cs
Pay_and_Bonus.cs
private void calculateButton_Click(object sender, EventArgs e)
{
    // 用于总薪、奖金和缴款的变量
    decimal grossPay = 0, bonus = 0, contributions = 0;

    if (IsValid(ref grossPay, ref bonus))
    {
        // 计算缴款金额。
        contributions = (grossPay + bonus) * CONTRIB_RATE;

        // 显示缴款。
        contributionLabel.Text = contributions.ToString("c");
    }
}
```

# 教程 6-8：练习“逐出”命令

# 图 6-30 断点位置

```csharp
void calculateButton_Click(object sender
```

命令。

**步骤 5：** 因为你按了 `F11`，接下来将高亮 `InputIsValid` 方法的第一行。再次按 `F11` 键将进入方法的下一行。

**步骤 6：** 现在你不再继续单步执行方法，而是将跳出方法。按 `Shift + F11` 键执行“调出”`Step Out`命令。在执行 `InputIsValid` 方法中剩余语句时，单步执行将暂停。你将返回到包含方法调用的 `calculateButtonClick_Click` 事件处理程序。

**步骤 7：** 现在你可以退出断点模式并恢复正常执行。请执行以下程序之一：

- 点击工具栏上的“继续”`Continue`按钮。
- 按 `F5`。
- 点击菜单栏上的“调试”`Debug`，然后点击“继续”`Continue`。

执行完上述任何一种程序后，应用程序将退出断点模式并恢复正常执行。点击应用程序表单上的“退出”`Exit`按钮以结束执行。

> ### 提示
>
> 当当前执行点不包含方法调用时，“逐入”`Step Into`和“逐过程”`Step Over`命令的效果是相同的。

### 关键术语

- 参数 `arguments`
- 代码复用
- 默认参数
- 分治法
- 方法体
- 模块化程序
- 具名参数
- 输出参数
- 参数 `parameter`
- 参数变量
- 帕斯卡命名法 `Pascal case`
- 按引用传递
- 按值传递
- 引用参数
- 返回点
- 返回类型
- 逐入命令 `Step Into command`
- 调出命令 `Step Out command`
- 逐过程命令 `Step Over command`
- 逐步细化
- 自顶向下设计
- 返回值的方法
- `void` 方法

### 复习题

### 单选题

- 1. 一般来说，将程序分成更小的代码单元（如方法）的程序被称为(n) ______。
  a. 面向对象程序
  b. 模块化程序
  c. 过程程序
  d. 方法驱动程序
- 2. 编写代码执行一次任务，然后在每次需要执行该任务时复用它，是使用方法的好处，被称为 ______。
  a. 代码复用
  b. 单次使用哲学
  c. 方法回收
  d. 代码重处理
- 3. 当你调用(n) ______ 时，它只需执行包含的语句然后终止。
  a. 内置方法
  b. 空方法
  c. 逻辑方法
  d. `void` 方法
- 4. 出现在方法定义开头的 ______ 列出了关于该方法的若干重要信息，包括方法的名称。
  a. 方法标题
  b. 方法描述
  c. 方法头
  d. 方法声明
- 5. ______ 是一组封装在大括号内的语句集合，在方法执行时被执行。
  a. 方法体
  b. 方法指定
  c. 方法代码
  d. 方法分类
- 6. ______ 是系统在调用方法时保存的内存地址，是方法结束后系统应该返回的位置。
  a. 调用地址
  b. 方法地址
  c. 返回点
  d. 返回位置
- 7. 程序员通常使用一种被称为 ______ 的技术将算法分解为多个方法。
  a. 原型设计
  b. 方法建模
  c. 算法划分
  d. 自顶向下设计
- 8. 发送到方法中的数据被称为 ______。
  a. 参数 `arguments`
  b. 引用
  c. 方法变量
  d. 数据项
- 9. ______ 是一种特殊变量，在方法被调用时接收参数。
  a. 引用变量
  b. 参数变量
  c. 形变量
  d. 方法变量
- 10. ______ 指定了应该将参数传递给哪个参数。
  a. 具名参数
  b. 特殊参数
  c. 常量参数
  d. 字面量参数
- 11. 为参数提供了(n)______，就可以在不显式向参数传递参数的情况下调用该方法。
  a. 本地参数
  b. 空参数
  c. 默认参数
  d. 表达式参数
- 12. 当参数被 ______ 时，只有参数值的副本会被传递给参数变量。
  a. 命名常量
  b. 按关联传递
  c. 按引用传递
  d. 按值传递
- 13. 当你想让方法能够更改作为参数传递给它的变量的值时，该变量必须被 ______。
  a. 按引用传递
  b. 本地变量
  c. 按值传递
  d. 命名常量
- 14. ______ 是一种特殊类型的参数变量，对于建立方法之间的双向通信有用。
  a. 通信变量
  b. 引用参数
  c. 方法参数
  d. 全局变量
- 15. (n) ______ 可以接收一个未初始化的值，但在方法所属执行结束之前，它必须被设置为某个值。
  a. 输入参数
  b. 引用参数
  c. 输出参数
  d. 默认参数
- 16. 方法的 ______ 是方法返回的值的类型。

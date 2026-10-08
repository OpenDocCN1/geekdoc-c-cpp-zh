
第 38 行：此语句将 `average` 变量转换为字符串并赋值给 `averageLabel` 控件的 `Text` 属性。使用"n1"格式将数字保留到一位小数。

第 4 步：回到设计器，双击 `clearButton` 控件。这将打开编辑器，你将看到一个名为 `clearButton_click` 的空处理程序。通过输入 Program 4 中第 49-53 行的代码来完成 `clearButton_click` 事件处理程序。

第 50–52 行：这些语句清空文本框和 `averageLabel` 控件的内容。

第 53 行：此语句将空字符串赋值给 `averageLabel` 控件的 `Text` 属性。当这些语句执行完成后，标签将变为空。回到设计器，双击 `exitButton` 控件。通过输入 Program 4 中第 58–59 行的代码来完成 `exitButton_click` 事件处理程序。

第 6 步：保存项目。然后，按下键盘上的 `(F5)` 键编译并运行应用程序。

首先，通过在文本框中输入数值并点击计算按钮来测试应用程序。你应该能看到测试平均分，如图 27 左侧所示。

接下来，为测试 1 输入一个非数值并点击计算按钮。这将抛出异常，并且你会看到图 27 右侧所示的消息框。

根据意愿继续测试应用程序。当你完成时，点击退出按钮，表单将关闭。

```cs
private void clearButtonClick(object sender, EventArgs e)
{
    // 清空输入和输出控件。
    test1TextBox.Text = "";
    test2TextBox.Text = "";
    test3TextBox.Text = "";
    averageLabel.text = "";
}

private void exitButton_Click(object sender, EventArgs e)
{
    // 关闭表单。
    this.Close();
}
```

### 节点 (Checkpoint)

+ 35 什么会导致应用程序抛出异常？

+ 36 当抛出异常时，如何退出断点模式（break mode）？

+ 37 `try-catch` 语句的 `try` 块包含什么类型的代码？

+ 38 什么导致程序跳转到 `catch` 子句并执行 `try-catch` 语句的 `catch` 块？

+ 39 当抛出异常时，如何显示默认的错误消息？

+ 40 为一个应用程序编写一个 `try-catch` 语句，该程序用于计算两个数字之和并显示结果。该程序使用两个名为 `value1TextBox` 和 `value2TextBox` 的 `TextBox` 控件来收集输入，并使用名为 `sumLabel` 的 `Label` 来显示结果。

# 8 使用命名常量

> 概念：命名常量是一个代表值的名称，该值在程序执行期间不能更改的。

假设以下语句出现在一个计算贷款相关数据的银行程序中：

`amount = balance * 0.069;`

在这样的程序中，会出现两个潜在问题。首先，除了原始程序员之外，其他人都不清楚 0.069 是什么。它看起来像是一个利率，但在某些情况下，会有与贷款支付相关的费用。在不费力检查程序其他部分的情况下，如何确定此语句的目的呢？第二个问题是，如果这个数字被用于程序中其他计算中，并且必须定期更改。假设该数字是利率，如果利率从 6.9% 变为 7.2% 会怎样？程序员必须在整个源代码中搜索该数字的所有出现处。

# 处理数据

可以使用命名常量来解决这些问题。命名常量是一个代表值的名称，该值在程序执行期间不能更改的。以下是在 C# 中声明命名常量的示例：

```cs
const double INTEREST_RATE = 0.129;
```

该语句声明了一个初始化为值 0.129 的命名常量 `INTEREST_RATE`。它看起来像普通的变量声明，区别在于数据类型之前出现了 `const` 单词，并且变量名全大写。`const` 关键字是一个修饰符，告诉编译器将变量设置为只读。如果语句尝试更改常量的值，在程序编译时将发生错误。当你声明命名常量时，需要一个初始化值。

并不要求常量名为大写字母，但许多程序员倾向于这样写，以便它们与普通变量名容易区分来。当你阅读程序代码并使用大写标识符时，你立即知道它是一个常量。

> 注意：在许多编程语言中，用大写字母写常量是传统，本文遵循了这种做法。在 C# 社区中，有些程序员遵循这种做法，有些则没有。在教室中，你应该使用老师偏好的命名约定。

使用命名常量的优点是它们让程序更具自解释性。语句

`amount = balance * 0.069;`

可以更改为

`amount = balance * INTEREST_RATE;`

新程序员可以阅读该语句并知道正在发生什么。显然，`balance` 正在乘以利率。这种方法的另一个优点是易于对程序进行广泛的更改。假设利率在整个程序中的十几个不同的语句中出现。当利率变化时，命名常量声明中的初始化值是唯一需要修改的值。如果利率增加到 7.2%，则声明可以更改为：

```cs
const double INTEREST_RATE = 0.072;
```

新值 0.072 将被被用在那些使用 `INTEREST_RATE` 常量的语句中。在教程 5 中，你将创建一个使用命名常量的应用程序。

# 将变量声明为字段 (Fields)

> 概念：字段（field）是在类级别声明的变量。字段的作用域是整个类。

到本章为止，我们处理过的所有变量都是局部变量。局部变量声明在方法内部，并且对该方法中的语句可见。另一种类型的变量是字段，它是在类内部声明但在方法之外的变量。字段的作用域是整个类，所以当你声明一个字段时，类中的所有方法都可以访问该变量。

通常，字段声明在类声明的顶部，在任何方法之前。图 28 显示了你在表单类内部编写字段声明的位置。当你需要编写字段声明时，可以在类的左大括号 (`{`) 之前插入空行，并在该空间编写字段声明。

图 28 在何插入字段声明

```cs
field1;
partial class Form1
{
	using System;
	using System.Collections.Generic;
	using System.ComponentModel;
	using System.Data;
	using System.Drawing;
	using System.Linq;
	using System.Text;
	using System.Windows.Forms;
namespace Example_Project
{
	public partial class Form1 : Form
	{
		public Form1()
		{
			InitializeComponent();
		}
	}
}
```

```csharp
{
  public partial class Form1 : Form {
    // 一个私有字段用于存储名称
    private string name = "Charles";

    public Form1() {
      InitializeComponent();
    }

    private void showNameButton_Click(object sender, EventArgs e) {
      MessageBox.Show(name);
    }

    private void chrisButton_Click(object sender, EventArgs e) {
      name = "Chris";
    }

    private void carmenButton_Click(object sender, EventArgs e) {
      name = "Carmen";
    }
  }
}
```

# Form类中字段的生命周期

当你在表类中声明一个字段时，字段的生命周期就是表单存在的时间。这意味着只要表单存在，字段就会存在于内存中。这与局部变量的生命周期不同，局部变量只在声明它的方法执行期间存在。局部变量在内存中来去去，但表单字段只要表单存在就一直存在。

你可以在 Field Demo 应用程序中看到这一点。`name` 字段在声明 `Form1` 时创建，只要 `Form1` 存在，它就会一直存在。当一个事件处理程序在字段中存储一个值时，该值将留在字段中，直到被不同的事件处理程序再次更改。因此，字段提供了一种存储值的方法，这些值不会在特定方法结束时消失。

### 注意

虽然字段很容易在类的方法之间共享数据，但你应该谨慎使用它们。过度使用字段会导致类代码的调试变得困难，特别是当类有许多方法时。如果字段中存储了错误的值，你将不得不跟踪类中访问该字段的每一个语句，以确定错误值来自哪里。在大多数情况下，字段应该只用于必须在多个方法之间共享且在方法未执行时继续存在于内存中的数据。

# 常量字段

常量字段是无法被类中的任何语句更改的字段。如果编译器发现尝试更改常量字段值的语句，将发生错误。

# 处理数据

常量字段使用 `const` 关键字声明并用一个值初始化。

以下是一个示例：

```sharp
private const decimal INTEREST_RATE = 0.075m;
```

该语句声明了一个名为 `INTEREST_RATE` 的常量十进制字段，并初始化为值 0.075。常量字段通常用于防止类中许多方法所需的不可变值。例如，假设一个银行程序使用常量字段来表示利率。如果利率在几个方法中使用，那么创建一个常量字段比在每个方法中创建一个同名的局部常量要容易得多。

这简化了代码的维护。如果利率发生变化，只需要更改常量字段的声明，而不需要更改多个局部声明。

注意：由于常量字段的值不能被类中的其他语句更改，因此你不必担心与过度使用普通非常量字段相关的许多潜在调试问题。

在在教程 5 中，你将创建一个应用程序，该程序在类表单中使用字段来存储数据，并使用常量字段来表示不变的值。

## 教程 5：

# 创建找零计数器应用程序

在本教程中，你将创建一个找零计数器（Change Counter）应用程序。该应用程序显示四种硬币的图像，价值分别为 5 分、10 分、25 分和 50 分。每当用户点击一次硬币图像时，该硬币的值就会加到总额中，并显示总额。图 30 显示了应用程序的表单以及所有控件的名称。

图 30 找零计数器表单

![](img/9467d25da5679b16515c9401daaae36c_177_0.png)

步骤 1：启动 Visual Studio（或 Visual C# Express）并开始一个名为 `Sale Price Calculator` 的新 Windows Forms 项目。

步骤 2：如图 30 所示设置应用程序的表单。注意表单的 `Text` 属性设置为 `Change Counter`。当你将每个控件放置在表单上时，图中显示了控件的名称，相关的属性设置请参考表 15。

**表 15 控件属性设置**

| 控件名称 | 控件类型 | 属性设置 |

| :--- | :--- | :--- |

| instructionLabel | Label | 字体: Microsoft Sans (样式: 粗, 大小: 10 点) 文字: Click the Coins |

| fiveCentsPictureBox | PictureBox | Image: 从 Samples Programs 中选择并导入 cents.png 文件。SizeMode: AutoSize |

| tenCentsPictureBox | PictureBox | Image: 从 Samples Programs 中选择并导入 10cents.png 文件。SizeMode: AutoSize |

| twentyCentsPictureBox | PictureBox | Image: 从 Samples Programs 中选择并导入 25cents.png 文件。SizeMode: AutoSize |

| fiftyCentsPictureBox | PictureBox | Image: 从 Samples Programs 中选择并导入 50cents.png 文件。SizeMode: AutoSize |

| outputDescriptionLabel | Label | 字体: Microsoft Sans (样式: 粗, 大小: 10 点) 文字: Total |

| totalLabel | Label | AutoSize: False 边框: FixedSingle 文字: (Text 属性的内容已清除。) 对齐方式:居中 |

| exitButton | Button | 文字: Exit |

步骤 3：一旦你设置好了表单及其控件，就可以开始编写代码。在教程结束时，程序 6 将显示完成的表单代码。请参考程序 6 以查看控件的声明（注意程序 6 中的数字仅引用）。首先，在解决方案中右键点击 `Form1` 并查看代码。查看程序 6 中第 15-22 行的声明：

**第 15 行**：该语句声明了一个名为 `FIVE_CENTS` 的常量字段，初始化为值 05。

**第 16 行**：该语句声明了一个名为 `TEN_CENTS` 的常量字段，初始化为值 10。

**第 17 行**：该语句声明了一个名为 `TWENTY_CENTS` 的常量字段，初始化为值 25。

**第 18 行**：该语句声明了一个名为 `FIFTY_CENTS` 的常量字段，初始化为值 50。

步骤 4：现在你可以为图片框控件创建事件处理程序了。返回设计器视图并双击 `fiveCentsPictureBox`。这将打开代码编辑器。查看程序 6 中第 31-35 行所示的代码：

**第 32 行**：该语句将 `FIVE_CENTS` 常量的值加到总额 `total`。

**第 35 行**：该语句将变量转换为字符串并赋值给 `totalLabel` 的 `Text` 属性。`c` 格式字符串会将数字格式化为货币。

步骤 5：返回设计器视图并双击 `tenCentsPictureBox`。这将打开代码编辑器。查看程序 6 中第 40-44 行所示的代码：

**第 41 行**：该语句将 `TEN_CENTS` 常量的值加到总额 `total`。

**第 44 行**：该语句将变量转换为字符串并赋值给 `totalLabel` 的 `Text` 属性。`c` 格式字符串会将数字格式化为货币。

步骤 6：返回设计器视图并双击 `twentyCentsPictureBox`。这将打开代码编辑器。查看程序 6 中第 49-53 行所示的代码：

**第 50 行**：该语句将 `TWENTY_CENTS` 常量的值加到总额 `total`。

**第 53 行**：该语句将变量转换为字符串并赋值给 `totalLabel` 的 `Text` 属性。`c` 格式字符串会将数字格式化为货币。

步骤 7：返回设计器视图并双击 `fiftyCentsPictureBox`。这将打开代码编辑器。查看程序 6 中第 58-62 行所示的代码：

**第 59 行**：该语句将 `FIFTY_CENTS` 常量的值加到总额 `total`。

**第 62 行**：该语句将变量转换为字符串并赋值给 `totalLabel` 的 `Text` 属性。`c` 格式字符串会将数字格式化为货币。

第 8 步：现在你为 Exit 按钮编写事件处理器。将视图切换回设计器（Designer）并双击 `exitButton` 控件。这将打开代码编辑器，你将看到一个名为 `exitButton_click` 的空事件处理器。通过输入程序 6 中 67-68 行所示的代码来完成 `exitButton_click` 事件处理器。

第 9 步：保存项目。然后，按键盘上的 `F5` 键或点击工具栏上的启动调试按钮来编译并运行应用程序。按你任意的顺序点击硬币图像来测试应用程序。每次点击硬币时，总额应更新为正确的金额。完成后，点击 Exit 按钮，表单应该关闭。


- **访问修饰符（ACCESS MODIFIER）**——关键字 `private` 是一个访问修饰符。当方法被声明为 `private` 时，它只能由方法所在类内部的代码调用。或者，声明为 `public` 的方法可以由类外部的代码调用。这很重要，因为某些应用程序有多个类，除非你特意想让方法对类外部代码可用，否则你应该将其声明为 `private`。

- **返回类型（RETURN TYPE）**——回想我们之前对 `void` 方法和有返回值方法的讨论。当关键字 `void` 出现在这里时，意味着该方法是 `void` 方法，不返回值。正如你在本章稍后将看到的，有返回值的方法在这里会列出一个数据类型。

- **方法名（METHOD NAME）**——你应该给每个方法一个描述性的名称。通常情况下，适用于变量名的规则也适用于方法名。示例中的方法命名为 `DisplayMessage`，因此我们可以很容易猜出该方法的功能：它显示一条消息。

- 在本书中，我们使用 Pascal case 来命名方法名。Pascal case 类似于 `camelCase`（我们一直以来用于变量名的命名约定），不同在于在 Pascal case 命名中，首字母始终大大写。在 C# 程序员中，使用 Pascal case 命名方法是一种标准约定，因为它可以将方法名与变量和字段名区分开。

- **括号（PARENTHESES）**——在头部中，方法名后面总是跟着一组括号。正如你在本章稍后看到的，你有时会在括号内编写声明，但目前括号是空的。

> 注意
> 方法头部永远不会以分号结束。

# 方法体

从方法头部之后的一行开始，一个或多个语句会出现在一组大括号（`{ }`）内。这些语句就是方法体，并在每次执行该模块时被执行。

当你编写方法定义时，Visual Studio 会自动对方法体中的语句进行缩进。缩进不是必须的，但它让代码更容易于阅读和调试。通过对方法体中的语句进行缩进，你在视觉上将它们与周围的代码隔离开。

# 在类内部声明方法

方法通常属于一个类，因此你必须在它所属的类内部编写方法定义。在本章中，所有的方法都将属于 `Form1` 类，如图 6-4 所示。

# 图 6-4 在 Form1 中编写方法定义

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace Example
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

# 调用方法

方法在被调用时执行。事件处理程序由特定事件调用，但其他方法通过方法调用语句执行。当方法被调用时，程序跳转到该方法并执行其体中的语句。这里有一个调用之前检查过的 `DisplayMessage` 方法的示例：

```csharp
DisplayMessage();
```

该语句只是方法名加上一组括号。因为是一个完整的语句，它以分号结束。

让我们来看使用 `DisplayMessage` 方法的完整程序。在本书的 `Chap06` 文件夹中有一个名为 `Simple Method` 的项目。图 6-5 显示了设计器中的表单，程序 6-1 显示了表单的代码。

# 图 6-5 Simple Method 应用程序的表单

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb128_776_0.png)

# 程序 6-1 Simple Method 应用程序的 Form1 代码

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
11 namespace Simple_Method
12 {
13     public partial class Form1 : Form
14     {
15         public Form1()
16         {
17             InitializeComponent();
18         }
19     
20     private void goButton_Click(object sender, EventArgs e)
21         {
22             MessageBox.Show("This is the
goButton_Click method.");
23             DisplayMessage();
24             MessageBox.Show("Back in the
goButton_Click method.");
25         }
26
27     private void DisplayMessage()
28         {
29             MessageBox.Show("This is the
DisplayMessage method.");
30         }
31     }
32 }
```

让我们逐步分析代码。当用户点击 `Go` 按钮时，会执行 `goButton_Click` 事件处理器。在事件处理器内部，第 22 行的语句会在框中显示"This is the goButton_Click method."然后，第 23 行调用 `DisplayMessage` 方法。如图 6-6 所示，程序跳转到 `DisplayMessage` 方法并执行其体内的语句。`DisplayMessage` 方法体中只有一条语句，即第 29 行。它显示"This is the DisplayMessage method."，然后方法结束。如图 6-7 所示，程序跳转回程序中调用 `DisplayMessage` 方法的部分，并从该点继续执行。在此处，程序在第 24 行继续执行，显示"Back in the goButton_Click method."`goButton_Click` 处理器在第 25 行结束。

# 图 6-6 调用 DisplayMessage 方法

```
private void goButtonClick(object sender, EventArgs e) {
    MessageBox.Show("This is the goButton_Click method.");
    DisplayMessage();
    MessageBox.Show("Back in the goButton_Click method.");
}
private void DisplayMessage() {
    MessageBox.Show("This is the DisplayMessage method.");
}
```

程序跳转到 `DisplayMessage` 方法并执行其体内的语句。

# 图 6-7 DisplayMessage 方法返回

```
private void goButton_Click(object sender, EventArgs e) {
    MessageBox.Show("This is the goButton_Click method.");
    DisplayMessage();
    MessageBox.Show("Back in the goButton_Click method.");
}

private void DisplayMessage() {
    MessageBox.Show("This is the DisplayMessage method.");
}
```

当 `DisplayMessage` 方法结束时，程序返回到调用它的程序部分，并在该点继续执行。

当调用一个方法时，系统会在“后台”执行一些操作，以便系统知道在方法结束后程序应该返回到哪里。首先，系统会保存要返回的位置的内存地址。这通常是紧接着方法调用之后出现的语句。这个内存位置被称为**返回点**。然后，系统跳转到该方法并执行其体内的语句。当方法结束时，系统跳转回返回点并恢复执行。

> 注意
> 当程序调用方法时，程序员通常说程序的控制权转移到了该方法。这简单意味着该方法接管了程序的执行控制。

在教程 6-1 中，你将实际练习编写和调用方法。

# 教程 6-1：创建和调用方法

本书中的 `Chap 06` 文件夹包含一个名为 `Lights` 的部分创建的项目。在本教程中，你将完成该项目，使其模拟灯的开启或关闭。该项目的表单（Form）在初始设置下如图 6-8 所示。

# 图 6-8 初始设置下的 Lights 项目表单

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_780_0.png)

以下是关于特定属性设置的一些细节：

- `lightOnPictureBox` 控件的 `Visible` 属性初始被设置为 `true`。

- `lightOffPictureBox` 控件的 `Visible` 属性初始被设置为 `false`。

- `StateLabel` 在应用程序运行时显示 `ON` 或 `OFF`，以指示灯的开启或关闭。初始时，控件的 `Text` 属性被设置为 `ON`。

运行时，用户点击 `Switch Light` 按钮，灯的状态就会反转。句话说，如果灯目前是开启的，它将被关闭；如果灯目前是关闭的，它将被开启。

当灯开启时，会发生以下操作：

- `lightOnPictureBox` 控件的 `Visible` 属性被设置为 `true`。

- `lightOffPictureBox` 控件的 `Visible` 属性被设置为 `false`。

- `StateLabel` 标签的 `Text` 属性被赋值字符串"ON"。

当灯关闭时，会发生以下操作：

- `lightOffPictureBox` 控件的 `Visible` 属性被设置为 `true`。

- `lightOnPictureBox` 控件的 `Visible` 属性被设置为 `false`。

- `StateLabel` 标签的 `Text` 属性被赋值字符串"OFF"。

为了代码模块化，你创建一个方法 `TurnLightOn`（包含开启灯的代码）和另一个方法 `TurnLightOff`（包含关闭灯的代码）。当你需要开启灯时，调用 `TurnLightOn` 方法；当你需要关闭灯时，调用 `TurnLightOff` 方法。

第 1 步：启动 Visual Studio。打开书中 `Student Sample Programs` 中 `Chap06` 文件夹下名为 `Lights` 的项目。

第 2 步：在设计器中打开 `Form1`。表单及其重要控件的名称如图 6-8 所示。

第 3 步：移动 `PictureBox` 控件，使其中一个叠在另一个上面，如图 6-9 所示。（在图中，`lightOnPictureBox` 控件在上方，但实际上哪个在上方并不重要。）此外，缩小表单宽度，并如图所示调整底部控件的位置。

# 图 6-9 重新定位的控件和调整大小的表单

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_782_0.png)

第 4 步：教程结束时的程序 6-2 显示了完整的代码。打开代码并输入程序 6-2 第 20-42 行的 `TurnLightOn` 和 `TurnLightOff` 方法。让我们仔细查看代码：第 20 行是 `TurnLightOn` 方法的开头，其目的是开启灯。执行它时，第 23 行让 `lightOnPictureBox` 可见，第 26 行让 `lightOffPictureBox` 不可见，第 29 行将 `StateLabel` 的 `Text` 属性设置为"ON"。第 32 行是 `TurnLightOff` 方法的开头，其目的是关闭灯。执行它时，第 35 行让 `lightOffPictureBox` 可见，第 38 行让 `lightOnPictureBox` 不可见，第 41 行将 `StateLabel` 的 `Text` 属性设置为"OFF"。

第 5 步：接下来，为按钮创建事件处理器。切换回设计器并双击 `switchButton`。第 47 行的 `if` 语句判断是否关闭。第 51 行的 `else` 分句执行，并在第 53 行调用 `TurnLightOn` 方法开启灯。

第 6 步：切换回设计器并双击 `exitButton`。在代码编辑器中你会看到一个名为 `exitButton_Click` 的事件处理器。通过输入程序 6-2 第 59-60 行的代码来完成 `exitButton_Click` 处理器。

第 7 步：保存项目。然后，按 `F5` 键或点击工具栏上的调试按钮（！）来编译并运行应用程序。应用程序运行时，多次点击 `Switch Light` 进行模拟。完成后，点击 `Exit` 按钮退出应用程序。

# 程序 6-2 Lights 应用中 Form1 的完整代码

```csharp
void exitButton_Click(object sender, EventArgs e)
{
    // Close the form.
    this.Close();
}
```

## 自顶向下设计

在本节中，我们讨论并演示了方法是如何运作的。你已经看到程序在调用方法时如何跳转到方法，并在方法结束时返回到调用该方法的程序部分。理解这些方法的机械机制至关重要。

与理解方法如何工作同样重要的是，理解如何使用方法将程序模块化。程序员通常使用一种名为**自顶向下设计**（top–down design）的技术来将算法分解为多个方法。自顶向下的设计过程如下如下：

- 程序要执行的整体任务被分解为子任务。

- 检查每个子任务，确定其是否可以进一步分解为更多的子任务。重复此步骤，直到无法识别出更多的子任务为止。

- 一旦确定了所有子任务，就可以将它们编写成代码。

这一过程被称为自顶向下设计，因为程序员最初从查看必须执行的最层任务开始，然后将这些任务分解为较低层次的子任务。

> 注意
> 自顶向下的设计过程有时被称为逐步精细化（stepwise refinement）。

### 检查点

- 6.1 `void` 方法和有返回值的方法之间有什么区别？

- 6.2 方法定义包含哪部分？

- 6.3 “调用方法”这个短语是什么意思？

- 6.4 当 `void` 方法执行时，到达方法结尾会发生什么？

- 6.5 描述自顶向下设计过程中涉及的步骤。

## 6.3 向方法传递参数

> 概念
> 参数（Argument）是在调用方法时传递到方法中的任何数据。形参数（Parameter）是接收传递给方法的参数的变量。

有时，不仅调用方法是有用的，向方法发送一个或多个数据也是有用的。发送到方法中的数据被称为参数。方法可以在计算或其他操作中使用这些参数。

你已经熟悉了如何在方法调用中使用参数。例如，查看以下语句：

```csharp
MessageBox.Show("Hello");
```

此语句调用了 `MessageBox.Show` 方法并将字符串 "Hello" 作为参数传递。这是另一个例子：

```csharp
number = int.Parse(str);
```

假设 `number` 是一个 `int` 变量而 `str` 是一个 `string` 变量。此语句调用 `int.Parse` 方法并将 `str` 变量作为参数传递。

如果你正在编写方法并希望它在被调用时接收参数，你必须为该方法配备一个或多个参数变量。参数变量（通常简单称为参数）是在方法被调用时接收参数的特殊变量。这是一个带有参数变量的方法示例：

```csharp
private void DisplayValue(int value)
{
    MessageBox.Show(value.ToString());
}
```

注意括号内出现的 `int` 变量声明 (`int value`)。这是参数变量的声明，它允许 `DisplayValue` 方法接受一个 `int` 值作为参数。这是一个调用 `DisplayValue` 方法的示例，将 5 作为参数传递进去：

```csharp
DisplayValue(5);
```

此语句执行 `DisplayValue` 方法。括号内列出的参数被赋值给方法的参数变量 `value`。如图 6-10 所示。

## 图 6-10 向 DisplayValue 方法传递值 5

```csharp
DisplayValue(5);

private void DisplayValue(int value) {
    MessageBox.Show(value.ToString());
}
```

在 `DisplayValue` 方法内部，变量 `value` 将包含任何传递给它的参数的值。如果我们传递 5 作为参数，该方法将在将在消息框中显示值 5。

你也可以将变量的内容和表达式的值作为参数。例如，以下语句通过传递各种参数调用了 `DisplayValue` 方法：

```csharp
DisplayValue(x);
DisplayValue(x * 4);
DisplayValue(int.Parse("700"));
```

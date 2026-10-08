
- 该语句将字符串拼接的结果赋值给变量，该结果为 `firstName` 控件的 `Text` 属性，后面跟着一个空格，然后是 `lastName` 控件的 `Text` 属性值。例如，如果用户在 `firstNameTextBox` 中输入了 Joe，在 `lastNameTextBox` 中输入了 Smith，这将 "Joe Smith" 赋值给 `fullName` 变量。

- 该语句将 `fullName` 变量赋值给 `fullNameLabel` 控件的 `Text` 属性。结果是存储在 `fullName` 变量中的字符串显示在 `fullNameLabel` 控件中。

## 变量

如果你运行该应用程序，图 3-7 显示了在输入名为 Chris、姓为 Jones 并点击 `showNameButton` 控件后，表单显示的示例。

### 图 3-7 在标签中显示的用户全名

![](img/8a88e1d8c69a687988c05f162ce32cac_141_0.png)

### 在使用之前声明变量

变量声明的目的是告诉编译器，你计划在程序中使用一个指定名称的变量来存储数据。变量声明会在内存中创建该变量。由于这个原因，变量的声明语句必须出现在方法中使用该变量的任何其他语句之前。这完全合逻辑，因为如果变量没有在内存中被创建，你就无法在变量中存储值。

### 局部变量

注意图 3-6 中的 `fullName` 变量是在事件处理程序内部声明的。在方法内部声明的变量被称为局部变量（locals）。局部变量属于其声明的方法，只有该方法内部的语句才能访问该变量。（“局部”一词表示该变量只能在其被声明的方法内部局部使用。）

如果一个方法中的语句尝试访问属于另一个方法的局部变量，就会发生错误。例如，让我们来看图 3-8 中的示例代码：

- 该语句声明了一个名为 `myName` 的字符串。该变量被声明在 `firstNumber` 事件处理程序内部，它是该方法的局部变量。

- 该语句同样位于 `firstNumber` 事件处理程序中，将 `nameTextBox` 控件的 `Text` 属性赋值给 `myName` 变量。

### 图 3-8 一个访问属于另一个方法的局部变量的方法

```csharp
private void firstNumberClick(object sender, EventArgs e) {
    // 声明一个字符串变量。
    string myName;
    // 将 nameTextBox 控件的 Text 属性
    // 赋值给 myName 变量。
    myName = nameTextBox.Text;
}

private void secondButtonClick(object sender, EventArgs e) {
    // 将 myName 变量赋值给 outputLabel
    // 控件的 Text 属性。
    outputLabel.Text = myName; // ERROR!
}
```

这条语句位于 `secondButton_Click` 事件处理程序中，尝试将 `myName` 变量赋值给 `outputLabel` 控件的 `Text` 属性。然而，该语句无法工作，因为 `myName` 变量是 `secondButton_Click` 事件处理程序的局部变量，`secondButton_Click` 中的语句无法访问它。

### 变量的作用域

程序员使用作用域（scope）来描述程序中可以访问的部分。变量仅对其作用域内的语句可见。

局部变量的作用域从变量声明开始，到其声明的方法结束。正如你在上一个示例中看到的，局部变量无法被方法外的语句访问。此外，局部变量无法被方法内部声明之前的代码访问。

### 变量的生命周期

变量的生命周期是在程序执行期间变量存在内存中的时间段。当声明变量的方法开始执行时，局部变量在内存中创建。当方法结束时，所有局部变量的生命周期都会被销毁。因此，局部变量的生命周期是其执行方法的时间。

### 重复变量名

你不能在同一个作用域内声明两个同名的变量。例如，如果你在一个事件处理程序中声明了一个名为 `productDescription` 的变量，你就不能在同一个事件处理程序中声明另一个同名的变量。但是，你可以在不同的方法中声明相同的变量。

### 赋值兼容性

只有当值与数据类型兼容时，你才能给变量赋值。只有字符串与字符串数据类型兼容，因此以下代码示例中的所有赋值均显示：

```sharp
1 // 声明并初始化一个字符串变量。
2 string productDescription = "Chocolate Truffle";
3 // 声明另一个字符串变量。
4 string favoriteProduct;
5 // 给变量赋值。
6 productDescription = "Large Medium-Roast Coffee";
7 // 显示变量的值。
8 MessageBox.Show(productDescription);
910 // 给变量分配不同的值。
11 favoriteProduct = "Chocolate Truffle";
1213 // 显示变量的值。
14 MessageBox.Show(favoriteProduct);
```

以下注释解释了这些行：

- 第 2 行使用字符串字面量初始化字符串变量。字符串字面量是赋值兼容的。

- 第 4 行声明另一个字符串变量。

- 第 6 行给变量赋值。这可行是因为字符串字面量与字符串兼容。

- 第 8 行显示变量的值。

- 第 11 行给变量分配不同的值。

- 第 14 行显示变量的值。

### 3.2 初步接触变量

# 144 第3章 处理数据

此代码示例说明了变量的两个重要特性：

- 变量在一次只包含一个值。

- 当你将一个值存储在变量时，该值将替换变量中原有的值。

教程 3-1 为你提供了一些使用变量的练习。你将创建一个应用程序，该程序使用 TextBox 获取输入值，将这些值存储在变量中，并在操作中使用这些变量。

## 教程 3-1:

出生日期字符串应用程序

在本教程中，你将创建一个应用程序，允许用户输入以下关于出生日的信息：

- 星期（周一、周二等）

- 月份名称（一月、二月等）

- 月份中的数字几几

- 年份

图 3-9 显示了应用程序的表单，以及所有控件的名称。当应用程序运行时，用户向每个 TextBox 输入每项数据。当用户点击 *Show-date* 时，应用程序将 TextBox 的内容连接成一个字符串，格式为 *Friday, June 1, 1990*。该字符串显示在 dateOutputLabel 控件中。当用户点击 *Clear* 按钮时，TextBox 和 dateOutputLabel 的内容将被清除。*Exit* 按钮关闭应用程序。

> 图 3-9 出生日期字符串

![](img/8a88e1d8c69a687988c05f162ce32cac_144_0.png)

**步骤 1:** 启动 Visual Studio（或 Visual Studio Express）并开始名为 *Birth Date String* 的新 Windows Forms Application。

**步骤 2:** 如图 3-9 所示设置应用程序表单。注意表单的 Text 属性设置为 *Birth Date String*。图中显示了控件的名称。在表单上放置每个控件时，请参考表 3-1 的相关属性设置。

**步骤 3:** 一旦设置好带有控件的表单，就可以为 Button 控件创建事件处理程序。在教程结束时，程序 3-1 显示了表单完成代码。编写事件处理程序时，将被指示参考程序 3-1。记住，程序 3-1 中显示的行号不是程序的一部分。它们仅供参考。

在设计器（Designer）中，双击 showDateButton 控件。这将控制代码编辑器，你会看到一个名为 showDateButton_Click 的空事件处理程序。通过输入程序 3-1 中第 22–30 行的代码来完成 showDateButton_click 事件处理程序。

让我们来看看代码：

第 23 行：此语句声明了一个名为 output 的字符串。

第 26-29 行：这些行是一个长语句，被分成了多行。该语句连接 TextBox 控件的 Text 属性，并带有相应的逗号和空格，创建日期字符串。生成的字符串赋值给 output 变量。

例如，假设用户输入了以下内容：

- dayOfTextBox 控件中输入 Friday。

- monthTextBox 控件中输入 June。

- dayOfMonthTextBox 控件中输入 1。

- yearTextBox 控件中输入 1990。

此语句中的连接产生字符串 "June 1, 1990"；它被赋值给 output 变量。

第 32 行：此语句将变量赋值给 dateOutputLabel 的 Text 属性。当此语句执行时，output 变量的内容将显示在 dateOutputLabel 控件中。

**步骤 4:** 将视图切换到设计器并双击 clearButton 控件。在代码编辑器中，你会看到一个名为 clearButton_click 的空事件处理程序。通过输入程序 3-1 中第 38–44 行所示的代码来完成 clearButton_click 事件处理程序。

让我们来看看代码：

**第 38-41 行：**每个语句将空字符串赋值给一个 TextBox 控件的 Text 属性。执行完成后，显示 TextBox 控件。

**第 44 行：**此语句将空字符串赋值给 dateOutputLabel 的 Text 属性。语句执行后，显示 label。

- 将视图切换设计器并双击代码编辑器中的 exitButton，你会看到一个名为 exitButton_click 的事件处理程序。通过输入程序 3-1 中第 49–50 行的代码完成 exitButton_click 事件处理程序。

- 保存项目。然后按键盘 F5 或点击工具栏上的 Start 运行应用程序。表单将如图 3-1 所示。通过向 TextBox 输入值并点击 Date 按钮来测试应用程序。日期应该显示，如右侧所示。点击 Clear，TextBox 和 Label 的内容应被清除。点击 Exit，表单应关闭。

图 3-1 出生日期应用程序

![](img/8a88e1d8c69a687988c05f162ce32cac_146_0.png)

表 3-1 控件属性设置

| 控件名称 | 控件类型 | 属性设置 |
|---|---|---|
| dayOfWeekPromptLabel | Label | Text: 输入星期 |
| monthPromptLabel | Label | Text: 输入月份 |
| dayOfMonthPromptLabel | Label | Text: 输入数字几 |
| yearPromptLabel | Label | Text: 输入年份 |
| dayOfTextBox | TextBox | 无属性更改 |
| monthTextBox | TextBox | 无属性更改 |
| dayOfMonthTextBox | TextBox | 无属性更改 |
| yearTextBox | TextBox | 无属性更改 AutoSize:False BorderStyle:Fixed Text:(Text属性的内容已清除.) TextAlign:MiddleCenterCenter |
| showDateButton | Button | Text: Show Date |
| clearButton | Button | Text: Clear |
| exitButton | Button | Text: Exit |

程序 3-1 出生日期应用程序 Form1 代码

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

namespace Birth_Date_String
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();

        private void showButton_Click(object sender, EventArgs e)
        {
            // 声明一个字符串变量
            string output;
            // 连接输入构建输出字符串
            output = dayOfWeekTextBox.Text + ", " + monthTextBox.Text + ", " + dayOfMonthTextBox.Text + ", " + yearTextBox.Text;
            // 在 Label 控件中显示输出字符串
            dateOutputLabel.Text = output;
        }

        private void clearButton_Click(object sender, EventArgs e)
        {
            // 清除 TextBox
            dayOfWeekTextBox.Text = "";
            monthTextBox.Text = "";
            dayOfMonthTextBox.Text = "";
            yearTextBox.Text = "";
            // 清除 dateOutputLabel 控件
            dateOutputLabel.Text = "";
        }

        private void exitButton_Click(object sender, EventArgs e)
        {
            // 关闭表单
            this.Close();
        }
    }
}
```

## 3.2 初识变量

在教程 3-1 中，第 26–29 行的语句展示了如何将一个语句拆分为多行的示例。通常，你会发现自己编写的语句长到无法放入代码窗口。如果你必须水平滚动代码窗口来查看长语句，你的代码将难以阅读。此外，如果你或你的老师选择打印代码，长到无法放进一页的语句将换行到下一行，使你的代码看起来杂乱无章。由于这些原因，最好将长语句拆多行。

在输入语句时，你可以在合适的地方简单地按 Enter 键以在下一行继续语句。然而，你不能拆分关键字、引用字符串或标识符（例如变量名或控件名）。

## 变量初始化

在 C# 中，变量在使用之前必须赋值。例如，看这段代码：

```csharp
string productDescription;
MessageBox.Show(productDescription);
```

这段代码声明了一个名为 productDescription 的字符串变量，然后尝试在消息框中显示该值。唯一的问题是我们没有给该变量赋值。当我们编译包含此内容的应用程序时，会得到类似 Use of unassigned local variable 'productDescription' 的错误消息。C# 编译器不会编译使用未赋值变量的代码。确保变量已赋值的方法是在声明变量时初始化它。例如，以下语句声明了一个名为 productDescription 的字符串变量，并立即将字符串 "Chocolate Truffle" 赋值给：

```csharp
string productDescription = "Chocolate Truffle";
```

我们说该语句用字符串 "Chocolate Truffle" 初始化了 productDescription 变量。另一个例子：

```csharp
string lastName = lastNameTextBox.Text;
```

假设这属于一个有一个名为 lastNameTextBox 的 TextBox 的应用程序。语句声明了一个名为 lastName 的字符串变量，并用 lastNameTextBox 控件的属性值对其初始化。

## 使用一个语句声明多个变量

在教程 3-1 中，第 26–29 行的语句展示了如何将一个语句拆分为多行的示例。通常，你会发现自己编写的语句长到无法放入代码窗口。如果你必须水平滚动代码窗口来查看长语句，你的代码将难以阅读。此外，如果你或你的老师选择打印代码，长到无法放进一页的语句将换行到下一行，使你的代码看起来杂乱无章。由于这些原因，最好将长语句拆多行。

在输入语句时，你可以在合适的地方简单地按 Enter 键以在下一行继续语句。然而，你不能拆分关键字、引用字符串或标识符（例如变量名或控件名）。

你可以用一个声明语句声明多个相同类型的变量。这是一个示例：

```csharp
string lastName, firstName, middleName;
```

此语句声明了名为 lastName、firstName 和 middleName 的三个字符串变量。注意逗号分隔了这些变量。这是一个一个语句声明并初始化变量的示例：

```csharp
string lastName = "Jones", firstName = "Jill", middleName = "Rebecca";
```

记住，如果语句跨越两或多行，你可以将其拆分。有时你需要在多行中进行变量声明，如下：

```csharp
string lastName = "Jones",
firstName = "Jill",
middleName = "Rebecca";
```

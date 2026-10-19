
点击工具栏上的**停止调试**按钮（■）来停止程序。
点击 IceCreamCost.cs [设计] 选项卡打开设计器窗口。

## 清除控件

TextBox 有一个 Clear() 方法用于清除其内容。然而，Label 则是通过将 Text 属性设置为 null（即空）或一个空字符串（用两个引号且中间无内容表示，即 ("")）来清除。你也可以使用这种方法来清除 TextBox。

- **步骤 2-7：** 双击 Clear 按钮创建按钮的点击事件处理器，并输入代码来清除控件：

```
private void btnClear_Click(object sender, EventArgs e)
{
    txtScoops.Clear();
    txtUnitPrice.Clear();
    lblCost.Text = null;
}
```

注意，Clear 是一个方法（程序单元）的名称，方法的名称末尾需要一对圆括号。

## 关闭窗体

要关闭正在运行的窗体，请使用该窗体的 Close() 方法。

- **步骤 2-8：** 双击 Close 按钮，并在 click 事件处理程序中输入代码：

```
private void btnExit_Click(object sender, EventArgs e)
{
    this.Close();
}
```

在上面的代码中，“this” 指的是当前窗体。

## IceCreamCost 窗体的完整代码

图 1-22 显示了完整代码。

**图 1-22：** IceCreamCost 的完整代码

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
```

## 常量

第 29 行声明了一个常量。第 29 行中的关键字 const

```
const double TAX_RATE = 5.5;
```

指明 TAX_RATE 是一个常量（而不是变量）。

常量用于表示在运行时不需要更改的字面量值。使用常量表示税率意味着税率是一个固定值。但是，如果税率要在运行时从文件或 TextBox 中读取，则使用变量更为合适。

该常量具有以下特征：

- 1. 常量的值在运行时不能更改。以下代码在运行时向常量 numberOfScoops 赋值是无效的：

  ```
  const int numberOfScoops = 0;
  numberOfScoops = 2; // Invalid
  ```

- 2. 常量必须在声明时通过赋予字面量值或常量来进行初始化。例如，以下语句：

  ```
  const int numberOfScoops = int.Parse(txtScoops.Text); // Invalid
  ```

  是无效的，因为赋予常量的值不是常量或字面量值。类似地，下面的语句也是无效的，因为该常量没有在声明时进行初始化：

  ```
  const int numberOfScoops; // Invalid
  ```

- 3. 常量在编译时会被其值替换。

- **步骤 3-3：** 双击 btnComputeTotal 以创建其 click 事件处理程序，并添加声明变量和常量的注释和语句，如图 1-26 所示。

**图 1-26：** 声明变量和常量的代码

```
22    // Compute the total cost for an order of ice cream, including sales tax.
23
24    // Declare variables to hold input data and computed results
25    int scoops;
26    double unitPrice, subTotal, salesTax, totalCost;
27
28    // Declare a constant to hold the tax rate
29    const double TAX_RATE = 5.5;
```

图 1-27 显示了从 TextBox 获取输入数据（与教程 2 中相同）以及计算小计、销售税和总成本的代码。

## 1.11 附加概念：常量、变量的作用域和 ListBox

**图 1-27：** 获取输入数据并计算结果的代码

```
// Get input data from TextBoxes:
unitPrice = double.Parse(txtUnitPrice.Text);
scoops = int.Parse(txtScoops.Text);

// Compute results
subTotal = unitPrice * scoops;
salesTax = subTotal * TAX_RATE / 100;
totalCost = subTotal + salesTax;
```

第 32 行中的语句将输入到 txtUnitPrice 中的数据转换为 double 类型，因为 unitPrice 是 double 类型。类似地，在第 33 行中，来自 txtScoops 的数据被转换为 int 类型，因为 scoops 是 int 类型变量。

注意，当一个表达式同时包含乘法和除法时（如第 37 行所示），在决定计算顺序时这两种运算的优先级是相同的。计算从左到右进行，例如 (subTotal * TAX_RATE) / 100，在这里是可以的，因为先做乘法还是先做除法没有区别。

- **步骤 3-4：** 输入图 1-27 中的代码。

## 在 ListBox 中显示数据

在此应用程序中，输出以两列显示在 ListBox 中，第一列用于标签，第二列用于数字，如图 1-28 所示。通过将第二列中的数字右对齐并将其格式化为两位小数，可以自动对齐小数。

**图 1-28：** 格式化输出

![](img/143bad48262566137acc9c41f668a88f_61_0.png)

ListBox 可用于显示列表项，也可以让用户从列表中选择一个或多个项。这里我们仅使用 ListBox 来显示输出。我们将在第 5 章更详细地讨论 ListBox。

## ListBox 的字体

为了使小数对齐，将 ListBox 的字体设置为 Courier New 之类的等宽字体也很重要。

- **步骤 3-5：** 将 ListBox 的字体类型更改为 Courier New。添加图 1-29 中的以下代码以在 ListBox 中显示结果。

**图 1-29：** 在 ListBox 中显示格式化输出的代码

```
// Display Results with decimals aligned
lstOutput.Items.Add(string.Format("{0,12}{1,10:C}", "Sub Total:", subTotal));
lstOutput.Items.Add(string.Format("{0,12}{1,10:C}", "Sales Tax:", salesTax));
lstOutput.Items.Add(""); // Add a blank line
lstOutput.Items.Add(string.Format("{0,12}{1,10:C}", "Total Cost:", totalCost));
```

完整的代码应如图 1-25 所示。

- **步骤 3-6：** 运行窗体：
  - 双击 Program.cs 打开代码窗口。
  - 指定 IceCreamTotal 作为要运行的窗体的名称：

    ```
    Application.Run(new IceCreamTotal());
    ```

单击“开始”按钮运行窗体并测试输入的代码。运行窗体时，在“勺数”中不输入任何数据。再次运行，并将单价设为 $3.90。

请注意，在这两种情况下，程序都会因错误消息而崩溃，您需要重新运行程序。本章稍后你将学习如何让程序更优雅地处理错误。

## 清除 ListBox

Items 集合的 Clear 方法会清除 ListBox 中的所有行（项）。图 1-30 显示了清除 TextBox 和 ListBox 的代码。

**图 1-30：** 清除控件的代码

```
private void cmdClear_Click(object sender, EventArgs e)
{
    txtScoops.Clear();
    txtUnitPrice.Clear();
    lstOutput.Items.Clear();
}
```

- **步骤 3-7：** 将图 1-30 中的代码添加到 Clear 按钮的 click 事件处理程序中。

## 1.12 异常处理：捕获错误

try 子句中任何语句出错都会导致方法抛出异常，跳过其余语句并跳转到 catch 子句。如果没有错误，则跳过 catch 子句中的语句（称为 catch 块）。

**图 1-32：** try-catch 语句

```
private void btnComputeTotal_Click(object sender, EventArgs e)
{
    try
    {
        // Compute the total cost for an order of ice cream, including sales tax.
        // Declare variables to hold input data and computed results
        int scoops;
        ...
        lstOutput.Items.Add(string.Format("{0,12}{1,10:C}", "Total Cost:", totalCost));
    }
    catch (Exception err)
    {
        MessageBox.Show(err.Message);
    }
}
```

使用 catch 子句为异常对象指定名称 err（或任何有意义的名称），如下所示：

```
catch (Exception err)
```

异常对象的一个常用属性是 Message 属性，它包含描述导致异常的错误的错误消息——也就是说，err.Message 包含具体的错误消息。

## MessageBox

MessageBox 是 .NET 中可用于显示消息的对象。MessageBox 的 Show 方法允许将任何字符串作为消息显示。例如，可以使用以下语句显示消息：

```
MessageBox.Show("Invalid data; please re-enter");
```

我们使用 MessageBox 来显示 err.Message 中包含的消息。在 catch 子句中，我们使用以下语句：

```
MessageBox.Show(err.Message);
```

以显示 err.Message，其值是一个描述错误的字符串。

- **步骤 3-10：** 在 btnComputeTotal_Click 事件处理程序中加入 try-catch 语句，如图 1-32 所示。

- **步骤 3-11：** 运行窗体。输入单价但不输入勺数数据后，单击 Compute Total 按钮。注意错误消息。重复一次，这次输入两组数据，但在单价中包含“$”符号。


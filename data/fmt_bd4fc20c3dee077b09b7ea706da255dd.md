
正如你在第3章中所回想的，将事件连接到事件处理器的代码存储在表单的 `Designer.cs` 文件中。大多数情况下，你不需要处理这些代码。但是，你可能需要删除或修改某些语句。

如果你删除了事件处理器，例如如果不这样做，尝试运行应用程序时将会得到错误。此错误将显示在错误列表（`Error List`）窗口中，并指示缺少事件处理器。纠正此问题的方法可以是双击错误列表窗口中的错误消息。这将打开表单的 `Designer.cs` 文件并跳转到包含缺失事件处理器接线的语句。然后，你就可以删除该语句。

同样，如果你修改了事件处理器的名称，你也需要修改事件接线语句中的名称。实现此操作最简单的方法是在重命名事件处理器时使用第3章中描述的重构（`refactoring`）。这会自动更新相应事件接线语句中的事件处理器名称。但是，如果你喜欢在重命名事件处理器时使用重构，可以使用此图中所示的技术将相应的事件连接到新重命的事件处理器。

要接线事件处理器，Visual Studio 使用*委托*（`delegate`），它是一个表示方法的对象。在本文插图中，代码使用了由 .NET Framework 提供的 `EventHandler` 委托。此委托定义了可以处理事件方法的类型和参数列表。然后，代码使用 `new` 关键字创建一个 `EventHandler` 委托。当创建此委托时，方法的名称会被传递给委托。最后，为了将文本框的 `TextChanged` 事件连接到委托指定的方法，Visual Studio 使用 `+=` 运算符。

尽管你可以使用 C# 语言定义自己的委托，但很少需要这样做。目前，你可以专注于使用 .NET Framework 提供的委托。大多数情况下，这意味着使用本图所示的 `System.EventHandler` 委托。

为了让 C# 识别某个方法为事件处理器，该方法必须包含示例所示由 `EventHandler` 委托定义的两个参数。第一个参数是一个名为 `sender` 的对象。当执行事件处理器时，此参数将接收发生事件的对象。第二个参数标识一个名为 `e` 的 `EventArgs` 对象，其中包含有关事件的信息。其具体内容取决于发生的事件。

### 文本框的默认事件处理器

如示例所示，事件处理器的方法声明

```csharp
private void textBox1_TextChanged(object sender, EventArgs e)
{
}
```

如示例所示，事件处理器的方法声明

```csharp
textBox1.TextChanged += new EventHandler(textBox1_TextChanged);
```

### 自定义事件处理器

事件处理器的方法声明

```csharp
private void ClearValue(object sender, EventArgs e)
{
}
```

连接到事件处理器的语句

```csharp
textBox1.TextChanged += new EventHandler(ClearValue);
```

## 描述

- 当你使用表单设计器生成事件处理器时，会在 `Designer.cs` 文件中生成接线语句。
- 委托是一个表示方法的对象。
- 使用 .NET Framework 提供的 `EventHandler` 委托来接线。
- 此委托定义了处理方法。
- 第一个参数 `sender` 接收发生事件的对象。
- 第二个参数标识一个 `EventArgs` 对象，其中包含事件的信息。
- 使用 `new` 关键字创建 `EventHandler` 委托。
- 创建委托时，将方法名称传递给委托。
- 使用 `+=` 运算符将文本框的 `TextChanged` 事件连接到委托指定的方法。
- 尽管你可以使用 C# 语言定义自己的委托，但很少需要这样做。
- 目前，你可以专注于使用 .NET Framework 提供的委托。
- 大多数情况下，这意味着使用本文所示的 `System.EventHandler` 委托。
- 为了让 C# 识别某个方法为事件处理器，该方法必须包含 `EventHandler` 委托定义的两个参数。
- 第一个参数是一个名为 `sender` 的对象。当执行事件处理器时，此参数将接收发生事件的对象。
- 第二个参数标识一个名为 `e` 的 `EventArgs` 对象，其中包含有关事件的信息。其具体内容取决于发生的事件。
- 默认情况下，事件处理器的名称由表单或控件名称、下划线和事件名称组成。
- 要生成自定义名称的事件处理器，你可以在事件列表中的事件右侧输入事件处理程序的名称并按回车键生成。
- 当你为控件生成事件处理器时，Visual Studio 会为该事件处理器生成方法声明，并如下一步所示连接（或*接线*）事件。

图 6-6 如何为任何事件生成事件处理器

6-7 显示了两个事件处理器的声明，以及将相应事件连接到这些处理器的语句。如你所见，第一个事件处理器是用默认名称生成的。相比之下，第二个事件处理器被赋予了一个自定义名称。

## 未来价值应用方法的代码

```csharp
private void btnCalculate_Click(object sender, EventArgs e)
{
    decimal monthlyInvestment = Convert.ToDecimal(txtMonthlyInvestment.Text);
    decimal yearlyInterestRate = Convert.ToDecimal(txtInterestRate.Text);
    int years = Convert.ToInt32(txtYears.Text);

    int months = years * 12;
    decimal monthlyInterestRate = yearlyInterestRate / 12 / 100;

    decimal futureValue = this.CalculateFutureValue(
        monthlyInvestment, monthlyInterestRate, months);
    txtFutureValue.Text = futureValue.ToString("c");
    txtMonthlyInvestment.Focus();
}
```

```csharp
private decimal CalculateFutureValue(decimal monthlyInterestRate, int months)
{
    decimal futureValue = 0m;
    for (int i = 0; i < months; i++)
    {
        futureValue = (futureValue + monthlyInvestment)
        * (1 + monthlyInterestRate);
    }
    return futureValue;
}
```

```csharp
private void btnExit_Click(object sender, EventArgs e)
{
    this.Close();
}
```

```csharp
private void ClearFutureValue(object sender, EventArgs e)
{
    txtFutureValue.Text = "";
}
```

- `CalculateFutureValue` 方法将计算逻辑与计算按钮 `Click` 事件事件处理程序的其余部分分离离开。
- 每月投资、年利率和年限文本框的 `TextChanged` 事件已绑定到 `ClearFutureValue` 事件处理程序上。因此，每当用户更改这些框中的任一数据时，未来价值文本框都会被清空。

![](img/3148667e42d4db35b3d08576aaa1fa01_198_0.png)

## 生成的部分代码

图 6-10 显示了未来价值应用生成的代码列表。这些代码存储在表单的 `Designer.cs` 文件中，位于 Windows Form 设计器生成的代码区域内。在此图中，你可以看到为三个控件生成的代码：一个按钮和两个文本框。

首先，`InitializeComponent` 方法从相应的类创建对象，并将这些对象分配给已经声明的相应变量。接下来，`InitializeComponent` 方法包含每个控件的一组语句。这些语句中的大多数设置了这些控件的初始属性。

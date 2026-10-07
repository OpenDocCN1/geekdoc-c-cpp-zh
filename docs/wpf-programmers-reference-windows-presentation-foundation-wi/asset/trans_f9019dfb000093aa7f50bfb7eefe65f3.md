

# 示例代码

本章的源代码可以在书籍网站 www.wrox.com 下载，其中包含了几个示例应用程序，这些程序执行相同的功能，但使用了不同的技术将后台代码（code-behind）附加到用户界面。

图 11-1 显示了其中一个运行程序。你可以拖动滚动条或在文本框中输入蓝色值来设置右侧显示颜色的红、绿、蓝分量。如果你点击应用（Apply）按钮，程序会将窗口背景颜色设置为与当前样本匹配。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_218_0.png)

图 11-2 显示的 ImageColors 示例程序演示了在一个程序中附加后台代码的所有不同技术。程序中的不同按钮以不同的方式附加到事件处理程序。请从书籍网站下载此程序的 C# 或 Visual Basic 版本以查看详情。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_218_1.png)

# 事件名称属性

将后台代码附加到控件事件的第一种方法是在 XAML 代码中使用一种属性。该属性的名称与你想要捕获的事件相同。它的值是后台代码中事件处理程序的名称。

例如，以下 XAML 代码定义了一个名为 `btnApply` 的 Button。`Click` 属性表明 `btnApply_Click` 程序捕获了控件的 Click 事件处理程序。

```
<Button Content="Apply" IsDefault="True"
Name="btnApply" Click="btnApply_Click"/>
```

遗憾的是，如果你只是在 XAML 代码中添加事件处理程序声明，程序将无法运行。如果你尝试在 Expression Blend 或 Visual Studio 中执行它，将收到一个错误，提示你的程序不包含事件处理程序例的定义。

# 匿名控件

你并不真的需要给控件命名来赋予它事件处理程序。例如，上代码中的 Button 不需要命名为 `btnApply` 或任何名称。`Click` 属性告诉程序要执行哪个事件处理程序。如果你永远不在代码中引用该 Button（例如为了启用或禁用它），那么你可以省略名称。
然而，某些开发项目对控件命名有标准，某些项目可能坚持任何带有事件处理程序的控件都必须有名称。

# 不再分离

程序在没有事件处理程序的情况下无法运行这一事实凸显了 UI 构建与后台代码之间分离的严重崩溃。这意味着在事件处理程序存在之前，UI 设计师无法测试界面，但事件处理程序界面的一部分，因此它们本不属于界面设计师的职责范畴。你可以认为程序员应该在写完事件处理程序后再在 XAML 代码中编写事件名称属性，但程序员不需要接触界面。
在实践中，这可能并不是一个大问题——它意味着界面设计师和程序员需要相互交流。
本章后面提到的附加后台代码的技术——在运行时添加事件处理程序以及使用 `Handles` 子句（Visual Basic）——避免了这个问题。

以下 C# 代码处理了上一个 XAML 代码中定义的事件：

```sharp
private void btnApply_Click(object sender, RoutedEventArgs e)
{
this.Background = borSample.Background;
}
```

这段代码捕获了 `btnApply` 的 Click 事件，并根据 `borSample.Background` 属性使用的值设置窗口的 `Background` 属性（更多细节请见此文）。
你的代码不需要做任何操作来连接事件处理程序以捕获事件——Expression Blend 和 Visual Studio 会为你处理这些。

# 事件名称属性 | 183

以下 XAML 片段显示了 `EventNameAttributes` 示例程序如何确定哪个事件处理由程序按钮、控制红色分量的滚动条和文本框引发的按键事件。其他滚动条和文本框的代码是类似的。

```
<ScrollBar Orientation="Horizontal" Minimum="0" Maximum="255"
Grid.Row="0" Grid.Column="0" Name="scRed" ValueChanged="scRed_ValueChanged" />

<TextBox Margin="2" Grid.Row="0" Grid.Column="1" Text="255"
HorizontalAlignment="Right" VerticalAlignment="Center"
Name="txtRed" TextChanged="txtRed_TextChanged" />

<Button Grid.Row="3" Grid.Column="0" Grid.ColumnSpan="3" Width="100"
Height="40"
Content="Apply" IsDefault="True"
Name="btnApply" Click="btnApply_Click"/>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_220_0.png)

以下 C# 片段显示了当你使用第一个滚动条或文本框更改红色分量以及点击应用按钮时，`EventNameAttributes` 程序是如何响应的。其他滚动条和文本框的处理程序是类似的。

```csharp
// 滚动条改变。更新对应的文本框。
private void scRed_ValueChanged(object sender,
    RoutedPropertyChanged<double> e)
{
    if (txtRed != null)
    {
        txtRed.Text = e.NewValue.ToString();
    }
}

// 文本框改变。更新对应的滚动条。
private void txtRed_TextChanged(object sender, TextChangedEventArgs e)
{
    if (scRed != null)
    {
        scRed.Value = double.Parse(txtRed.Text);
    }
}
```


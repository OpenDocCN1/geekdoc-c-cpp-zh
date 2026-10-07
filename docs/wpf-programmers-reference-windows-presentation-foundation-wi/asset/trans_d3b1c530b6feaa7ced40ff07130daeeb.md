
图 11-3 显示了显示滚动条控件 `scrGreen` 事件的 Visual Studio 窗口。在此图中，该控件 `ValueChanged` 事件的下拉列表列出了具有 `ValueChanged` 事件正确签名的后置代码方法。（注意那个闪电按钮，它可以让窗口显示属性的事件）。

# 使用 XAML IntelliSense

在 Visual Studio 中创建事件处理程序的第三种方法是在 XAML 编辑器中使用 XAML IntelliSense。当你输入等号并开始输入事件属性名称时，IntelliSense 会显示所有可以捕获该事件的现有事件处理器列表。列表顶部是特殊项 `<Event Handler>`。如果你选择此条目，Visual Studio 将插入一个事件处理程序名称并创建一个事件处理程序存根。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_223_0.png)

图 11-3

> 如果你使用的是 Visual Basic，这种最后的方法会创建一个事件名称属性，而不是使用 `Handles` 子句。这是合理的，因为你正在通过在 XAML 代码编辑器中输入事件名称属性来创建 XAML 代码。

# NO HANDLES CLAUSE

图 11-4 IntelliSense 显示了具有 `TextBox txtBlue` 正确签名的后置代码方法。

| 设计 | XAML | |
| :--- | :--- | :--- |
| 100 % | | |
| <TextBox Name="txtGreen" TextChanged="txtGreen TextChanged" /> | | |
| <TextBox Margin="2" Grid.Row="2" Grid.Column="1" Width="230" /> | | |
| HorizontalContentAlignment="Right" VerticalContentAlignment="Center" /> | | |
| <Border Grid.Row="6" Grid.Column="0" /> | | |
| BorderBrush="Black" BorderTh="txtRed_TextChanged" /> | | |
| <New Event Handler Name="Sample"/ /> | | |
| txtGreen_TextChanged | <Button Grid.Row="3" Grid.Column="0" Content="Apply" IsDefault="True" /> |

图 11-4

如果你使用的是 C#，可以跳过此节，但如果你使用的是 Visual Basic，有时可以简化事件处理器。

Visual Basic 支持松散委托（Relaxed Delegates）。这些允许你将例程参数的数据类型替换为与实际传递给例程的数据一致的其他类型。这让你能够使事件处理器的参数比 Visual Studio 默认创建的更具体或不那么具体，有时可以简化代码。

例如，考虑 Visual Basic 生成的空 `Button Click` 事件处理器：

```vb
Private Sub btnApplyClick(ByVal sender As System.Object, _
    ByVal e As System.Windows.RoutedEventArgs)

End Sub
```

现在，假设此事件处理器仅绑定到 `Button Click` 事件。那么你知道 `sender` 参数始终是一个 `Button`，因此你可以在事件处理程序的声明中将其数据类型更改为 `Button`。

同时，你可能不需要使用参数 `e`。该参数包含有关事件的信息，例如代表事件的 `RoutedEventArgs` 对象，以及一个你可以从后续处理中设置为 `True` 的 `Handled` 标志。某些处理器也不需要这些信息。在这种情况下，你可以将参数的数据类型更改为通用且简单的 `Object`，而不是更琐的 `System.Windows.RoutedEventArgs`。

以下代码显示了修改后的事件处理器。事件处理器中的新行代码将 `Button` 的内容转换为字符串。如果 `Button` 显示简单的标题，代码将显示该标题。

```vb
Private Sub btnApplyClick(ByVal sender As Button, _
    ByVal e As Object)
MessageBox.Show(sender.Content.ToString())
End Sub
```

当 `sender` 被声明为 `System.Object` 时，你无法对它做很多操作。要访问其属性，你需要将它转换为 `Control`、`Button` 或其他更具体的类。

将 `sender` 参数声明为 `Button` 类型允许代码直接进行该转换并将其视为 `Button`。在这种情况下，这意味着你可以查看控件的 `Content` 属性。

松散委托还允许在你不需要使用参数时完全省略参数列表。以下代码显示了 `btnApply_Click` 事件处理器的最简单形式：

```vb
Private Sub btnApply_Click()

End Sub
```

当然，现在你无法再引用参数 `sender` 和 `e`，因为它们已存在了；这并不是一个问题。在许多应用程序中，按钮、菜单项、工具栏按钮和其他控件都绑定到它们自己的私有事件处理器，且没有控件共享这些处理器。只有 `btnApply` 按钮会将其 `Click` 事件发送到 `btnApply_Click` 事件处理器，此例程可以假设用户点击了它。在这种情况下，你使用松散委托来省略参数并使代码更易读。

`EventNameAttributesRelaxed` 示例程序在以下片段中使用 Visual Basic 通过其红色滚动条、红色文本框和 Apply 按钮来处理值。代码在 Visual Basic 中的效果与之前的 C# 版本一样，且没有事件处理器参数。

```vb
' 滚动条已更改。更新相应的文本框。
Private Sub scrRed_Changed()
    If txtRed Is Nothing Then Exit Sub
    txtRed.Text = CInt(scrRed.Value).ToString()
    ShowSample()
End Sub
```

```vb
' 文本框已更改。更新相应的滚动条。
Private Sub txtRed_Changed()
    ' 将值保持在范围内。
    Dim value As Integer
```


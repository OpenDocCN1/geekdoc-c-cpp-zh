

使用命令模式（Commanding）不仅能让代码在集中的地方处理操作，命令对象还为启用和禁用触发它的控件提供了一个中心点。例如，考虑一个复制命令。如果没有选择任何可以复制的文本，那么命令对象就可以禁用 [Ctrl]+C、右键菜单、“编辑：复制”以及任何触发复制的其它操作。

WPF 定义了许多命令对象，你可以将它们绑定到控件上以定义操作。某些命令与其他控件具有特殊关系，因此可以根据你的需要自动执行操作。最后，你可能需要定义新的命令对象来处理 WPF 未预料的其他操作。

接下来的章节描述了这三类命令对象：WPF 预定义的可以自动动作的命令、WPF 预定义但不能自动动作的命令，以及你在代码中定义的自定义命令。

## 带有动作的预定义命令

某些控件会自动为你实现命令绑定。例如，`TextBox` 知道如何提供复制、粘贴、撤销和重做操作。如果程序在 `TextBox` 获得焦点时执行预定义的 `ApplicationCommands.Copy` 命令，那么 `TextBox` 将将其选内容复制到剪贴板。

此外，你只需要告诉项目或按钮其命令是 `ApplicationCommands.Copy`，控件就会根据需要自动触发相应的操作。你不需要写一行代码！

图 19-2 显示的 `TextBoxCommands` 示例演示了 `TextBox` 控件支持的预定义命令。工具栏被程序的“编辑”菜单部分遮挡，包含复制、剪切、粘贴和重做命令，与菜单中显示的类似。

复制和剪切的菜单项以及工具栏按钮是禁用的，因为 `TextBox` 没有选择文本（你可以看到上方文本框中单词后有一个光标），所以这些命令没有意义。“粘贴”命令是启用的，因为在截屏时剪贴板中有文本，你可以将其粘贴到 `TextBox` 中。撤销和重做命令始终处于状态。（如果命令对象能根据 `TextBox` 是否存在可以撤销或重做的更改来适当启用和禁用会更好，但目前并没有这样做。）

以下代码显示了程序是如何生成它的：

```xml
<Menu DockPanel.Dock="Top">
  <MenuItem Header="Edit">
    <!-- 调用命令的菜单项 -->
    <MenuItem Command="ApplicationCommands.Copy"/>
    <MenuItem Command="ApplicationCommands.Cut"/>
    <MenuItem Command="ApplicationCommands.Paste"/>
    <Separator/>
    <MenuItem Command="ApplicationCommands.Undo"/>
    <MenuItem Command="ApplicationCommands.Redo"/>
  </MenuItem>
</Menu>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_386_0.png)

TextBoxCommands

代码将每个 `MenuItem` 的 `Command` 属性设置为预定义应用命令的名称。

## 简名称

命令名称前的 `ApplicationCommands.` 是可选的，例如，你可以将复制命令称为 `Copy` 而不是 `ApplicationCommands.Copy`。编写全名可以明显看出这些应用命令，但你可以使用任何你认为易读的样式。

`MenuItem` 会自动处理。它们会自动显示相应的文本和快捷键组合。当你调用其中一个菜单项时，它会激活命令对象，该对象让获得焦点的 `TextBox` 执行相应的操作。

## 简单方法

这是最简单的命令场景。它使用了一个预定义命令、一个内置支持该命令的控件（`TextBox`）以及一个内置支持表示和调用命令的控件（`MenuItem`）。

以下代码显示了程序是如何制作工具栏的：

```xml
<ToolBarTray Dock.Dock="Top" Background="Transparent">
  <ToolBar Band="1" BandIndex="1" Background="Transparent">
    <Button Command="Copy" Content="{Binding RelativeSource={RelativeSource}, Path=Command.Text}"/>
    <Button Command="Cut" Content="{Binding RelativeSource={RelativeSource}, Path=Command.Text}"/>
    <Button Command="Paste" Content="{Binding RelativeSource={RelativeSource}, Path=Command.Text}"/>
    <Separator/>
    <Button Command="Undo" Content="{Binding RelativeSource={RelativeSource}, Path=Command.Text}"/>
    <Button Command="Redo" Content="{Binding RelativeSource={RelativeSource}, Path=Command.Text}"/>
  </ToolBar>
</ToolBarTray>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_387_0.png)

TextBoxCommands

与 `MenuItem` 类似，工具栏的 `Button` 属性设置为它们执行的命令名称。但与 `MenuItem` 不同，`Button` 不会自动显示命令的文本和快捷键，程序包含了设置按钮文本的 XAML 代码。

每个 `Button` 的 `Content` 属性都被设置为一个绑定，该绑定让 WPF 像处理按钮一样获取其 `Command` 属性，从而让按钮显示命令的相应文本。

## 设置按钮文本

> 你可以显式地将按钮的 `Text` 设置为复制、剪切等，但这会增加与命令名称不匹配的额外错误几。像 `ApplicationCommands.Copy` 这样的命令会在任何适当控件允许操作时自动启用。例如，当 `textbox` 选中内容时，复制命令会激活其控件。如果你愿意，可以将命令绑定到 `textbox`。程序图 19 显示了当 `textbox` 没有焦点时如何禁用按钮。以下代码显示了程序是如何生成它的：

```xml
<StackPanel>
  <ToolBarTray Dock.Dock="Top" Background="Transparent">
    <ToolBar Band="1" BandIndex="1" Background="Transparent">
      <!-- 命令 -->
      <Button Command="Copy" Content="{Binding RelativeSource={RelativeSource}, Path=Command.Text}"/>
      <Button Command="Cut" Content="{Binding RelativeSource={RelativeSource}, Path=Command.Text}"/>
      <Button Command="Paste" Content="{Binding RelativeSource={RelativeSource}, Path=Command.Text}"/>
      <Separator/>
      <Button Command="Undo" Content="{Binding RelativeSource={RelativeSource}, Path=Command.Text}"/>
      <Button Command="Redo" Content="{Binding RelativeSource={RelativeSource}, Path=Command.Text}"/>
    </ToolBar>
  </ToolBarTray>
</StackPanel>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_388_0.png)
![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_388_1.png)


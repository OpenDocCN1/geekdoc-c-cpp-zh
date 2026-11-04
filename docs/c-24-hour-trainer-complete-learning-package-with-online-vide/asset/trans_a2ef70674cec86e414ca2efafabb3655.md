
> **注意** 对话框常常会设置其他属性，使其行为更像标准对话框。其中一些包括：
> 
> - 将 FormBorderStyle 设置为 FixedDialog，这样用户就无法调整对话框大小。
> - 设置 MinimumSize 和 MaximumSize 以保持对话框大小合理。（如果给对话框设置了可调整大小的边框。）
> - 将 MinimizeBox 和 MaximizeBox 设置为 False，这样用户就无法最小化或最大化对话框。
> - 将 ShowInTaskbar 设置为 False，这样对话框就不会使任务栏变得杂乱。

> **注意** 如果设置 Tab 键顺序，使焦点从窗体顶部开始并依次向下移动，就可以让对话框更加易用。例如，如果对话框包含 Name、Street、City、State 和 ZIP 文本框，焦点应按照该顺序在这些文本框之间移动。
> 
> 用户可以按 Tab 键在字段之间移动，并在所有值填写完毕后按 Enter 或 Esc。有经验的用户可以非常快速地填写这类对话框。

## 设置对话框结果

程序使用 ShowDialog 方法显示对话框。此方法返回一个值，指示用户单击了哪个按钮。如第 8 课所述，程序可以检查该返回值，以确定应如何处理对话框的结果。第 8 课中的示例在处理用户的选择之前，会检查 ShowDialog 是否返回了值 DialogResult.OK。

对话框窗体的 DialogResult 属性决定调用 ShowDialog 返回什么值。例如，可以使用以下代码让对话框的 OK 按钮将窗体的 DialogResult 属性设置为 DialogResult.OK，从而告诉调用程序用户单击了 OK 按钮：

```
// Return OK to ShowDialog.
private void okButton_Click(object sender, EventArgs e)
{
    DialogResult = DialogResult.OK;
}
```

设置窗体的 DialogResult 属性不仅决定返回结果，还会关闭对话框，使 ShowDialog 调用返回，调用代码可以继续执行。

这意味着你可以用一行代码设置对话框的返回结果并关闭对话框。输入一行代码应该不算什么难事，但信不信由你，还有一种更简单的方法来关闭对话框。

如果设置 Button 的 DialogResult 属性，则单击该 Button 时，它会自动设置窗体的 DialogResult 属性。例如，假设将 cancelButton 的 DialogResult 属性设置为 DialogResult.Cancel。当用户单击该 Button 时，它会自动将窗体的 DialogResult 属性设置为 DialogResult.Cancel，因此窗体会自动关闭。这样，你完全无需编写任何代码，就能设置返回值并关闭窗体。

如果你觉得设置一个 Button 属性仍然太麻烦，甚至可以避免这样做，至少对于 Cancel 按钮可以如此。当你设置窗体的 CancelButton 属性时，C# 会自动将该 Button 的 DialogResult 属性设置为 DialogResult.Cancel。

请注意，当你设置窗体的 AcceptButton 属性时，C# 不会自动设置该 Button 的 DialogResult 属性。其假设是 OK Button 可能需要先验证用户在窗体上输入的数据，再决定是否关闭对话框。例如，如果用户没有填写所有必填字段，OK Button 可能会显示一条消息，要求用户填写剩余字段，而不是关闭对话框。

> 注意 实际上，这些方法会隐藏对话框，使控制权返回调用代码，但它们不会调用其 Close 方法。这意味着对话框不会被销毁，因此调用代码可以查看用户在对话框上输入的值。

如果你不想执行任何验证，只需将 OK Button 的 DialogResult 属性设置为 DialogResult.OK。

## 使用自定义对话框

程序使用自定义对话框的方式与使用标准对话框完全相同。它会创建、初始化并显示对话框。它会检查返回结果，并采取适当的操作。

程序创建对话框的方式略有不同，因为可以在运行时将标准对话框添加到窗体，而自定义对话框不能这样做。要使用自定义对话框，代码需要创建对话框窗体的新实例，如第 9 课所述。

以下代码展示了程序如何显示新建客户对话框：

```
// Let the user create a new customer.
private void newCustomerButton_Click(object sender, EventArgs e)
{
    // Create and display a NewCustomerDialog.
    NewCustomerDialog newCustomerDialog;
    newCustomerDialog = new NewCustomerDialog();
    if (newCustomerDialog.ShowDialog() == DialogResult.OK)
    {
        // ... Create the new customer here ...
    }
}
```

代码声明一个变量来引用该对话框，并创建该对话框的新实例。它使用 ShowDialog 方法显示对话框，并检查返回结果。如果用户单击 OK，程序会采取创建新客户所需的任何步骤，例如向数据库添加记录。

## 试一试

在本“试一试”中，你将生成并使用图 10-2 所示的简单自定义对话框。该对话框允许你输入姓名。如果输入非空值并单击 OK，主窗体会将你输入的姓名添加到 ListBox 中。

![](img/d5be6ade75773ca6cec5c78f96a98bb1_189_0.png)

图 10-2

本“试一试”还会让你稍微练习使用 ListBox 控件，展示如何添加和移除项。

## 本课要求

本课中，你需要：

- 创建图 10-2 左上角所示的主窗体。将 New Comedian 按钮设为窗体的 AcceptButton，将 Delete Comedian 按钮设为窗体的 CancelButton。
- 创建图 10-2 右下角所示的对话框。以显而易见的方式设置 AcceptButton 和 CancelButton 属性。
- 让 New Comedian 按钮显示该对话框。如果对话框返回 DialogResult.OK，则将新喜剧演员的姓名添加到 ListBox 中。
- 让 Delete Comedian 按钮从 ListBox 中移除当前选中的喜剧演员。
- 当用户单击对话框的 Cancel 按钮时，隐藏对话框并返回 `DialogResult.Cancel`。
- 当用户单击对话框的 OK 按钮时，检查所输入姓名的长度。如果长度为 0，则显示一条消息，要求用户输入姓名。如果长度大于 0，则隐藏对话框并返回 `DialogResult.OK`。

> 注意 你可以从网站 www.wrox.com/go/csharp24hourtrainer2e 下载本课的代码和资源。

## 提示

- 使用 `ListBox` 的 `Items.Add` 方法向 `ListBox` 添加新项。
- 使用 `ListBox` 的 `Items.Remove` 方法移除选中项（由 `SelectedItem` 属性标识）。
- 检查 `nameTextBox.Text.Length == 0`，以判断对话框中输入的姓名是否为空。可以使用类似以下代码，在长度为 0 时执行一种操作，在长度不为 0 时执行另一种操作。注意 if 语句新增的 else 部分。如果条件为 true，则执行 if 子句之后的语句。如果条件为 false，则执行 else 子句之后的语句。（第 18 课会更详细地介绍 if 和 else。）
- 不要忘记将 `nameTextBox` 控件的 `Modifiers` 属性设置为 `Public`，以便主窗体的代码可以使用它。

```
if (nameTextBox.Text.Length == 0)
{
    ... Display a message here ...
}
else
{
    ... Return DialogResult.OK here ...
}
```

## 分步操作

创建图 10-2 左上角所示的主窗体。将 New Comedian 按钮设为窗体的 AcceptButton，将 Delete Comedian 按钮设为窗体的 CancelButton。

1. 启动一个新项目，并大致按图 10-2 所示添加一个 Label、一个 ListBox 和两个 Button。
2. 将 ListBox 的 Anchor 属性设置为 Top、Bottom、Left、Right。将 Button 的 Anchor 属性设置为 Top、Right。
3. 将窗体的 AcceptButton 属性设置为 New Comedian 按钮。将其 CancelButton 属性设置为 Delete Comedian 按钮。

创建图 10-2 右下角所示的对话框。以显而易见的方式设置 AcceptButton 和 CancelButton 属性。

1. 打开“项目”菜单，选择“添加 Windows 窗体”。输入名称 NewComedianDialog，然后单击“添加”。
2. 大致按图 10-2 所示添加一个 Label、一个 TextBox、一个 PictureBox 和两个 Button。
3. 将 TextBox 的 Anchor 属性设置为 Top、Left、Right。将 Button 的 Anchor 属性设置为 Bottom、Right。
4. 在 PictureBox 中放置你选择的图像，并将其 Anchor 属性设置为 Top、Bottom、Left。将其 SizeMode 属性设置为 Zoom。
5. 将对话框的 AcceptButton 属性设置为 OK 按钮。将其 CancelButton 属性设置为 Cancel 按钮。
6. 将对话框的 FormBorderStyle 属性设置为 FixedDialog，将其 ControlBox 属性设置为 False，并将其 ShowInTaskbar 属性设置为 False。

> 注意 设置控件的 Anchor 属性可以更容易地按你喜欢的方式调整窗体大小。所有内容都排列好后，将 FormBorderStyle 设置为 FixedDialog 可防止用户调整窗体大小，因此 Anchor 属性在运行时实际上不起作用。

让 New Comedian 按钮显示该对话框。如果对话框返回 DialogResult.OK，则将新喜剧演员的姓名添加到 ListBox 中。

1. 为 New Comedian 按钮创建事件处理程序。使用类似以下代码：

```
// Create a new comedian entry.
private void newComedianButton_Click(object sender, EventArgs e)
{
    NewComedianDialog newComedianDialog;
    newComedianDialog = new NewComedianDialog();
    if (newComedianDialog.ShowDialog() == DialogResult.OK)
    {
        // Add the new comedian.
        comedianListBox.Items.Add(
            newComedianDialog.nameTextBox.Text);
    }
}
```

让 Delete Comedian 按钮从 ListBox 中移除当前选中的喜剧演员。

1. 为 Delete Comedian 按钮创建事件处理程序。使用类似以下代码：

```
// Remove the currently selected comedian.
private void deleteComedianButton_Click(object sender, EventArgs e)
{
    comedianListBox.Items.Remove(comedianListBox.SelectedItem);
}
```


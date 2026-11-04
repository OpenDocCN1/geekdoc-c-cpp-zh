
私有可访问性有一个方面有时会让人困惑。私有字段对同一个类的任意实例中的任何代码都可见，而不仅仅是对该类的同一个实例可见。

例如，假设你构建了一个 Person 类，其中有一个名为 salary 的私有字段。不仅一个实例中的所有代码都能看到自己的 salary 值，而且任意 Person 对象都能看到任意其他 Person 对象的 Salary 值。

> NOTE 注意，公共字段被认为是不好的编程风格。最好改为创建公共属性。第 23 课解释了原因，并说明了如何创建属性。不过，公共字段确实可用，而且对于本次关于可访问性的讨论已经足够了。

## 限制作用域和可访问性

尽可能限制作用域和可访问性，以限制能够访问它的代码，这是一种良好的编程实践。例如，如果某段代码不该使用某个特定字段，就没有理由给它这个机会。这不仅能降低你错误使用该变量的可能性，还会将该变量从智能感知中移除，这样它就不会出现在那里扰乱你的选择并造成混淆。

如果你能使用在事件处理程序或其他方法内部局部声明的变量，那就这样做。事实上，如果你能在方法内部的代码块中（例如在循环中）声明变量，那就这样做。这样变量的作用域就非常有限，因此在你处理不相关的代码时，它不会造成妨碍。

如果你需要多个方法共享同一个值，或者需要在多次方法调用之间跟踪某个值，就把该值存储在私有字段中。只有当另一个窗体（或其他类）中的代码需要使用某个变量时，才将该变量设为公共。

## 动手试试

在本动手练习中，你将构建图 13-1 所示的程序。你将使用字段让两个窗体通信并执行简单计算。你还将试用一个新控件：ListView。

![](img/d5be6ade75773ca6cec5c78f96a98bb1_243_0.png)

图 13-1

### 课程要求

在本课中，你将：

-   创建图 13-1 右侧所示的 NewItemForm。
    -   提供公共字段，让主窗体获取用户输入的数据。
    -   当用户单击“确定”按钮时，将项名称、单价和数量值复制到公共字段中。
-   创建图 13-1 左侧所示的主窗体。
    -   当用户单击主窗体的“添加项”按钮时，让程序显示 NewItemForm。如果用户输入数据并单击“确定”按钮，则在主窗体的 ListView 控件中显示输入的值，并更新总计。

> NOTE 你可以从网站 www.wrox.com/go/csharp24hourtrainer2e 下载本课的代码和资源。

### 提示

-   记得适当设置 NewItemForm 的 AcceptButton、CancelButton、FormBorderStyle 和 ControlBox 属性。
-   由于主窗体的总计必须在用户添加项时保留其值，因此它必须是一个字段。
-   要让主窗体看到用户在 NewItemForm 上输入的值，请使用公共字段。

### 分步操作

-   创建图 13-1 右侧所示的 NewItemForm。
    1.  按图 13-1 所示排列控件。
    2.  将窗体的 AcceptButton 属性设置为“确定”按钮，将 CancelButton 属性设置为“取消”按钮。“确定”按钮将始终关闭窗体，因此将其 DialogResult 属性设置为 OK。
    3.  将窗体的 FormBorderStyle 属性设置为 FixedDialog。将其 ControlBox 属性设置为 False。
-   提供公共字段，让主窗体获取用户输入的数据。
    a.  声明供程序在计算中使用的公共字段。使用类似下面的代码，并将其放在任何方法之外：

```
// Public fields. (They should really be properties.)
public string ItemName;
public decimal PriceEach, Quantity;
```

当用户单击“确定”按钮时，将项名称、单价和数量值复制到公共字段中。

-   a.  将用户输入的值复制到上一步创建的字段中。

创建图 13-1 左侧所示的主窗体。

-   1.  创建 ListView、Button、Label 和 TextBox。设置它们的 Anchor 属性，并将 TextBox 设为只读。
-   2.  要让 ListView 按所示在列表中显示各项：
    a.  将其 View 属性设置为 Details。
    b.  选择其 Columns 属性，然后单击右侧的省略号按钮，打开图 13-2 所示的 ColumnHeader 集合编辑器。单击四次“添加”按钮以创建四列。使用右侧的属性编辑器设置每一列的 Name 和 Text 属性，并将数值列的 TextAlign 设置为 Right。

![](img/d5be6ade75773ca6cec5c78f96a98bb1_245_0.png)

图 13-2

当用户单击主窗体的“添加项”按钮时，让程序显示 NewItemForm。如果用户输入数据并单击“确定”，则在主窗体的 ListView 控件中显示输入的值，并更新总计。

-   1.  该按钮的 Click 事件处理程序应使用类似下面的代码：

```
// A private field to keep track of grand total
// across multiple calls to the event handler.
private decimal GrandTotal = 0;
```

```
// Let the user add a new item to the list.
private void addItemButton_Click(object sender, EventArgs e)
{
    NewItemForm frm = new NewItemForm();
    if (frm.ShowDialog() == DialogResult.OK)
    {
        // Get the new values.
        decimal priceEach = frm.PriceEach;
        decimal quantity = frm.Quantity;
        decimal totalPrice = priceEach * quantity;

        // Add the values to the ListView.
        ListViewItem lvi = itemsListView.Items.Add(frm.ItemName);
        lvi.SubItems.Add(priceEach.ToString("C"));
        lvi.SubItems.Add(quantity.ToString());
        lvi.SubItems.Add(totalPrice.ToString("C"));

        // Add to the grand total and display the new result.
        GrandTotal += totalPrice;
        grandTotalTextBox.Text = GrandTotal.ToString("C");
    }
}
```

> NOTE 如果一个窗体的代码试图直接访问另一个窗体中的字段，并在同一条语句中对该值执行操作，则可能会出现设计时错误。例如，假设本动手练习的主窗体使用以下代码：
> 
> ```
> MessageBox.Show(frm.Quantity.ToString());
> ```
> 
> 这里，frm 是指向 NewItemForm 对话框实例的变量，Quantity 是该对话框中的一个字段。在这种情况下，Visual Studio 会在设计时发出以下警告：
> 
> 访问 'NewItemForm.Quantity' 上的成员可能会导致
> 运行时异常，因为它是按引用封送类的字段
> 
> 这里的问题比较隐蔽，只有在程序跨进程或跨计算机边界使用该对话框时才会发生，例如，当你的程序试图显示一个定义在另一个编程线程上的对话框时。
> 
> 这个警告可能不像汽车里的低油压警告那么重要，但一般来说忽略警告并不好。幸运的是，让这个警告消失很容易。只需将返回的结果复制到局部变量中，然后操作该变量，而不是直接操作对话框的字段。例如，你可以使用以下代码：
> 
> ```
> decimal quantity = frm.Quantity;
> MessageBox.Show(quantity.ToString());
> ```

## 练习

1.  复制你为“动手试试”构建的程序，并修改“新建项”窗体，使其“确定”按钮仅当三个 TextBox 都包含非空白文本时才启用。

2.  [困难] 复制你为练习 1 构建的程序，并向主窗体添加一个新的“删除项”按钮，用于删除当前选中的项。提示：
    -   将 ListView 控件的 MultiSelect 属性设置为 False，并将其 FullRowSelect 属性设置为 True。
    -   仅当在 ListView 控件中选中了某个项时，才启用该按钮。
    -   ListView 控件的 SelectedIndices 属性是当前选中项的集合。使用该集合的 Count 属性来确定是否选中了任何项。
    -   使用以下代码从 ListView 控件中移除选中的项：

```
// Delete the selected item.
private void deleteItemButton_Click(object sender, EventArgs e)
{
    // Get the selected item.
    ListViewItem item = itemsListView.SelectedItems[0];

    // Get the item's Total Price.
    decimal totalPrice =
        decimal.Parse(item.SubItems[2].Text, NumberStyles.Any);

    // Subtract from the grand total and display the new result.
    GrandTotal -= totalPrice;
    grandTotalTextBox.Text = GrandTotal.ToString("C");

    // Remove the item from the ListView.
    itemsListView.Items.Remove(item);
}
```

3.  如果你正确输入了练习 2 中所示的代码，那么你的程序包含一个 bug。（要看到它，请添加一个项，然后删除它。）使用调试器修复程序。

4.  使用与练习 3 类似的设计，让用户填写预约日历。主窗体应包含一个 ListView，其列标题为“主题”、“日期”、“时间”和“备注”。NewAppointmentForm 应提供 TextBox，供用户输入这些值，并应具有公共字段 AppointmentSubject、AppointmentDate、AppointmentTime 和 AppointmentNotes，以便主窗体获取输入的值。主窗体应显示预约数量，而不是总计。仅当“主题”、“日期”和“时间”非空白时，才启用“新建预约”窗体的“确定”按钮。

5.  构建一个包含 ListBox、TextBox 和 Button 的窗体。当用户单击该 Button 时，显示一个对话框，让用户输入一个数字。为该对话框提供一个公共字段，以便将值返回给主窗体。


## 事件处理方法

示例 10–7 包含事件处理方法的标题。所有事件处理方法通常具有相同的签名。它们不返回任何内容；其 `return` 类型为 `void`。它们接受两个参数。第一个参数 `object` sender 表示引发事件的源，第二个参数是事件的数据。例如，对于 `MouseEventArgs` 事件，可访问的数据包括单击了哪个鼠标按钮（左键、右键或两者）、单击次数，以及单击鼠标按钮时鼠标指针在屏幕上的位置的 x 和 y 坐标。这些数据可以从第二个参数获取。

`delegate` 维护一个事件的已注册事件处理程序列表。若要标识你希望接收通知的事件，请注册该事件，并通过键入事件处理方法的体来指定事件发生时要执行的操作。事件处理程序使用委托调用。

接下来的各节重点介绍一些最有趣的事件，你可以将它们包含在应用程序中以添加功能。将使用 Visual Studio 创建一个应用程序；添加控件、设置其属性并编写其事件程序。

## ListBox 控件对象

ListBox 控件是一个功能非常强大的部件，可以添加到 Windows 应用程序中。ListBox 控件可用于显示项目列表，用户可以从中进行单选或多选。如果项目总数超过可显示的数量，控件会自动添加滚动条。你可以在设计时或运行时动态地向 ListBox 控件添加或从中移除项目。

### 创建用于承载 ListBox 控件的窗体

要体验使用 ListBox 对象，使用 Windows 应用程序模板在 Visual Studio 中创建一个新项目。请参见后面的图 10–5。它显示了完成后的窗体。选择 Windows 应用程序模板时，会自动生成一个空白窗体。该窗体的 Name 属性设置为 ClubForm。ClubForm 的 Font 属性设置为 12 磅。此属性在 Form1 对象上设置，因此添加到 ClubForm 的其他对象将已设置好；这将成为应用程序的默认字体。此过程可确保各控件在字体选择上保持一致。当然，如果需要一个或多个控件使用不同字体，也可以为单个控件设置 Font。为 ClubForm 设置 BackColor 蓝色 (128, 128, 255)。Text 属性设置为“计算机俱乐部郊游报名”。

![](img/e33ae760e23d89eac66541252ad65de8_581_0.png)

> 请记住，你需要使用“窗体设计器”窗口在设计时设置属性。如果你位于“代码编辑器”而不是“窗体设计器”中，请从“视图”菜单中选择“设计器”，或按 Shift+F7。按 F7 返回“代码编辑器”。如果你选择不使用“属性”窗口设置属性，可以将程序语句添加到 `FormLoad()` 事件处理方法中以进行赋值。

将一个 TextBox 对象拖到 ClubForm 对象上，并放置在窗体底部。Name 属性设置为 `txtBoxResult`。此文本框存储列表框选择的结果。向 ClubForm 添加一个 Label 对象，放在 TextBox 对象左侧，其 Text 属性设置为“结果”。

### 添加 ListBox 控件对象

向 ClubForm 的左上角添加另一个 Label 对象，其 Text 属性设置为“选择活动”。将一个 ListBox 对象拖到“选择活动”标签下方。其 Name 属性设置为 `lstBoxEvents`。使用 BackColor 属性设置控件的背景色。它设置为黄色 (255, 255, 192)。ForeColor 属性设置为蓝色 (0, 0, 192)，以便字体字符显示为蓝色。Items 属性用于设置列表框的初始值。单击 Items 属性中 Collection 一词右侧带有省略号的按钮，会显示“字符串集合编辑器”窗口。使用此编辑器在单独的行上键入列表框的值。图 10–2 显示了为列表框集合键入值后的窗口。键入以下字符串值，每个值单独一行：

- "电影"
- "舞蹈"
- "乘船游览"
- "晚餐"
- "徒步"
- "游乐园"
- "体育赛事"

![](img/e33ae760e23d89eac66541252ad65de8_582_0.png)

图 10–2   字符串集合编辑器

为 `ListBox` `object` 将 Sorted 属性设置为 `true`。这样你就不必按排序后的项目顺序将值键入集合。通过将 Sorted 属性设置为 `true`，它们会按排序显示——就像你按该顺序键入它们一样。通过单击控件 `object` 并使用标准 Windows 大小调整手柄拖动 `object` 来调整控件 `object` 的大小，以便仅显示四个字符串。如果窗口太小而无法显示所有选项，则在运行应用程序时会自动向 `ListBox` 对象添加滚动条。

将控件放置到大致位置后，使用“格式”、“对齐”菜单选项来对齐相关控件，使它们一致地放置在同一行或同一列。通过将鼠标用作选择工具，在控件周围绘制一个框来选择多个控件，或者在选择多个控件时按住 Ctrl 键。

### 注册 ListBox 事件

要添加功能，需要为 `ListBox` 控件 `object` 注册一个事件。举例来说，你可能想知道项目选择何时更改。当它更改时，你可能希望显示或使用该选择。在“窗体设计器”中，双击控件时，会为该特定控件注册默认事件。该已注册事件的事件处理方法会添加到源代码中。

你可能不想为控件的默认事件编写方法。你感兴趣的可能是另一个事件。`button` `object` 的默认事件是 Button Click 事件。因此，当你在“窗体设计器”中双击按钮时，会注册 `buttonName_Click` 事件。这通常是 Button 对象所关注的事件。单击 **属性** 窗口中的 `Event` 图标（闪电符号），会显示可为所选 `object` 注册的事件选择。

双击 `ListBox` 控件会添加示例 10-8 中所示的行，该行将 `SelectedIndexChanged` 事件注册为关注的事件。

### 示例 10-8

```
    this.lstBoxEvents.SelectedIndexChanged += new
        System.EventHandler(this.lstBoxEvents_SelectedIndexChanged);
```

“窗体设计器”还会将示例 10-9 中所示的方法体为空的方法添加到程序中。

### 示例 10-9

```
    private void lstBoxEvents_SelectedIndexChanged(object sender,
        System.EventArgs e)
    {
    }
```

### ListBox 事件处理程序

ListBox 类的属性之一是 SelectedItem。它返回一个表示所选字符串项的对象。如果使用此属性检索选择，则必须将该对象转换为字符串对象，以便在“结果”文本框中显示它。txtBoxResult 对象的 Text 属性用于显示选择。将示例 10-10 中的语句添加到 `lstBoxEvents_SelectedIndexChanged()` 方法的主体中，以便在事件触发时显示选择。

### 示例 10-10

```
private void lstBoxEvents_SelectedIndexChanged(object sender,
                                             System.EventArgs e)
{
        this.txtBoxResult.Text =
                this.lstBoxEvents.SelectedItem.ToString();
}
```

`ToString()` 方法用于将项对象转换为字符串以便显示；Text 属性也可用于从 ListBox 控件对象检索数据。如果使用 Text 属性而不是 SelectedItem 属性，则无需添加 `ToString()` 方法。因此，`lstBoxEvents_SelectedIndexChanged` 方法的主体可以如示例 10-11 所示。

### 示例 10-11

```
private void lstBoxEvents_SelectedIndexChanged(object sender,
                                             System.EventArgs e)
{
        this.txtBoxResult.Text = this.lstBoxEvents.Text;
}
```

图 10–3 显示了 SelectedIndexChanged 事件触发后由示例 10–11 生成的输出。请注意，各项按字母顺序显示。Sorted 属性重新排列了各项。

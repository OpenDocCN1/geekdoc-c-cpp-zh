
# 第 14 章 使用 Windows Forms 构建图形用户界面：第一部分

## 外观观察 14.3

你可以通过在 GroupBox 或 Panel 内部锚定（anchoring）和停靠（docking）控件来组织 GUI。GroupBox 或 Panel 本身也可以在 Form 内部进行锚定或停靠。这可以将控件划分为“组”，并方便地进行布局。

要创建一个 GroupBox，请从工具箱（Toolbox）将其拖动到 Form 上。然后，从工具箱将新控件拖入 GroupBox 中。这些控件会被添加到 GroupBox 的 `Controls` 属性中，并成为 GroupBox 的一部分。GroupBox 的 `Text` 属性用于标识该 GroupBox 的标题。

要创建一个 Panel，请从工具箱将其拖动到 Form 上。你可以通过将控件从工具箱拖入 Panel 直接向其添加控件。要启用滚动条，请将 Panel 的 `AutoScroll` 属性设置为 `true`。如果 Panel 调整大小后无法显示所有控件，则会显示滚动条（图 14.23）。滚动条用于在设计时和运行期间查看 Panel 中的所有控件。在图 14.23 中，我们将 Panel 的 `BorderStyle` 属性设置为 `FixedSingle`，以便你可以在 Form 中看到该 Panel。

![](img/57baed2319be0bb1b5f98674846f2711_604_0.png)

图 14.23 | 创建带有滚动条的 Panel。

14.24 中的程序使用 GroupBox 和 Panel 来排列按钮。当这些按钮被点击时，它们的事件处理程序会更改 Label 上的文本。

```csharp
// Fig 14.24: GroupBoxPanelExampleForm.cs
// 使用 GroupBoxes 和 Panels 布局按钮。
using System;
using System.Windows.Forms;

namespace GroupBoxPanelExample
{
    // 显示 GroupBox 和 Panel 的 Form
    public partial class GroupBoxPanelExampleForm : Form
    {
```

图 14.24 | 使用 GroupBoxes 和 Panels 布局按钮。（2 部分中的第 1 部分）

## 14.6 GroupBoxes 和 Panels

```csharp
// 默认构造函数
public GroupBoxPanelExampleForm() {
    InitializeComponent();
}

// Hi Button 的事件处理程序
private void hiButtonClick(object sender, EventArgs args) {
    messageLabel.Text = "Hi pressed"; // 更改 Label 中的文本
}

// Bye Button 的事件处理程序
private void byeButtonClick(object sender, EventArgs args) {
    messageLabel.Text = "Bye pressed"; // 更改 Label 中的文本
}

// Far Left Button 的事件处理程序
private void leftButtonClick(object sender, EventArgs args) {
    messageLabel.Text = "Far Left pressed"; // 更改 Label 中的文本
}

// Far Right Button 的事件处理程序
private void rightButtonClick(object sender, EventArgs args) {
    messageLabel.Text = "Far Right pressed"; // 更改 Label 中的文本
}
```

![](img/57baed2319be0bb1b5f98674846f2711_605_0.png)

**14.24** | 使用 GroupBoxes 和 Panels 布局按钮。（2 部分中的第 2 部分）

主GroupBox 有两个按钮——hiButton（显示 Hi）和 ByeButton（显示 Bye）。Panel（命名为 mainPanel）也有两个按钮，leftButton（显示 Far Left）和 rightButton（显示 Far）。mainPanel 的 `AutoScroll` 属性设置为 `true`，当 Panel 的内容超过 Panel 的可见区域时，滚动条就会出现。Label（命名为 messageLabel）初始为空白。要控制 mainGroupBox 或 Panel，Visual Studio 会调用每个容器的 `Controls` 的 `Add` 方法。此属性位于文件 `GroupBoxPanelExampleForm.Designer.cs` 所在部分类中。

四个按钮的事件处理程序位于第 18–39 行。第 20、26、38 行更改 `messageLabel` 的文本，以指示用户点击了哪个按钮。

## 14.7 CheckBoxes 和 RadioButtons

C# 有两种可以处于开启/关闭或真/假状态的状态按钮——CheckBoxs 和 RadioButtons。像 Button 类一样，CheckBox 和 RadioButton 类派生自 ControlBase 类。

### 14.7.1 CheckBoxes

CheckBox 是一个小正方形，为空白或包含勾选标记。当用户点击 Check 选中它时，框中会出现勾选标记。如果用户点击 Check 取消选中，则勾选标记会被移除。你可以通过将 `Three-State` 属性设置为 `true`，使 CheckBox 在三种状态（*已选中*、*未选中*和*不确定*）之间切换。可以同时选择任意数量的 CheckBox。常用 CheckBox 属性列表和和一个常用事件见图 14.25。

| CheckBox 属性及事件 | 描述 |
|---|---|
| **常用属性** | |
| Appearance | 默认情况下，该属性设置为 `Normal`，CheckBox 显示为传统的复选框。如果设置为 `Button`，CheckBox 将显示为按钮，在按下且 CheckBox 被选中时会循环显示。此属性返回一个 `bool` 值。 |
| Checked | 指示 CheckBox 是*已选中*（包含勾选标记）还是*未选中*（空白）。默认值为 *false*（*未选中*）。 |
| CheckState | 使用 `CheckState` 枚举值指示 CheckBox 是*已选中*还是*未选中*。 |
| Text | 指定文本。 |
| Three-State | 为 `true` 时，CheckBox 有三种状态——*已选中*、*未选中*和*不确定*。 |
| **常用事件** | |
| Changed | 每次 `CheckState` 发生变化时触发。 |

*(注：由于提供的原始文本存在大量重复和 OCR 错误，此处已根据逻辑流进行了整合和清理。)*

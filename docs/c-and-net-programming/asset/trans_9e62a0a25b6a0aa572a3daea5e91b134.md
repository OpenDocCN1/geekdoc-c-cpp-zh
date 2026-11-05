
## 说明

- **EventArgs** 是所有事件数据的基类。除构造函数外，EventArgs 类仅从 Object 继承其所有方法，不过它确实添加了一个公共静态字段 *empty*，表示没有状态的事件（以允许高效使用无状态事件）。
- 如果事件没有数据传递，则传递的事件参数的类型为 EventArgs，它没有任何公共属性，本质上是一个占位符。如果有数据需要传递，例如鼠标单击的位置或按下了哪个键，则事件参数将是派生自 EventArgs 的类型，并且它将具有用于传递数据的属性。
- 事件处理程序的一般签名如下
- 一些事件使用基类 EventArgs，但 EventArgs 不包含有关事件的任何有用附加信息。需要事件处理程序了解事件的附加信息的控件将传入派生自 EventArgs 的类型的对象。
- 例如，TreeView AfterCollapse 事件处理程序接收的类型为 TreeViewEventArgs 的参数，派生自 EventArgs。TreeViewEventArgs 具有属性 Action 和 Node，每个属性的值都特定于实际事件。

```
private void Handler (object sender, EventArgs e)
```

```
Private Sub Handler (ByVal sender As Object, ByVal e As EventArgs)
```

## 11. 鼠标事件

### 1. 常用控件事件

| 事件 | 事件参数 | 描述 |
|---|---|---|
| Click | EventArgs | 当控件被鼠标单击时触发。 |
| ControlAdded | ControlEventArgs | 当新控件添加到 Control.ControlCollection 时触发。 |
| ControlRemoved | ControlEventArgs | 当控件从 Control.ControlCollection 中移除时触发。 |
| DockChanged | EventArgs | 如果 Dock 属性——即控件停靠到父容器的哪条边——因用户交互或程序控制而更改时触发。 |
| DoubleClick | EventArgs | 当控件被双击时触发。如果控件同时具有 Click 和 DoubleClick 事件处理程序，则 DoubleClick 会被 Click 事件抢占。 |
| Enter | EventArgs | 当控件获得焦点时触发。对 Form 对象被抑制。对于嵌套控件，会沿容器层次结构向上向下级联。 |
| Layout | LayoutEventArgs | 当影响控件布局的任何更改发生时触发（例如，控件被调整大小或子控件被添加或移除）。 |
| Leave | EventArgs | 当焦点离开控件时触发。 |
| Move | EventArgs | 当控件移动时触发。 |
| Paint | PaintEventArgs | 当控件重绘时触发。 |
| ParentChanged | EventArgs | 当控件的父容器更改时触发。 |
| Resize | EventArgs | 当控件调整大小时触发。通常更可取使用 Layout 事件。 |
| SizeChanged | EventArgs | 当 Size 属性因用户交互或程序控制而更改时触发。通常更可取使用 Layout 事件。 |
| TextChanged | EventArgs | 当 Text 属性因用户交互或程序控制而更改时触发。 |
| Validating | CancelEventArgs | 当控件正在验证时触发。如果 CancelEventArgs.Cancel 属性设为 true，则所有后续焦点事件将被抑制。如果 Control.CausesValidation 属性设为 false 则被抑制。 |
| Validated | EventArgs | 当控件完成验证时触发。如果传递给 Validating 事件的 CancelEventArgs.Cancel 属性设为 true 则被抑制。如果 Control.CausesValidation 属性设为 false 则被抑制。 |

### 2. 控件拖放事件

| 事件 | 事件参数 | 描述 |
|---|---|---|
| DragDrop | DragEventArgs | 当拖放操作完成时触发。 |
| DragEnter | DragEventArgs | 当对象被拖到控件上时触发。此时拖放操作仍在进行中（即用户尚未松开鼠标按钮）。 |
| DragLeave | DragEventArgs | 当对象从控件上拖离时触发。 |
| DragOver | DragEventArgs | 当对象在控件上拖动时触发。 |
| GiveFeedback | GiveFeedbackEventArgs | 在拖放操作期间触发，以允许修改鼠标指针。 |

### 3. 控件鼠标事件

| 事件 | 事件参数 | 描述 |
|---|---|---|
| MouseEnter | EventArgs | 当鼠标指针进入控件时触发。 |
| MouseMove | MouseEventArgs | 当鼠标指针在控件上移动时触发。 |
| MouseHover | EventArgs | 当鼠标悬停在控件上时触发。 |
| MouseDown | MouseEventArgs | 当鼠标指针位于控件上方时鼠标按钮被按下时触发。 |
| MouseWheel | MouseEventArgs | 当控件具有焦点时鼠标滚轮移动时触发。 |
| MouseUp | MouseEventArgs | 当鼠标指针位于控件上方时鼠标按钮被释放时触发。 |
| MouseLeave | EventArgs | 当鼠标指针离开控件时触发。 |

## 12. 键盘事件

键盘事件提供对按键生成事件实现的访问。

### 1. 所有控件的键事件

| 事件 | 事件数据 | 描述 |
|---|---|---|
| KeyDown | KeyEventArgs | 当按键按下时触发。KeyDown 事件发生在 KeyPress 事件之前。 |
| KeyPress | KeyPressEventArgs | 当生成字符的键被按下时触发。KeyPress 事件发生在 KeyDown 事件之后，KeyUp 事件之前。 |
| KeyUp | KeyEventArgs | 当按键释放时触发。 |

- KeyDown 和 KeyPress 事件并不相同，因为它们在键盘事件流中的不同点触发，并且在 EventArgs 对象中包含不同的信息。
- 与 KeyDown 和 KeyUp 事件关联的 KeyEventArgs 事件数据提供了关于按键的低级信息。
- 此信息用于确定是否按下了大写或小写字符。它还说明是否与之组合按下了任何修饰键（Alt、Ctrl 或 Shift）。

### 2. KeyEventArgs 属性（KeyDown 和 KeyUp）

| 属性 | 数据类型 | 描述 |
|---|---|---|
| Alt | Boolean | 只读值指示 Alt 键是否被按下。`true` 如果按下，`false` 否则。 |
| Control | Boolean | 只读值指示 Ctrl 键是否被按下。`true` 如果按下，`false` 否则。 |
| Shift | Boolean | 只读值指示 Shift 键是否被按下。`true` 如果按下，`false` 否则。 |
| Modifiers | Keys | 只读标志指示按下的修饰键（Alt、Ctrl、Shift）的组合。修饰键可使用按位或运算符组合。 |
| Handled | Boolean | 指示事件是否已处理的数值。`false` 直到另行设置。 |
| KeyCode | Keys | 包含所按键的键码的只读值。典型值包括 A 键、Alt 和 BACK（退格）。 |
| KeyData | Keys | 包含所按键的键码的只读值，并结合修饰符标志以指示修饰键（Alt、Ctrl、Shift）的组合。 |
| KeyValue | integer | 键码属性以只读整数形式表示。 |

### 3. Unicode 和 ASCII 字符

- ASCII 字符集（美国信息交换标准委员会）中的每个字符都由一个字节（8 位）数据表示，共表示 256 个字符。前 128 个字符（由 7 位表示）是标准化的，通常称为低位 ASCII 字符。上面 128 个字符未标准化，尽管许多成熟的字符集使用全部 256 个字符。
- Unicode 字符是 ASCII 字符集的超集。它们由两个字节表示，允许最多 65,536 个字符。Unicode 技术被引入以便于表示英语以外的语言，特别是中文和日文等没有有限字母表的亚洲语言。Unicode 还允许字符集包含比 ASCII 字符集多得多的字符，例如特殊符号和字符样式。

### 4. KeyPressEventArgs 属性（KeyPress）

| 属性 | 描述 |
|---|---|
| Handled | 指示事件是否已处理的布尔值。false 直到另行设置。当为 true 时，按键不会显示。 |
| KeyChar | 包含合成 ASCII 字符的只读 char 类型值。 |

## 示例 1

```
//illustration of Button events
using System;
using System.Drawing;
using System.Collections;
using System.ComponentModel;
using System.Windows.Forms;
using System.Data;

public class EventsForm : Form{
private Button m_nameButton;
private Button m_okButton;
private Label m_nameLabel;
private Container m_components = null;

public EventsForm(){
initializeComponents();
}
private void initializeComponents(){
m_nameLabel=new Label();
m_nameButton = new Button();
m_okButton = new Button();

SuspendLayout();

m_nameLabel.Location=new Point(16,16);
m_nameLabel.Text="Click User NAME button";
m_nameLabel.Size=new Size(300,23);
```

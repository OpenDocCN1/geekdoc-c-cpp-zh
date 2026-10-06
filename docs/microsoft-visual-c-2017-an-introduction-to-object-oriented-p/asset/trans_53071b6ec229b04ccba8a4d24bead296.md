

# 理解控件

(续)

| 属性 | 描述 |
|---|---||
| Bottom | 获取控件底部与其容器客户区域顶部之间的距离（以像素为单位） |
| Bounds | 获取或设置控件的大小和位置（包括其非客户元素），相对于父控件的，以像素为单位 |
| CanFocus | 获取一个值，表示控件是否可以接收焦点 |
| CanSelect | 获取一个值，表示控件是否可以被选中 |
| Capture | 获取或设置一个值，表示控件是否捕获了鼠标 |
| Container | 获取包含该组件（继承自 Component）的 IContainer 接口 |
| ContainsFocus | 获取一个值，表示控件或其一个子控件当前是否具有输入焦点 |
| Cursor | 获取或设置当鼠标指针悬停在控件上时显示的光标 |
| Disposing | 获取一个值，表示基类 Control 类是否处于释放过程中 |
| Dock | 获取或设置哪些控件边界停靠在其父控件上，并决定控件如何随父控件调整大小 |
| Enabled | 获取或设置一个值，表示控件是否能响应用户操作 |
| Focused | 获取一个值，表示控件是否具有输入焦点 |
| Font | 获取或设置控件显示文本的字体 |
| | 获取或设置控件的前景颜色 |
| HasChildren | 获取一个值，表示控件是否包含一个或多个子控件 |
| Height | 获取或设置控件的高度 |
| IsDisposed | 获取一个值，表示控件是否已释放 |
| Left | 获取控件左边缘与其容器客户区域左边缘之间的距离（以像素为单位） |
| Location | 获取或设置控件左上角相对于其容器左上角的坐标 |
| Margin | 获取或设置控件之间的间距 |
| ModifierKeys | 获取一个值，表示哪些修饰键（Shift, Ctrl, Alt）处于按下状态 |

**表 12-2** 选定的公共 Control 属性（续）

# 第 12 章 使用控件

(续)

| 属性 | 描述 |
| --- | --- |
| MouseButtons | 获取一个值，表示哪一个鼠标按键处于按下状态 |
| MousePosition | 获取鼠标光标在屏幕坐标系中的位置 |
| Name | 获取或设置控件的名称 |
| Parent | 获取或设置控件的父容器 |
| Right | 获取控件右边缘与其容器客户区域左边缘之间的距离（以像素为单位） |
| Size | 获取或设置控件的高度和宽度 |
| TabIndex | 获取或设置控件在容器内的制表顺序 |
| TabStop | 获取或设置一个值，表示用户是否可以使用按键给控件赋予焦点 |
| Text | 获取或设置与此控件关联文本 |
| Top | 获取或设置控件顶部与其容器客户区域顶部之间的距离（以像素为单位） |
| TopLevelControl | 获取未被其他 Windows Forms 控件包含的父控件；通常，这是包含该控件的最外层 Form |
| Visible | 获取或设置一个值，表示控件及其所有父控件是否都显示 |
| Width | 获取或设置控件的宽度 |

表 12-2 选定的公共 Control 属性

> 表 12-2 中每个属性的描述指示了该属性是否为只读；此类属性只获取值而不进行设置。

> 你已经使用 Visual Studio 中的属性窗口更改了 Label、TextBox 和 Button 的属性（如 Text 和 Visible）。在本章中你学到的其他控件都可以以相同的方式进行操作。

> 一个项目可以包含多个 Form，每个 Form 都有自己的控件。你将在本章后面的“你来做做”练习中学习如何向项目添加更多 Form。

# 两个真理和一个谎言
理解控件

1. Control 类实现了用户在屏幕上看到的 GUI 对象所需的基本功能。
2. 大多数控件具有 Font 和 ForeColor 属性。
3. 每个控件都有 width 和 Height 属性。

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_567_0.png)

# 检查 IDE 自动生成的代码

图 12-2 显示在 IDE 中创建的 Form。执行了以下操作：

1. 启动了一个新的 Windows 并命名为 FormWithLabelAndButton。
2. 将一个 Label 拖到 Form1 上。使用 IDE 中的属性窗口，将 Label 的 Text 属性更改为 "Click the button"，并将其 Font 更改为 Georgia、加粗且大小为 16。其 Name 未从默认的 label1 更改。
3. 将一个 Button 拖到 Form1 上。将 Button 的 Text 属性更改为 "OK"，并将其 Name 从默认的 button1 更改为 okButton。

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_567_1.png)

图 12-2 由 FormWithLabelAndButton 程序生成的 Form

# 第 12 章 使用控件

当设计器中拖动控件或在属性窗口中更改属性时，Visual Studio 会在 Form1.Designer.cs 中自动生成代码。打开 Form1.Designer.cs 文件时，可以在 InitializeComponent() 方法附近看到以下行：

```
private System.Windows.Forms.Label label1
private System.Windows.Forms.Button okButton;
```

如果你继续向 Form 添加控件，将在 InitializeComponent() 方法上方看到更多的声明：

```
#region Designer code
/// <summary>
/// Windows 设计所需的。
/// 不要修改此编辑器的内容。
/// </summary>
```

在 InitializeComponent() 方法中，你可以看到以下内容：

```c
private void InitializeComponent()
{
    this.label1 = new System.Windows.Forms.Label();
    this.okButton = new System.Windows.Forms.Button();
    this.ResumeLayout();
    this.label1.AutoSize = true;
    this.label1.Font = new System.Drawing.Font("Georgia", 16.2F, System.Drawing.FontStyle.Bold);
    this.label1.Location = new System.Drawing.Point((byte)(0));
    this.label1.Name = "label1";
    this.label1.Size = new System.Drawing.Size(24, 32);
    this.label1.TabIndex = 0;
    this.label1.Text = "Click the button";
}
```

图 12-3 中的代码显示了此 Form 的所有实例。你可以看到 Font、Location、Name、Size 和 Text 已根据程序员在 IDE 中的选择分配了值。label1 的 TabIndex 默认认为 0；TabIndex 决定了用户在按下 Tab 键时控件获取焦点的顺序。此属性通常对于 Button 等可选择项更有用。

如果你返回可视化设计器并对表单及其组件进行更改（例如移动标签），当你下次查看代码时，它将已相应更新。


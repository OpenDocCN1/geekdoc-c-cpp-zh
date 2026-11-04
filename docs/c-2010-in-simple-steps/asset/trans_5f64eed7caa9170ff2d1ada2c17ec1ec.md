
**表 6.1：ToolStrip 类的值得注意的属性**

| 属性 | 描述 |
|---|---|
| Orientation | 获取 ToolStripPanel 对象的方向 |
| ShowItemToolTips | 获取或设置一个值，该值指示是否显示工具栏项目的工具提示 |
| Stretch | 获取或设置一个值，该值指示 ToolStrip 控件是否在 ToolStripContainer 类中从端到端拉伸 |
| TabStop | 获取或设置一个值，该值指示用户是否可以使用 TAB 键将焦点赋予工具栏项目 |
| TextDirection | 获取或设置 ToolStrip 控件上文本出现的方向 |

表 6.2 列出了 ToolStrip 类的值得注意的方法：

**表 6.2：ToolStrip 类的值得注意的方法**

| 方法 | 描述 |
|---|---|
| GetItemAt | 在指定位置检索工具栏项目 |
| GetNextItem | 从指定参考点检索下一个工具栏项目并按指定方向移动它 |

表 6.3 列出了 ToolStrip 类的值得注意的事件：

**表 6.3：ToolStrip 类的值得注意的事件**

| 事件 | 描述 |
|---|---|
| AutoSizeChanged | 在 AutoSize 属性更改时发生 |
| ItemAdded | 在向 ToolStripItemCollection 类添加新的工具栏项目时发生 |
| ItemClicked | 在单击工具栏项目时发生 |
| ItemRemoved | 从 ToolStripItemCollection 类中移除工具栏项目时发生 |
| LayoutCompleted | 在 ToolStrip 控件的布局完成时发生 |
| LayoutStyleChanged | 在 LayoutStyle 属性更改时发生 |

## 注

ToolStrip 类被 MenuStrip、StatusStrip 和 ContextMenuStrip 类继承。

ToolStrip 控件包含各种类型的控件，例如按钮、组合框、标签和文本框，这些被称为工具栏项目。工具栏项目是 ToolStripItem 类的实例，该类存在于 System.Windows.Forms 命名空间中。各个工具栏项目是直接或间接继承 ToolStripItem 类的类的实例。表示 ToolStrip 控件的工具栏项目的类如下：

- ToolStripButton：创建可包含文本或图像的工具栏按钮
- ToolStripLabel：创建可包含文本、图像和超链接的工具栏标签
- ToolStripTextBox：创建用户可在其中输入文本的工具栏文本框
- ToolStripComboBox：创建 ToolStrip 控件的工具栏组合框
- ToolStripSeparator：创建在逻辑上对工具栏项目进行分组的工具栏垂直线
- ToolStripDropDownButton：创建显示下拉列表的工具栏按钮
- ToolStripSplitButton：创建左侧为标准按钮、右侧为下拉按钮的组合

ToolStripItem 类及其派生类具有多个属性、方法和事件，可用于处理工具栏项目。表 6.4 列出了 ToolStripItem 类的值得注意的属性：

**表 6.4：ToolStripItem 类的值得注意的属性**

| 属性 | 描述 |
|---|---|
| Alignment | 获取或设置一个值，该值表示项目是相对于 ToolStrip 控件的起始位置还是末尾位置对齐 |
| Anchor | 获取或设置工具栏项目所绑定的容器的边缘 |
| AutoSize | 获取或设置一个值，表示项目是否自动调整大小 |
| AutoToolTip | 获取或设置一个值，表示是否对 ToolStripItem 工具提示使用 Text 属性或 ToolTipText 属性 |
| Available | 获取或设置一个值，表示是否应将工具栏项目放置在 ToolStrip 控件中 |
| CanSelect | 获取一个值，表示项目是否可以被选中 |
| DisplayStyle | 获取或设置一个值，表示是否在工具栏项目上显示文本和图像 |
| Dock | 获取或设置哪个工具栏项目边框停靠在其父控件上，并确定工具栏项目随其父控件如何调整大小 |
| Image | 获取或设置在工具栏项目上显示的图像 |
| Margin | 获取或设置两个相邻工具栏项目之间的空间 |
| Name | 获取或设置工具栏项目的名称 |
| Text | 获取或设置要在工具栏项目上显示的文本 |
| TextDirection | 获取在工具栏项目上使用的文本方向 |
| ToolTipText | 获取或设置作为控件的工具提示出现的文本 |
| Visible | 获取或设置一个值，指定是否显示工具栏项目 |

表 6.5 列出了 ToolStripItem 类的值得注意的方法：

**表 6.5：ToolStripItem 类的值得注意的方法**

| 方法 | 描述 |
|---|---|
| DoDragDrop | 启动拖放操作 |
| GetCurrentParent | 检索包含当前工具栏项目的 ToolStrip 控件 |
| PerformClick | 在其 Click 事件发生时激活工具栏项目 |
| Select | 在 ToolStrip 控件中选择一个项目 |

表 6.6 列出了 ToolStripItem 类的值得注意的事件：

**表 6.6：ToolStripItem 类的值得注意的事件**

| 事件 | 描述 |
|---|---|
| AvailableChanged | 在 Available 属性的值发生变化时发生 |
| Click | 在用户单击工具栏项目时发生 |
| DisplayStyleChanged | 在 DisplayStyle 属性的值发生变化时发生 |
| OwnerChanged | 在工具栏项目的拥有者发生变化时发生 |
| TextChanged | 在工具栏项目的 Text 属性发生变化时发生 |

现在你已经了解了 ToolStripItem 类的一些重要属性、方法和事件，让我们创建一个名为 ToolStripDemo 的 Windows 窗体应用程序，在其中可以使用这些属性、方法和事件。执行以下步骤创建 ToolStripDemo 应用程序：

1. 单击 Start→All Programs→Microsoft Visual Studio 2010→Microsoft Visual Studio 2010 以打开 Visual Studio 2010 集成开发环境（IDE）。
2. 从菜单栏中选择 File→New→Project 以打开新建项目对话框。
3. 在新建项目对话框的 Installed Templates 窗格中选择 Visual C#→Windows。
4. 从 Installed Templates 窗格的右侧选择 Windows Forms Application。
5. 在 Name 文本框中输入 ToolStripDemo 作为应用程序的名称。
6. 在 Location 组合框中输入要保存应用程序的文件夹路径。在我们的例子中，我们选择了默认位置，即 C:\Users\temp\Documents\Visual Studio 2010\Projects。
7. 在新建项目对话框中单击 OK 按钮。ToolStripDemo 应用程序已创建。
8. 选择设计器中出现的 Form1 表单并按 F4 键以在属性窗口中查看其属性。将 Form1 表单的 Text 和 Size 属性分别设置为 ToolStripDemo 和 479, 300。
9. 从 Toolbox 拖动一个 Label 控件并将其放置到设计器中的 Form1 表单上，并将其 Text 和 Location 属性分别设置为 This is a demonstration of the ToolStrip control 和 97, 127。
10. 从 Toolbox 的 Menus & Toolbars 选项卡拖动一个 ToolStrip 控件并将其放置到设计器中的 Form1 表单上。Form1 表单现在显示如下所示，如图 C6-6.1 所示：

    ![](img/2db4b8b2cb67e7ccc52477a61fe289ab_188_0.png)

    图 C6-6.1

请注意，ToolStrip 控件 toolStrip1 出现在 Form1 表单的顶部以及组件托盘中，该托盘显示为 Form1 表单设计器底部的一个矩形条。这是因为 toolStrip1 控件的 Dock 属性默认设置为 Top。你可以将 Dock 属性更改为 Left、Right、Fill、Bottom 或 None。现在，你需要向 toolStrip1 控件添加工具栏项目。你可以在设计时或运行时添加工具栏项目。让我们执行以下步骤在设计时向 toolStrip1 控件添加工具栏项目：

11. 在设计器中选择 toolStrip1 控件并按 F4 键以打开属性窗口。



# 684 第 15 章 使用 Windows Forms 构建图形用户界面：部分 2

![](img/57baed2319be0bb1b5f98674846f2711_684_0.png)

图 15.37 | MDI 父窗口和 MDI 子窗口。

要创建一个 MDI Form，请将 Form 的 `IsMdiContainer` 属性设置为 `true`。该 Form 的外观发生变化，如图 15.38 所示。接下来，创建一个子 Form 类并添加到 Form 中。执行此操作，在解决方案管理器中右键点击，选择“项目” > “添加 Windows 窗单...”并为文件命名。根据需要编辑 Form。要将子 Form 添加到父窗，我们必须创建一个新的子对象，将其 `MdiParent` 属性设置为父 Form，并调用子 Form 的 `Show` 方法。通常，向父窗添加子 Form 如下：

```
ChildFormClass child = new ChildFormClass();
child.MdiParent = parentForm;
child.Show();
```

单文档界面 (SDI) | 多文档界面 (MDI)

![](img/57baed2319be0bb1b5f98674846f2711_684_1.png)

图 15.38 | SDI 和 MDI 窗体。

在大多数情况下，由父 Form 创建子窗口，因此 `parentForm` 引用如此。创建子窗口的代码通常位于事件处理程序内部，它响应用户操作创建一个新窗口。菜单选择（例如点击“文件”，然后选择“新建”子菜单）是创建新子窗口的常用技术。

类属性 `MdiChildren` 返回子 Form 引用的数组。如果父窗口想要检查所有子窗口的状态（例如，确保在父窗口关闭之前所有窗口都已保存），这将非常有用。属性 `ActiveMdiChild` 返回活动子窗口的引用；如果没有活动子窗口，则返回 `null`。
MDI 窗口的其他特征见图 15.39。

# 15.12 多文档界面 (MDI) 窗体 685

| MDI Form 属性、方法和事件 | 描述 |
| :--- | :--- |
| **常用 MDI 子窗口属性** | |
| IsMdiChild | 表示 Form 是否为 MDI 子窗口。如果为 `true`，则是 MDI 子窗口（只读属性）。 |
| MdiParent | 指定子窗口的 MDI 父 Form。 |
| **常用 MDI 父窗口属性** | |
| ActiveMdiChild | 返回 Form 当前活动的 MDI 子窗口（如果没有活动子窗口则返回 `null`）。 |
| IsMdiContainer | 表示 Form 是否可以作为 MDI 父窗口。如果为 `true`，则 Form 可以是 MDI 父窗口。默认值为 `false`。 |
| MdiChildren | 返回 MDI 子 Form 数组。 |
| **常用方法** | |
| LayoutMdi | 决定 MDI 父窗口上子窗口的显示。该方法接受 `MdiLayout` 枚举作为参数，可能的值有 `ArrangeIcons`、`Cascade`、`TileHorizontal` 和 `TileVertical`。图 描述了这些值的效果。 |
| **常用事件** | |
| MdiChildActivate | 当 MDI 子窗口关闭或激活时生成。 |

**图 15.39** | MDI Form 属性、方法和事件。

子窗口可以独立于父窗口进行最小化、最大化和关闭。图 40 显示了两个图像：一个包含两个最小化的子窗口，另一个包含一个最大化的子窗口。当父窗口最小化或关闭时，子窗口也会最小化或关闭。

![](img/57baed2319be0bb1b5f98674846f2711_685_0.png)

**图 15.40** | 最小化和最大化的子窗口。注意图 40(b) 中的标题栏。当窗口最大化时，其标题栏插入父窗口的标题栏中。当子窗口最小化时，其标题栏会显示恢复图标，用于将子窗口恢复到最小化或最大化之前的尺寸。

C# 提供了一个属性来跟踪 MDI 容器中打开的子窗口。`MenuStrip` 类的 `MdiWindow` 属性（如果有）显示打开窗口列表，用户可以通过它将相应的窗口带到前台。当打开一个新的子窗口时，列表末尾会添加条目（图 41）。如果打开了十个或更多子窗口，列表将包含“更多选项...”，允许用户从对话框中选择窗口。

# 良好的编程实践 15.1

在 MDI 应用中，包含一个显示打开窗口列表的菜单。这有助于用户快速选择子窗口。

![](img/57baed2319be0bb1b5f98674846f2711_686_0.png)

MDI 容器允许您组织子窗口的布局。MDI 应用中的子窗口可以通过调用父 Form 的 `LayoutMdi` 方法进行排列。`LayoutMdi` 方法接受一个枚举，允许使用 `ArrangeIcons`、`Cascade`、`TileHorizontal` 和 `TileVertical`。平铺窗口完全填充父窗口且不重叠；此类窗口可以水平（`TileHorizontal`）或垂直（`TileVertical`）排列。层叠窗口（`Cascade` 值）会重叠——每个的大小相同，并尽可能显示标题栏。`ArrangeIcons` 值排列最小化窗口的图标。如果最小化窗口散落在父窗口周围，`ArrangeIcons` 值将它们整齐地排列在父窗口的左下角。图 42 说明了 Mdi 布局的用法。

图 15.41 | MenuStrip 属性 `MdiWindow.MdiListItem` 示例。

`UsingMDIForm` 类（图 43）演示了 MDI 窗口。`UsingMDIForm` 使用三个 `ChildForm` 实例（图 44），每个实例包含一个显示图像的 `PictureBox`。父 MDI Form 包含一个允许用户创建和排列子 Form 的菜单。

# 15.12 多文档界面 (MDI) 窗体 687

| **MDI 父 Form** | 图 15.43 展示了 `UsingMDIForm.cs` |
| :--- | :--- |
| a) ArrangeIcons | ![](img/57baed2319be0bb1b5f98674846f2711_687_0.png) |
| b) Cascade | ![](img/57baed2319be0bb1b5f98674846f2711_687_1.png) |
| c) TileHorizontal | ![](img/57baed2319be0bb1b5f98674846f2711_687_2.png) |
| d) TileVertical | ![](img/57baed2319be0bb1b5f98674846f2711_687_3.png) |

| **MDI 父 Form** | 图 15.42 | `MDILayout` 枚举值。 |
| **文件菜单** | 这些菜单中的第一个“文件”（`StripMenuItem`）包含“退出”项（`exitStripMenuItem`）和“新建”子菜单（`newStripMenuItem`），由每个类型子窗口的项组成。 |
| **窗口菜单** | 第二个菜单“窗口”（`windowStripMenuItem`）提供了布局 MDI 子窗口的选项，以及活动 MDI 子窗口列表。 |



![](img/3f5ef6be1748bb746e5f71a483bba4d0_520_0.png)

## 图 15.37 | MDI 父窗口和 MDI 子窗口。

创建 MDI Form 时，将 Form 的 IsMdiContainer 属性设置为 true。Form 的外观会发生变化，如图 15.38 所示。接下来，创建一个要添加到 Form 的子 Form 类。为此，在解决方案资源管理器中右键单击项目，选择 项目 > 添加 Windows 窗体... 并命名文件。按需编辑 Form。要将子 Form 添加到父窗口，必须创建一个新的子 Form 对象，将其 MdiParent 属性设置为父 Form 并调用子 Form 的 Show 方法。一般来说，要将子 Form 添加到父窗口，写入

```
ChildFormClass childForm = New ChildFormClass();
childForm.MdiParent = parentForm;
childForm.Show();
```

![](img/3f5ef6be1748bb746e5f71a483bba4d0_520_1.png)

## 图 15.38 | SDI 和 MDI 形式。

在大多数情况下，父 Form 创建子窗口，因此 parentForm 引用为 this。创建子窗口的代码通常位于事件处理程序中，该处理程序响应用户操作创建新窗口。菜单选择（例如 File，然后是子菜单选项 New，然后是子菜单选项 Window）是创建新子窗口的常见技术。

Class Form 属性 MdiChildren 返回子 Form 引用的数组。如果父窗口想要检查所有子窗口的状态（例如，在父窗口关闭前确保全部已保存），这很有用。属性 ActiveMdiChild 返回活动子窗口的引用；如果没有活动的子窗口则返回 null。MDI 窗口的其他特性在图 15.39 中描述。

| MDI 父级和 MDI 子级属性、方法及事件 | 描述 |
|---|---|
| **常用的 MDI 子级属性** | |
| IsMdiChild | 表示 Form 是否为 MDI 子窗口。如果为 true，则 Form 是 MDI 子窗口（只读属性）。 |
| MdiParent | 指定子窗口的 MDI 父 Form。 |
| **常用的 MDI 父级属性** | |
| ActiveMdiChild | 返回当前活动的 MDI 子 Form（如果没有活动的子窗口则返回 null）。 |
| IsMdiContainer | 表示 Form 是否可以作为 MDI 父窗口。如果为 true，则 Form 可以作为 MDI 父窗口。默认值是 false。 |
| MdiChildren | 以 Form 数组的形式返回 MDI 子窗口。 |
| **常用方法** | |
| LayoutMdi | 确定 MDI 父窗口上子窗体的显示方式。该方法以 MdiLayout 枚举作为参数，可能的值有 ArrangeIcons、Cascade、TileHorizontal 和 TileVertical。图 15.42 描述了这些值的作用。 |
| **常用事件** | |
| MdiChildActivate | 当 MDI 子窗口被关闭或激活时触发。 |

图 15.39 | MDI 父级和 MDI 子级属性、方法及事件。

子窗口可以独立于父窗口最小化、最大化和关闭。图 15.40 显示了两幅图像：一幅包含两个最小化的子窗口，另一幅包含一个最大化的子窗口。当父窗口被最小化或关闭时，子窗口也会被最小化或关闭。

父窗口图标：最小化、最大化和关闭

最大化子窗口图标：最小化、还原和关闭

![](img/3f5ef6be1748bb746e5f71a483bba4d0_521_0.png)

最小化子窗口图标：还原、最大化和关闭

父标题栏指示最大化的子窗口

## 图 15.40 | 最小化和最大化的子窗口。

请注意图 15.40(b) 中的标题栏为 **Form1 - [Child1]**。当子窗口被最大化时，其标题栏文本会插入到父窗口的标题栏中。当子窗口被最小化或最大化时，其标题栏会显示一个还原图标，可用于将子窗口恢复到之前的大小（即最小化或最大化之前的大小）。

C# 提供了一个属性来帮助跟踪 MDI 容器中打开的子窗口。类 **MenuStrip** 的属性 **MdiWindowListItem** 指定哪个菜单，如果有的话，显示打开的子窗口列表，用户可以从中选择以将相应窗口带到前台。当打开一个新的子窗口时，会在列表末尾添加一个条目（图 15.41）。如果打开十个或更多子窗口，列表将包含选项 **More Windows...**，允许用户从对话框中的列表中选择窗口。

## 良好编程实践 15.1

*在 MDI 应用中，包含一个显示打开的子窗口列表的菜单。这有助于用户快速选择子窗口。*

MDI 容器允许您组织其子窗口的放置。MDI 应用中的子窗口可以通过调用父 Form 的方法 **LayoutMdi** 来排列。方法 LayoutMdi 接受一个 **MdiLayout** 枚举，其值可以为 **ArrangeIcons**、**Cascade**、**TileHorizontal** 和 **TileVertical**。平铺的窗口完全填满父窗口且不重叠；此类窗口可以水平排列（值 **TileHorizontal**）或垂直排列（值 **TileVertical**）。级联窗口（值 **Cascade**）会重叠——每个窗口大小相同并且尽可能显示可见的标题栏。值 ArrangeIcons 对任何最小化的子窗口的图标进行排列。如果最小化的窗口散布在父窗口周围，值 ArrangeIcons 会将它们整齐地排列在父窗口的左下角。图 15.42 说明了 MdiLayout 枚举的值。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_522_0.png)

**图 15.41** | MenuStrip 属性 MdiWindowListItem 示例。

类 UsingMDIForm（图 15.43）演示了 MDI 窗口。类 UsingMDIForm 使用三个子 Form ChildForm（图 15.44）的实例，每个实例包含一个显示图像的 PictureBox。父 MDI Form 包含一个菜单，使用户能够创建和排列子 Form。

### a) ArrangeIcons

![](img/3f5ef6be1748bb746e5f71a483bba4d0_523_0.png)

### b) Cascade

![](img/3f5ef6be1748bb746e5f71a483bba4d0_523_1.png)

### c) TileHorizontal

![](img/3f5ef6be1748bb746e5f71a483bba4d0_523_2.png)

### d) TileVertical

![](img/3f5ef6be1748bb746e5f71a483bba4d0_523_3.png)

## 图 15.42 | MDI 布局枚举值。

## MDI 父 Form

图 15.43 展示了类 UsingMDIForm——应用的 MDI 父 Form。该 Form 最先创建，包含两个顶级菜单。其中第一个菜单 File（fileToolStripMenuItem）同时包含一个 Exit 项（exitToolStripMenuItem）和一个 New 子菜单（newToolStripMenuItem），该子菜单由每种类型子窗口的项组成。第二个菜单 Window（windowToolStripMenuItem）提供排列 MDI 子窗口的选项，以及活动 MDI 子窗口的列表。

```csharp
// Fig. 15.43: UsingMDIForm.cs
// Demonstrating use of MDI parent and child windows.
using System;
using System.Windows.Forms;

namespace UsingMDI
{
    // Form demonstrates the use of MDI parent and child windows
    public partial class UsingMDIForm : Form
    {
        // constructor
        public UsingMDIForm()
        {
            InitializeComponent();
        }
    }
}
```

## 图 15.43 | 演示 MDI 父窗口和子窗口的使用。 （第 1 部分，共 3 部分。）

```csharp
17  // create Lavender Flowers image window
18  private void lavenderToolStripMenuItem_Click(
19      object sender, EventArgs e)
20  {
21      // create new child
22      var child = new ChildForm(
23          "Lavender Flowers", "lavenderFlowers");
24      child.MdiParent = this; // set parent
25      child.Show(); // display child
26  }
27
28  // create Purple Flowers image window
29  private void purpleToolStripMenuItem_Click(
30      object sender, EventArgs e)
31  {
32      // create new child
33      var child = new ChildForm(
34          "Purple Flowers", "purpleFlowers");
35      child.MdiParent = this; // set parent
36      child.Show(); // display child
37  }
38
39  // create Yellow Flowers image window
40  private void yellowToolStripMenuItem_Click(
41      object sender, EventArgs e)
42  {
43      // create new child
44      var child = new ChildForm(
45          "Yellow Flowers", "yellowFlowers");
46      child.MdiParent = this; // set parent
47      child.Show(); // display child
48  }
49
50  // exit app
51  private void exitToolStripMenuItem_Click(
52      object sender, EventArgs e)
53  {
54      Application.Exit();
55  }
56
57  // set Cascade layout
58  private void cascadeToolStripMenuItem_Click(
59      object sender, EventArgs e)
60  {
61      this.LayoutMdi(MdiLayout.Cascade);
62  }
63
64  // set TileHorizontal layout
65  private void tileHorizontalToolStripMenuItem_Click(
66      object sender, EventArgs e)
67  {
68      this.LayoutMdi(MdiLayout.TileHorizontal);
69  }
```

## 图 15.43 | 演示 MDI 父窗口和子窗口的使用。 （第 2 部分，共 3 部分。）




(like Products) 直接在选项卡中，或通过选项卡的 Caption 属性添加。 当您完成选项卡的标签后，Access 会在当前选项卡的右侧添加一个新的空白选项卡。

> **提示**
> 
> 您可以将现有窗体拖到导航窗体的选项卡区域，以将其添加为子窗体。

## FIGURE 17.7

导航窗体具有用于嵌入子窗体的较大区域。

![](img/1e45673ab6eca9d20e67635ff5b9b318_540_0.png)

水平选项卡

子窗体区域

在图 17.7 中，选择导航窗体模板时选择了水平选项卡选项，并将一个选项卡命名为 Products，这会生成一个新的 Add New 选项卡。水平选项卡的替代方案（垂直选项卡，左；垂直选项卡，右；等等）显示在图 17.6 中。

Product 选项卡的属性表（显示在图 17.8 中）包括数据选项卡上的 Navigation Target Name 属性，用于指定用作选项卡子窗体的 Access 窗体。 从 Navigation Target Name 属性的下拉列表中选择一个窗体，Access 会为您创建与子窗体的关联。

## FIGURE 17.8

使用 Navigation Target Name 属性指定选项卡的子窗体。

![](img/1e45673ab6eca9d20e67635ff5b9b318_541_0.png)

完成的导航窗体显示在图 17.9 中。自动生成的导航窗体极大地使用了屏幕空间。可以做很多事情来增强此窗体，例如删除导航窗体的页眉部分并减少子窗体周围的空白空间。图 17.9 中显示的 frmProducts 包含在 Chapter17.accdb 示例数据库中。

> 提示
> 如果您已经知道要添加到导航窗体的窗体的名称，可以在新选项卡中输入它。 例如，如果您在新选项卡中输入 frmProducts 而不是仅输入 Products，则 frmProducts 会自动添加为子窗体。然后您可以编辑选项卡名称以删除 frm 前缀（如果您愿意）。

## 多项窗体

单击“创建”功能区的“窗体”组中的“更多窗体”按钮，然后单击“多项”按钮，以基于“导航窗格”中选择的表或查询创建基于表格的窗体。表格窗体与数据表类似，但比普通数据表更具吸引力。

拆分窗体方向属性（在窗体的属性表中“格式”选项卡上）决定数据表位于窗体区域的顶部、底部、左侧或右侧。默认情况如图 17.11 所示，数据表区域位于底部。frmCustomers_SplitForm 包含在 Chapter17.accdb 示例数据库中。

## FIGURE 17.11

创建拆分窗体时，您想要从列表中选择记录并在窗体中编辑它们。使用分隔条调整窗体上下部分的尺寸。

![](img/1e45673ab6eca9d20e67635ff5b9b318_544_0.png)

## 数据表窗体

单击“创建”功能区的“窗体”组中的“更多窗体”按钮，然后单击“数据表”按钮，以创建看起来像表或查询数据表的窗体。数据表窗体在您想要以行列格式查看数据但想要限制显示和可编辑的字段时很有用。

要基于 tblProducts 创建数据表窗体，请按照以下步骤操作：

- 1. 在导航窗格中选择 tblProducts。
- 2. 选择功能区的“创建”选项卡。
- 3. 单击“窗体”组中的“更多窗体”按钮，然后单击“数据表”。您可以通过从功能区上的“视图”下拉菜单中选择“数据表视图”来查看您创建的任何窗体作为数据表。打开时，数据表窗体默认以数据表视图显示。

> 提示
> 某些窗体的“允许数据表视图”属性默认设置为“否”。对于这些窗体，“视图”下拉菜单中不会显示“数据表视图”选项。您将在本章后面的“介绍属性”部分了解有关窗体属性的更多信息。

## 调整窗体区域大小

在设计视图中，带有网格线的区域是您向窗体添加控件的位置。这是窗体显示时的大小。通过将光标放在区域的任何边框上并拖动区域的边框来使区域变大或变小，即可调整窗体的网格区域大小。图 17.12 显示了正在调整大小的空白窗体的设计视图。

## 保存您的窗体

您可以通过单击“快速访问工具栏”中的“保存”按钮随时保存窗体。 当要求您为窗体命名时，请为其指定有意义的名称（例如，frmProducts、frmCustomers 或 frmProductList）。一旦您为窗体命名，下次单击“保存”时就不会再次提示您。

关闭窗体后进行更改时，Access 会询问您是否保存它。如果您不保存窗体，自您打开窗体以来（或自上次单击“保存”以来）的所有更改都将丢失。如果您对结果满意，建议在工作时经常保存窗体。

> 提示
> 如果您要对窗体进行大量更改，可能需要复制窗体。 例如，如果您想处理窗体 frmProducts，可以在导航窗格中复制然后粘贴窗体，并将其命名为例如 frmProductsOriginal。稍后，当您完成更改并对其进行测试后，可以删除原始副本。

## FIGURE 17.12

空白窗体的设计视图。通过拖动右下角调整窗体区域大小。

![](img/1e45673ab6eca9d20e67635ff5b9b318_546_0.png)

窗体设计表面

调整大小光标

## 使用控件

控件和属性构成了窗体和报表的基石。在开始将它们应用于自定义窗体和报表之前，了解控件和属性的基本概念至关重要。

## 第五部分：使用 Access 窗体和报表

> 注意
> 尽管本章是关于窗体的，但您会了解到窗体和报表共享许多共同特征，包括控件以及您可以对它们执行的操作。随着您在本章学习控件，您将能够在创建报表时应用几乎所有学到的内容。

控件是窗体或报表上的任何对象，例如标签或文本框。这些是任何 Windows 应用程序中使用的相同类型的控件，例如 Access、Excel、基于 Web 的 HTML 表单，或在任何语言中使用的控件，例如 VB.NET、C++ 或 C#。尽管每种语言或产品具有不同的文件格式和不同的属性，但 Access 中的文本框与任何其他 Windows 产品中的文本框相似。

您使用控件输入数据并使用控件显示数据。控件可以绑定到表中的字段（当在控件中输入值时，它也会保存在某些底层表字段中），也可以不绑定并在窗体中显示但在关闭窗体时不保存。控件也可以是未保存数据的对象，例如线条或矩形。

一些未内置于 Access 的控件是单独开发的——这些是 ActiveX 控件。ActiveX 控件扩展了 Access 的基本功能集，可从各种供应商处获得。

无论您使用的是窗体还是报表，创建和使用控件基本上遵循相同的过程。在本章中，我们从窗体的角度解释控件。

## 对控件进行分类

窗体和报表包含许多不同类型的控件。您可以使用设计选项卡上的控件组向窗体添加这些控件，如图 17.13 所示。将鼠标悬停在控件上会显示一个屏幕提示，告诉您该控件是什么。

FIGURE 17.13
设计选项卡让您在窗体的设计视图中添加和自定义控件。

![](img/1e45673ab6eca9d20e67635ff5b9b318_547_0.png)

表 17.1 简要描述了基本的 Access 控件。

## TABLE 17.1 Controls in Access Forms

| Control | What It Does |
|---|---|
| Text box | Displays and allows users to enter or edit data. |
| Label | Displays static text that the user can't change. |
| Button | Also called a **command button**. Runs macros or VBA code when clicked. |
| Tab control | Displays a tabbed interface where each tab contains different controls. |
| Link | Creates a link to a web page, a picture, an e-mail address, or a program. |
| Web browser control | Adds a web browser to your form to display web pages. |
| Navigation control | Provides a tabbed interface that displays subforms. Selecting from the Navigation control on the Create Ribbon creates a form with this control. |
| Option group | Holds multiple option buttons, check boxes, or toggle buttons. |
| Insert page break | Usually used for reports and indicates a physical page break. |
| Combo box | A combination of a box and a list box. It includes a text box area at the top for entering text and a drop-down list box for selecting from a list. |
| Chart | Displays data in a graphical format. |
| Line | A graphical line of variable thickness and color, which is used for separation. |
| Toggle button | This is a two-state button—up or down—which usually uses pictures or icons instead of text to display different states. |
| Rectangle | A rectangle can be any color or size or can be filled in or blank; the rectangle is used to group related controls visually. |
| List box | A list of values that is always displayed on the form or report. |
| Check box | A two-state control, shown as a square that contains a check mark if it's on and an empty square if it's off. Before a check box's value is set, it appears as a grayed-out square. |
| Unbound object frame | Holds an OLE object or embedded picture that isn't tied to a table field and can include graphs, pictures, sound files, and video. |
| Attachment | Manages attachments for the Attachment data type. Attachment fields (see Chapter 3) provide a way to attach external files (such as music or video clips or Word documents) to Access tables. |
| Option button | Also called a radio button, this button is displayed as a circle with a dot when the option is on. |
| Subform/subreport | Displays another form or report within the main form or report. |
| Bound object frame | Holds an OLE object or embedded picture that is tied to a table field. |
| Image | Displays a bitmap picture with very little overhead. |


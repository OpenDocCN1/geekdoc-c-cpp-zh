

使用 Format 事件可在报表在打印之前对某一节内的控件应用特殊格式。Format 在例如根据报表数据中的某些条件隐藏不想打印的控件时很有用。事件过程在 Access 将该节加载到内存中布局时运行，但在报表发送到打印机之前运行。

您可以为报表的任何节设置 On Format 和 On Print 事件属性。但是，On Retreat 不适用于页眉或页脚节。图 26.4 显示了报表属性表的事件选项卡。注意，属性表顶部的下拉列表显示报表已被选中，因此事件选项卡中的事件与报表本身相关，而非报表上的单个控件。

## FIGURE 26.4
为报表的 On No Data 事件指定事件过程。

![](img/1e45673ab6eca9d20e67635ff5b9b318_898_0.png)

除了 NoData 事件之外，Format 事件也经常被使用。图 26.5 显示了如何向报表节的 Format 事件添加代码以控制报表上控件的可见性。

图 26.5 中说明的 Detail0_Format 事件过程首先检查 txtQtyInStock 控件的值。如果 txtQtyInStock 的值小于 10，则显示 lblLowStock；否则，警告控件将被隐藏。

## Tip
Access 通过在节类型后附加数字来命名报表的各节，例如 Detail0。您可以通过更改该节的 Name 属性来重命名这些节。

## FIGURE 26.5
运行事件过程以显示或隐藏报表上的控件。

![](img/1e45673ab6eca9d20e67635ff5b9b318_899_0.png)

在本书中，您将看到许多使用事件和事件过程来操作窗体、报表和控件的示例。

## Paying Attention to Event Sequence
有时即使用户执行一个相当简单的操作，也会在短时间内引发多个事件。例如，每当用户在键盘上按下某个键时，就会按顺序引发 KeyDown、KeyPress 和 KeyUp 事件。同样，点击鼠标左键会触发 MouseDown 和 MouseUp 事件，以及 Click 事件。作为 VBA 开发人员，您有权决定在 Access 应用程序中编程哪些事件。

事件并非随机发生。事件实际上会以可预测的方式触发，具体取决于引发事件的控件。有时处理事件最棘手的部分是跟踪事件发生的顺序。例如，可能并不直观的是 Enter 事件发生在 GotFocus 事件之前（参见表 26.5），或者 KeyDown 事件发生在 KeyPress 事件之前（参见表 26.3）。

## Looking at common event sequences
以下是最常见窗体场景的事件序列：

- **Opening and closing forms:**
  - **When a form opens:** Open (form) → Load (form) → Resize (form) → Activate (form) → Current (form) → Enter (control) → GotFocus (control)
  - **When a form closes:** Exit (control) → LostFocus (control) → Unload (form) → Deactivate (form) → Close (form)
- **Changes in focus:**
  - **When the focus moves from one form to another:** Deactivate (form1) → Activate (form2)
  - **When the focus moves to a control on a form:** Enter → GotFocus
  - **When the focus leaves a form control:** Exit → LostFocus
  - **When the focus moves from control1 to control2:** Exit (control1) → LostFocus (control1) → Enter (control2) → GotFocus (control2)
  - **When the focus leaves the record in which data has changed, but before entering the next record:** BeforeUpdate (form) → AfterUpdate (form) → Exit (control) → LostFocus (control) → Current (form)
  - **When the focus moves to an existing record in Form view:** BeforeUpdate (form) → AfterUpdate (form) → Current (form)
- **Changes to data:**
  - **When data is entered or changed in a form control and the focus is moved to another control:** BeforeUpdate → AfterUpdate → Exit → LostFocus
  - **When the user presses and releases a key while a form control has the focus:** KeyDown → KeyPress → KeyUp
  - **When text changes in a text box or in the text box portion of a combo box:** KeyDown → KeyPress → Change → KeyUp
  - **When a value that is not present in the drop-down list is entered into a combo box’s text area:** KeyDown → KeyPress → Change → KeyUp → NotInList → Error
  - **When data in a control is changed and the user presses Tab to move to the next control:**
    - Control1: KeyDown → BeforeUpdate → AfterUpdate → Exit → LostFocus
    - Control2: Enter → GotFocus → KeyPress → KeyUp
  - **When a form opens and data in a control changes:** Current (form) → Enter (control) → GotFocus (control) → BeforeUpdate (control) → AfterUpdate (control)
  - **When a record is deleted:** Delete → BeforeDelConfirm → AfterDelConfirm

- When the focus moves to a new blank record on a form and a new record is created when the user types in a control: Current (form) → Enter (control) → GotFocus (control) → BeforeInsert (form) → AfterInsert (form)

- Mouse events:

- When the user presses and releases (clicks) a mouse button while the mouse pointer is on a form control: MouseDown → MouseUp → Click

- When the user moves the focus from one control to another by clicking the second control:
  - Control1: Exit → LostFocus
  - Control2: Enter → GotFocus → MouseDown → MouseUp → Click

- When the user double-clicks a control other than a command button: MouseDown → MouseUp → Click → DblClick → MouseUp

## Writing simple form and control event procedures
编写简单的过程来验证窗体或控件的事件序列非常容易。利用前面的信息来确定在您的应用程序中应利用哪个事件。意外的行为通常可以追溯到附加到发生得太晚或太早而无法捕获应用程序所需信息的事件的过程。

Chapter26.accdb 示例数据库包含一个名为 frmEventLogger 的窗体，它会将命令按钮、文本框和切换按钮的每个事件打印到 Debug 窗口中。该窗体未绑定到记录集，因此事件列表与绑定窗体略有不同。它用于演示仅通过轻微操作就会触发多少个 Access 事件。例如，点击命令按钮一次，然后按 Tab 键到文本框并按下键盘上的一个键会触发以下事件：

- cmdButton_MouseDown
- cmdButton_MouseUp
- cmdButton_Click
- cmdButton_KeyDown
- cmdButton_Exit
- cmdButton_LostFocus
- txtText1_Enter
- txtText1_GotFocus
- txtText1_KeyPress
- txtText1_KeyPress
- txtText1_KeyUp
- txtText1_KeyDown
- txtText1_KeyPress
- txtText1_Change
- txtText1_KeyUp

您必须打开代码编辑器并显示 Immediate 窗口才能看到这些事件的显示。从 Access 环境中的任何位置按 Ctrl+G，代码编辑器会立即打开并显示 Immediate 窗口。然后，使用 Alt+Tab 返回到主 Access 屏幕，打开窗体，点击各种控件并在文本框中输入内容。您将看到使用 Ctrl+G 返回到 Immediate 窗口时会出现大量事件消息。

显然，这些事件远比您想要编程的要多。注意，在命令按钮上，MouseDown 和 MouseUp 事件在 Click 事件之前触发。此外，按下 Tab 键时会出现 KeyDown 事件，然后命令按钮的 Exit 事件在其 LostFocus 事件之前触发。（当然，随着 Tab 键的按下，焦点会从命令按钮移开到文本框。）

此外，注意文本框会引发不止一个 KeyPress 事件。第一个是来自 Tab 键的 KeyPress，第二个是按下键盘字符时发生的 KeyPress。尽管看起来很奇怪，Tab 键的 KeyPress 事件会被文本框捕获而不是命令按钮，但当考虑到表面下发生的事情时，这是有意义的。Tab 键是移动焦点到选项卡序列中下一个控件的指令。Access 实际上在将 KeyPress 事件传递给窗体上的控件之前移动焦点。这意味着焦点移动到文本框，并且文本框接收由 Tab 键引发的 KeyPress。

请记住，您只为对应用程序有意义的事件编写代码。任何不包含代码的事件都会被 Access 忽略，对应用程序没有影响。

此外，很可能您偶尔会为特定任务编程错误的事件。例如，您可能想通过向控件的 Enter 事件添加代码来更改控件的外观。（许多开发人员更改控件的 BackColor 或 ForeColor，以便用户可以轻松看到哪个控件具有焦点。）您很快就会发现 Enter 事件是不可靠的焦点获得指示器。GotFocus 和 LostFocus 事件专门用于控制用户界面，而 Enter 和 Exit 事件在性质上更“概念化”，在 Access 应用程序中并不经常被编程。

这个小例子或许可以解释为什么 Access 支持如此多的不同事件。Microsoft 经过精心设计，使 Access 能够处理不同类别的事件，例如数据或用户界面任务。这些事件为您提供了一个丰富的编程环境。您几乎总能找到完全正确的控件、事件或编程技巧，让 Access 按您需要的方式工作。

## Opening a form with an event procedure
大多数应用程序需要多个窗体和报表来完成应用程序的业务功能。不是要求应用程序用户浏览数据库容器以确定哪些窗体和报表完成哪些任务，应用程序通常会提供一个开关板窗体来帮助用户在整个


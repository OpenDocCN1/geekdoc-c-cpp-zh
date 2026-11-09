
### 打开周薪应用程序，然后测试应用程序：

- 1. 启动 Visual Studio 2008（或 Visual Basic 2008 Express Edition）。打开 **周薪解决方案（Weekly Pay Solution.sln）** 文件，该文件位于 ClearlyVB\Chap17\Weekly Pay Solution 文件夹中。如有必要，请打开设计器窗口。

- 2. 启动应用程序。在“小时”框中输入 **41**，然后在“工资率”框中输入 **9**。单击**计算**按钮。计算按钮的 Click 事件过程会计算并显示正常工资、加班工资和总工资。参见图 17-4。

![](img/cf88270932e011575089da06b940a1d9_390_0.png)

图 17-4：显示计算金额的界面

- 3. 现在将小时数从 41 改为 **4**，但暂时不要单击**计算**按钮。注意，界面仍然显示 41 小时的工资金额；这是因为在您单击**计算**按钮之前，这些金额不会更新。单击**计算**按钮以更新工资金额，然后点击**退出**按钮。

为了避免混淆，最好在 txtHours 控件中的小时数或 txtRate 控件中的工资率发生变化时，从界面中移除工资金额。您可以通过在每个文本框的 **TextChanged 事件**过程中输入以下三个赋值语句来实现：lblRegular.Text = String.Empty、lblOvertime.Text = String.Empty 和 lblGross.Text = String.Empty。文本框的 **TextChanged 事件**在文本框内容发生更改时发生。您还可以通过将赋值语句输入到子过程中，然后在两个 **TextChanged** 事件过程中输入相应的 **Call** 语句来移除工资金额。您将使用后一种方法，因为在子过程中输入赋值语句可避免多次输入它们。此外，如果应用程序被修改——例如，如果用户希望您将字符串“N/A”而不是空字符串分配给标签——您只需要在代码中的一个位置进行更改。

### 输入 ClearLabels 子过程和 Call 语句，然后测试应用程序：

- 1. 打开代码编辑器窗口。单击 Public Class frmMain 行下方的 **空白行**，然后按 **Enter**。输入图 17-5 中所示的 ClearLabels 过程。

![](img/cf88270932e011575089da06b940a1d9_391_0.png)

- 2. 打开 txtHours 控件的 TextChanged 事件过程的代码模板。输入 **Call ClearLabels()** 并按 **Enter**。现在打开 txtRate 控件的 TextChanged 事件过程的代码模板。输入 **Call ClearLabels()** 并按 **Enter**。

- 3. 保存解决方案，然后启动应用程序。在“小时”框中输入 **41**，然后在“工资率”框中输入 **9**。单击**计算**按钮。图 17-4 中先前显示的正常工资、加班工资和总工资金额将出现在界面中。

- 4. 现在将小时数从 41 改为 4。更改小时数会导致 txtHours 控件的 TextChanged 事件发生。因此，计算机将处理事件过程中输入的 Call ClearLabels() 语句。在处理该语句时，计算机会暂时离开事件过程，以处理 ClearLabels 过程中的代码。ClearLabels 过程中的赋值语句会移除界面中三个标签控件的内容。处理完赋值语句后，计算机将处理 ClearLabels 过程的 End Sub 子句，该子句结束该过程。然后计算机返回到 txtHours 控件的 TextChanged 事件过程，并处理 Call 语句下方的那行代码。在这种情况下，Call 语句下方的那行是 End Sub，它结束事件过程。

- 5. 单击**计算**按钮，然后将工资率从 9 改为 **9.55**。注意，当您对工资率进行更改时，工资金额会从界面中移除。单击**计算**按钮，然后点击**退出**按钮。

要完成周薪应用程序，您需要为“清除”按钮的 Click 事件过程编写代码。该过程应移除两个文本框的内容。还应从三个标签控件中移除工资金额。

### 编写清除按钮的 Click 事件过程的代码，然后测试该过程：

- 1. 打开 btnClear 控件的 Click 事件过程的代码模板。输入 **'清除文本框和标签控件** 并按 **Enter** 两次。
- 2. 输入 **txtHours.Text = String.Empty** 并按 **Enter**，然后输入 **txtRate.Text = String.Empty** 并按 **Enter**。您可以使用 ClearLabels 过程从标签控件中移除工资金额。输入 **Call ClearLabels()** 并按 **Enter**。
- 3. 保存解决方案，然后启动应用程序。在“小时”框中输入 **10**，然后在“工资率”框中输入 **5**。单击**计算**按钮。标签控件中将显示数值 50.00、0.00 和 50.00。单击**清除**按钮以移除文本框和标签控件的内容，然后点击**退出**按钮。
- 4. 关闭代码编辑器窗口，然后关闭解决方案。

## 小测验 1

- 1. Call 语句中的项被称为 ________。
  - a. 实参
  - b. 形参
  - c. 传递者
  - d. 以上都不是。
- 2. 您可以在代码编辑器窗口中，在 ________ 输入您的子过程。
  - a. Public Class 行上方
  - b. 第一个事件过程上方
  - c. End Class 行下方
  - d. 以上所有。
- 3. 当文本框的内容发生更改时，文本框的 ________ 事件发生。
  - a. ChangedText
  - b. ModifiedText
  - c. TextModified
  - d. TextChanged

过程。当仅传递内容时，接收过程不会获得对内存中变量的访问权；因此，它无法更改存储在变量中的值。当接收过程需要知道变量的内容，但不需要更改内容时，您会按值传递变量。除非另有指定，否则在 Visual Basic 中，变量按值传递。您将在下一步骤中编码的“生日快乐”应用程序将两个变量按值传递给一个子过程。

### 打开生日快乐应用程序，然后为该应用程序编码：

- 1. 打开 **Birthday Solution（Birthday Solution.sln）** 文件，该文件位于 ClearlyVB\Chap17\Birthday Solution 文件夹中。如有必要，请打开设计器窗口。当用户单击“显示消息”按钮时，按钮的 Click 事件过程将提示用户输入名和年龄。然后它将调用一个子过程，以生日消息显示这两个输入项，如下所示：“罗伯，18岁生日快乐！”

- 2. 打开代码编辑器窗口。找到 btnDisplay 控件的 Click 事件过程。该代码提示用户输入名字和年龄（以年为单位），并将值存储在 strName 和 strAge 变量中。

- 3. 您将使用名为 DisplayMessage 的子过程来显示生日消息。该子过程需要知道该人的名字和年龄，但不需要更改这两个值。因此，您将按值传递 strName 和 strAge 变量。首先，输入相应的 Call 语句。单击 btnDisplay 控件的 Click 事件过程中 End Sub 子句上方的 **空白行**，然后输入 **Call DisplayMessage(strName, strAge)** 并按 **Enter**。不要担心 Call 语句中 DisplayMessage 下方出现的锯齿线。当您在代码编辑器窗口中输入 DisplayMessage 过程后，该锯齿线将消失。

- 4. 现在输入 DisplayMessage 过程。该过程需要两个形参来存储 Call 语句传递给它的值。由于 Call 语句传递两个字符串，因此两个形参都必须是 String 变量。单击 Public Class frmMain 行下方的 **空白行**，然后按 **Enter** 插入另一个空白行。输入 **Private Sub DisplayMessage(ByVal strPerson As String, ByVal strYears As String)** 并按 **Enter**。参见图 17-6。注意，Call 语句中实参的个数、数据类型和顺序与过程头中相应形参的个数、数据类型和顺序匹配。还要注意，形参的名称不需要与相应实参的名称相同。实际上，为了避免混淆，通常最好为实参和形参使用不同的名称。

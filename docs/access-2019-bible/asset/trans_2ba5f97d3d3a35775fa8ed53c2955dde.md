

所有以井号（#）开头的关键字仅供 VBA 编译器识别。这些关键字（#Const、#If、#Else 和 #End If）构成对 VBA 编译器的指令，用于在项目的编译版本中包含（或排除）某些语句。

（使用编译器指令进行条件编译在第 24 章中介绍。）

前一幅图中出现的 #Const 指令可以出现在模块的任何位置，只要它位于 #If 指令之上即可。#Const 的逻辑位置是在模块的声明部分，因为 #Const 值对模块是全局的。在图中，编译器常量被设置为 False，这意味着 #If 和 #End If 之间的语句不会被编译到应用程序的 VBA 项目中。在这种情况下，MsgBox 语句不会被处理，也不会出现在用户界面中。将 #Const 指令的值设置为 True 则会在代码运行时显示 MsgBox 语句。

编译器指令也可以用于 MsgBox 之外的语句。例如，你可以使用编译器指令有条件地将功能、额外帮助或其他功能编译到应用程序中。编译器指令对于抑制用于调试目的且在将应用程序交给用户之前必须静音的 MsgBox 语句特别有效。你只需将 #Const 语句设置为 True 即可轻松重新激活 MsgBox 语句。

continued
这是 Access VBA 项目中用于同一目的的术语和语法在不同部分差异很大的一个地方。
如果你好奇的话，你可以为编译器常量指定任何你想要的名称。本节中的示例仅出于方便使用 gDEBUG1，但它也可以是 MyCompilerConstant、Betty、DooDah 或任何其他有效的常量名称。

## 使用 Debug.Print

第二种常用的调试技术是使用 Debug.Print 将消息输出到“立即”窗口。（Print 实际上是 Debug 对象的 方法。）图 27.5 显示了 sSQL 变量在“立即”窗口中的外观。

### FIGURE 27.5

Use Debug.Print to output messages to the Immediate window.

![](img/1e45673ab6eca9d20e67635ff5b9b318_921_0.png)

以下代码可以在 Chapter27.accdb 中的 modUsingDebugDotPrint 模块中找到。它几乎与 modUsingMsgBox 中的代码相同，只是它不是使用 MsgBox 检查变量，而是使用 Debug.Print：

```
Sub UsingDebugDotPrint()
Dim db As DAO.Database
Dim rs As DAO.Recordset
Dim sSQL As String

Set db = CurrentDb

sSQL = "SELECT DISTINCTROW OrderDetails.OrderID, " _
& "OrderDetails.ProductID, " _
& "Products.ProductName, " _
& "OrderDetails.UnitPrice, " _
& "OrderDetails.Quantity, " _
& "OrderDetails.Discount, " _
& "CCur(OrderDetails.UnitPrice*Quantity) AS ExtendedPrice " _
& "FROM Products INNER JOIN OrderDetails " _
& "ON Products.ProductID = OrderDetails.ProductID " _
& "ORDER BY OrderDetails.OrderID;"

Debug.Print "sSQL: " & sSQL

Set rs = db.OpenRecordset(sSQL, DB_OPEN_DYNASET)

rs.Close
Set rs = Nothing
Set db = Nothing

End Sub
```

与 MsgBox 语句不同，你不需要做任何特殊操作来从用户界面中抑制 Debug.Print 输出。Debug.Print 的输出只会进入“立即”窗口，而由于最终用户永远看不到“立即”窗口，因此你不必担心用户会遇到调试消息。

Debug.Print 的问题从图 27.5 中显而易见。长字符串在“立即”窗口中不会换行。此外，必须可见“立即”窗口才能查看其输出。但这些限制相对无害，你会在应用程序中经常使用 Debug.Print。

> NOTE
> 有些人报告说过多的 Debug.Print 语句会减慢应用程序的速度。即使“立即”窗口不可见，Access 也会执行代码中发现的 Debug.Print 语句。你可能需要考虑用“编译器指令”边栏中描述的编译器指令将每个 Debug.Print 语句包围起来，以将其从最终用户版的应用程序中移除。

## 使用 Access 调试工具

Access 提供了完整的调试工具和其他功能。你使用这些工具来监视 VBA 代码的执行，在语句处暂停代码执行以便在该时刻检查变量的值，并执行其他调试任务。

## 使用“立即”窗口运行代码

通过选择 View ▸ Immediate Window 或按 Ctrl+G 打开“立即”窗口（也称为“调试”窗口）。你可以在任何时候打开“立即”窗口（例如，在设计窗体时）。有时在处理窗体或报表时，你会发现测试一行代码或运行一个过程（两者都由“立即”窗口支持）很有用。

“立即”窗口如图 27.6 所示。“立即”窗口允许与代码进行一定的交互，并为 Debug.Print 语句提供输出区域。基本的调试过程包括停止执行以便检查代码和变量、动态监视变量值以及逐步执行代码。

### FIGURE 27.6

Get to know the Immediate window. You'll use it a lot in Access.

![](img/1e45673ab6eca9d20e67635ff5b9b318_923_0.png)

“立即”窗口最基本的使用之一是运行代码，例如内置函数，或你编写的子程序和函数。图 27.7 显示了在“立即”窗口中运行的几个示例。

### FIGURE 27.7

Running code from the Immediate window is a common practice.

![](img/1e45673ab6eca9d20e67635ff5b9b318_923_1.png)

图 27.7 中的第一个示例显示了如何运行已添加到 VBA 项目中的子过程（UsingDebugDotPrint）。该子过程包含一个 Debug.Print 语句，返回一个长的 SQL 语句，并在按下 Enter 键时在过程名称下方显示该输出。

在第二个示例中，内置的 Now() 函数已从“立即”窗口运行，返回当前日期和时间。Now() 函数名称前面的问号（?）是 Print 关键字的快捷方式。代替输入 ?Now，你可以输入 Print Now。问号和 Print 关键字都是指示“立即”窗口显示（或打印）Now() 函数返回的值。

图 27.7 中的第三个示例显示了从“立即”窗口调用函数（IsLastDayOfMonth）。与 Now() 一样，问号用于指示 VBA 返回函数的值。传递了一个必需的参数，结果显示在函数调用下方。此函数为此示例已从 Private 改为 Public，因为只有 Public 函数才能从“立即”窗口调用。

## 使用断点暂停执行

你通过在代码中设置断点来暂停执行。当 Access 遇到断点时，执行会立即停止，允许你切换到“立即”窗口以设置或检查变量的值。

设置断点很容易。打开代码窗口并单击语句左侧的灰色“边距指示器”栏，以在该语句处停止执行（见图 27.8）。或者，将光标定位在该行并单击“断点”工具栏按钮。断点本身显示为代码窗口左侧边缘灰色栏中的一个大棕色点，以及代码后面的棕色高亮。断点语句的文本以粗体字体显示。

### FIGURE 27.8

Setting a breakpoint is easy.

![](img/1e45673ab6eca9d20e67635ff5b9b318_924_0.png)

### Tip

你可以在“选项”对话框的“编辑器格式”选项卡中更改所有这些颜色和字体特征。

删除断点只需单击“边距指示器”栏中的断点指示器即可。关闭应用程序时也会自动删除断点。

当执行到达断点时，Access 会暂停执行并在断点处打开模块（见图 27.9）。现在你使用“立即”窗口（见前一节）来检查变量的值并执行其他操作，或使用本节中描述的任何其他调试工具。代码窗口和“立即”窗口都不是模态的，因此你仍然可以完全访问开发环境。

### FIGURE 27.9

Execution stops on the breakpoint.

![](img/1e45673ab6eca9d20e67635ff5b9b318_925_0.png)

图 27.10 说明了在断点处暂停执行时查看变量值的两种技术。本地窗口包含当前过程中所有变量的名称和当前值。你可以通过从“视图”菜单中选择“本地窗口”来打开本地窗口。如果你想以略有不同的格式查看变量的值，请在“立即”窗口中使用 Print 命令（?）来显示变量的值。


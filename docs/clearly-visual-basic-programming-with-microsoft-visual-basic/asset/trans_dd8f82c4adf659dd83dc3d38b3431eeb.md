
- a. 列出输出项和输入项，以及任何处理项，然后使用伪代码创建合适的算法。

- b. 创建一个新的 Visual Basic Windows 应用程序。分别将解决方案、项目和窗体文件命名为 Shopper Solution、Shopper Project 和 frmMain.vb。将应用程序保存在 ClearlyVB\Chap11 文件夹中。如有必要，将窗体名称改为 frmMain。

- c. 创建合适的界面。包含一个 Exit 按钮。编写 Exit 按钮的 Click 事件过程以及该问题的算法代码。将奖励积分显示为整数。保存解决方案。

- d. 启动并测试应用程序。停止应用程序，然后关闭解决方案。

![](img/cf88270932e011575089da06b940a1d9_264_0.png)

- 10. 打开 FigureThisOut Solution（FigureThisOut Solution.sln）文件，该文件位于 ClearlyVB\Chap11\FigureThisOut Solution 文件夹中。打开代码编辑器窗口，研究 btnDisplay 控件的 Click 事件过程。该过程执行什么任务？收取各种费率的规则是什么？测试应用程序以验证你的答案是否正确。停止应用程序，然后关闭解决方案。

![](img/cf88270932e011575089da06b940a1d9_264_1.png)

- 11. 在本练习中，你要找出应用程序代码中的一个错误。打开 SwatTheBugs Solution（SwatTheBugs Solution.sln）文件，该文件位于 ClearlyVB\Chap11\SwatTheBugs Solution 文件夹中。该应用程序应根据用户输入的总价显示运费。如果总价小于 $1，运费为 $0。如果总价大于或等于 $1 但小于 $100，运费为 $5。如果总价大于或等于 $100 但小于 $501，运费为 $10。如果总价大于或等于 $501 但小于 $1001，运费为 $12。如果总价大于或等于 $1001，运费为 $14。启动应用程序。使用以下总价测试应用程序：100、501、1500、500.75、30 和 1000.33。注意，应用程序对其中一些总价未显示正确的运费。打开代码编辑器窗口并研究代码。找出并更正代码中的错误。保存解决方案，然后启动并测试应用程序。

## “试一试”练习答案

- 1. 要修改 btnDisplay 控件的 Click 事件过程，请将 If...Then...Else 语句改为：

```vb
Select Case intCode
    Case 1
        lblName.Text = "Payroll"
    Case 2
        lblName.Text = "Personnel"
    Case 3
        lblName.Text = "IT"
    Case Else
        lblName.Text = "Invalid code"
End Select
```

- 2. 要修改 btnCalc 控件的 Click 事件过程，请将外层的 If...Then...Else 语句改为：

```vbnet
Select Case chkEmployee.Checked
    Case True
        decTotal = decTotal * (1 - decEMP_DISC_RATE)
    Case Else
        If intQuantity > 20 Then
            decTotal = decTotal * (1 - decNON_EMP_DISC_RATE)
        End If
End Select
```

## 12

### 测试，测试……1、2、3

学习完第 12 章后，你应该能够：

- 为应用程序选择合适的测试数据
- 防止在文本框中输入不需要的字符
- 使用 MessageBox.Show 方法创建消息框
- 去除字符串开头和结尾的空格

![](img/cf88270932e011575089da06b940a1d9_266_0.png)

### 你的应用程序能通过测试吗？

正如你在第 3 章所学，问题解决过程的最后一步是在将程序发布给用户之前对其进行严格测试。你使用计算机以及一组包含有效数据和无效数据的示例数据来测试程序。有效数据是程序期望用户输入的数据。使用有效数据进行测试，以确保程序产生正确结果。另一方面，无效数据是程序不期望用户输入的数据。无效数据通常源于用户输入错误、以不正确格式输入数据或遗漏必填项。使用无效数据进行测试，以确保程序不会因输入错误而显示错误结果或意外终止。图 12-1 列出了为应用程序选择合适测试数据的一些准则。你将使用这些准则来测试本章中的几个应用程序。（后续章节会向列表中添加更多准则。）

**选择测试数据的准则**

- 1. 不输入任何数据测试应用程序。
- 2. 如果应用程序的代码期望某个文本框中包含数字，请为该文本框同时使用有效值和无效值。通常，测试数据中应包含数字 0，以及正整数和负整数、正非整数和负非整数，以及字母数字文本。
- 3. 如果应用程序的代码包含选择结构，请使用能够测试每个分支的值。如果条件包含一个值范围，测试数据应包含该范围的最低值和最高值，以及范围内的一个值。如果条件比较字符串，测试数据中应包含大写文本和小写文本。

**图 12-1：** 选择应用程序测试数据的准则

### Only Cookies 版本 1 应用程序

图 12-2 显示了 Only Cookies 版本 1 应用程序的界面。该界面提供一个文本框，用于输入订购的曲奇磅数；磅数可以包含小数位。每磅曲奇售价 5 美元。当用户单击 Calculate 按钮时，该按钮的 Click 事件过程会计算并显示订单总价。Click 事件过程如图 12-3 所示。请注意，该过程使用一个 Integer 命名常量表示每磅价格，并使用两个 Decimal 变量分别表示订购磅数和总价。

![](img/cf88270932e011575089da06b940a1d9_268_0.png)

**图 12-2：** Only Cookies 版本 1 应用程序的界面

```vbnet
Private Sub btnCalc_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles btnCalc.Click
    ' calculates and displays the total price

    Const intPRICE As Integer = 5
    Dim decOrdered As Decimal
    Dim decTotalPrice As Decimal

    ' assign user input to a variable
    Decimal.TryParse(txtOrdered.Text, decOrdered)

    ' calculate and display total price
    decTotalPrice = decOrdered * intPRICE
    lblTotalPrice.Text = decTotalPrice.ToString("C2")
End Sub
```

**图 12-3：** Only Cookies 版本 1 应用程序中 Calculate 按钮的 Click 事件过程

在测试 Only Cookies 版本 1 应用程序之前，你将使用图 12-1 中的准则，以及图 12-2 和图 12-3 所示的界面和代码，创建一组测试数据。你需要将测试数据及其预期结果记录到测试图表中。第一条准则是：不输入任何数据来测试应用程序。如界面和代码所示，用户在此应用程序中只输入一项数据：订购的曲奇磅数。如果用户在未在 Pounds ordered 框中输入值的情况下单击 Calculate 按钮，则该过程应在 Total price 框中显示 $0.00。（该过程代码中的“C2”格式字符串会将总价格式化为带美元符号和两位小数的形式。）在测试图表中，记录“未输入数据”和 $0.00，如图 12-4 所示。

| 测试数据 | 预期结果 |
|---|---|
| 未输入数据 | $0.00 |

**图 12-4：** 应用程序测试图表中的第一条记录

Only Cookies 版本 1 应用程序期望用户在 Pounds ordered 文本框中输入一个数字。因此，根据图 12-1 中的第二条准则，你应通过在文本框中输入有效值和无效值来测试应用程序。如该准则所述，用于测试的典型值包括数字 0、正整数和负整数、正非整数和负非整数，以及字母数字文本。首先列出用户可能作为订购磅数输入的有效值。例如，用户可能输入数字 0，或正整数 10 和 25；也可能输入正非整数 4.5。预期结果为 $0.00、$50.00、$125.00 和 $22.50。（回想一下，每磅价格为 5 美元。）如果用户想计算退款，也可能输入负数，例如负整数 -3 或负非整数 -6.5。使用这些值的预期结果为 ($15.00) 和 ($32.50)。你将测试数据及其预期结果记录到测试图表中，如图 12-5 所示。

| 测试数据 | 预期结果 |
|---|---|
| 未输入数据 | $0.00 |
| **有效值：** 0 | $0.00 |
| 10 | $50.00 |
| 25 | $125.00 |
| 4.5 | $22.50 |
| -3 | ($15.00) |
| -6.5 | ($32.50) |

**图 12-5：** 应用程序测试图表中输入的有效值

现在考虑用户可能误输入的值。在当前应用程序中，用户可能无意中输入字母 x、# 符号或 3O（数字 3 后跟大写字母 O）。如果用户输入无效值，应用程序应在 Total price 框中显示 $0.00。图 12-6 显示了输入到测试图表中的无效值及其预期结果。请注意，测试数据包含数字 0、正整数和负整数、正非整数和负非整数，以及字母数字文本。


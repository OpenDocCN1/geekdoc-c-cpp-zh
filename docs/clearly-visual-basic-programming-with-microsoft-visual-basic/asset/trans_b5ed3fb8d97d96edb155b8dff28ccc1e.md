
- 5. 在 lblPayments 控件中显示利率和付款之前，该过程应清除控件中先前已有的任何信息。键入**clear label control**，按**Enter**，然后键入**lblPayments.Text = String.Empty**，再按两次**Enter**。
- 6. 算法中的第3步是一个前置测试循环，你希望其中的指令按精确的次数处理——本例中为从4%到7%，步长为1%。你将使用 For...Next 语句编写这个计数器循环。键入**calculate and display the monthly payments**并按**Enter**。键入**For decRate As Decimal = .04 To .07 Step .01**并按**Enter**。注意 For...Next 语句的*startValue*、*endValue*和*stepValue*可以包含小数位，并且计数器变量的数据类型为 Decimal。
- 7. 将 Next 子句更改为**Next decRate**，然后保存解决方案。

## FINANCIAL.PMT 方法

根据图 15-7 所示的算法，循环中的第一条指令应根据本金、期限和当前年利率计算月付款额。计算贷款定期付款额的数学公式相当复杂，因此 Visual Basic 提供了替你执行该计算的方法，该方法称为**Financial.Pmt 方法**。（“Pmt”代表“Payment”，即付款。）图 15-8 展示了该方法的基本语法，并列出了语法中三个参数各自的含义。*Rate*和*NPer*（期数）参数必须使用相同的单位表示。如果*Rate*是月利率，则*NPer*必须指定月付款次数。同样，如果*Rate*是年利率，则*NPer*必须指定年付款次数。图 15-8 还包含使用 Financial.Pmt 方法的示例。示例1计算一笔贷款本金$9,000、期限3年、年利率5%的贷款的年付款额。如示例所示，Financial.Pmt 方法返回并四舍五入到分的年付款额为 -3,304.88。这意味着，如果你以5%的年利率借款$9,000，期限3年，则需要每年支付$3,304.88，共支付三次，才能还清贷款。注意，Financial.Pmt 方法返回的是负数。要将负数变为正数，可以在该方法前面加上负号运算符，如下所示：**-Financial.Pmt(.05, 3, 9000)**。如你在第6章中所学，负号运算符会反转数字的符号：负数前加上负号运算符会变为正数，正数前加上负号运算符会变为负数。图 15-8 中示例2的 Financial.Pmt 方法计算一笔贷款本金$12,000、期限5年、年利率6%的贷款的月付款额。在此示例中，*Rate*和*NPer*参数以月为单位而不是以年为单位表示。该贷款的月付款额四舍五入到分并转换为正数后为 231.99。（Financial.Pmt 方法也可用于计算投资而非贷款的定期付款额。你将在计算机练习 7 中学习如何执行此操作。）

```
Private Sub btnCalc_Click(ByVal sender As Object, ByVal e As System.EventArgs)
    ' calculates and displays monthly payment amounts

    Dim decPrincipal As Decimal
    Dim decPayment As Decimal
    Dim intTerm As Integer

    ' assign input to variables
    Decimal.TryParse(txtPrincipal.Text, decPrincipal)
    Integer.TryParse(txtTerm.Text, intTerm)

    ' clear label control
    lblPayments.Text = String.Empty

    ' calculate and display the monthly payments
    For decRate As Decimal = 0.04 To 0.07 Step 0.01
        decPayment = -Financial.Pmt(decRate / 12, intTerm * 12, decPrincipal)
        lblPayments.Text = lblPayments.Text & decRate.ToString("P0") _
            & "  ->  " & decPayment.ToString("C2") _
            & ControlChars.NewLine
    Next decRate
End Sub
```

*输入这 3 行代码*

**图 15-9：** 在 btnCalc 控件的 Click 事件过程中输入的附加代码

- 3. 图 15-9 中 For...Next 循环中的指令将使用 4%、5%、6% 和 7% 的利率执行四次。保存解决方案，然后启动应用程序。首先显示一笔贷款本金$12,000、期限5年的贷款的月付款额。在**本金**框中键入 **12000**，然后在**期限**框中键入 **5**。单击**计算月付款额**按钮。界面中会显示四个利率和月付款额，如图 15-10 所示。

![](img/cf88270932e011575089da06b940a1d9_352_0.png)

**图 15-10：** 界面中显示的利率和月付款额

- 4. 删除本金框和期限框中的输入内容，然后点击**计算月付款额**按钮；这样做会导致运行时错误，也称为**异常**。代码编辑器会突出显示遇到错误的语句，并显示一个提供相关错误信息的帮助框。在本例中，代码编辑器突出显示包含 Financial.Pmt 方法的语句，帮助框指出 NPer 参数不包含有效值。
- 5. 将鼠标指针放在突出显示语句中的 intTerm 上，如图 15-11 所示。该变量包含数字 0，因为未在期限框中输入期限。

![](img/cf88270932e011575089da06b940a1d9_353_0.png)

**图 15-11：** 无效 NPer 值导致的运行时错误的结果

- 6. 单击菜单栏上的**调试**，然后单击**停止调试**。

如前所述，Financial.Pmt 方法包含一个用于计算定期付款额的复杂数学公式。期限出现在公式的除数部分；因此，其值不能为0，因为在数学上不可能除以零。

**完成 btnCalc 控件的 Click 事件过程，然后测试应用程序：**

- 1. 单击“' calculate and display the monthly payments”注释上方的**空行**，然后按 **Enter** 插入一个空行。键入**' determine whether the term is valid**并按 **Enter**。键入图 15-12 所示的选择结构。你需要将该注释和 For...Next 语句移到选择结构的 false 路径中。

输入以下选择结构

```
' clear label control
lblPayments.Text = String.Empty

' determine whether the term is valid
If intTerm = 0 Then
    MessageBox.Show("Please enter a valid term.", _
        "Monthly Payment Calculator", _
        MessageBoxButtons.OK, MessageBoxIcon.Information)
Else
    ' calculate and display the monthly payments
    For decRate As Decimal = 0.04 To 0.07 Step 0.01
        decPayment = -Financial.Pmt(decRate / 12, intTerm * 12, decPrincipal)
        lblPayments.Text = lblPayments.Text & decRate.ToString("P0") _
            & "  ->  " & decPayment.ToString("C2") _
            & ControlChars.NewLine
    Next decRate
End If
End Sub
```

**图 15-12：** 在过程中输入的选择结构

- 2. 保存解决方案，然后启动应用程序。单击**计算月付款额**按钮。消息框中会显示“Please enter a valid term.”（请输入有效期限。）。单击**确定**按钮关闭消息框。
- 3. 在**本金**框中键入 **12000**，然后在**期限**框中键入 **5**。单击**计算月付款额**按钮。界面中会显示利率和月付款额，如前文图 15-10 所示。
- 4. 单击**退出**按钮。关闭代码编辑器窗口，然后关闭解决方案。

## 小测验 2

- 1. 编写一条 Visual Basic 语句，播放名为 Giggle.wav 的音频文件。
- 2. 若要通过 Financial.Pmt 方法显示年付款额，你需要 ________。
    - a. 将年利率除以 12
    - b. 将年利率乘以 12
    - c. 使用年利率
- 3. 可以使用 ________ 运算符将负数（例如 Financial.Pmt 方法返回的数）变为正数。


13. 单击 `Next decRate` 子句中**最后一个 e 之后**，然后按 **Enter** 在该子句下方插入一个空行。

14. 外层循环中的最后一条指令应在 Payments 框中显示一个空行。这将把当前期限的信息与上一期限的信息分隔开。在 `Next decRate` 子句下方的空行中，键入 **`txtPayments.Text = txtPayments.Text & ControlChars.NewLine`**。

15. 保存解决方案，然后将屏幕上的代码与图 16-9 中显示的代码进行比较。

```vb
Private Sub btnCalc_Click(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles btnCalc.Click
    ' calculates and displays monthly payment amounts
    ' using terms of 2 through 5 years and rates from 4% through 7%

    Dim decPrincipal As Decimal
    Dim decPayment As Decimal

    ' assign principal to a variable
    Decimal.TryParse(txtPrincipal.Text, decPrincipal)

    ' clear the Payments box
    txtPayments.Text = String.Empty

    ' calculate and display the monthly payments
    For intTerm As Integer = 2 To 5
        txtPayments.Text = txtPayments.Text _
            & "Term: " & intTerm.ToString & ControlChars.NewLine
        For decRate As Decimal = 0.04 To 0.07 Step 0.01
            decPayment = -Financial.Pmt(decRate / 12, intTerm * 12, decPrincipal)
            txtPayments.Text = txtPayments.Text & decRate.ToString("P0") _
                & " -> " & decPayment.ToString("C2") _
                & ControlChars.NewLine
        Next decRate
        txtPayments.Text = txtPayments.Text & ControlChars.NewLine
    Next intTerm
End Sub
```

**图 16-9：** btnCalc 控件的 Click 事件过程

现在你将测试代码，以确定它是否能正确运行。

### 测试 Monthly Payment Calculator 应用程序

1. 启动应用程序。在 Principal 框中键入 **12000**，然后单击 **Calculate Monthly Payments** 按钮。期限、利率和月供将显示在界面中，如图 16-10 所示。

![](img/cf88270932e011575089da06b940a1d9_374_0.png)

**图 16-10：** 显示期限、利率和付款的界面

2. 使用滚动条查看 4 年期和 5 年期的月供。

3. 删除 Principal 框中的内容，然后单击 **Calculate Monthly Payments** 按钮。每个期限内的每个利率都会显示 $0.00 的月供。

4. 单击 **Exit** 按钮。关闭代码编辑器窗口，然后关闭解决方案。

## 但我想换一种方式

除了使用两个 `For...Next` 语句来编写 Monthly Payment Calculator 应用程序外，你也可以使用两个 `Do...Loop` 语句，或者一个 `For...Next` 语句和一个 `Do...Loop` 语句。在下一组步骤中，你将修改 Monthly Payment Calculator 应用程序，使其使用 `Do...Loop` 语句来跟踪年利率。

### 修改 Monthly Payment Calculator 应用程序

1. 使用 Windows 复制 Monthly Payment Solution-Version 1 文件夹。将副本保存到 `ClearlyVB\Chap16` 文件夹中。将副本重命名为 Monthly Payment Solution-Version 2。

2. 打开 Monthly Payment Solution-Version 2 文件夹中包含的 **Monthly Payment Solution**（**Monthly Payment Solution.sln**）文件。打开设计器窗口，然后打开代码编辑器窗口。

3. 找到 btnCalc 控件的 Click 事件过程。按图 16-11 所示修改该过程的代码。请注意，当你使用 `Do...Loop` 语句（而不是 `For...Next` 语句）来跟踪年利率时，必须包含用于声明、初始化和更新 `decRate` 变量的指令。

- 输入此声明语句
- 输入此注释和初始化语句
- 将此 `For` 子句替换为此 `Do` 子句
- 输入此注释和更新语句
- 将此 `Next` 子句替换为此 `Loop` 子句

```vb
Dim decPrincipal As Decimal
Dim decPayment As Decimal
Dim decRate As Decimal

' assign principal to a variable
Decimal.TryParse(txtPrincipal.Text, decPrincipal)

' clear the Payments box
txtPayments.Text = String.Empty

' calculate and display the monthly payments
For intTerm As Integer = 2 To 5
    txtPayments.Text = txtPayments.Text _
        & "Term: " & intTerm.ToString & ControlChars.NewLine
    ' initialize counter
    decRate = 0.04
    Do Until decRate > 0.07
        decPayment = -Financial.Pmt(decRate / 12, intTerm * 12, decPrincipal)
        txtPayments.Text = txtPayments.Text & decRate.ToString("P0") _
            & "  " & decPayment.ToString("C2") _
            & ControlChars.NewLine
        ' update counter
        decRate = decRate + 0.01
    Loop
    txtPayments.Text = txtPayments.Text & ControlChars.NewLine
Next intTerm
```

**图 16-11：** btnCalc 控件的 Click 事件过程中包含的修改后代码

4. 保存解决方案，然后启动应用程序。在 Principal 框中键入 **12000**，然后单击 **Calculate Monthly Payments** 按钮。期限、利率和月供将显示在界面中，如前文图 16-10 所示。单击 **Exit** 按钮。关闭代码编辑器窗口，然后关闭解决方案。

## 小测验 1

1. 编写代码，使用两个前测循环以及字母 X 显示以下图案。外层循环使用 `Do...Loop` 语句。嵌套循环使用 `For...Next` 语句。将图案显示在 `lblPattern` 控件中。

    ```
    XXXX
    XXXX
    XXXX
    ```

2. 使用外层循环的 `For...Next` 语句和嵌套循环的 `Do...Loop` 语句重写问题 1 中的代码。

3. 要使文本框显示滚动条，必须将其 __________ 属性设置为 True。

    a. DisplayBars  
    b. Multiline  
    c. Scrollable  
    d. ScrollBars

## 小结

- 重复结构可以嵌套，这意味着你可以将一个重复结构放在另一个重复结构内。

- 要使嵌套重复结构正确工作，它必须完全包含在外层重复结构中。

- 当文本框的 Multiline 属性设置为 True 时，它可以接受多行文本。

- 文本框的 ScrollBars 属性决定控件上是否显示滚动条。但是，要使 ScrollBars 属性生效，必须将文本框的 Multiline 属性设置为 True。

- 可以通过将文本框的 ReadOnly 属性设置为 True，来阻止用户编辑文本框的内容。

## 关键术语

- **Multiline 属性**——指定文本在控件中是否可以跨多行的文本框属性

- **ReadOnly 属性**——指定用户是否可以编辑文本框内容的文本框属性

- **ScrollBars 属性**——指示控件上是否显示滚动条的文本框属性；与 Multiline 属性配合使用

## 小测验答案

### 小测验 1

**1.**

```vb
Dim intOuter As Integer
intOuter = 1
Do While intOuter < 4
    For intNested As Integer = 1 To 4
        lblPattern.Text = lblPattern.Text & "X"
    Next intNested
    lblPattern.Text = lblPattern.Text & ControlChars.NewLine
    intOuter = intOuter + 1
Loop
```

**2.**

```vb
Dim intNested As Integer
For intOuter = 1 To 3
    intNested = 1
    Do While intNested < 5
        lblPattern.Text = lblPattern.Text & "X"
        intNested = intNested + 1
    Loop
    lblPattern.Text = lblPattern.Text & ControlChars.NewLine
Next intOuter
```

**3.** b. Multiline

## 复习题

1. 以下哪一项不会在 `lblAsterisks` 控件中每行显示四个星号，共显示三行？

    a. `lblAsterisks.Text = "****" & ControlChars.NewLine & "****" & ControlChars.NewLine & "****"`

    b.

    ```vb
    For intCounter As Integer = 1 To 3
        lblAsterisks.Text = lblAsterisks.Text & "****" & ControlChars.NewLine
    Next intCounter
    ```

    c.

    ```vb
    For intX As Integer = 1 To 4
        For intY As Integer = 1 To 3
            lblAsterisks.Text = lblAsterisks.Text & "*"
        Next intY
        lblAsterisks.Text = lblAsterisks.Text & ControlChars.NewLine
    Next intX
    ```

    d.

    ```vb
    For intX As Integer = 1 To 3
        For intY As Integer = 1 To 4
            lblAsterisks.Text = lblAsterisks.Text & "*"
        Next intY
        lblAsterisks.Text = lblAsterisks.Text & ControlChars.NewLine
    Next intX
    ```

2. 以下代码中的 `MessageBox.Show` 方法将被处理多少次？

```vb
For intX As Integer = 4 To 11 Step 3
    For intY As Integer = 1 To 3
        MessageBox.Show("Hello")
    Next intY
Next intX
```

    a. 9  
    b. 10  
    c. 11  
    d. 以上都不是。

3. 复习题 2 中的嵌套循环结束时，`intY` 变量中的值是多少？

    a. 0  
    b. 1  
    c. 3  
    d. 以上都不是。


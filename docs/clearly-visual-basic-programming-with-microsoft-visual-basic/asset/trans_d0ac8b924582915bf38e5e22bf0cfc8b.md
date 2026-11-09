
- 2. 打开“代码编辑器”窗口。图 8-1 显示了在 btnCalc 控件的 Click 事件过程中输入的代码。红色细框提示您有三行代码包含语法错误。但是，如果您没有非常仔细地注意代码，可能会注意不到它们。

```vb
Private Sub btnCalc_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles btnCalc.Click
    ' calculates and displays the total sales

    ' declare variables
    Dim intNorth As Integer
    Dim intSouth As Integer
    Dim intEast As Integer
    Dim intWest As Integer
    Dim intTotal As Integer

    ' assign input to variables
    Integer.TryParse(txtNorth.Text, intNorth
    Integer.TryParse(txtSouth.Text, intSouth)
    Integer.TryParse(txtEast.Text, intEast)
    Integer.TryParse(txtWest.Text, intWest)

    ' calculate total sales
    inTotal = intNorth + intSouth + intEast + intWest

    ' display total sales
    lblTotal.Text = intTotal.ToString("C0")

End Sub
```

**图 8-1：** btnCalc 控件的 Click 事件过程

- 3. 启动应用程序。如果出现图 8-2 所示的对话框，请单击**否**按钮。

![](img/cf88270932e011575089da06b940a1d9_168_0.png)

**图 8-2：** 对话框

- 4. 图 8-3 所示的“错误列表”窗口会在 IDE 底部打开。“错误列表”窗口指示代码包含三个错误。该窗口提供了每个错误的说明以及每个错误在代码中的位置。（您可以将鼠标指针定位在窗口的上边框，直到鼠标指针看起来像这样：[调整大小光标]，然后按住鼠标左键并向上或向下拖动边框，以更改“错误列表”窗口的大小。）

![](img/cf88270932e011575089da06b940a1d9_169_0.png)

**图 8-3：** IDE 中的“错误列表”窗口

- 5. 在“错误列表”窗口中双击**未定义类型“Intger”。** “代码编辑器”会将插入点放在遇到错误的那一行，如图 8-4 所示。第一个错误只不过是一个输入错误：程序员原本想输入的是 Integer。

![](img/cf88270932e011575089da06b940a1d9_169_1.png)

**图 8-4：** 插入点位于包含第一个错误的行中

- 6. 您可以自己修复第一个语法错误，只需输入缺少的字母 e；或者，也可以让“代码编辑器”为您更正错误。在这一步中，您将看到如何让“代码编辑器”发挥作用。将鼠标指针悬停在字母 r 下方出现的红色细框上。会出现一个“错误”图标（红色圆圈中的白色感叹号）以及一个向下箭头。（如果看不到向下箭头，请将鼠标指针悬停在“错误”图标上，直到向下箭头出现。）单击**向下箭头**以显示修复错误的建议列表。参见图 8-5。

![](img/cf88270932e011575089da06b940a1d9_170_0.png)

**图 8-5：** 可能的解决方案列表

- 7. 单击列表中的**将“Intger”更改为“Integer”**。“代码编辑器”会将 Dim 语句中的 Intger 更改为 Integer，并从“错误列表”窗口中移除该错误。

- 8. 在“错误列表”窗口中双击**缺少“)”。** “代码编辑器”会将插入点放在包含第一个 TryParse 方法的行中，因为该语句缺少右括号。将鼠标指针悬停在字母 h 下方出现的红色细框上。当“错误”图标和向下箭头出现时，单击**向下箭头**。单击列表中的**插入缺少的“)”**。“代码编辑器”会插入缺少的括号，并从“错误列表”窗口中移除该错误消息。

- 9. 在“错误列表”窗口中双击**未声明名称“intTotal”。** “代码编辑器”会将插入点放在计算总销售额的语句开头。将鼠标指针悬停在字母 l 下方出现的红色细框上。当“错误”图标和向下箭头出现时，单击**向下箭头**。如消息所示，“代码编辑器”无法提供任何更正该错误的建议。参见图 8-6。

![](img/cf88270932e011575089da06b940a1d9_170_1.png)

**图 8-6：** 没有可用更正建议时出现的消息

```vb
Private Sub btnCalc_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles btnCalc.Click
    ' calculates and displays a 10%, 20%, and
    ' 30% discount on an item's price

    ' declare variables
    Dim decPrice As Decimal
    Dim decDiscount10 As Decimal
    Dim decDiscount20 As Decimal
    Dim decDiscount30 As Decimal

    ' calculate discounts
    decDiscount10 = decPrice * 0.1
    decDiscount20 = decPrice * 0.2
    decDiscount30 = decPrice * 0.3

    ' display discounts
    lbl10.Text = decDiscount10.ToString("N2")
    lbl20.Text = decDiscount20.ToString("N2")
    lbl30.Text = decDiscount30.ToString("N2")
End Sub
```

**图 8-7：** 在 btnCalc 控件的 Click 事件过程中输入的代码

- 3. 启动应用程序。在 Price 文本框中输入 **100**，然后单击**计算**按钮。界面显示每个折扣都是 $0.00，这是不正确的。单击**退出**按钮以停止应用程序。

- 4. 您将使用“调试”菜单运行 Visual Basic 调试器，这是一个帮助您定位代码中逻辑错误的工具。单击菜单栏上的**调试**。该菜单的“逐语句”选项将启动您的应用程序，并允许您逐句执行代码。它通过一次执行一条语句，并在执行每条语句之前立即暂停来实现这一点。单击**逐语句**。在 Price 文本框中输入 **100**，然后单击**计算**按钮。调试器会突出显示要执行的第一条指令。在本例中，它突出显示 btnCalc_Click 过程头。此外，一个箭头指向该指令，如图 8-8 所示，并且代码的执行已暂停。（如果界面仍显示在屏幕上，请单击“代码编辑器”窗口的标题栏。）

```vb
Private Sub btnCalc_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles btnCa...
    ' calculates and displays a 10%, 20%, and
    ' 30% discount on an item's price

    ' declare variables
    Dim decPrice As Decimal
    Dim decDiscount10 As Decimal
    Dim decDiscount20 As Decimal
```

**图 8-8：** 突出显示的过程头

将文本框的值赋给 decPrice 变量。换句话说，该过程中缺少一条语句。

```vb
Private Sub btnCalc_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles btnCa
    ' calculates and displays a 10%, 20%, and
    ' 30% discount on an item's price

    ' declare variables
    Dim decPrice As Decimal
    Dim decDiscount10 As Decimal
    Dim decDiscount20 As Decimal
    Dim decDiscount30 As Decimal

    ' calculate discounts
    decDiscount10 = decPrice * 0.1
    decDiscount20 = decPrice * 0.2
    decDiscount30 = decPrice * 0.3
```

**图 8-10：** 在执行突出显示的语句之前存储在 decPrice 中的值

- 8. 单击菜单栏上的**调试**，然后单击**停止调试**以停止调试器。单击最后一条 Dim 语句下方的空白行，然后按 **Enter** 插入另一个空白行。键入 `' assign price to a variable`，然后按 **Enter**，再键入 `Decimal.TryParse(txtPrice.Text, decPrice)`，然后按 **Enter**。

- 9. 保存解决方案。单击菜单栏上的**调试**，然后单击**逐语句**。在 Price 文本框中输入 **100**，然后单击**计算**按钮。（如果界面仍显示在屏幕上，请单击“代码编辑器”窗口的标题栏。）按 **F8** 处理过程头。调试器会突出显示 `Decimal.TryParse(txtPrice.Text, decPrice)` 语句，并暂停代码的执行。

- 10. 在处理突出显示的语句之前，txtPrice 控件的 Text 属性应包含 100，这是您在控件中输入的值。将鼠标指针放在突出显示语句中的 txtPrice.Text 上。框内显示 Text 属性包含预期值。100 用引号括起来，因为它被视为字符串。（正如您在第七章中学到的，字符串是用引号括起来的文本。）

- 11. decPrice 变量应包含其初始值 0D。将鼠标指针放在突出显示语句中的 decPrice 上。框内显示该变量包含预期值。

- 12. 按 **F8** 处理 TryParse 方法。调试器会突出显示 `decDiscount10 = decPrice * 0.1` 语句，然后暂停代码的执行。将鼠标指针放在 TryParse 方法中的 decPrice 上，如图 8-11 所示。请注意，在计算机处理该方法后，decPrice 变量包含数字 100D。


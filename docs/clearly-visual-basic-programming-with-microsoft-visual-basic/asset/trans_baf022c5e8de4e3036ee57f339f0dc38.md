

### 示例 3

```vb
    Do While strId Like "###"
```

当 strId 变量中存储的字符串以三个数字开头，后跟零个或多个字符时，该条件求值为 True；否则求值为 False。会使该条件求值为 True 的*字符串*示例包括“178”和“983Ab”。会使该条件求值为 False 的*字符串*示例包括“X34”和“34Z5”。

### 示例 4

```vb
    If strFirstName.ToUpper Like "T[OI]M" Then
```

当 strFirstName 变量中存储的字符串（转换为大写后）为“TOM”或“TIM”时，该条件求值为 True。当 strFirstName 变量不包含“TOM”或“TIM”时——例如，当其包含“TAM”或“Tommy”时——该条件求值为 False。

### 示例 5

```vb
    If strLetter Like "[a-z]" Then
```

当 strLetter 变量中存储的字符串为小写字母时，该条件求值为 True；否则求值为 False。

### 示例 6

```vb
    For intIndex As Integer = 0 To strUserEntry.Length - 1
        If strUserEntry.Substring(intIndex, 1) Like "[!a-zA-Z]" Then
            intNonLetter = intNonLetter + 1
        End If
    Next intIndex
```

将 strUserEntry 变量中包含的每个字符与字母表中的小写字母和大写字母进行比较，并统计不是字母的字符数。

**图 24-14：** *Like 运算符的语法和示例（接上一页）*

## 修改产品 ID 应用程序

在本章前面，你编写了产品 ID 应用程序，它显示用户输入的产品 ID 列表。你可能还记得，每个产品 ID 恰好包含五个字符。在下面这组步骤中，你将修改该应用程序，以确保这五个字符是三个字母后跟两个数字。

![](img/cf88270932e011575089da06b940a1d9_567_0.png)

在完成下一组步骤之前，观看 Ch24-Like 运算符视频可能会有帮助。

要修改产品 ID 应用程序，然后测试该应用程序：

- 1. 使用 Windows 复制 Product Solution 文件夹。将该副本保存在 ClearlyVB\Chap24 文件夹中。将副本重命名为 Modified Product Solution。
- 2. 打开 ClearlyVB\Chap24\Modified Product Solution 文件夹中包含的 **Product Solution (Product Solution.sln)** 文件。打开设计器窗口。
- 3. 打开代码编辑器窗口，并找到 btnAdd 控件的 Click 事件过程。将 'remove any leading and trailing spaces' 注释更改为 '**remove any leading and trailing spaces, then convert to uppercase.**'。同时将 strId = txtId.Text.Trim 语句更改为 **strId = txtId.Text.Trim.ToUpper.**。
- 4. 将 'verify length' 注释更改为 '**verify that the ID contains 3 letters followed by 2 numbers.**'。同时将 If 子句更改为 **If strId Like "[A-Z][A-Z][A-Z]##" Then**。
- 5. 在 If 子句下方的语句中，将 strId.ToUpper 更改为 **strId**。最后，将 MessageBox.Show 方法中的消息更改为 **"Invalid product ID"**。图 24-15 显示了修改后的 Click 事件过程。修改后的注释和代码在图中以底纹显示。

```vb
Private Sub btnAdd_Click(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles btnAdd.Click
    ' add product ID to listing

    Dim strId As String

    ' remove any leading and trailing spaces, then convert to uppercase
    strId = txtId.Text.Trim.ToUpper

    ' verify that the ID contains 3 letters followed by 2 numbers
    If strId Like "[A-Z][A-Z][A-Z]##" Then
        lblListing.Text = lblListing.Text & strId _
            & ControlChars.NewLine
    Else
        MessageBox.Show("Invalid product ID", _
            "Product ID", MessageBoxButtons.OK, _
            MessageBoxIcon.Information)
    End If

    txtId.Focus()
End Sub
```

图 24-15：修改后的注释和代码

- 4. 如果 strMessage 变量包含字符串“Today is Monday”，以下哪一项会将数字 9 赋给 intNum 变量？
  - a. intNum = strMessage.Substring("M")
  - b. intNum = strMessage.Substring("M", 1)
  - c. intNum = strMessage.IndexOf("M")
  - d. intNum = strMessage.IndexOf(0, "M")

- 5. 如果 strName 变量包含字符串“John Jones”，以下哪一项会将该变量的内容更改为“John K. Jones”？
  - a. strName = strName.Replace(" ", " K. ")
  - b. strName = strName.Insert(5, "K. ")
  - c. strName = strName.Insert(4, " K.")
  - d. 以上所有。

## 练习题

- 1. **试一试** strAmount 变量包含字符串“3,123,560”。编写 Visual Basic 语句，将该变量的内容更改为“3123560”；使用 Replace 方法。现在 strAmount 变量包含字符串“3123560”，编写 Visual Basic 语句，将该变量的内容更改为“$3,123,560”。（试一试练习的答案位于本章末尾。）

- 2. **试一试** 打开 ClearlyVB\Chap24\Zip Solution 文件夹中包含的 Zip Solution (Zip Solution.sln) 文件。打开设计器窗口。Display Shipping Charge 按钮的 Click 事件过程应根据用户输入的 ZIP 代码显示相应的运费。为有效，ZIP 代码必须恰好包含五位数字，且前三位数字必须是“605”或“606”。“605” ZIP 代码的运费为 $25。“606” ZIP 代码的运费为 $30。如果 ZIP 代码无效，则显示相应消息。编写该过程。保存解决方案，然后启动应用程序。使用以下 ZIP 代码测试应用程序：60677、60511、60344 和 7130。停止应用程序，然后关闭解决方案。（试一试练习的答案位于本章末尾。）

- 3. **修改此项目** 在本练习中，你将修改本章中编写的 Phone Numbers 应用程序。使用 Windows 复制 Phone Solution 文件夹。将该副本保存在 ClearlyVB\Chap24 文件夹中。将副本重命名为 Phone Solution-MODIFY THIS。打开 ClearlyVB\Chap24\Phone Solution-MODIFY THIS 文件夹中包含的 Phone Solution (Phone Solution.sln) 文件。打开设计器窗口。btnSave 控件的 Click 事件过程应确定用户是否按所需格式输入了电话号码：三位数字、一个连字符、三位数字、一个连字符和四位数字。如果格式不正确，则显示相应消息。适当地修改该过程。保存解决方案，然后启动应用程序。使用以下电话号码测试应用程序：1-234-567890 和 999-888-1111。停止应用程序，然后关闭解决方案。

- 4. **入门** 打开 ClearlyVB\Chap24\CityState Solution 文件夹中包含的 CityState Solution (CityState Solution.sln) 文件。打开设计器窗口。该界面提供了一个文本框，用于输入城市名称，后跟一个逗号、一个空格和一个州名。Display Message 按钮的 Click 事件过程应显示消息“cityName is located in stateName”，其中 cityName 和 stateName 是用户输入的城市和州的名称。编写该过程。保存解决方案，然后启动并测试应用程序。停止应用程序，然后关闭解决方案。

- 5. **中级** 打开 ClearlyVB\Chap24\Color Solution 文件夹中包含的 Color Solution (Color Solution.sln) 文件。打开设计器窗口。Display Color 按钮的 Click 事件过程应显示用户输入的商品编号所对应商品的颜色。所有商品编号都恰好包含五个字符。所有商品都有四种颜色：蓝色、绿色、红色和白色。商品编号中的第三个字符表示商品颜色，如下所示：B 或 b 表示蓝色，G 或 g 表示绿色，R 或 r 表示红色，W 或 w 表示白色。当商品编号不恰好包含五个字符，或第三个字符不是有效颜色字符之一时，该过程应显示相应消息。保存解决方案，然后启动应用程序。使用 12b45 作为商品编号测试应用程序。该过程应在 lblColor 控件中显示单词“Blue”。使用以下有效商品编号测试应用程序：99G44、abr55 和 78w99。现在使用以下无效商品编号测试应用程序：12x 和 23abc。停止应用程序，然后关闭解决方案。

- 6. **高级** 打开 ClearlyVB\Chap24\Jacobson Solution 文件夹中包含的 Jacobson Solution (Jacobson Solution.sln) 文件。打开设计器窗口。该界面提供了一个用于输入密码的文本框。该文本框的 CharacterCasing 属性设置为 Upper。密码可以包含 5、6 或 7 个字符，但不能包含空格字符。Display New Password 按钮应使用以下三条规则创建并显示新密码。第一，将所有元音（A、E、I、O 和 U）替换为字母 X。第二，将所有数字替换为字母 Z。第三，反转密码中的字符。保存解决方案，然后启动并测试应用程序。停止应用程序，然后关闭解决方案。

- 7. 打开 ClearlyVB\Chap24\FigureThisOut Solution 文件夹中包含的 FigureThisOut Solution (FigureThisOut Solution.sln) 文件。打开代码编辑器窗口并研究现有代码。btnDisplay 控件的 Click 事件过程执行什么任务？启动并测试应用程序。停止应用程序。关闭代码编辑器窗口，然后关闭解决方案。

![](img/cf88270932e011575089da06b940a1d9_571_0.png)


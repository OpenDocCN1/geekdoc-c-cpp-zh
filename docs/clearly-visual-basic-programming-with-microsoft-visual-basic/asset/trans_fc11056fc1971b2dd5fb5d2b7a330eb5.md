
数字 2 到 6 出现在界面中。停止应用程序，然后关闭解决方案。（如果需要重新创建 numbers.txt 文件，请在 IDE 的窗口中打开该文件。如有必要，删除文件内容，然后键入数字 1 到 5，每键入一个数字后按 Enter。）

### 进阶

- 6. 每年 7 月和 8 月，政治意识组织（PAO）向其所在地区的选民发送一份问卷。问卷询问选民的政党（民主党、共和党或无党派）和年龄。根据返回的问卷，该组织的秘书统计该地区民主党人、共和党人和无党派人士的人数。秘书想要一个应用程序，用来将每位受访者的信息（政党和年龄）保存到顺序访问文件中。该应用程序还应计算并显示每个政党的选民人数。创建一个新的 Visual Basic Windows 应用程序。分别将解决方案、项目和窗体文件命名为 PAO Solution、PAO Project 和 frmMain.vb。将应用程序保存在 ClearlyVB\Chap23 文件夹中。如有必要，将窗体名称更改为 frmMain。创建图 23-14 所示的界面。Party 文本框应仅接受 Backspace 键以及字母 D、d、R、r、I 或 i。Age 文本框应仅接受数字和 Backspace 键。为 Write to File 和 Display Totals 按钮编写 Click 事件过程。保存解决方案，然后启动并测试应用程序。停止应用程序，然后关闭解决方案。

![](img/cf88270932e011575089da06b940a1d9_547_0.png)

图 23-14：PAO 应用程序的用户界面

![](img/cf88270932e011575089da06b940a1d9_547_1.png)

- 7. 打开 FigureThisOut Solution（FigureThisOut Solution.sln）文件，该文件位于 ClearlyVB\Chap23\FigureThisOut Solution 文件夹中。打开“代码编辑器”窗口并研究现有代码。为什么 btnWrite 控件的 Click 事件过程中的 true 分支先打开顺序访问文件用于输出，然后关闭文件，再打开它用于追加？启动并测试应用程序。停止应用程序。关闭“代码编辑器”窗口，然后关闭解决方案。

![](img/cf88270932e011575089da06b940a1d9_548_0.png)

- 8. 在本练习中，你要找出应用程序代码中的一个错误。打开 SwatTheBugs Solution（SwatTheBugs Solution.sln）文件，该文件位于 ClearlyVB\Chap23\SwatTheBugs Solution 文件夹中。打开“代码编辑器”窗口并研究现有代码。启动应用程序，然后使用 Sue 和 1000 测试，再使用 Pete 和 5000 测试。单击“调试”，然后单击“停止调试”。打开 bonus.txt 文件。注意该文件为空。关闭 bonus.txt 窗口。定位并更正代码中的任何错误。保存解决方案，然后再次启动并测试应用程序。停止应用程序，然后关闭解决方案。

## “TRY THIS”练习答案

- 1. 图 23-15 显示了 btnSave 和 btnDisplay 控件的 Click 事件过程。

```vb
Private Sub btnSave_Click(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles btnSave.Click
    ' writes a gross pay amount to a sequential access file

    ' declare a StreamWriter variable
    Dim outFile As IO.StreamWriter
    ' open the file for append
    outFile = IO.File.AppendText("gross.txt")
    ' write the amount on a separate line in the file
    outFile.WriteLine(txtGrossPay.Text)
    ' close the file
    outFile.Close()
    ' clear the Gross pay box, then set the focus
    txtGrossPay.Text = String.Empty
    txtGrossPay.Focus()
End Sub

Private Sub btnDisplay_Click(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles btnDisplay.Click
    ' reads gross pay amounts from a sequential access file
    ' and displays them in the interface

    ' declare variables
    Dim inFile As IO.StreamReader
    Dim strGrossPay As String
    Dim decGrossPay As Decimal

    ' clear previous amounts from the Gross pay box
    txtContents.Text = String.Empty

    ' determine whether the file exists
    If IO.File.Exists("gross.txt") = True Then
        ' open the file for input
        inFile = IO.File.OpenText("gross.txt")
        ' process the loop instructions until the end of the file
        Do Until inFile.Peek = -1
            ' read an amount
            strGrossPay = inFile.ReadLine
            ' display the amount
            Decimal.TryParse(strGrossPay, decGrossPay)
            txtContents.Text = txtContents.Text _
                & decGrossPay.ToString("C2") & ControlChars.NewLine
        Loop
        ' close the file
        inFile.Close()
    Else
        MessageBox.Show("Can't find the gross.txt file", _
            "ABC Company", MessageBoxButtons.OK, _
            MessageBoxIcon.Information)
    End If
End Sub
```

**图 23-15**（接上一页）

- 2. 图 23-16 显示了 btnDisplay 控件的 Click 事件过程。

```vb
Private Sub btnDisplay_Click(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles btnDisplay.Click
    ' reads the 5 names from a sequential access file and stores
    ' them in an array, sorts the names and then displays them

    Dim strFriends(4) As String
    Dim inFile As IO.StreamReader
    Dim intSubscript As Integer

    ' clear previous names from the My friends box
    lblFriends.Text = String.Empty

    ' determine whether the file exists
    If IO.File.Exists("names.txt") = True Then
        ' open the file for input
        inFile = IO.File.OpenText("names.txt")
        ' start the subscript at 0
        intSubscript = 0
        ' process the loop instructions until the
        ' end of the file or the array is filled
        Do Until inFile.Peek = -1 _
            OrElse intSubscript = strFriends.Length
            ' read a name and store it in the array
            strFriends(intSubscript) = inFile.ReadLine
            intSubscript = intSubscript + 1
        Loop
        ' close the file
        inFile.Close()

        Array.Sort(strFriends)

        For intSubscript = 0 To strFriends.Length - 1
            lblFriends.Text = lblFriends.Text _
                & strFriends(intSubscript) & ControlChars.NewLine
        Next intSubscript
    Else
        MessageBox.Show("Can't find the names.txt file", _
            "Friends", MessageBoxButtons.OK, _
            MessageBoxIcon.Information)
    End If
End Sub
```

**图 23-16**（接上一页）

## 24 字符串部分

学习第 24 章后，你应该能够：

- 确定字符串中的字符数
- 删除字符串开头和结尾的空格
- 替换字符串中的字符
- 在字符串中插入字符
- 搜索字符串
- 访问字符串中的字符
- 使用模式匹配比较字符串

### 处理字符串

很多时候，应用程序需要以某种方式操作（处理）字符串数据。例如，它可能需要查看库存零件编号中的第一个字符，以确定该零件在仓库中的位置。或者，它可能需要搜索地址以确定街道名称。在本章中，你将学习在 Visual Basic 中操作字符串的几种方法。第一种字符串操作技术向你展示如何确定字符串中的字符数。

### 有多少个字符？

如果应用程序期望用户输入七位电话号码或五位邮政编码，应用程序的代码应验证用户输入的字符数是否符合要求。字符串中包含的字符数存储在字符串的 **Length 属性**中。不出所料，该属性中存储的值是整数。图 24-1 显示了 Length 属性的语法，并包含使用该属性的示例。

**使用 Length 属性**

| 语法 | 用途 |
|---|---|
| *字符串*.Length | 存储字符串中包含的字符数 |

**示例 1**
```vb
strFullName = "Lee Thompson"
intNumChars = strFullName.Length
' assigns the number 12 to the intNumChars variable
```

**示例 2**
```vb
Do
    strPhone = InputBox("7-digit phone number (no dashes)", "Phone")
Loop Until strPhone.Length = 7
' gets a phone number from the user until the phone number contains exactly 7 characters
```

图 24-1：Length 属性的语法和示例

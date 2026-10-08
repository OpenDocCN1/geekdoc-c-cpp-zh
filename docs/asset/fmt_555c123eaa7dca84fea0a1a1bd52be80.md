
```vbsharp
12304   mySeekMo = "0" + mySeekMo
12305   End If
12306   Dim intLenDay As Integer = mySeekDay.Length
12307   If (intLenDay = 1) Then
12308   mySeekDay = "0" + mySeekDay
12309   End If
12310   ///定义要保存的日期
12311   Dim myDateToSave As String = mySeekMo + "/"
12312   + mySeekDay + "/" + mySeekYr
12313   ///定义要保存的字符串
12314   Dim myStringToSave As String = myDateToSave
12315   + " " + txtBoxAddInfo.Text
12316   //定义 StreamReader
12317   Dim mySR As StreamReader = New
12318   StreamReader("C:\Target Files\BlockedDates.txt")
12319   //读取被屏蔽的日期列表
12320   Dim myStrBlockedDate As String = "XX"
12321   //避免从空字符串开始
12322   ///
12323       ListBox.Items.Clear()
12324   While (myStrBlockedDate <> "")
12325       If (myStrBlockedDate <> "") Then
12326           Exit While
12327   End If
12328   myStrBlockedDate = mySR.ReadLine()
12329       // 读取的字符串为空时结束
12330       If (myStrBlockedDate <> "") Then
12331           ListBox.Items.Add(myStrBlockedDate)
12332   End If
12333   End While
12334   Dim intBlockedDateCount As Integer = 
12335   ListBox.Items.Count
12336   ///
12337   Dim intFlagBlocked As Integer = 0
12338   Dim intBlockedLoop As Integer = 0
12339   Dim intBlockedDateFound = 0
12340   For intBlockedLoop = 0 To
12341     intBlockedCount-1
12342       ListBox.SelectedIndex = intBlockedLoop
12343   myStrBlockedDate = 
12344   Convert.ToString(ListBox.SelectedItem)
12345   If (myDateToSave = myStrBlockedDate) Then
12346   intBlockedDateFound += 1
12347   End If
12348   Next
12349   If (intBlockedDateFound = 0) Then
12350   // 如果选择的日期未匹配到
12351   屏蔽的日期，则保存该项
12352   Dim myWrt As StreamWriter = New
12353   StreamWriter("C:\App Target Files\ToDo.txt",
12354   True)
12355      myWrt.WriteLine(myStringToSave)
12356      myWrt.Close()
12357      myWrt.Dispose()
12358   End If
12359   //释放 StreamWriter 和文件
12360   If (intBlockedDateFound >= 1) Then
12361   // 无法保存到屏蔽日期，返回
12362   到用户屏幕
12363   MessageBox.Show("This is a blocked date, Blocked Date vs Save") = ""
12364   txtAddInfo.Text = ""
12365   Return
12366   End If
12367   //重置添加文本框为空
12368   txtAddInfo.Text = ""
12369   ListBox1.Sorted = True
12370   ListBox1.Visible = True
12371   //重新加载 ToDo 项目文件
12372   btnToDoDo.PerformClick()
12373   End Sub // 结束 SaveInfo
12374   //
12375   Private Sub btnBlockedDates_Click(sender As
12376   System.Object, as System.EventArgs) Handles
12377   btnBlockedDates.Click
12378   ListBox1.Visible = True
12379   ListBox1.Items.Clear()
12380   Dim myRdr As StreamReader = New
12381   StreamReader("C:\App Target Files\BlockedDates.txt")
12382   Dim strBlockedDates As String = "XX"
12383   While (strBlockedDates <> "")
12384     strBlockedDates = myRdr.ReadLine()
12385     If (strBlockedDates = "") Then
12386       myRdr.Close()
12387       Return
12388     End If
12389     If (strBlockedDates <> "")
12390       1stBoxBlocked.Items.Add(strBlockedDates)
12391       1stBoxBlocked.Sorted = True
12392       btnHideDates.Visible = True
12393     End If
12394   End Sub // 结束屏蔽日期
12395   //
12396   Private Sub btnHideDates_Click(sender As
12397   System.Object, e as System.EventArgs Handles
12398   btnHideDates.Click
12399   1stBoxBlocked.Items.Clear()
12400   1stBoxBlocked.Visible = False
12401   End Sub
12402   //
12403   Private Sub btnSaveAndRepeat_Click(sender As
12404   System.Object, e as System.EventArgs Handles
12405   btnSaveAndRepeat.Click
12406   Dim myToStrToSave As String =
12407   txtBoxAddInfo.Text
12408   Dim intCheckedRepeat As Integer = 1
12409   If (radRepeatTimes.Checked) Then
12410     intCheckedRepeat = 3
12411   End If
12412   If (rad6Times.Checked) Then
12413     intCheckedRepeat = 6
12414   End If
12415   If (rad9Times.Checked) Then
12416     intCheckedRepeat = 9
12417   End If
12418   If (rad12Times.Checked) Then
12419     intCheckedRepeat = 12
12420   End If
12421   If (radRepeat24Times.Checked) Then
12422     intCheckedRepeat = 24
12423   End If
12424   If (radRepeat36Times.Checked) Then
12425     intCheckedRepeat = 36
12426   End If
12427   //
12428   DatePicker1.CustomFormat = "MM/dd/yyyy"
12429   Dim myToSave As DateTime =
12430   DatePicker1.Value
12431   //测试代码
12432   MessageBox.Show(Convert.ToString(myBaseDate));
12433   //
12434   //保存到文件
12435   //
12436   Dim XX As Integer = 1
12437   //重复保存 ToDo 项目
12438   For XX = 1 To intCheckedRepeat
12439     Dim mySW As StreamWriter = New
12440     StreamWriter("C:\Target Files\ToDo.txt",
12441     True)
12442     //测试代码
12443     MessageBox.Show(Convert.ToString(myBaseDate));
12444     mySeekDay = ""
12445     mySeekMo = ""
12446     mySeekYr = ""
12447     //从 DatePicker 获取日期
12448     intIdxItemFound = 20
12449     //填充选择日期变量
12450     mySeekDay = Convert.ToString(myDateToSave.Day)
12451     mySeekMo = Convert.ToString(myDateToSave.Month)
12452     mySeekYr = Convert.ToString(myDateToSave.Year)
12453     //为个位数月份字符串添加前缀"0"
12454     Dim intLenMo As Integer = mySeekMo.Length
12455     If (intLenMo = 1) Then
12456     mySeekMo = "0" + mySeekMo
12457     End If
12458     Dim intLenDay As Integer = mySeekDay.Length
12459     If (intLenDay = 1) Then
12460     mySeekDay = "0" + mySeekDay
12461     End If
12462   //定义保存的日期字符串
12463   Dim myStringToSave As String = mySeekMo
12464   + "/" + mySeekDay + "/" + mySeekYr
12465   //定义要保存的字符串
12466   myStringToSave = myDateTimeToSave + " " +
12467   txtBoxAddInfo.Text
12468   mySW.WriteLine(myStringToSave)
12469   mySW.Close()
12470   mySW.Dispose()
12471   myDateToSave.Add(1)
12472   If (mySeekMo = 12) Then
12473     myDateToSave.Add(1)
12474   End If
12475   Next
12476   //测试代码
12477   MessageBox.Show(Convert.ToString(myBaseDate));
12478   //
12479   //重置按钮
12480   radRepeatTimes.Checked = False
12481   rad6Times.Checked = False
12482   rad9Times.Checked = False
12483   rad12Times.Checked = False
12484   radRepeat24Times.Checked = False
12485   radRepeat36Times.Checked = False
12486   ListBox1.Clear()
12487   txtAddInfo.Text = ""
12488   End Sub // 结束 SaveInfo
```

# Appendix H... VB 表单属性

```vbsharp
// Form1 代码
Public Class Form1
    Dim intPass As Integer = 11
```

# 简单的编程 C# 和 Visual Basic...

```csharp
12552 Dim intMultiplied As Integer
12553 intMultiplied = myForm.intMyNumber()
12554 MessageBox.Show(Convert.ToString(intMultiplied))
12555 End Sub
12556 //
12557 Private Sub btnExit_Click(sender As
12558 System.Object, e As System.EventArgs) Handles
12559 btnExit.Click
12560 Application.Exit()
12561 End Sub
12562 End Class

12564 // Form2 代码

12566 Public Class Form2
12567 //
12568 Private intToReturn As Integer
12569 --------------------------------------
12570 Public Property intMyNumber() As Integer
12571 Get
12572 Return intToReturn * 2
12573 End Get
12574 //
12575 Set(value As Integer)
12576 intToReturn = value
12577 End Set
12578 End Property
12579 --------------------------------------
12580 //
12581 Private Sub btnShowForm1_Click(sender As
12582 System.Object, e As System.EventArgs) Handles
12583 btnShowForm1.Click
12584 Dim myForm As Form1 = New Form1()
12585 Me.Hide()
12586 myForm.Show()
12587 End Sub
12588 --------------------------------------
12589 //
12590 Private Sub btnMyProperty_Click(sender As
12591 System.Object, e As System.EventArgs) Handles
12592 btnMyProperty.Click
12593 intMyNumber = 88
12593 Dim myIntTemp As Integer = intMyNumber
12594 MessageBox.Show(Convert.ToString(myIntTemp))
12595 End Sub

12596 //

12597 Private Sub Button1_Click(sender As)
12598 System.Object, e As System.EventArgs) Handles
12599 btnExit.Click
12600 Application.Exit()
12601 End Sub
12602 End Class
```

## 附录 I VS VB 类项目

```
Fystudent.calculatemark = Val(sub1.Text)
Fystudent.calculatemark = Val(sub2.Text)
Fystudent.calculatemark = Val(sub3.Text)
Fystudent.calculatemark = Val(sub4.Text)
Totaldisplay.Text = "Total Marks : " & fystudent.calculatemark
Persdisplay.Text = "Percentage : " & fystudent.percentage(fystudent.calculatemark)
Elseif i = 2 Then
Dim systudent As New SYBCA
Systudent.calculatemark = Val(sub1.Text)
Systudent.calculatemark = Val(sub2.Text)
Systudent.calculatemark = Val(sub3.Text)
Systudent.calculatemark = Val(sub4.Text)
Totaldisplay.Text = "Total Marks : " & systudent.calculatemark
Persdisplay.Text = "Percentage : " & systudent.percentage(systudent.calculatemark)
Elseif i = 3 Then
Dim tystudent As New TYBCA
```
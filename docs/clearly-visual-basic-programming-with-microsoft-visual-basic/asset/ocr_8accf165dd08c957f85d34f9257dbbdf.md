+   7. If the Subtraction check box is not selected, it means that the user wants addition. Therefore, the outer selection structure’s false path should add together both integers. Click after the letter **f** in the first End If line, then press **Enter** to insert a blank line. Type **else** and press **Enter**, then type `intAnswer = intNum2 + intNum1`. Figure 10-8 shows the code entered in the procedure.

```
~~~vb
Private Sub btnCalc_Click(ByVal sender As Object, ByVal e As System.EventArgs)
    ' calculates either the sum of or the difference between two numbers

    Dim intNum1 As Integer
    Dim intNum2 As Integer
    Dim intAnswer As Integer

    ' assign numbers to variables
    Integer.TryParse(txtNum1.Text, intNum1)
    Integer.TryParse(txtNum2.Text, intNum2)

    ' calculate and display the difference or sum
    If chkSubtract.Checked = True Then
        If intNum1 > intNum2 Then
            intAnswer = intNum1 - intNum2
        Else
            intAnswer = intNum2 - intNum1
        End If
    Else
        intAnswer = intNum1 + intNum2
    End If
    lblAnswer.Text = intAnswer
End Sub
~~~

插图标注：左侧 **nested selection structure**（嵌套选择结构）；右侧 **outer selection structure**（外层选择结构）。
```

**Figure 10-8:** Code entered in the btnCalc control’s Click event procedure

+   8. Save the solution, then start the application. Type **22** in the Number 1 text box and type **12** in the Number 2 text box, then click the **Calculate** button. The btnCalc control’s Click event procedure adds together both integers and displays the sum (34) in the Answer label.

+   9. Click the **Subtraction** check box, then click the **Calculate** button. The btnCalc control’s Click event procedure subtracts the smaller integer (12) from the larger integer (22), and then displays the difference (10) in the Answer label.

+   10. Change the contents of the Number 1 text box to **5**, then click the **Calculate** button. The btnCalc control’s Click event procedure subtracts the smaller integer (5) from the larger integer (12), and then displays the difference (7) in the Answer label. See Figure 10-9.
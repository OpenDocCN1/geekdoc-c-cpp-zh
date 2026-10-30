```
Private Sub CloseButton_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles CloseButton.Click
    ' Close this form.

    Me.Close()
End Sub

Private Sub HoursTextBox_Validating(ByVal sender As System.Object, _
    ByVal e As System.ComponentModel.CancelEventArgs) _
    Handles HoursTextBox.Validating
    ' Test the hours for numeric.
    Dim HoursDecimal As Decimal

    If Decimal.TryParse(HoursTextBox.Text, HoursDecimal) Then
        ErrorProvider1.Clear()
    Else
        ErrorProvider1.SetError(HoursTextBox, _
            "The hours must be numeric.")
        HoursTextBox.SelectAll()
        e.Cancel = True
    End If
End Sub

Private Sub RateTextBox_Validating(ByVal sender As Object, _
    ByVal e As System.ComponentModel.CancelEventArgs) _
    Handles RateTextBox.Validating
    ' Test pay rate for numeric.
    Dim RateDecimal As Decimal

    If Decimal.TryParse(RateTextBox.Text, RateDecimal) Then
        ErrorProvider1.Clear()
    Else
        ErrorProvider1.SetError(RateTextBox, _
            "The hours must be numeric.")
        RateTextBox.SelectAll()
        e.Cancel = True
    End If
End Sub

Private Sub PayrollForm_FormClosing(ByVal sender As Object, _
    ByVal e As System.Windows.Forms.FormClosingEventArgs) _
    Handles Me.FormClosing
    ' Do not allow validation to cancel the form's closing.

    e.Cancel = False
    ' Release the instance of this form.
    AnInstance = Nothing
End Sub

Private Sub SelectControlInError(ByVal ErrorTextBox As TextBox)
    ' Select the control in error.

    With ErrorTextBox
        .SelectAll()
        .Focus()
    End With
End Sub
End Class
```
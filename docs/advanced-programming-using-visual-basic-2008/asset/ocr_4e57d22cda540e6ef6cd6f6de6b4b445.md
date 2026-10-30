```
If Decimal.TryParse(HoursTextBox.Text, HoursDecimal) Then
    If Decimal.TryParse(RateTextBox.Text, RateDecimal) Then
        ' Both values converted successfully.
        Try
            Dim APayroll As New Payroll(HoursDecimal, RateDecimal)
            PayTextBox.Text = APayroll.Pay.ToString('C')
        Catch Err As ApplicationException
            ' Catch exceptions from the Payroll class.
            Select Case Err.Source
                Case "Hours"
                    ErrorProvider1.SetError(HoursTextBox, _
                        Err.Message)
                    With HoursTextBox
                        .SelectAll()
                        .Focus()
                    End With
                Case "Rate"
                    ErrorProvider1.SetError(RateTextBox, _
                        Err.Message)
                    With RateTextBox
                        .SelectAll()
                        .Focus()
                    End With
            End Select
        End Try
    Else
        ' Rate did not pass validation.
        ErrorProvider1.SetError(RateTextBox, _
            "The rate must be numeric.")
    End If
Else
    ' Hours did not pass validation.
    ErrorProvider1.SetError(HoursTextBox, _
        "The hours must be numeric.")
End If
End Sub

Private Sub ClearButton_Click(ByVal sender As System.Object, _
ByVal e As System.EventArgs) Handles ClearButton.Click
    ' Clear the screen fields.
    ErrorProvider1.Clear()
    With NameTextBox
        .Clear()
        .Focus()
    End With
    HoursTextBox.Clear()
    RateTextBox.Clear()
    PayTextBox.Clear()
End Sub

Private Sub HoursTextBox_Validating(ByVal sender As Object, _
ByVal e As System.ComponentModel.CancelEventArgs) _
Handles HoursTextBox.Validating
    ' Test hours for numeric.
    Dim HoursDecimal As Decimal
```
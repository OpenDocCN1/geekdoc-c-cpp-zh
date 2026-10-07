btnApply Button sends its Click event to the btnApply_Click event handler this routine can assume the user clicked this. In that case you use Relaxed Delegates to omit parameters and make the code a little easier to read.

The EventNameAttributesRelaxed example program uses the Visual basic in the following fragment to handle the values by its red scroll, red textbox, and Apply button. The code works as well as the earlier C# version in Visual Basic and without event handler parameters.

```
' A ScrollBar has been changed. Update the corresponding TextBox.
Private Sub scrRed_Changed()
    If txtRed Is Nothing Then Exit Sub
    txtRed.Text = CInt(scrRed.Value).ToString()
    ShowSample()
End Sub
```

```
' A TextBox has been changed. Update the corresponding ScrollBar.
Private Sub txtRed_Changed()
    ' Keep the value within bounds.
    Dim value As Integer
    Try
        value = CInt(txtRed.Text)
    Catch ex As Exception
        value = 0
    End Try
    If value < 0 Then value = 0
    If value > 255 Then value = 255
    txtRed.Text = value.ToString()
    If scrRed Is Nothing Then Exit Sub
    scrRed.Value = value
    ShowSample()
End Sub
```

```
' Display a sample of the color.
Private Sub ShowSample()
    If borSample Is Nothing Then Exit Sub
```

```
Dim r, g, b As Byte
Try
    r = CByte(txtRed.Text)
Catch ex As Exception
    r = 0
End Try
Try
    g = CByte(txtGreen.Text)
Catch ex As Exception
    g = 0
End Try
Try
```
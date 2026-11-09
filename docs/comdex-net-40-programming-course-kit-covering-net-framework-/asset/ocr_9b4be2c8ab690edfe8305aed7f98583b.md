![](bbox=[0.431, 0.137, 0.592, 0.316])

Fig.VB-2.51

+   9. **Double-click** the **Button** control in the form and add the highlighted code snippet shown in Listing 2.6 to Code Editor:

# Listing 2.6: Using the MsgBox Function

```
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As
    System.EventArgs) Handles Button1.Click
    Dim Result As Integer
    Result = MsgBox("This is a message box!", MsgBoxStyle.OkCancel +
    MsgBoxStyle.Information + MsgBoxStyle.SystemModal, "Message Box")
    If (Result = MsgBoxResult.Ok) Then
        TextBox1.Text = "You have clicked OK"
    End If
End Sub
```

In Listing 2.6, you create a message box and store the result of the selection in an **Integer** variable named, **Result**. If the user clicks the **OK** button at run time, the text **You have clicked OK** is added to the text box present on the form.

+   10. Press the F5 key on the keyboard to run the application. As a result, the output is displayed (Fig.VB-2.52).
+   11. Click the **Show Message Box** button (Fig.VB-2.52). A message box displaying the message, **This is a message box!**, appears (Fig.VB-2.53).
+   12. Click the **OK** button in the message box (Fig.VB-2.53). As a result, the text, **You have clicked OK**, appears in the text box present on the form, as shown in Fig.VB-2.54:

![](bbox=[0.229, 0.632, 0.375, 0.744])

![](bbox=[0.454, 0.684, 0.573, 0.744])

![](bbox=[0.651, 0.633, 0.794, 0.744])

Fig.VB-2.52

Fig.VB-2.53

Fig.VB-2.54

# Using the MessageBox.Show Function

Similar to the MsgBox function, the MessageBox.Show function also allows you to display a message box when you run a Windows Forms application. The syntax of the MessageBox.Show function is as follows:

```
Public Shared Function Show (
    text As String, …
```
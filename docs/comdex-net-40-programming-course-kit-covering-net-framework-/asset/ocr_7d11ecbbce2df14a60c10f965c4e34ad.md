+   1. *Start* Visual Studio 2010.
+   2. *Select* **File**→**New** → **Project** from the menu bar. The **New Project** dialog box opens.
+   3. *Select* **Visual Basic**→**Windows** from the **Installed Templates** section in the left pane of the **New Project** dialog box.
+   4. *Select* the **Windows Forms Application** template in the middle pane to create a Windows Forms application.
+   5. *Enter* the name of the application as **MySaveFileDialog** (also available on the CD) in the **Name** text box and an appropriate location for the application in the **Location** combo box.
+   6. *Click* the **OK** button to close the **New Project** dialog box. The **MySaveFileDialog** application is created (Fig.VB-4.43).
+   7. *Drag and drop* a **Label** control, a **TextBox** control, and a **Button** control on the form from the **Toolbox**.
+   8. *Set* the **Text** properties of the **Label** control and the **Button** control to **Enter text** and **Save Text**, respectively, by using the **Properties** window.
+   9. *Set* the **Multiline** property of the **TextBox** control to **True** by using the **Properties** window and then *resize* the **TextBox** control to accommodate multiple lines of text (Fig.VB-4.43).
+   10. *Drag and drop* a **SaveFileDialog** control on the form from the **Dialogs** tab of the **Toolbox**. The **SaveFileDialog** control is added to the component tray, as shown in Fig.VB-4.43.

![](bbox=[0.335, 0.411, 0.688, 0.617])

11. *Double-click* the **Save Text** button in the form and *add* the highlighted lines of code, as shown in Listing 4.7, to the Code Editor.

# Listing 4.7: Showing the Code for the Button1_Click Event Handler

```
```vb
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As
    System.EventArgs) Handles Button1.Click
    SaveFileDialog1.Filter = "Text files (*.txt)|*.txt"
    SaveFileDialog1.InitialDirectory =
    Environment.SpecialFolder.MyDocuments.ToString()
    If SaveFileDialog1.ShowDialog = DialogResult.OK Then
        If SaveFileDialog1.CheckFileExists = False Then
            System.IO.File.WriteAllText(SaveFileDialog1.FileName,
            TextBox1.Text, System.Text.Encoding.UTF8)
        End If
    End If
    TextBox1.Text = ""
End Sub
```
```
+   1. *Start* Visual Studio 2010.
+   2. *Select* **File**→**New**→**Project** from the menu bar. The **New Project** dialog box opens.
+   3. *Select* **Visual Basic**→**Windows** from the **Installed Templates** section in the left pane of the **New Project** dialog box.
+   4. *Select* the **Windows Forms Application** template in the middle pane to create a Windows Forms application.
+   5. *Enter* the name of the application as **MyOpenFileDialog** (also available on the CD) in the **Name** text box and an appropriate location for the application in the **Location** combo box.
+   6. *Click* the **OK** button to close the **New Project** dialog box. The **MyOpenFileDialog** application is created (Fig.VB-4.39).
+   7. *Drag and drop* a **Label** control, a **PictureBox** control, and a **Button** control on the form from the **Toolbox** and set the **Text** properties of the **Label** control and the **Button** control to **Image file:** and **Open Image**, respectively.
+   8. *Drag and drop* an **OpenFileDialog** control on the form from the **Dialogs** tab of the **Toolbox**. The **OpenFileDialog** control is added to the component tray, as shown in Fig.VB-4.39.

![](bbox=[0.338, 0.363, 0.686, 0.574])

Fig.VB-4.39

+   9. *Double-click* the **Open Image** button in the form and *add* the highlighted lines of code, as shown in Listing 4.6, to the Code Editor:

# **Listing 4.6:** Showing the Code for the **Button1_Click Event Handler**

```
```vb
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As
    System.EventArgs) Handles Button1.Click
    If Not (OpenFileDialog1.ShowDialog() = DialogResult.Cancel) Then
        PictureBox1.Image = Image.FromFile(OpenFileDialog1.FileName)
    End If
    Label1.Text = "" & OpenFileDialog1.SafeFileName
End Sub
```
```

Listing 4.6 shows the code for the event handler of the Click event of the Button control. When the Open Image button is clicked at runtime, the Open dialog box appears which prompts you to select a file. In the If statement, we have called the ShowDialog method of the OpenFileDialog control to display the Open dialog box and checked whether this method returns a value other than Cancel. The file that you select in the Open dialog box is displayed in the picture box if you click any button other than the Cancel button in the Open dialog box. In addition, the name of the file you select appears in the label.

+   10. *Press* the F5 key on the keyboard to run the application. The output of the application appears (Fig.VB-4.40).
+   11. *Click* the **Open Image** button on the form to display the **Open** dialog box, as shown in Fig.VB-4.40:
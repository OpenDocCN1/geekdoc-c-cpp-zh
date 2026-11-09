Table 3.22 lists the important methods of the ProgressBar class:

**Table 3.22: Noteworthy Methods of the ProgressBar Class**

| Method | Description |
|---|---|
| Increment | Increments the current position of the ProgressBar control by the specified amount, which is an integer value |
| PerformStep | Increments the current position of the ProgressBar control by the amount specified in the Step property |

Perform the following steps to use the ProgressBar control in a Windows Forms application:

+   1. *Start* Visual Studio 2010.
+   2. *Select* File→New→Project from the menu bar. The New Project dialog box opens.
+   3. *Select* Visual Basic→Windows from the Installed Templates section in the left pane of the New Project dialog box.
+   4. *Select* the Windows Forms Application template in the middle pane to create a new Windows Forms application.
+   5. *Enter* the name of the application as ProgressBarControl (also available on the CD) in the Name text box and an appropriate location for the application in the Location combo box.
+   6. *Click* the OK button to close the New Project dialog box. The ProgressBarControl application is created (Fig.VB-3.47).
+   7. *Drag and drop* one PictureBox control, one Button control, one ProgressBar control, and one Timer control on the form from the Toolbox.
+   8. *Set* the Text property of the Button control to Add Image by using the Properties window, as shown in Fig.VB-3.47:

![](bbox=[0.334, 0.494, 0.689, 0.703])

+   9. *Double-click* the Button control in the form and *add* the following highlighted line of code to the Code Editor:

```
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click
    Timer1.Enabled = True
End Sub
```

The highlighted line of code in the preceding code snippet enables the Timer control when the user clicks the Button control, Button1, at runtime.

+   10. *Double-click* the Timer control in the component tray and *add* the following highlighted code snippet to the Code Editor:
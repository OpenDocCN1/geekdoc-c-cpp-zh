+   2. Select **File**→**New**→**Project** from the menu bar. The **New Project** dialog box opens.
+   3. Select **Visual Basic**→**Windows** from the **Installed Templates** section in the left pane of the **New Project** dialog box.
+   4. Select the **Windows Forms Application** template in the middle pane to create a Windows Forms application.
+   5. Enter the name of the application as **MyFontDialog** (also available on the CD) in the **Name** text box and an appropriate location for the application in the **Location** combo box.
+   6. Click the **OK** button to close the **New Project** dialog box. The **MyFontDialog** application is created (Fig.VB-4.47).
+   7. Drag and drop a **Label** control, a **TextBox** control, and a **Button** control on the form from the **Toolbox** and set the **Text** properties of the **Label** control and the **Button** control to **Enter text:** and **Change Font**, respectively, by using the **Properties** window.
+   8. Drag and drop a **FontDialog** control on the form from the **Dialogs** tab of the **Toolbox**. The **FontDialog** control is added to the component tray, as shown in Fig.VB-4.47:

![](bbox=[0.335, 0.349, 0.687, 0.556])

Fig.VB-4.47

+   9. *Double-click* the **Change Font** button in the form and add the highlighted lines of code, as shown in Listing 4.8, to the **Code Editor**:

# **Listing 4.8:** Showing the Code for the Button1_Click Event Handler

```
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click
    FontDialog1.FontMustExist = True
    FontDialog1.ShowColor = True
    FontDialog1.ShowHelp = True
    If FontDialog1.ShowDialog = DialogResult.OK Then
        TextBox1.Font = FontDialog1.Font
        TextBox1.ForeColor = FontDialog1.Color
    End If
End Sub
```

Listing 4.8 shows the code for the event handler of the **Click** event of the **Button** control. In the highlighted lines, we have first set the **FontMustExist**, **ShowColor**, and **ShowHelp** properties of the **FontDialog** control to **True**. This implies that the Font dialog box will display options to select font and font color, along with a **Help** button. In addition, if you specify a font that does not exist, an error message appears. When you click the **OK** button in the **Font** dialog box, then the font and the color selected in the **Font** dialog box are applied to the text in the text box on the form.

+   10. Press the **F5** key on the keyboard to run the application. The output of the application appears (Fig.VB-4.48).
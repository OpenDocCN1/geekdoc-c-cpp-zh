**Table 3.17: Noteworthy Properties of the PictureBox Class**

| Property | Description |
|---|---|
| SizeMode | Specifies the mode of display of the image in the PictureBox control, such as Normal, StretchImage, and CenterImage |
| WaitOnLoad | Obtains or sets a value indicating whether the image is loaded synchronously |

Table 3.18 lists the important methods of the PictureBox class:

**Table 3.18: Noteworthy Methods of the PictureBox Class**

| Method | Description |
|---|---|
| CancelAsync | Cancels the asynchronous loading of an image |
| Load | Displays an image in the PictureBox control |
| LoadAsync | Loads an image asynchronously |

Perform the following steps to use the **PictureBox** control in a Windows Forms application:

+   1. *Start* Visual Studio 2010.
+   2. *Select* **File→New Project** from the menu bar. The **New Project** dialog box opens.
+   3. *Select* **Visual Basic→Windows** from the **Installed Templates** section in the left pane of the **New Project** dialog box.
+   4. *Select* the **Windows Forms Application** template in the middle pane to create a Windows Forms application.
+   5. *Enter* the name of the application as **PictureBoxControl** (also available on the CD) in the **Name** text box and an appropriate location for the application in the **Location** combo box.
+   6. *Click* the **OK** button to close the **New Project** dialog box. The **PictureBoxControl** application is created (Fig.VB-3.39).
+   7. *Drag* and drop a **PictureBox** control on the form from the **Toolbox**.
+   8. *Select* the **PictureBox** control in the form, *select* the **Image** property of the **PictureBox** control in the **Properties** window, and click the ellipsis button (...) in front of the **Image** property, to add an image to the **PictureBox** control, as shown in Fig.VB-3.39.

![](bbox=[0.354, 0.597, 0.669, 0.78])

Fig.VB-3.39

The **Select Resource** dialog box opens (Fig.VB-3.40).

+   9. *Click* the **Import** button, as shown in Fig.VB-3.40:
+      The **Open** dialog box appears (Fig.VB-3.41).
+   10. *Browse* and select the image that you want to add to the **PictureBox** control (Fig.VB-3.41).
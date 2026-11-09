Visual Basic 2010 provides you controls that contain functionality for the built-in dialog boxes available for Windows Forms applications. You can add these controls in a Windows Forms application to allow the users of the application to work with the built-in dialog boxes. These controls are available in the **Dialogs** and **Printing** tabs of the **Toolbox**. Some commonly used dialog box controls are given as follows:

+   - The FolderBrowserDialog control
+   - The OpenFileDialog control
+   - The SaveFileDialog control
+   - The FontDialog control
+   - The ColorDialog control
+   - The PrintDialog and PrintDocument controls

Let’s now discuss each of these controls, one by one.

# Using the FolderBrowserDialog Control

The **FolderBrowserDialog** control allows users to work with the **Browse For Folder** dialog box where they can browse through folders, create new folders, and select folders to view the containing files. It displays the available physical drives (such as C: and D:) and the folders on those drives in a hierarchical tree structure. The **FolderBrowserDialog** class, which is placed inside the **System.Windows.Forms** namespace, provides the functionality for the **FolderBrowserDialog** control. Table 4.13 lists the noteworthy properties of the FolderBrowserDialog class:

**Table 4.13: Noteworthy Properties of the FolderBrowserDialog Class**

| Property | Description |
|---|---|
| Description | Returns or sets the descriptive text displayed just above the hierarchical tree in the **Browse For Folder** dialog box. |
| RootFolder | Returns or sets the root folder from where the browsing starts. By default, the desktop is selected as the root location for browsing. |
| SelectedPath | Returns or sets the path of the folder selected by a user. |
| ShowNewFolderButton | Returns or sets a value that indicates whether the **Browse For Folder** dialog box allows users to create new folders. |

Perform the following steps to use the FolderBrowserDialog control in a Windows Forms application:

+   1. *Start* Visual Studio 2010.
+   2. *Select* **File→New→Project** from the menu bar. The **New Project** dialog box opens.
+   3. *Select* Visual Basic→Windows from the **Installed Templates** section in the left pane of the **New Project** dialog box.
+   4. *Select* the Windows Forms Application template in the middle pane to create a Windows Forms application.
+   5. *Enter* the name of the application as **MyFolderBrowserDialog** (also available on the CD) in the **Name** text box and an appropriate location for the application in the **Location** combo box.
+   6. *Click* the **OK** button to close the **New Project** dialog box. The **MyFolderBrowserDialog** application is created (Fig.VB-4.34).
+   7. *Drag and drop* a **Label** control, a **TextBox** control, and a **Button** control on the form from the **Toolbox** and set the **Text** properties of the Label control and the Button control to **Select a folder:** and **Browse...**, respectively, by using the **Properties** window.
+   8. *Drag and drop* a **FolderBrowserDialog** control on the form from the Dialogs tab of the **Toolbox**. The FolderBrowserDialog control is added to the component tray, as shown in Fig.VB-4.34:
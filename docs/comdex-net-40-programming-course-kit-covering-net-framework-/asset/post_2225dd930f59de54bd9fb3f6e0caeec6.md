
![](img/9862a98a1a2d3bb14334137965a1ec60_162_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_162_1.png)

Fig.VB-4.31 shows the **StatusStrip1** control in the form after adding items to it:

![](img/9862a98a1a2d3bb14334137965a1ec60_162_2.png)

- 26. *Double-click* the **TextBox** control in the form and add the highlighted lines of code, as shown in Listing 4.3, to the Code Editor:

### Listing 4.3: Showing the Code for the TextBox1_TextChanged Event Handler

```
Private Sub TextBox1_TextChanged(ByVal sender As System.Object, ByVal e As
    System.EventArgs) Handles TextBox1.TextChanged
        Dim str() As String = TextBox1.Text.Split(" "c, ControlChars.NewLine)
        ToolStripStatusLabel1.Text = ("Words: " & str.Length & ", " &
        "Characters (with spaces): " & TextBox1.TextLength)
    End Sub
```

Listing 4.3 shows the code for the event handler of the TextChanged event of the TextBox control. This event handler executes when text is entered or changed in the text box at runtime. In the highlighted lines, we have declared an array of String type, named str, which stores words that are delimited by a whitespace or new line from the text entered in the text box. The number of words (number of elements in the str array) and number of characters entered in the text box are displayed in the ToolStripStatusLabel control.

- 27. *Double-click* the **StatusStrip** control in the form and add the highlighted line of code, as shown in Listing 4.4, to the Code Editor:

### Listing 4.4: Showing the Code to Handle the ItemClicked Event of the StatusStrip Control

```
Private Sub StatusStrip1_ItemClicked(ByVal sender As System.Object, ByVal e As
System.Windows.Forms.ToolStripItemClickedEventArgs) Handles StatusStrip1.ItemClicked
    MessageBox.Show("Item clicked: " & e.ClickedItem.Name)
End Sub
```

Listing 4.4 shows the event handler for the **ItemClicked** event of the **StatusStrip** control. This event handler executes when an item of the **StatusStrip** control is clicked at runtime. The name of the item that was clicked is displayed in a message box.

- 28. Press the **F5** key on the keyboard to run the application. The output of the application appears (Fig.VB-4.32).
- 29. Enter some text in the text box, **Enter text**. The **ToolStripStatusLabel** control of the **StatusStrip** control displays the number of words and characters entered in the text box. (Fig.VB-4.32).
- 30. Click the **ToolStripDropDownButton** control, **Alignment** (Fig.VB-4.32). A drop-down menu displaying two menu items appears along with a message box displaying the **StatusStrip** item that you have clicked (Fig.VB-4.33).
- 31. Click the **OK** button to close the message box. (Fig.VB-4.33).

![](img/9862a98a1a2d3bb14334137965a1ec60_163_0.png)

You have learned about the **StatusStrip** control. In the next section, you learn how to work with dialog boxes in Visual Basic 2010.

## Working with Dialog Boxes

Visual Basic 2010 provides you several built-in dialog boxes to be used in Windows Forms applications. These built-in dialog boxes provide a UI that facilitates interaction between an application and its users to help users to perform a number of tasks, such as changing the font of text entered in a text box, opening a file, saving the changes made in a file, and printing a file. The UI of these built-in dialog boxes consists of controls that contain functionality required to perform a specific task.

The dialog boxes available for the Windows Forms applications are represented through some classes, for example, the **Font** dialog box is represented through the **FontDialog** class. All the classes that represent these dialog boxes inherit the **System.Windows.Forms.CommonDialog** class. This class contains the **ShowDialog** method that displays a dialog box and returns the result of the dialog box. The result returned is a member of the **System.Windows.Forms.DialogResult** enumeration and it corresponds to the button that is clicked by the user in the dialog box. The members of the **DialogResult** enumeration are listed in Table 4.12:

**Table 4.12: Members of the DialogResult Enumeration**

| Member | Description |
|---|---|
| OK | Corresponds to the **OK** button on the dialog box |
| Cancel | Corresponds to the **Cancel** button on the dialog box |
| Yes | Corresponds to the **Yes** button on the dialog box |
| No | Corresponds to the **No** button on the dialog box |
| Abort | Corresponds to the **Abort** button on the dialog box |
| Retry | Corresponds to the **Retry** button on the dialog box |
| Ignore | Corresponds to the **Ignore** button on the dialog box |
| None | Returns nothing and implies that the dialog box remains visible unless closed explicitly |

Visual Basic 2010 provides you controls that contain functionality for the built-in dialog boxes available for Windows Forms applications. You can add these controls in a Windows Forms application to allow the users of the application to work with the built-in dialog boxes. These controls are available in the **Dialogs** and **Printing** tabs of the **Toolbox**. Some commonly used dialog box controls are given as follows:

- The FolderBrowserDialog control
- The OpenFileDialog control
- The SaveFileDialog control
- The FontDialog control
- The ColorDialog control
- The PrintDialog and PrintDocument controls

Let’s now discuss each of these controls, one by one.

### Using the FolderBrowserDialog Control

The **FolderBrowserDialog** control allows users to work with the **Browse For Folder** dialog box where they can browse through folders, create new folders, and select folders to view the containing files. It displays the available physical drives (such as C: and D:) and the folders on those drives in a hierarchical tree structure. The **FolderBrowserDialog** class, which is placed inside the **System.Windows.Forms** namespace, provides the functionality for the **FolderBrowserDialog** control. Table 4.13 lists the noteworthy properties of the FolderBrowserDialog class:

**Table 4.13: Noteworthy Properties of the FolderBrowserDialog Class**

| Property | Description |
|---|---|
| Description | Returns or sets the descriptive text displayed just above the hierarchical tree in the **Browse For Folder** dialog box. |
| RootFolder | Returns or sets the root folder from where the browsing starts. By default, the desktop is selected as the root location for browsing. |
| SelectedPath | Returns or sets the path of the folder selected by a user. |
| ShowNewFolderButton | Returns or sets a value that indicates whether the **Browse For Folder** dialog box allows users to create new folders. |

Perform the following steps to use the FolderBrowserDialog control in a Windows Forms application:

- 1. *Start* Visual Studio 2010.
- 2. *Select* **File→New→Project** from the menu bar. The **New Project** dialog box opens.
- 3. *Select* Visual Basic→Windows from the **Installed Templates** section in the left pane of the **New Project** dialog box.
- 4. *Select* the Windows Forms Application template in the middle pane to create a Windows Forms application.
- 5. *Enter* the name of the application as **MyFolderBrowserDialog** (also available on the CD) in the **Name** text box and an appropriate location for the application in the **Location** combo box.
- 6. *Click* the **OK** button to close the **New Project** dialog box. The **MyFolderBrowserDialog** application is created (Fig.VB-4.34).
- 7. *Drag and drop* a **Label** control, a **TextBox** control, and a **Button** control on the form from the **Toolbox** and set the **Text** properties of the Label control and the Button control to **Select a folder:** and **Browse...**, respectively, by using the **Properties** window.
- 8. *Drag and drop* a **FolderBrowserDialog** control on the form from the Dialogs tab of the **Toolbox**. The FolderBrowserDialog control is added to the component tray, as shown in Fig.VB-4.34:

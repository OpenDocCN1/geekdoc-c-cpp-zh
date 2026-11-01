
![](img/d7d2ffa0a76feaab821930e95daace93_837_0.png)

## FIGURE 29-2

![](img/d7d2ffa0a76feaab821930e95daace93_837_1.png)

## FIGURE 29-3

Note that if you want to, you can also display the creation time, last access time, and last modification time for folders using the DirectoryInfo property. You display these properties only for a selected file to keep things simple.

```csharp
{
    throw new FileNotFoundException(\"File not found: \" + fileFullName);
}
textBoxFileName.Text = theFile.Name;
textBoxCreationTime.Text = theFile.CreationTime.ToLongTimeString();
textBoxLastAccessTime.Text = theFile.LastAccessTime.ToLongDateString();
textBoxLastWriteTime.Text = theFile.LastWriteTime.ToLongDateString();
textBoxFileSize.Text = theFile.Length.ToString() + \" bytes\";
}
```

code download FileProperties.sln

Note that you take the precaution of throwing an exception if there are any problems locating a file at the specified location. The exception itself will be handled in the calling routine (one of the event handlers). Finally, you define a method, DisplayFolderList(), which displays the contents of a given folder in the two list boxes. The full pathname of the folder is passed in as a parameter to this method:

```csharp
protected void DisplayFolderList(string folderFullName)
{
    DirectoryInfo theFolder = new DirectoryInfo(folderFullName);

    if (!theFolder.Exists)
    {
        throw new DirectoryNotFoundException(\"Folder not found: \" + folderFullName);
    }

    ClearAllFields();
    textBoxFolder.Text = theFolder.FullName;
    currentFolderPath = theFolder.FullName;

    // list all subfolders in folder
    foreach(DirectoryInfo nextFolder in theFolder.GetDirectories())
        listBoxFolders.Items.Add(nextFolder.Name);

    // list all files in folder
    foreach(FileInfo nextFile in theFolder.GetFiles())
        listBoxFiles.Items.Add(nextFile.Name);
}
```

code download FileProperties.sln

Next, you examine the event handlers. The event handler that manages the event that is triggered when the user clicks the Display button is the most complex because it needs to handle three different possibilities for the text the user enters in the text box. For instance, it could be the pathname of a folder, the pathname of a file, or neither of these:

```csharp
protected void OnDisplayButtonClick(object sender, EventArgs e)
{
    try
    {
        string folderPath = textBoxInput.Text;
        DirectoryInfo theFolder = new DirectoryInfo(folderPath);

        if (theFolder.Exists)
        {
            DisplayFolderList(theFolder.FullName);
            return;
        }

        FileInfo theFile = new FileInfo(folderPath);
if (theFile.Exists)
{
    DisplayFolderList(theFile.Directory.FullName);
    int index = listBoxFiles.Items.IndexOf(theFile.Name);
    listBoxFiles.SetSelected(index, true);
    return;
}

throw new FileNotFoundException("There is no file or folder with "
    + "this name: " + textBoxInput.Text);
}
catch(Exception ex)
{
    MessageBox.Show(ex.Message);
}
}
```

In this code, you establish if the supplied text represents a folder or file by instantiating DirectoryInfo and FileInfo instances and examining the Exists property of each object. If neither exists, you throw an exception. If it's a folder, you call DisplayFolderList() to populate the list boxes. If it's a file, you need to populate the list boxes and sort out the text boxes that display the file properties. You handle this case by first populating the list boxes. You then programmatically select the appropriate filename in the Files list box. This has exactly the same effect as if the user had selected that item — it raises the item-selected event. You can then simply exit the current event handler, knowing that the selected item event handler will immediately be called to display the file properties.

The following code is the event handler that is called when an item in the Files list box is selected, either by the user or, as indicated previously, programmatically. It simply constructs the full pathname of the selected file, and passes it to the DisplayFileInfo() method presented earlier:

```csharp
protected void OnListBoxFilesSelected(object sender, EventArgs e)
{
    try
    {
        string selectedString = listBoxFiles.SelectedItem.ToString();
        string fullFileName = Path.Combine(currentFolderPath, selectedString);
        DisplayFileInfo(fullFileName);
    }
    catch(Exception ex)
    {
        MessageBox.Show(ex.Message);
    }
}
```

The event handler for the selection of a folder in the Folders list box is implemented in a very similar way, except that in this case you call DisplayFolderList() to update the contents of the list boxes:

```csharp
protected void OnListBoxFoldersSelected(object sender, EventArgs e)
{
    try
    {
        string selectedString = listBoxFolders.SelectedItem.ToString();
        string fullPathName = Path.Combine(currentFolderPath, selectedString);
        DisplayFolderList(fullPathName);
    }
    catch(Exception ex)
{
    MessageBox.Show(ex.Message);
}
}
```

Finally, when the Up button is clicked, DisplayFolderList() must also be called, except that this time you need to obtain the path of the parent of the folder currently being displayed. This is done with the FileInfo.DirectoryName property, which returns the parent folder path:

```csharp
protected void OnUpButtonClick(object sender, EventArgs e)
{
    try
    {
        string folderPath = new FileInfo(currentFolderPath).DirectoryName;
        DisplayFolderList(folderPath);
    }
    catch(Exception ex)
    {
        MessageBox.Show(ex.Message);
    }
}
```

*code download FileProperties.sln*

## MOVING, COPYING, AND DELETING FILES

As mentioned, moving and deleting files or folders is done by the MoveTo() and Delete() methods of the FileInfo and DirectoryInfo classes. The equivalent methods on the File and Directory classes are Move() and Delete(). The FileInfo and File classes also implement the methods CopyTo() and Copy(), respectively. However, no methods exist to copy complete folders — you need to do that by copying each file in the folder.

Using all these methods is quite intuitive — you can find detailed descriptions in the SDK documentation. This section illustrates their use for the particular cases of calling the static Move(), Copy(), and Delete() methods on the File class. To do this, you will build on the previous FileProperties example and call its iteration FilePropertiesAndMovement. This example will have the extra feature that whenever the properties of a file are displayed, the application gives you the option of deleting that file or moving or copying the file to another location.

![](img/d7d2ffa0a76feaab821930e95daace93_841_0.png)

### FilePropertiesAndMovement Sample

Figure 29-4 shows the user interface of the new sample application.

As you can see, FilePropertiesAndMovement is similar in appearance to FileProperties, except for the group of three buttons and a text box at the bottom of the window. These controls are

FIGURE 29-4

enabled only when the example is actually displaying the properties of a file; at all other times, they are disabled. The existing controls are also squashed up a bit to stop the main form from getting too big. When the properties of a selected file are displayed, FilePropertiesAndMovement automatically places the full pathname of that file in the bottom text box for the user to edit. Users can then click any of the buttons to perform the appropriate operation. When they do, a message box is displayed that confirms the action taken by the user (see Figure 29-5).

When the user clicks the Yes button, the action is initiated. There are some actions in the form that the user can take that will then cause the display to be incorrect. For instance, if the user moves or deletes a file, you obviously cannot continue to display the contents of that file in the same location. In addition, if you change the name of a file in the same folder, your display will also be out of date. In these cases, FilePropertiesAndMovement resets its controls to display only the folder where the file resides after the file operation.

### Looking at the Code for FilePropertiesAndMovement

To code this process, you need to add the relevant controls, as well as their event handlers, to the code for the FileProperties sample. The new controls are given the names buttonDelete, buttonCopyTo, buttonMoveTo, and textBoxNewPath.

First, look at the event handler that is called when the user clicks the Delete button:

```csharp
protected void OnDeleteButtonClick(object sender, EventArgs e)
{
    try
    {
        string filePath = Path.Combine(currentFolderPath,
            textBoxFileName.Text);
        string query = "Really delete the file\n" + filePath + "?\n";
        if (MessageBox.Show(query,
            "Delete File?", MessageBoxButtons.YesNo) == DialogResult.Yes)
        {
            File.Delete(filePath);
            DisplayFolderList(currentFolderPath);
        }
    }
    catch(Exception ex)
    {
        MessageBox.Show("Unable to delete file. The following exception"
            + " occurred:\n" + ex.Message, "Failed");
    }
}
```

code download FilePropertiesAndMovement.sln

The code for this method is contained in a try block because of the obvious risk of an exception being thrown if, for example, you don't have permission to delete the file, or the file is moved by another process after it has been displayed but before the user presses the Delete button. You construct the path of the file to be deleted from the CurrentParentPath field, which contains the path of the parent folder, and the text in the textBoxFileName text box, which contains the name of the file.

The methods to move and copy the file are structured in a very similar manner:

```csharp
protected void OnMoveButtonClick(object sender, EventArgs e)
{
    try
    {
        string filePath = Path.Combine(currentFolderPath,
            textBoxFileName.Text);
        ...
    }
}
```

![](img/d7d2ffa0a76feaab821930e95daace93_842_0.png)

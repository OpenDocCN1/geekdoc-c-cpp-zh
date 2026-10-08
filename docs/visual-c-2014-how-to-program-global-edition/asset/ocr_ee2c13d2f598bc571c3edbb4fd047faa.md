# 15.10 ListView Control 677

```
// add icon images to ImageList
fileFolderImageList.Images.Add(Properties.Resources.folder);
fileFolderImageList.Images.Add(Properties.Resources.file);

// load current directory into browserListView
LoadFilesInDirectory(currentDirectory);
displayLabel1.Text = currentDirectory;
```

a) GUI showing app's default folder

![](bbox=[0.335, 0.283, 0.79, 0.415])

b) GUI showing the contents of c:\Users directory

![](bbox=[0.335, 0.458, 0.79, 0.592])

c) Dialog that appears if you try to access a directory for which you do not have permission

![](bbox=[0.335, 0.643, 0.69, 0.728])

Fig-15.31 | Displaying directories and their contents in a ListView. (Part 4 of 4)

# Method ListViewTestForm_Load

Method ListViewTestForm_Load (lines 113–122) handles the Form's Load event. When the app loads, folder and file icons are added to the Images collection of Folder-ImageList (lines 116–117). Since the ListView SmallImageList property is set to this ImageList, the ListView can display these icons for each item. Because the folder icon added, has array index 0, and the file icon has index 1. The app also loads its home directory (obtained at line 14) into the ListView when it first loads (line 120) and displays the directory path (line 121).
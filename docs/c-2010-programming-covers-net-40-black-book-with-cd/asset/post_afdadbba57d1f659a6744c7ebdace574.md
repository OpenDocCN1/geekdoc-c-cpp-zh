
![](img/e073a4882197be4ab61103cbe0bcb394_1437_0.png)

## Figure 29.8: Showing the List of System Drives

4. Select the desired drive from the Select Drive list box. All the directories contained in the selected drive appear in the Select Directory list box, as shown in Figure 29.9:

![](img/e073a4882197be4ab61103cbe0bcb394_1437_1.png)

## Figure 29.9: Showing Directories of the Selected Drive

So far, you have learned how to display the list of directories for the specified drive in the list box. Now, let's learn how to get the list of subdirectories under a specific directory.

## Getting the List of Subdirectories

As discussed, subdirectories are the directories within a directory. They further consist of files that arrange the data in a proper and organized format. Perform the following steps to retrieve and display subdirectories:

- 1. Add another ListBox control and a Label control on the Form1 form of the DirectoriesExample application, and change the Text property of the Label control to Select Subdirectory, as shown in Figure 29.10:

![](img/e073a4882197be4ab61103cbe0bcb394_1437_2.png)

## Figure 29.10: Adding the ListBox Control to the DirectoriesExample Application

- 2. Generate the SelectedIndexChanged event of the listbox2 control by double-clicking it and add the code, shown in Listing 29.5, to this event:

## Listing 29.5: Showing the Code for the SelectedIndexChanged Event of the listBox2 Control

```
private void listBox2_SelectedIndexChanged(object sender, EventArgs e)
{
    DirectoryInfo dir = new DirectoryInfo(listBox2.SelectedItem.ToString());
    DirectoryInfo[] dirs = dir.GetDirectories();
    listBox3.Items.Clear();
    foreach (DirectoryInfo di in dirs)
    {
        listBox3.Items.Add(di.FullName);
    }
    return;
}
```

3. Press the F5 key to run the application.

4. Select the desired drive and directory from the Select Drive and Select Directory list boxes, respectively. All the subdirectories of that particular directory appear in the Select Subdirectory list box, as shown in Figure 29.11:

![](img/e073a4882197be4ab61103cbe0bcb394_1438_0.png)

Now, let's learn how to list files of a specific subdirectory.

## Getting the List of Files in Subdirectories

As discussed, subdirectories consist of files that contain information and data. Let's perform the following steps to list files of a subdirectory:

- 1. Add one more ListBox control and eight more Label controls to the Form form of the DirectoriesExample application and change the Text property of the four Label controls to Files in:, Total files in directory:, Directory created on:, and Directory last accessed on:, respectively, as shown in Figure 29.12:

![](img/e073a4882197be4ab61103cbe0bcb394_1438_1.png)

## Chapter 29: File Handling in C# 2010

- 2. Add the code, shown in Listing 29.6, to the SelectedIndexChanged event of the listbox3 control:

```
private void listBox3_SelectedIndexChanged(object sender, EventArgs e) {
    DirectoryInfo root = new DirectoryInfo(listBox3.SelectedItem.ToString());
    FileInfo[] files = root.GetFiles();
    label10.Text = root.CreationTime.ToString();
    label11.Text = root.LastAccessTime.ToString();
    listBox4.Items.Clear();
    int filecounter = 0;
    foreach (FileInfo file in files) {
        listBox4.Items.Add(file.Name);
        filecounter = filecounter + 1;
    }
    label19.Text = filecounter.ToString();
    label18.Text = listBox3.SelectedItem.ToString();
}
```

- 3. Press the F5 key to run the application.

- 4. Select the desired subdirectory from the Select Subdirectory list box. The files within the selected subdirectory appear in the listbox4 control (the Files in: list box), as shown in Figure 29.13:

![](img/e073a4882197be4ab61103cbe0bcb394_1439_0.png)

Now, let’s discuss about creating, renaming, and deleting a directory

## Creating, Renaming, and Deleting a Directory

In .NET, you can manage directories with the help of the DirectoryInfo class of the System.IO namespace. Let’s perform the following steps to create, rename, and delete a directory:

- 1. Create a Windows application, named DirectoryOperations (also available on the CD-ROM).
- 2. Add three Button controls, nine Label controls, one Tab control, two TextBox controls, and four ListBox controls on the Form1.cs form of the DirectoryOperations application.
- 3. Change the Text property of the Label controls to Select Drive, Directories in, Selected Drive, Type Name, Select a Drive, Select a Directory to Rename, New Name, Select Drive, and Select a Directory to Delete, respectively.
- 4. Change the Text property of the Button controls to Create Directory, Rename Directory, and Delete Directory, respectively.
- 5. Arrange all the controls on the Form1.cs form, as shown in Figure 29.14:

![](img/e073a4882197be4ab61103cbe0bcb394_1440_0.png)

## Figure 29.14: Showing the Design View of the DirectoryOperations Application

6. Open the Form1.cs file of the DirectoryOperations application and replace the existing code with the code shown in Listing 29.7:

## Listing 29.7: Showing the Code for Form1.cs of the DirectoryOperations Application

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
using System.IO;
namespace DirectoryOperations
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        public void GetDriveList()
        {
            DriveInfo[] allDrives = DriveInfo.GetDrives();
            listBox1.Items.Clear();
            foreach (DriveInfo d in allDrives)
            {
                listBox1.Items.Add(d.Name);
                listBox4.Items.Add(d.Name);
                listBox6.Items.Add(d.Name);
```

```
public void GetRootDirList()
{
    DirectoryInfo dir = new DirectoryInfo(listBox1.SelectedItem.ToString());
    DirectoryInfo[] dirs = dir.GetDirectories("*", SearchOption.TopDirectoryOnly);
    listBox2.Items.Clear();
    foreach (DirectoryInfo di in dirs)
    {
        listBox2.Items.Add(di.FullName);
    }
    return;
}

public void GetRootDirList__Rename()
{
    DirectoryInfo dir = new DirectoryInfo(listBox4.SelectedItem.ToString());
    DirectoryInfo[] dirs = dir.GetDirectories("*", SearchOption.TopDirectoryOnly);
    listBox3.Items.Clear();
    foreach (DirectoryInfo di in dirs)
    {
        listBox3.Items.Add(di.FullName);
    }
    return;
}

public void GetRootDirList__Delete()
{
    DirectoryInfo dir = new DirectoryInfo(listBox6.SelectedItem.ToString());
    DirectoryInfo[] dirs = dir.GetDirectories("*", SearchOption.TopDirectoryOnly);
    listBox5.Items.Clear();
    foreach (DirectoryInfo di in dirs)
    {
        listBox5.Items.Add(di.FullName);
    }
    return;
}

public void CreateDir()
{
    string drive = listBox1.SelectedItem.ToString();
    string name = textBox1.Text;
    string dirname = drive + name;
    DirectoryInfo di = new DirectoryInfo(@dirname);
    try
    {
        if (di.Exists)
        {
            MessageBox.Show("That path exists already.");
            return;
        }
        di.Create();
        MessageBox.Show("The directory was created successfully.");
    }
    catch (Exception e)
    {
        MessageBox.Show("The process failed: {0}", e.ToString());
    }
```

```
finally { }
public void RenameDir()
{
    string dirname = listBox3.SelectedItem.ToString();
    string tragetdrive = listBox4.SelectedItem.ToString();
    string newname = textBox2.Text;
    string targetdirname = tragetdrive + newname;
    Directory.Move(dirname, targetdirname);
    GetRootDirList__Rename();
}
public void DeleteDir()
{
    string dirname = listBox5.SelectedItem.ToString();
    Directory.Delete(dirname);
    GetRootDirList__Delete();
}
private void button3_Click(object sender, EventArgs e)
{
    DeleteDir();
}
private void listBox1_SelectedIndexChanged(object sender, EventArgs e)
{
    label3.Text = listBox1.SelectedItem.ToString();
    GetRootDirList();
}
private void listBox4_SelectedIndexChanged(object sender, EventArgs e)
{
    GetRootDirList__Rename();
}
private void listBox6_SelectedIndexChanged(object sender, EventArgs e)
{
    GetRootDirList__Delete();
}
private void button1_Click(object sender, EventArgs e)
{
    CreateDir();
    GetRootDirList();
}
private void button2_Click(object sender, EventArgs e)
{
    RenameDir();
}
private void Form1_Load(object sender, EventArgs e)
{
    GetDriveList();
    label3.Text = "";
}
}
```

NOTE
To add the code, you need to generate the Load event of Form1, the SelectedIndexChanged event of the respective ListBox controls, and the Click event of the Button controls by double-clicking the respective controls.

7. Press the F5 key to run the application. All the drives appear in the Select Drive list box. When you select a drive, the directories contained within the drive appear in the Directories in: D:\ list box, as shown in Figure 29.15:

3. Add the System.IO namespace and the code, given in Listing 29.3, in the Click event of the Button control:

# Listing 29.3: Showing the Code for the Click Event of the Button Control

```
private void button1_Click(object sender, EventArgs e)
{
    DirectoryInfo dir = new DirectoryInfo(@"c:\windows");
    {
        if (dir.Exists)
        {
            MessageBox.Show("Directory Exists");
        }
        else {
            MessageBox.Show("Directory not Exist");
        }
    }
}
```

4. Press the F5 key to run the application. When you click the Check Directory button, a message box appears, displaying a message whether the specified directory exists or not, as shown in Figure 29.6:

![](bbox=[0.4, 0.335, 0.67, 0.535])

# Figure 29.6: Checking the Existence of a Directory

Now, let’s discuss about displaying the list of directories available in particular drives.

# Getting the List of Directories

A drive may contain numerous directories. To get the list of directories in a drive, let’s create an application, named DirectoriesExample (also available on the CD-ROM) and perform the following steps:

+   1. Add two ListBox controls and two Label controls to the Form1 designer, and change the Text property of the Label controls to Select Drive and Select Directory, respectively, as shown in Figure 29.7:

![](bbox=[0.31, 0.67, 0.735, 0.89])

# Figure 29.7: Showing the Design View of the DirectoriesExample Application
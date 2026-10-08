CreateDirectory contains information about a directory. Much of the information contained in class DirectoryInfo also can be accessed via the methods of class Directory.

| static Method | Description |
| --- | --- |
| CreateDirectory | Creates a directory and returns its associated DirectoryInfo object. |
| Delete | Deletes the specified directory. |
| Exists | Returns true if the specified directory exists and false otherwise. |
| GetDirectories | Returns a string array containing the names of the subdirectories in the directory. |
| GetFiles | Returns a string array containing the names of the files in the specified directory. |
| GetCreationTime | Returns a DateTime object representing when the directory was created. |
| GetLastAccessTime | Returns a DateTime object representing when the directory was last accessed. |
| GetLastWriteTime | Returns a DateTime object representing when items were last written to the directory. |
| Move | Moves the specified directory to a specified location. |

Fig. 17.12 Directory class methods.

# 17.9.1 Demonstrating Classes File and Directory

Class TestForm (Fig 17.13) uses File and Directory methods to access file and directory information. The Form contains the inputTextBox, in which the user enters a file or directory name. Each time that the user presses while typing in the TextBox, the program calls inputTextBox_KeyDown (lines 19–76). If the user presses the Enter (line 22), this method displays the file's or directory's contents, depending on the user input. (If the user does not press the Enter, this method returns without displaying any content).

```
// Fig. 17.13: FileTest.cs
// Using classes File and Directory.
using System;
using System.Windows.Forms;
using System.IO;

namespace FileTest
{
    // displays contents of files and directories
    public partial class FileTestForm : Form
{
        // parameterless constructor
        public FileTestForm()
    }
```

Fig. 17.13 | Using classes File and Directory. (Part i of 4).
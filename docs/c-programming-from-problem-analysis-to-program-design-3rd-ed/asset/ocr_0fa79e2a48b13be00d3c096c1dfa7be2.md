# Writing Text Files

All attempts to access text files should be enclosed inside try...catch blocks to check for exceptions. This is not required in C#, but is encouraged to avoid unhandled exceptions being thrown during run time. The constructor for the StreamWriter class is overloaded, in that you can include additional arguments such as a Boolean variable indicating whether the file should be appended to or overwritten if it already exists. If you do not include an argument for the Append mode, a new file is created by default, overwriting any previously created versions. Using the Append mode enables you to add lines onto the end of an existing file.

![](bbox=[0.15, 0.36, 0.22, 0.42])

Constructing an object of the StreamWriter class using true as the second argument enables you to append values onto the end of a file. The following statement opens the file named info.txt, stored in the project subdirectory, so that records will be added onto the end of the file:

```
fileOut = new StreamWriter("../../../info.txt", true);
```

Values are placed in the file in a sequential fashion. A pointer moves through the file, keeping up with the current location into which the next values are to be placed in the file. After the file is created, the Close( ) method is used to finish storing the values. When the Close( ) method is called, any values waiting in the buffer to be written are flushed to the file and the resources associated with the file are released. Example 13-3 creates a text file containing the user's favorite sayings. This example illustrates using exception-handling techniques with the StreamWriter class. For the sake of brevity, the SayingsGUI.Designer.cs and Program.cs Windows Forms generated code is not included in the listing.

The application includes a Textbox object for data entry and a Label object for displaying error messages. The label is originally set to null (an empty value) at design time. One Button object is included. Its event-handler method is used to save the entry to the text file.

# Example 13-3

```
// SayingGUI.cs
// Windows application that retrieves
// and stores values from a text box
// in a text file.
using System;
using System.Drawing;
using System.Collections;
using System.ComponentModel;
using System.Windows.Forms;
using System.Data;
using System.IO;  // Added for file access
```
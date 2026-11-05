
specify the relative path, you do not give a drive letter. Instead, you either simply type the file-name indicating the file will be stored in the starting location or specify a path relative to the starting location. If the file is stored in the same Visual Studio folder that holds the project and source code files, you would write `"../../filename"`. This indicates to go up two directory levels from the bin\debug or bin\release folders to retrieve the file.

All of the applications you have designed were Debug versions. After an application is debugged and you are ready to deploy or distribute it, you can build a Release version. You switch from Debug to Release versions. The Release version contains no debugging information and is considered an optimized solution. To switch to the Release version, select **Release** from the **Solutions Configuration** list box on the Standard Visual Studio toolbar. You can also make that change using the **Properties** dialog box for the project.

![](img/e33ae760e23d89eac66541252ad65de8_821_0.png)

If you do not specify the full path for the filename, Visual Studio uses the bin\Debug or bin\Release subdirectory of the current project. To specify the full path, you must either use escape characters for the backslash or the verbatim string character (`@`). To specify that the file is stored at C:\CSharpProjects\Proj1, you would include as an argument either `("c:\CSharpProjects\Proj1")` using two backslashes for each backslash, or you would write `(@"C:\CSharpProjects\Proj1")`. When you place an @ in front of the string, it becomes a verbatim string.

The filename may be sent as a string literal or specified as a variable with a string value. The following statements construct objects of the `StreamWriter` and `StreamReader` classes:

```
StreamWriter outputFile = new StreamWriter("someOutputFileName");
StreamReader inputFile = new StreamReader("someInputFileName");
```

![](img/e33ae760e23d89eac66541252ad65de8_821_1.png)

The identifiers of `outputFile`, `someOutputFileName`, `inputFile`, and `someInputFileName` are all user-supplied identifiers. `outputFile` and `inputFile` represent the file stream objects. `someOutputFileName` and `someInputFileName` would be replaced by the actual filenames associated with the file—the names you see from **My Computer** or **Windows Explorer**. If you are creating a data file, place a file extension such as .dat, .da, or .txt onto the end of the file so that it can be distinguished from the other files on your system. Files that end in .txt can be easily opened for inspection in Notepad.

To avoid fully qualifying references to objects of these classes, include the `System.IO` namespace.

```
using System.IO;
```

When you use the `Write()` or `WriteLine()` methods with the instantiated stream object, the characters are written to the file specified by the filename. The values are stored in the file as text characters—string objects. `ReadLine()` reads a line of characters and returns the data as a string. The following statements write and read a test message to and from files after an object of the StreamWriter class has been constructed:

```
outputFile.WriteLine("This is the first line in a text file");
```

```
string inValue = inputFile.ReadLine( );
```

Tables 13-5 and 13-6 show members of the StreamWriter and StreamReader classes.

## Table 13-5 StreamWriter members

| StreamWriter members | Description |
|---|---|
| AutoFlush | (Property) Gets or sets a value indicating whether the StreamWriter flushes its buffer to the underlying stream after calls to the Write( ) or WriteLine( ) methods |
| Close( ) | Closes the current StreamWriter |
| Dispose( ) | Releases the unmanaged resources used by the StreamWriter |
| Flush( ) | Clears all buffers for the current writer and causes any buffered data to be written to the underlying stream |
| NewLine | (Property) Gets or sets the line terminator string used by the current TextWriter |
| Write( ) | Writes the characters to the stream |
| WriteLine( ) | Writes the characters to the stream, followed by a line terminator |

## Table 13-6 StreamReader members

| StreamReader members | Description |
|---|---|
| Close( ) | Closes the current StreamReader |
| DiscardBufferedData( ) | Allows the StreamReader to discard its current data |
| Dispose( ) | Releases the unmanaged resources used by the StreamReader |
| Peek( ) | Returns the next available character but does not consume it |
| Read( ) | Reads the next character or next set of characters from the input stream |
| ReadBlock( ) | Reads a specified number of characters from the current stream and writes the data to buffer, beginning at the index |
| ReadLine( ) | Reads a line of characters from the current stream and returns the data as a string |
| ReadToEnd( ) | Reads the stream from the current position to the end of the stream |

## Writing Text Files

All attempts to access text files should be enclosed inside try...catch blocks to check for exceptions. This is not required in C#, but is encouraged to avoid unhandled exceptions being thrown during run time. The constructor for the StreamWriter class is overloaded, in that you can include additional arguments such as a Boolean variable indicating whether the file should be appended to or overwritten if it already exists. If you do not include an argument for the Append mode, a new file is created by default, overwriting any previously created versions. Using the Append mode enables you to add lines onto the end of an existing file.

![](img/e33ae760e23d89eac66541252ad65de8_823_0.png)

Constructing an object of the StreamWriter class using true as the second argument enables you to append values onto the end of a file. The following statement opens the file named info.txt, stored in the project subdirectory, so that records will be added onto the end of the file:

```
fileOut = new StreamWriter("../../../info.txt", true);
```

Values are placed in the file in a sequential fashion. A pointer moves through the file, keeping up with the current location into which the next values are to be placed in the file. After the file is created, the Close( ) method is used to finish storing the values. When the Close( ) method is called, any values waiting in the buffer to be written are flushed to the file and the resources associated with the file are released. Example 13-3 creates a text file containing the user's favorite sayings. This example illustrates using exception-handling techniques with the StreamWriter class. For the sake of brevity, the SayingsGUI.Designer.cs and Program.cs Windows Forms generated code is not included in the listing.

The application includes a Textbox object for data entry and a Label object for displaying error messages. The label is originally set to null (an empty value) at design time. One Button object is included. Its event-handler method is used to save the entry to the text file.

## Example 13-3

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

```csharp
namespace SayingsApp
{
    public partial class SayingGUI : Form
    {
        private StreamWriter fil;  // Declares a file stream object

        public SayingGUI()
        {
            InitializeComponent();
        }

        // Form load event handler used to construct
        // object of the StreamWriter class, sending the
        // new filename as an argument. Enclosed in
        // try...catch block.
        private void SayingGUI_Load(object sender,
                                    System.EventArgs e)
        {
            try
            {
                fil = new StreamWriter("saying.txt");
            }
            catch (DirectoryNotFoundException exc)
            {
                lblMsg.Text = "Invalid directory"
                            + exc.Message;
            }

            catch (System.IO.IOException exc)
            {
                lblMsg.Text = exc.Message;
            }
        }

        // When the button is clicked, write the characters
        // to the text file.
        private void btnSaying_Click(object sender,
                                     System.EventArgs e)
        {
            try
            {
                fil.WriteLine(this.txtBxSaying.Text);
                this.txtBxSaying.Text = "";
            }

            catch (System.IO.IOException exc)
            {
                lblMsg.Text = exc.Message;
            }
        }
    }
}
```

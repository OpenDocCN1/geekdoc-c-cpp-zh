> NOTE
> If you do not specify the full path for the filename, Visual Studio uses the bin\Debug or bin\Release subdirectory of the current project. To specify the full path, you must either use escape characters for the backslash or the verbatim string character (@). To specify that the file is stored at C:\CSharpProjects\Proj1, you would include as an argument either ("c:\\CSharpProjects\\Proj1") using two backslashes for each backslash, or you would write (@"c:\CSharpProjects\Proj1"). When you place an @ in front of the string, it becomes a verbatim string.

The filename may be sent as a string literal or specified as a variable with a string value. The following statements construct objects of the StreamWriter and StreamReader classes:

```
StreamWriter outputFile = new StreamWriter("someOutputFileName");
StreamReader inputFile = new StreamReader("someInputFileName");
```

> NOTE
> The identifiers of outputFile, someOutputFileName, inputFile, and someInputFileName are all user-supplied identifiers. outputFile and inputFile represent the file stream objects. someOutputFileName and someInputFileName would be replaced by the actual filenames associated with the file—the names you see from Computer or Windows Explorer. If you are creating a data file, place a file extension such as .dat, .dta, or .txt onto the end of the file so that it can be distinguished from the other files on your system. Files that end in .txt can be easily opened for inspection in Notepad.

To avoid fully qualifying references to objects of these classes, include the System.IO namespace.

```
using System.IO;
```

When you use the Write() or WriteLine() methods with the instantiated stream object, the characters are written to the file specified by the filename. The values are stored in the file as text characters—string objects. ReadLine() reads a line of characters and returns the data as a string. The following statements write and read a test message to and from files after an object of the StreamWriter class has been constructed:

```
outputFile.WriteLine("This is the first line in a text file");
string inValue = inputFile.ReadLine();
```
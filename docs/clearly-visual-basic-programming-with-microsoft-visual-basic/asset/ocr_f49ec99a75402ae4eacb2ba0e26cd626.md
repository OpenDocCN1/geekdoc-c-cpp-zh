# DECLARING A STREAMREADER VARIABLE

```
Syntax

{Dim | Private} streamReaderVariableName As IO.StreamReader

Example

Dim inFile As IO.StreamReader
declares a StreamReader variable named inFile
```

**Figure 23-7:** Syntax and an example of declaring a StreamReader variable

**To begin coding the Read from File button's Click event procedure:**

+   1. Locate the code template for the btnRead control's Click event procedure.
+   2. Click the **blank line** below the ' declare variables comment. Type **dim inFile as io.streamreader** and press **Enter**.

After declaring a StreamReader variable, you can use the **OpenText method** to open a sequential access file for input, which automatically creates a StreamReader object. When a file is opened for input, the computer can read the lines of text stored in the file. Figure 23-8 shows the OpenText method's syntax along with an example of using the method. The *fileName* argument in the example does not include a folder path, so the computer will search for the report.txt file in the current project's bin\Debug folder. If the computer finds the file, it opens the file for input; otherwise, a runtime error occurs, causing the application to end abruptly. You assign the StreamReader object created by the OpenText method to a StreamReader variable, which you use to refer to the file in code.

# CREATING A STREAMREADER OBJECT BY OPENING A SEQUENTIAL ACCESS FILE

```
Syntax

IO.File.OpenText(fileName)

Example

inFile = IO.File.OpenText("report.txt")
opens the report.txt file for input; creates a StreamReader object and assigns it to the inFile variable
```

**Figure 23-8:** Syntax and an example of creating a StreamReader object by opening a file
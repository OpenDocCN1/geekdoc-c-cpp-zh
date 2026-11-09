
```vb
' assign IDs and prices to the array
gifts(0).strId = "BX35"
gifts(0).intPrice = 13
gifts(1).strId = "CR20"
gifts(1).intPrice = 10
gifts(2).strId = "FE15"
gifts(2).intPrice = 12
gifts(3).strId = "KW10"
gifts(3).intPrice = 24
gifts(4).strId = "MM67"
gifts(4).intPrice = 4

' assign the product ID to a variable
strSearchFor = txtId.Text.ToUpper

' search the array for the product ID
' continue searching until there are
' no more array elements to search or
' the product ID is found
strFound = "N"
Do Until intSubscript = gifts.Length _
    OrElse strFound = "Y"
    If gifts(intSubscript).strId = strSearchFor Then
        strFound = "Y"
    Else
        intSubscript = intSubscript + 1
    End If
Loop

' determine whether the product ID
' was found in the array
If strFound = "Y" Then
    lblPrice.Text = gifts(intSubscript).intPrice.ToString("C0")
Else
    MessageBox.Show("Invalid product ID", _
        "Treasures Gift Shop", MessageBoxButtons.OK, _
        MessageBoxIcon.Information)
End If
End Sub
```

**Figure 22-18** *(continued from previous page)*

## SEQUENTIAL ACCESS FILES

In addition to getting data from the keyboard and sending data to the computer screen, an application also can get data from and send data to a file on a disk. Getting data from a file is referred to as “reading from the file,” and sending data to a file is referred to as “writing to the file.”

Files to which data is written are called **output files**, because the files store the output produced by an application. Files that are read by the computer are called **input files**, because an application uses the data in the files as input.

Most input and output files are composed of lines of text that are both read and written sequentially—in other words, in consecutive order, one line at a time, beginning with the first line in the file and ending with the last line in the file. Such files are referred to as **sequential access files**, because of the manner in which the lines of text are accessed.

Examples of text stored in sequential access files include an employee list, a memo, or a sales report. You will use a sequential access file in the Game Show Contestants application, which you code in the remaining sections of this chapter.

Figure 23-1 shows the application’s user interface. The interface provides a text box for entering a contestant’s name. The Write to File button will write the name to a sequential access file. The Read from File button will read each name from the sequential access file and display each in the Contestants box. (The txtContestants control’s Multiline and ReadOnly properties are set to True, and its ScrollBars property is set to Vertical.) You will code the Write to File button first.

![](img/cf88270932e011575089da06b940a1d9_531_0.png)

Figure 23-1: User interface for the Game Show Contestants application

### WRITE THOSE LINES OF TEXT

An item of data—such as the string “Yolanda”—is viewed differently by a human being and a computer. To a human being, the string represents a person’s name; to a computer, it is merely a sequence of characters. Programmers refer to a sequence of characters as a **stream of characters**. In Visual Basic, you use a **StreamWriter object** to write a stream of characters to a sequential access file. Before you create the StreamWriter object, you first declare a variable to store the object in the computer’s internal memory. Figure 23-2 shows the syntax and an example of declaring a StreamWriter variable. The IO in the syntax stands for “Input/Output.”

### DECLARING A STREAMWRITER VARIABLE

```
Syntax
{Dim | Private} streamWriterVariableName As IO.StreamWriter

Example
Dim outFile As IO.StreamWriter
declares a StreamWriter variable named outFile
```

**Figure 23-2:** Syntax and an example of declaring a StreamWriter variable

**To open the Game Show Contestants application, and then begin coding the application:**

- 1. Start Visual Studio 2008 (or Visual Basic 2008 Express Edition). Open the **Contestant Solution (Contestant Solution.sln)** file, which is contained in the ClearlyVB\Chap23\Contestant Solution folder. If necessary, open the designer window.
- 2. Open the Code Editor window, then locate the code template for the btnWrite control’s Click event procedure. Click the **blank line** below the ' declare a StreamWriter variable comment. Type **dim outFile as io.streamwriter** and press **Enter**.

After declaring a StreamWriter variable, you can use the syntax shown in Figure 23-3 to create a StreamWriter object. As the figure indicates, creating a StreamWriter object involves opening a sequential access file using one of two methods: CreateText or AppendText. You use the **CreateText method** to open a sequential access file for output. When you open a file for output, the computer creates a new, empty file to which data can be written. If the file already exists, the computer erases the contents of the file before writing any data to it. You use the **AppendText method** to open a sequential access file for append. When a file is opened for append, new data is written after any existing data in the file. If the file does not exist, the computer creates the file for you. In addition to opening the file, both methods automatically create a StreamWriter object to represent the file in the application. You assign the StreamWriter object to a StreamWriter variable, which you use to refer to the file in code. Also included in Figure 23-3 are examples of using the CreateText and AppendText methods. When processing the statement in Example 1, the computer searches for the pay.txt file in the ClearlyVB\Chap23 folder on the C drive. If the file exists, its contents are erased and the file is opened for output; otherwise, a new, empty file is created and opened for output. The statement creates a StreamWriter object and assigns it to the outFile variable. Unlike the *fileName* argument in Example 1, the *fileName* argument in Example 2 does not contain a folder path. Therefore, the computer will search for the file in the default folder, which is the current project's bin\Debug folder. In this case, if the computer locates the report.txt file in the default folder, it opens the file for append. If it does not find the file, it creates a new, empty file and then opens the file for append. Like the statement in Example 1, the statement in Example 2 creates a StreamWriter object and assigns it to the outFile variable.

**CREATING A STREAMWRITER OBJECT BY OPENING A SEQUENTIAL ACCESS FILE**

```
Syntax
IO.File.method(fileName)
```

| method | Description |
| --- | --- |
| CreateText | opens a sequential access file for output |
| AppendText | opens a sequential access file for append |

```
Example 1
outFile = IO.File.CreateText("C:\ClearlyVB\Chap23\pay.txt")
opens the pay.txt file for output; creates a StreamWriter object and assigns it to the outFile variable

Example 2
outFile = IO.File.AppendText("report.txt")
opens the report.txt file for append; creates a StreamWriter object and assigns it to the outFile variable
```

**Figure 23-3:** Syntax and examples of creating a StreamWriter object by opening a file

When the user clicks the Write to File button in the Game Show Contestants application, the name entered in the Name box should be added to the end of the existing names in the file; therefore, you will need to open the sequential access file for append. A descriptive name for a file that stores the names of contestants is contestants.txt. Although it is not a requirement, the “txt” (short for “text”) filename extension is commonly used when naming sequential access files; this is because the files contain text.

**To continue coding the btnWrite control's Click event procedure:**

- 1. Click the **blank line** below the ' open the file for append comment.
- 2. Type **outFile = io.file.appendtext("contestants.txt")** and press **Enter**.

After opening a file for either output or append, you can begin writing data to it. You can do this using either the **Write method** or the **WriteLine method**; however, in most cases you will use the WriteLine method. The difference between both methods is that the WriteLine method writes a newline character after the data. Figure 23-4 shows the syntax and an example of both methods. As the figure indicates, when using the Write method, the next character written to the file will appear immediately after the letter o in the string “Hello”. When using the WriteLine method, however, the next character written to the file will appear on the line immediately below the string. Notice that you do not need to include the file’s name in either method’s syntax. This is because the data will be written to the file associated with the StreamWriter variable.

### WRITING DATA TO A SEQUENTIAL ACCESS FILE

```
Syntax

streamWriterVariableName.Write(data)
streamWriterVariableName.WriteLine(data)

Example 1

outFile.Write("Hello")

Result

Hello|
the next character will appear immediately after the letter o

Example 2

outFile.WriteLine("Hello")

Result

Hello
|
the next character will appear on the next line
```

**Figure 23-4:** Syntax and examples of writing data to a sequential access file

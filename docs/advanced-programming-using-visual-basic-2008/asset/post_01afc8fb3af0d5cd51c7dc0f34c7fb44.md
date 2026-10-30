
A simple way to read and write small amounts of data is to use the StreamReader and StreamWriter objects. Generally, you write the StreamWriter code first, to create the data file. Then you can write the StreamReader code to read the file that you just created.

## Writing Data

To write data to a file, you first have the user input the data into text boxes and then write the data to the disk. The steps for writing data are:

- Declare a new StreamWriter object, which also declares the name of the data file. Instantiating a new StreamWriter object opens the file. The file must be open before you can write in the file. If the file does not already exist, a new one is created. The default location for the file is the directory from which the .exe is running. If you are running from the IDE in Debug mode, the default directory is the bin\Debug directory beneath the folder for the current project. You also can specify the complete path of the file. Set the BooleanAppend argument to true to specify that you want to append data to an existing file.
- Use the StreamWriter’s WriteLine method to copy the data to a buffer in memory. (A buffer is just a temporary storage location.)
- Call the StreamWriter’s Close method, which transfers the data from the buffer to the file and releases the system resources used by the stream. After you write a file, you can view it using a text editor or the VS IDE.

## Instantiating a StreamWriter Object

```
Dim ObjectName As New StreamWriter("FileName")
Dim ObjectName As New StreamWriter("FileName", BooleanAppend)
```

## Examples

```
Dim PhoneStreamWriter As New StreamWriter("Phone.txt")
Dim NamesStreamWriter As New StreamWriter("C:\MyFiles\Names.txt")
Dim LogFileStreamWriter As New StreamWriter("C:\MyFiles\LogFile.txt", True)
```

The StreamWriter object has both a Write and a WriteLine method. The difference between the two is that the WriteLine method places a carriage-return character at the end of the elements for each execution of the method.

## The WriteLine Method

```
ObjectName.WriteLine(DataToWrite)
```

The DataToWrite argument may be string or numeric. The WriteLine method converts any numeric data to string and actually writes string data in the file.

## Examples

```
PhoneStreamWriter.WriteLine(NameTextBox.Text)
PhoneStreamWriter.WriteLine(PhoneTextBox.Text)

NameStreamWriter.WriteLine("Sammy")

BankBalanceStreamWriter.WriteLine(BalanceDecimal.ToString)
```

## Closing a File

Use the StreamWriter’s Close method when finished writing the data.

## Reading Files

Use the StreamReader class to read the data from a file that you created with a StreamWriter.

The steps for reading the data from a file are

- Declare an object of the StreamReader class. The constructor declares the filename and optional path. Instantiating the object opens the file so that you can read from it. However, if no such file exists, an exception occurs. For this reason, you should declare the StreamReader object in a procedure so that you can enclose it in a Try / Catch block.
- Use the ReadLine method to read the data. You may need to use a loop to retrieve multiple records.
- When finished, close the stream using the StreamReader’s Close method.

## Instantiating a StreamReader Object

```
Dim ObjectName As New StreamReader("FileName")
```

## Examples

```
Try
    Dim NameStreamReader As New StreamReader("C:\MyFiles\Names.txt")
Catch
    MessageBox.Show("File does not exist")
End Try
```

```
' In declarations section, to create a module-level variable.
Private PhoneStreamReader As StreamReader
' In a procedure, to catch an exception for a missing file.
Try
    PhoneStreamReader = New StreamReader("Phone.txt")
Catch
    MessageBox.Show("File does not exist")
End Try
```

## The ReadLine Method

The StreamReader’s ReadLine method, which has no arguments, reads the next line from the file. Assign the data read to the desired location, such as a label, a text box, or a string variable.

```
NameLabel.Text = PhoneStreamReader.ReadLine()
```

## Checking for the End of the File

The StreamReader's Peek method looks at the next element without really reading it. The value returned when you peek beyond the last element is negative 1 (-1).

```
If PhoneStreamReader.Peek <> -1 Then
NameLabel.Text = PhoneStreamReader.ReadLine()
PhoneLabel.Text = PhoneStreamReader.ReadLine()
End If
```

The ReadLine method does not throw an exception when you attempt to read past the end of the file.

## Project Resources

Graphic and sound files used by a project are stored in the Resources folder. You can add files to the Resources folder when you set the Image property of a PictureBox control or display the Resource tab of the Project Designer (Project / ProjectName Properties). After you have added a file to the Resources folder, you can easily refer to it using the new My object.

My.Resources.Ding (refers to the sound file Ding.wav, stored in the Resources folder).

My.Resources.Logo (refers to the graphic file Logo.gif, stored in the Resources folder).

## Playing a Sound

To play a sound file that is stored in the Resources folder, use

```
My.Computer.Audio.Play(My.Resources.Ding, AudioPlayMode.WaitToComplete)
```

## XML Files

More and more documents are being stored as XML files. In Chapter 13 we discussed XML as a part of database files. The same format also is used for word processing and other types of office files.

node (a file can have only one) and branching out in child nodes. A child also can contain child nodes. Nodes that are at the same level are referred to as siblings.

## XML File Terminology

| Term | Meaning | Example from books.xml |
|---|---|---|
| `<> </>` | Start tag and end tag. | `<price> 5.99 </price>`<br>`<emptyNode></emptyNode>` or `<emptyNode/>` |
| Element | Contents within a set of tags. | `<title>The Goriass</title>`<br>``<author>`<br>`    `<name>Plato</name>`<br>`</author>` |
| Node | A branch on the tree; the root node is the most outside with the child nodes inside. | Root node `<bookstore>`<br>Child nodes `<book>`<br>`<title>` and `<author>` are child nodes of `<book>` |
| Sibling | Nodes at the same level. | `<title>` and `<author>` |
| Attribute | Name values assembled within an element; the name of the attribute is assigned a value enclosed in either single or double quotes. | `<book genre="autobiography" publicationdate="1981" ISBN="1-861003-11-0">` |
| Text | Value placed within tags. | `<first-name>Benjamin</first-name>` |
| Comment | Used for remarks only. | `<!-- This file represents a fragment of a book store inventory database -->` |

A node may have additional attributes with values assigned. The value may be placed in either single quotes or double quotes. In the following line, genre, publicationdate, and ISBN are attributes.

```
`<book genre="autobiography" publicationdate="1981" ISBN="1-861003-11-0">`
```

VB includes XDocument and XElement classes for working with xml files.

## Loading an XML File into an XDocument Object

You can use the Load method of an XDocument to read an XML file. For the Filename entry, you can specify a complete path or a URI; otherwise the Load method looks in the current directory, which is bin\Debug in your VB project.

```
Dim BookXDocument As XDocument = XDocument.Load("books.xml")
Private CustomerXDocument As XDocument = XDocument.Load("C:\Data\customers.xml")
Dim InventoryDocument = XDocument.Load(CurDir() & "\inventory.xml")
```

## Loading an XML File into an XElement Object

In addition to using an XDocument, you also can load an XML file into an XElement object. The difference between the two is that the XDocument contains the information about the document from the top of the file, while the root node is the first item in an XElement object.

```
Dim BookData = XElement.Load("books.xml")
```

## APPENDIX

## C

## Deployment

## Deploying Windows Applications

Deployment refers to the process of distributing an application to users. You can choose from the two older methods of deployment—XCopy and Windows Installer—or the newer ClickOnce deployment introduced with Visual Studio 2005. Many third-party tools are also available for deploying applications.

XCopy deployment simply means to copy the executable file to the destination computer, which must have .NET installed. XCopy is acceptable for only the simplest application. No entries are made in the registry or the Programs menu, and conflicts with component versions are possible.

Using Windows Installer, you can create a Setup application and distribute a program on CD. The user runs the Setup wizard to install the program. When you update the program, you must create a new installation CD and the user must reinstall the entire application.

## ClickOnce Deployment

ClickOnce deployment is the current deployment tool from Microsoft. Using ClickOnce, you can distribute applications through a Web page, a network file share, or media such as a CD. You can set up the deployment so that the application automatically checks for updates and the user does not have to reinstall the entire application.

ClickOnce overcomes the basic problems found with Windows Installer deployment. A user no longer needs to reinstall an entire application; updates can be made for only those portions that have changes. Installing an application does not require Administrative privileges; ClickOnce provides the ability to grant Code Access Security permissions for an application. Another advantage is that applications deployed with ClickOnce do not share components, which does away with the version conflicts of shared components when installing or uninstalling programs.

## Using the Publish Tab

To use the ClickOnce deployment, first open the application in the VS IDE, open the Project Designer (Project / Properties), and click on the Publish tab.

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_623_0.png)

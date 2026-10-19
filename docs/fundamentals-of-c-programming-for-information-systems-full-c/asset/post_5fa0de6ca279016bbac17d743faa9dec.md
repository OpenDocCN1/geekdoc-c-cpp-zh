
## Programming Assignment 3

The main goal of this assignment is to give you experience in working with database tables, text files, DataGridView and ListView.

This assignment is a modified version of assignment 2. A major change is the use of database tables (instead of sequential files) to store information. You are to develop an application for “Ace Auto Rentals,” which is a small business that rents automobiles.

The Rentals database used in this assignment can be found in Tutorial_Starts/DataFiles folder. This database includes two tables: the Rental table that stores information on car rentals, and AutoTypes that contains the daily rental rates for different types of automobiles. Copy the database file to a local folder.

The following is a sample of the records in the Rental table:

| RentalId | CustNumber | CustName | RentalDate | NumOfDays | AutoTypeId | DiscCategory | TotalCost |
|---|---|---|---|---|---|---|---|
| 1001 | 10138 | Josh Philip | 11/5/2015 | 2 | 3 | Business | 81 |
| 1002 | 10150 | Mini George | 10/10/2015 | 1 | 2 | Favorite | 48 |
| 1003 | 10144 | Jeffrey Mathews | 12/22/2015 | 3 | 1 | State | 179.5 |
| 1004 | 10130 | Cathy Arnold | 12/21/2015 | 2 | 2 | Standard | 120 |
| 1005 | 10135 | Gina Rodriguez | 11/22/2015 | 5 | 4 | Standard | 200 |
| 1006 | 10126 | Faith Abraham | 11/23/2015 | 4 | 3 | Favorite | 112 |
| 1007 | 10115 | Chris Cheng | 12/22/2015 | 4 | 2 | Standard | 80 |
| 1008 | 10124 | Sashi Nair | 12/20/2015 | 2 | 6 | Business | 45 |

The following table shows the field types of Rentals. The data types char() and varchar() are text data.

| Name | Data Type | Allow Nulls |
|---|---|---|
| RentalId | int | ☐ |
| CustNumber | char(5) | ☑ |
| CustName | varchar(40) | ☑ |
| RentalDate | date | ☑ |
| NumOfDays | int | ☑ |
| AutoTypeId | int | ☑ |
| DiscCategory | varchar(15) | ☑ |
| TotalCost | float | ☑ |

The AutoTypes table appears as follows:

| AutoTypeId | Description | DailyRate |
|---|---|---|
| 1 | SUV | 70 |
| 2 | mini-van | 60 |
| 3 | luxury | 45 |
| 4 | full-size | 40 |
| 5 | mid-size | 35 |
| 6 | compact | 25 |

### Part 1

Create a form named DisplayRentals that lets the user display Rental records, one at a time, as shown below.

![](img/143bad48262566137acc9c41f668a88f_428_0.png)

**Note:** If the version of SQL Server you use is incompatible with the database, when you create the data source, you will be asked whether you want to update the database. Answer “Yes.” Again, make sure that you answer “No” when the DataSource Configuration Wizard asks you whether you want to copy the database to the project folder. (If you answer “Yes,” the changes you make to the table will be lost the next time you run the project.)

The primary key, RentalId, is an auto-increment field. To view the fields and their properties, right click Rental table in Server Explorer window, and select Open Table Definition. The T-SQL window displays the SQL that creates the table. The keyword IDENTITY(1,1) specifies that RentalId is an auto-increment field that increments by 1, starting with 1.

To view the data tables, open RentalDataSet.xsd. Select RentalId field and view its properties. Make sure that the auto-increment properties are set as follows:

![](img/143bad48262566137acc9c41f668a88f_428_1.png)

## Appendix A: Binary Files

### A.1 Writing to Binary Files

The key differences between text files and binary files are

- 1. Text files store all data as text, whereas binary files store data in its original form without converting to text, using the standard internal representation of numbers, dates, and so on. Therefore, the contents of text files can be viewed and edited in a text editor like Notepad, but binary files are not readable in a text editor.
- 2. Data typically is written to text files by combining an entire record into a single string and writing it in a separate line using the WriteLine() method of StreamWriter. Data is written to binary files individually using the Write() method of BinaryWriter. Data is not grouped into rows.
- 3. The StreamWriter object to write data to text files can be created without explicitly creating a FileStream object. However, creating a BinaryWriter to write data to a binary file requires creating the FileStream object that is used by the BinaryWriter, as follows:

```
FileStream variableName = new FileStream("FileName", FileMode);
BinaryWriter variableName = new BinaryWriter(FileStream object);
```

**Example**

```
FileStream examsStream = new FileStream("Exams.bin", FileMode.Append);
BinaryWriter examsWriter = new BinaryWriter(examsStream);
```

FileMode.Append: Append specifies that new data is added to existing data. If the file doesn’t exist, it will be created.

FileMode.OpenOrCreate would overwrite existing data when new data is written. If the file doesn’t exist, it will be created.

**Tutorial: Working with Binary Files**

- Step A-1: Open the project, Ch8_FilesAndArrays. Open the WriteToBinaryFile form that has the same user interface as the WriteToTextFile form that you used in Chapter 8. Open the code window. Figure A-1 shows the complete code to write data from the TextBoxes to a specified file.
- Step A-2: Add the code in lines 19 and 20, and in lines 30 and 32 from Figure A-1. Run the project. Select a folder and enter Exams.bin for file name.
- Step A-3: Enter the name, score1 and score2, for five students as shown below, save them, and exit the form:

|  |  |  |
|---|---|---|
| Mike Burns | 75 | 92 |
| Cathy Arnold | 86 | 95 |
| Wesley Mathews | 82 | 90 |
| Jerry Luke | 70 | 89 |
| Gina Rodriguez | 77 | 94 |

Open Exams.bin with Notepad. (Right click the file, select Open with, and select Notepad.) Note that the two scores are not readable because they are not stored as text.

**Figure A-1: Writing to binary file**

```
9  using System.Windows.Forms;
10 using System.IO;    // Add this line
11 namespace Ch8_FilesAndArrays
12 {
13     public partial class WriteToBinaryFile : Form
14     {
15         public WriteToBinaryFile()
16         {
17             InitializeComponent();
18         }
19         FileStream examsStream;     // Declare variable to represent FileStream object
20         BinaryWriter examsWriter;   // Declare variable to represent BinaryWriter object
21         private void WriteToBinaryFile_Load(object sender, EventArgs e)
22         {
23             ExamsSaveDialog.ShowDialog();   // Display Save As Dialog box
24             // Get the file name selected by the user and save in the variable fileName
25             string fileName = ExamsSaveDialog.FileName;
26
27             if (fileName.Length > 0)    // if the user selected a file
28             {
29                 //Create FileStream object and assign to examsStream:
30                 examsStream = new FileStream(fileName, FileMode.Append);
31                 //Create BinaryWriter objects and assign to examsWriter:
32                 examsWriter = new BinaryWriter(examsStream);
33             }
34             else
35             {
36                 MessageBox.Show("No file selected");
37                 btnSave.Enabled = false;
38             }
39         }
```

### A.2 Reading Binary Files

Data is read from a Binary file using the BinaryReader object. Similar to the BinaryWriter object, the BinaryReader object uses the FileStream object, created as follows:

```
FileStream variableName = new FileStream(@"FileName", FileMode);
BinaryReader variableName = new BinaryReader(FileStream);
```

**Example:**

```
FileStream examsStream = new FileStream(@"E:\Exams.bin", FileMode.Open);
BinaryReader examsReader = new BinaryReader(examsStream);
```

FileMode.Open: Opens the file if it exists; if not, an exception is thrown.

The code to read Exams.bin file (which was created in the form WriteToBinaryFile), and compute the average score for each student, is shown in Figure A-2. Exams.bin contains the name, score1 and score2, for multiple students.

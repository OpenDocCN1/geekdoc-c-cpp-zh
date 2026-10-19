Open Exams.bin with Notepad. (Right click the file, select Open with, and select Notepad.) Note that the two scores are not readable because they are not stored as text.

# Figure A-1: Writing to binary file

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

# A.2 Reading Binary Files

Data is read from a Binary file using the BinaryReader object. Similar to the BinaryWriter object, the BinaryReader object uses the FileStream object, created as follows:

```
FileStream variableName = new FileStream(@"FileName", FileMode);
BinaryReader variableName = new BinaryReader(FileStream);
```

# Example:

```
FileStream examsStream = new FileStream(@"E:\Exams.bin", FileMode.Open);
BinaryReader examsReader = new BinaryReader(examsStream);
```

FileMode.Open: Opens the file if it exists; if not, an exception is thrown.

The code to read Exams.bin file (which was created in the form WriteToBinaryFile), and compute the average score for each student, is shown in Figure A-2. Exams.bin contains the name, score1 and score2, for multiple students.
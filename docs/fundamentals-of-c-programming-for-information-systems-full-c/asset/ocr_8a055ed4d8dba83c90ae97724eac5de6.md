# ReadLine method

The StreamReader provides a method called ReadLine to read the line at the current read position and then advance the position to the next line. This method is used within a loop to sequentially read each line of data. This is how you would use a loop to read each line and display the line in a ListBox named lstDisplay:

```
string currentLine;
while (examsReader.EndOfStream == false) // or. !examsReader.EndOfStream
{
    // Read current line and store it in a string variable
    currentLine = examsReader.ReadLine();
    lstDisplay.Items.Add(currentLine);    // Display the line
}
examsReader.Close();
```

# EndOfStream property

The EndOfStream property of StreamReader has the value true when the current read position is at the end of the file. The header of the while loop in the above code, while (examsReader.EndOfStream == false), uses the EndOfStream property to terminate the loop when EndOfStream is true. That is, the loop continues while EndOfStream is false.

The statement
    currentLine = examsReader.ReadLine();
reads the current line and stores the entire line as a single string in the string variable, currentLine. At the end of the first iteration through the loop, the string variable currentLine would have the following value: "Mike Burns, 75, 92"

Thus, the loop reads each line, stores it in the string variable currentLine, and then displays it to give the output shown in Figure 8-1.

# Figure 8-1: Data from the Exams.txt file

```
Mike Burns, 75, 92
Cathy Arnold, 86, 95
Wesley Mathews, 82, 90
Jerry Luke, 70, 89
Gina Rodriguez, 77, 88
```
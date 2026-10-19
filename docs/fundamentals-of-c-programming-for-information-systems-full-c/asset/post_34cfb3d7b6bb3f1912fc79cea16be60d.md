
`ArrayName` is the name of a one-dimensional array, and `SearchValue` is the value you are trying to find in an array. The method returns the index of the first element that matches the specified value. If no value is found, the method returns -1.

For example,

```csharp
Array.IndexOf(names, "Mike Burns")
```

returns the index of the first element of the names array that matches the specified value, Mike Burns.

Figure 8-14 shows the code that uses this method to find a vendor’s phone number by searching for a specified name.

## Figure 8-14: Code to find the phone number using IndexOf method

```
private void btnFindPhone_Click(object sender, EventArgs e)
{
    string searchName = txtVendorName.Text;
    string fmtStr = "{0,-15}{1,8}";
    lstDisplay.Items.Clear();

    // Method 1: Use IndexOf method to find the record
    int index = Array.IndexOf(names, searchName);
        //if there is no match, index would be -1.
    if (index >= 0)
        lstDisplay.Items.Add(string.Format(fmtStr, searchName,
                                           phoneNumbers[index]));
    else
        MessageBox.Show("Sorry, name not found");
}
```

**Line 60** uses the IndexOf method to get the index of the element in the Names array that matches the value of SearchName.

**Lines 62–64** display the corresponding element from phoneNumbers array if the index is not -1. If not, a message is displayed.

Figure 8-15 shows an alternate method that uses a loop to compare the value of SearchName with each element in the Names array.

## Figure 8-15: Using a loop to search a field

```
// Method 2: Use for loop to find the record
for (index = 0; index < recordCount; index++)
{
    if (searchName == names[index])
    {
        lstDisplay.Items.Add(String.Format(fmtStr, names[index],
                                            phoneNumbers[index]));
        return;
    }
}
MessageBox.Show("Sorry, there is no Vendor by that name");
```

Step 2-5: Add the code from Figure 8-15.

Test the code by typing in the value AMTRAK, which is one of the vendor names in the Vendor.txt file.

## Tutorial 3: Using a ComboBox to Select the Search Name

This tutorial creates a different version of the application where the vendor names are added to the ComboBox, and when the user selects a name, the phone number is automatically displayed in the ListBox on the form named SmallFiles, as shown in Figure 8-16. The use of ComboBox to select a vendor is appropriate only if the number of vendors is relatively small. It is time consuming to load a large data set into a ComboBox.

## Figure 8-16: The SmallFiles Form with ComboBox to Select Name

![](img/143bad48262566137acc9c41f668a88f_265_0.png)

In this form called SmallFiles, you learn how to add items to a ComboBox from a file, and see an application of the SelectedIndexChanged event.

Step 3-1: Open the form, SmallFiles.

Two major aspects of the revised code are

- 1. The load event handler of the form, which reads data from Vendor.txt into two arrays, also adds vendor names to the ComboBox.
- 2. The SelectedIndexChanged event of the ComboBox finds the phone number for the selected name, whenever the user selects a vendor.

The complete code is shown in Figure 8-17. Because the use of ComboBox to select a vendor is appropriate only if the number of vendors is relatively small, the code does not include resizing of arrays. You use the same vendor file, Vendor.txt.

## 8.5 Writing to Text Files

You can write data to a text file using the StreamWriter class available in the System.IO namespace of Framework Class Library.

## Tutorial 4: Writing Scores to Text File

Let’s develop a form that writes data from Text Boxes into a text file. Figure 8-18 shows the form named WriteToTextFile.

## Figure 8-18: The WriteToTextFile form

![](img/143bad48262566137acc9c41f668a88f_268_0.png)

### The StreamWriter Object

The StreamWriter class can be used to write data into a text file. The StreamWriter object is created using the following syntax:

```
StreamWriter VariableName = new StreamWriter(@"Path and FileName", append flag);
```

If append flag is true, data are appended to existing data, if any. If append flag is false, existing data, if any, are overwritten. In both cases, if the specified file does not exist, a new file is created.

If no path is specified, it is assumed to be Bin\Debug folder of the project directory. The "@" prefix is not needed when the path is not specified. For example, to write data to Exams.txt with the append option, the StreamWriter object is created as follows:

```
StreamWriter examsWriter = new StreamWriter("Exams.txt", true);
```

### The WriteLine Method of StreamWriter

The WriteLine method of StreamWriter writes a string as a separate line into a file. Use this method to write all three data items for each student into a separate line in Exams.txt file.

### Declaring Variables at the Class Level

Because data are to be written multiple times (each time when the user clicks the Save button) to Exams.txt, you create the StreamWriter once when the form is loaded, use it each time the Save button is clicked, and close the StreamWriter when the form is closed. That means the variable (examsWriter) that references StreamWriter is used in three different methods:

- the Load event of the form,
- the Click event of the Save button, and

Step 4-5: Run the form.

The program breaks at line 25, which creates the examsWriter object. The form is not visible at this time because the code is part of the Load event handler.
Click Run to complete loading the form.
Remove the break.

Because examsWriter is created in the Load event, it is available when the form is open, and it is ready to be used for writing within the Click event handler of the Save button, shown in Figure 8-20.

## Figure 8-20: Code to write data to Exams.txt

```
private void btnSave_Click(object sender, EventArgs e)
{
    string name, score1, score2;
    // Store all data in string variables.
    name = txtName.Text;
    score1 = txtScore1.Text;
    score2 = txtScore2.Text;
    // Combine name & scores and store in Exams.txt
    examsWriter.WriteLine(name + "," + score1 + "," + score2);
    MessageBox.Show("Data Saved.");
}
```

Note that the above code writes the data using the StreamWriter every time the user clicks the Save button without having to create the StreamWriter and close it each time.

To write the data, the name, score1 and score2 are combined into a single string, (name + "," + score1 + "," + score2), with commas between each data item. The commas are inserted to make it easy to split the string if the data are read back in a program.

Step 4-6: Open the Click event handler of Save button. Fill in the missing code from Figure 8-20 to write data to Exams.txt file.

Step 4-7: Run the form. Enter data for name, score1 and score2, and click Save.

Click OK when you get the message “Data Saved.”

Step 4-8: View the Bin\Debug folder of your project directory. Open the Exams.txt file that was created earlier in the form ReadTextFile. You will not find the record that you entered and was supposed to have been written to it. What happened?

The data are written to the external device (hard disk, flash drive, etc.) only when the StreamWriter is closed. Until then, data written by StreamWriter are held in the buffer temporary memory. You have not added the code to close the Stream Writer.

### FormClosing Event of Forms

The StreamWriter object should be available until the form is closed. So, you should close StreamWriter only when the form is closed. This can be done by closing StreamWriter within the FormClosing event

Step 4-13: In line 25, change the append flag to false as follows:

```csharp
examsWriter = new StreamWriter("Exams.txt", false);
```

Add a third set of data and save it. Close the form.
Open Exams.txt and view it. You should see only the third set of data, because the previous records were overwritten.
Now, change the append flag back to true.

It’s time to practice! Do Exercise 8-3

### Directory Class

The Directory class in System.IO namespace provides several methods to work with directories (folders), including methods to create folders and to check whether a specified path exists. Figure 8-23 shows two commonly used methods of Directory class.

## Figure 8-23: Methods of Directory class

| Method | Function |
|---|---|
| Exists(path) | Returns true if the path exists and false if the path does not exist |
| CreateDirectory(path) | Creates the directories in the specified path |

You may create Exams.txt file in the WriteToTextFiles form by specifying a path other than the one for the default directory. Use the above methods to check whether the directories in the specified path exist, and to create them if they do not exist. Figure 8-24 shows the code to create the path E:\Csharp\output if it does not exist, and to use that path to write the data.

## Figure 8-24: Create a path using Directory class

```csharp
string path = @"E:\Csharp\output\";
if (!(Directory.Exists(path)))
    Directory.CreateDirectory(path);
examsWriter = new StreamWriter(path + "Exams.txt", true);
```

If the drive E: is invalid, you will get an error. If the directory, Csharp, does not exist, it is created, and the directory, output, is created within Csharp. If Csharp folder exists but output folder does not exist, it will be created.

The last statement,

examsWriter = new StreamWriter(path + "Exams.txt", true);

uses the newly created path to write the data.

Step 4-14:

Temporarily, replace the statement in line 25 by the code in Figure 8-24 to create a directory and use it to write the data. Run the project.
Enter a new record and save it. Verify that a new directory Csharp\output is created, and the file Exams.txt is created within it.
Remove the code that you inserted, and change line 25 back to its original form with no path specified.

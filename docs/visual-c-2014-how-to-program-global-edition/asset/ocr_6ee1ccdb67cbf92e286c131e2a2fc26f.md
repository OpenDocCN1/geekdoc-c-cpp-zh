# 752 Chapter 17 Files and Streams

```
// get next record available in file
var inputRecord = FileReader.ReadLine();
if (inputRecord != null)
{
    string[] inputFields = inputRecord.Split(',');
    // copy stream-array values to TextBox values
    SetTextBoxValues(inputFields);
}
else
{
    // close StreamReader and underlying file
    FileReader.Close();
    openButton.Enabled = true; // enable Open File button
    nextButton.Enabled = false; // disable Next Record button
    ClearTextBoxes();
}
// notify user if no records in file
MessageBox.Show("No more records in file", string.Empty, MessageBoxButtons.OK, MessageBoxIcon.Information);
catch (IOException)
{
    MessageBox.Show("Error Reading from File", "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
}
```

![](bbox=[0.327, 0.638, 0.672, 0.883])

**Fig. 17.6** | Reading a sequential-access file. (Part 3 of 4.)
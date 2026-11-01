![](bbox=[0.16, 0.11, 0.9, 0.54])

Figure 6.39. Setting the Filter property of the OpenFileDialog

```
```csharp
private void openFileButton_Click(object sender, EventArgs e)
{
}
```
```

Code 6.15

+   7. Firstly, we will add the code line DialogResult openFileResult = textFileOpenFileDialog.ShowDialog(); which will launch the file opening dialog box.
+   8. When the user selects a text file and clicks OK in the file opening dialog, the FileName property of the OpenFileDialog will be assigned to the selected filename. We will take this FileName and assign it to a new string with the code line string fileName = textFileOpenFileDialog.FileName;. The variable fileName will then contain the selected file's name.
+   9. Then, we will use a special method ReadAllText() to read the contents of the text file. This method reads a text file and assigns the contents of the text file to a string variable. The code line string text = File.ReadAllText(fileName); will do this job. Note that the method ReadAllText() is not included in the default libraries existing
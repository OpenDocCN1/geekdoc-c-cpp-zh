# Review Questions

**8.8** The following form, discussed earlier, lets the user save multiple sets of data into a text file by clicking the Save button after entering each set of data.

![](bbox=[0.147, 0.169, 0.522, 0.282])

The code shown below writes the name and the two scores from TextBoxes into the file Exams.txt.

```
```csharp
StreamWriter examsWriter;
private void WriteToTextFiles_Load(object sender, EventArgs e)
{
    examsWriter = new StreamWriter("Exams.txt", true);
}
private void btnSave_Click(object sender, EventArgs e)
{
    string name, score1, score2;
    name = txtName.Text;
    score1 = txtScore1.Text;
    score2 = txtScore2.Text;
    examsWriter.WriteLine(name + ", " + score1 + ", " + score2);
}
private void WriteToTextFiles_FormClosing(object sender, FormClosingEventArgs e)
{
    examsWriter.Close();
}
```
```

The streamWriter named examsWriter is declared at the class level, created in the Load event of the form, used in the Click event of the button multiple times and closed within the FormClosing event. What would be the effect of moving the declaration statement (`StreamWriter examsWriter;`) to the beginning of the Load event handler of the form, as follows?

```
```csharp
// StreamWriter examsWriter;
private void WriteToTextFiles_Load(object sender, EventArgs e)
{
    StreamWriter examsWriter;
    examsWriter = new StreamWriter("Exams.txt", true);
}
```
```
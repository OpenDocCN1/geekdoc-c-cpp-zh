```
    {
        if (File.Exists(path))
        {
            StreamWriter streamWriter = new StreamWriter(path,true);
            if (txtAppendText.Text != string.Empty)
            {
                string appendedText = "\r\n" + txtAppendText.Text;
                streamWriter.WriteLine(appendedText);
            }
            streamWriter.Close();
            txtHiddenAppendedText.Text = txtAppendText.Text;
            txtShowFile.Text = string.Empty;
            FileInfo file = new FileInfo(path);
            txtShowFile.Text = File.ReadAllText(path);
        }
        catch (Exception ex)
        {
            lblError.Text = ex.Message;
        }
    }
```

Figure 21.8 shows the Web page after appending the book name at the position 11:

![](bbox=[0.18, 0.466, 0.84, 0.685])

**Figure 21.8: Displaying the Web page after Clicking the Append Button**

In case we want to undo the append operation, we can use the Cancel button. To revert back the changes, a hidden text box is maintained with the original content of the file. Listing 21.12 shows the C# code for the cancel operation:

**Listing 21.12: Showing the btnCancelAppend_Click() Method**

```
    protected void btnCancelAppend_Click(object sender, EventArgs e)
    {
        txtAppendText.Text = txtHiddenAppendedText.Text;
    }
```
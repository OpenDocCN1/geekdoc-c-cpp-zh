```
directoryTextBox.Text = Application.StartupPath;
}
```

Give the Search button a Click event handler that searches for the desired files.

1. Use code similar to the following:

```
// Search for files matching the pattern
// and containing the target string.
private void searchButton_Click(object sender, EventArgs e)
{
    // Get the file pattern and target string.
    string pattern = patternComboBox.Text;
    string target = targetTextBox.Text.ToLower();

    // Clear the result list.
    fileListBox.Items.Clear();

    // Search for files.
    DirectoryInfo dirinfo =
        new DirectoryInfo(directoryTextBox.Text);
    foreach (FileInfo fileinfo in
        dirinfo.GetFiles(pattern, SearchOption.AllDirectories))
    {
        // See if we need to look for target text.
        if (target.Length > 0)
        {
            // If this file contains the target string,
            // add it to the list.
            string content =
                File.ReadAllText(fileinfo.FullName).ToLower();
            if (content.Contains(target))
                fileListBox.Items.Add(fileinfo);
        }
        else
        {
            // Just add this file to the list.
            fileListBox.Items.Add(fileinfo);
        }
    }
}
```

# EXERCISES

+   1. Write a program that sorts a text file. (Hint: Load the file's lines of text into an array and use Array.Sort to do the actual sorting.) Test the program on the file Names.txt included in this lesson's download.

+   2. Write a program that removes duplicate entries from a text file. (Hint: Copy the program you built for Exercise 1. After you sort the array, run through the entries, copying them into a new list. If you see a duplicate entry, skip it and write it to the Console window.) Test the program on the file Names.txt included in this lesson's download.
```
```csharp
        // display the number of files with current extension
        resultsTextBox.AppendText(
            $"found {found[current]} {current} files." +
            Environment.NewLine);

        found.Clear(); // clear results for new search


    }

    // search directory using LINQ
    private void SearchDirectory(string folder)
    {
        // files contained in the directory
        string[] files = Directory.GetFiles(folder);

        // subdirectories in the directory
        string[] directories = Directory.GetDirectories(folder);

        // find all file extensions in this directory
        var extensions =
            from file in files
            group file by Path.GetExtension(file);

        foreach (var extension in extensions)
        {
            if (found.ContainsKey(extension.Key))
            {
                found[extension.Key] += extension.Count(); // update count
            }
            else
            {
                found[extension.Key] = extension.Count(); // add count
            }
        }

        // recursive call to search subdirectories
        foreach (var subdirectory in directories)
        {
            SearchDirectory(subdirectory);
        }
    }

    // allow user to delete backup files (.bak)
    private void CleanDirectory(string folder)
    {
        // files contained in the directory
        string[] files = Directory.GetFiles(folder);

        // subdirectories in the directory
        string[] directories = Directory.GetDirectories(folder);
```
```

Fig. 17.14 | Using LINQ to search directories and determine file types. (Part 2 of 3.)
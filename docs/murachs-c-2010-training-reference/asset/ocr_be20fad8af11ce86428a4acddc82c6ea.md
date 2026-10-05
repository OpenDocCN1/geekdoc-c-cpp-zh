# The exception classes for file I/O

| Class | Description |
|---|---|
| IOException | The base class for exceptions that are thrown during the processing of the stream, file, or directory. |
| DirectoryNotFoundException | Occurs when a directory or file path can't be found. |
| FileNotFoundException | Occurs when a file can't be found. |
| EndOfStreamException | Occurs when an application attempts to read beyond the end of a stream. |

# Code that uses exception classes

```
string dirPath = "C:\# 2010\Files\";
string filePath = dirPath + "Products.txt";
FileStream fs = null;
try {
    fs = new FileStream(filePath, FileMode.Open);
    // code that uses the file stream
    // to read and write data from the file
}
catch (FileNotFoundException) {
    MessageBox.Show(filePath + " not found.", "File Not Found");
}
catch (DirectoryNotFoundException) {
    MessageBox.Show(dirPath + " not found.", "Directory Not Found");
}
catch (IOException ex) {
    MessageBox.Show(ex.Message, "IOException");
}finally {
    if (fs != null)
        fs.Close();
}
```

# Description

+   - To catch any I/O exception, you can use the IOException.
- To catch specific I/O exceptions, you can use the exception classes that inherit the IOException class such as the three shown in this figure.

Figure 21-4 How to use the exception classes for file I/O
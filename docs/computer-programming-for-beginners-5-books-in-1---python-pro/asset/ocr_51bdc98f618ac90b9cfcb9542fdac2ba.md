```
file");
```

# Overwriting Text

If you need to overwrite a file, use the *File.WriteAllText()* method. The method will delete the text in the file and replace it with the one that you specify. This method can be used as demonstrated below:

```
// To open the file MyFile.txt and write the text into it. If the file does not exist, a new one will be created and opened for writing.
File.WriteAllText(@"C:\MyFile.txt", "This text will be used for replacing the current text in the file.");
```

With the Static File Class, one can perform various operations. This is demonstrated below:

```
//Check whether the file exists at the specified location or not
bool isFileExists = File.Exists(@"C:\MyFile.txt"); // it will return false
```

```
//Copy MyFile.txt as the new file MyNewFile.txt
File.Copy(@"C:\MyFile.txt", @"D:\MyNewFile.txt");
```

```
// Check when the file was lastly accessed
DateTime lastAccessTime = File.GetLastAccessTime(@"C:\MyFile.txt");
```

```
//get the last time the file was written
DateTime lastWriteTime = File.GetLastWriteTime(@"C:\MyFile.txt");
```

```
// Transfer the file to a new location
File.Move(@"C:\MyFile.txt", @"D:\MyFile.txt");
```

```
//Open file and returns FileStream for reading bytes from the file
FileStream fs = File.Open(@"D:\MyFile.txt", FileMode.OpenOrCreate);
```

```
//Open the file and return a StreamReader for reading a string from the file
StreamReader sr = File.OpenText(@"D:\MyFile.txt");
```

```
//Delete the file
File.Delete(@"C:\MyFile.txt");
```

The above shows that with the Static File class, it becomes easy for us to work
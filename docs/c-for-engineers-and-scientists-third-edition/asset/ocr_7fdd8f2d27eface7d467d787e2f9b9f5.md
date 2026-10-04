# 8.8 Chapter Summary

+   1. A data file is a collection of data stored together in an external storage medium under a common name.

+   2. A data file is connected to a file stream by using fstream's open() method. method connects a file's external name with an internal object name. After the file is opened, all subsequent accesses to the file require the internal object name.

+   3. A file can be opened in input or output mode. An opened output file stream creates a new data file or erases the data in an existing file. An opened input file stream makes existing file's data available for input. An error condition occurs if the file does not exist and can be detected by using the fail() method.

+   4. All file streams must be declared as objects of the istream or ofstream class. Therefore, a declaration similar to either of the following must be included with the declaration to open the file:

```
ifstream inFile;
ofstream outFile;
```

The stream object name inFile and outFile can be replaced with any user-selected object name.

+   5. In addition to any files opened in a function, the standard stream objects cin, cout, and cerr are declared and opened automatically when a program runs. cin is an input file stream used for data entry (usually from the keyboard), cout is an output file stream used for data display (usually on screen), and cerr is an output file stream used for displaying error messages (usually on screen).

+   6. Data files can be accessed randomly by using the seekg(), tellg(), seekp(), tellp() methods. The g versions of these methods are used to alter and query the file position marker for input file streams, and the p versions do the same for output file streams.

+   7. Table 8.6 lists class-supplied methods for file manipulation. The getline() method is defined in the string class, and all other methods are defined in the fstream class.

| Method Name | Description |
| --- | --- |
| get() | Extract the next character from the input stream and return it as an int. |
| get(chrVar) | Extract the next character from the input stream and assign it to chrVar. |
| getline(fileObject, strObj, termChar) | Extract the next string of characters from the input file stream and assign them to strObj until the specified terminating character is detected. If omitted, the default terminating character is a newline. |
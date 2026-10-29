3. File stream objects are created from the ifstream, ofstream, or fstream classes. File stream objects declared as ifstream objects are created as input streams, and file streams declared as ofstream objects are created as output streams. File stream objects declared as fstream objects must indicate the type of stream explicitly. To do this, use declaration statements similar to the following (inFile and outFile are user-selected object names):

```
ifstream inFile; or fstream(inFile, ios::in)
ofstream outFile; or fstream(outFile, ios::out)
```

4. After a file stream object is created, it's connected to a file by using an open() method. This method connects a file's external name with an internal stream object name. After the file is opened, all subsequent accesses to it require the internal stream object name.

5. An opened output file stream creates a new data file or erases the data in an existing opened file. An opened input file stream makes an existing file's data available for input. An error condition results if the file doesn't exist and can be detected by using the fail() method.

6. In addition to any files opened in a function, the standard stream objects cin, cout, and cerr are declared and opened automatically when a program runs. cin is an input file stream object used for data entry (usually from the keyboard), cout is an output file stream object used for data display (usually onscreen), and cerr is an output file stream object used for displaying system error messages (usually onscreen).

7. Data files can be accessed randomly by using the seekg(), seekp(), tellg(), and tellp() methods. The g versions of these methods are used to alter and query the file position marker for input file streams, and the p versions do the same for output file streams.

8. Table 9.5 lists class-supplied methods for file manipulation. The getline() method is defined in the string class, and all other methods are defined in the fstream class. These methods can be used by all ifstream and ofstream files.

# Table 9.5 File Manipulation Methods

| Method Name | Description |
|---|---|
| get() | Extract the next character from the input stream and return it as an int. |
| get(chrVar) | Extract the next character from the input stream and assign it to chrVar. |
| getline(fileObj, string, termChar) | Extract the next string of characters from the input file stream object and assign them to string until the specified terminating character is detected. If omitted, the default terminating character is a newline. |
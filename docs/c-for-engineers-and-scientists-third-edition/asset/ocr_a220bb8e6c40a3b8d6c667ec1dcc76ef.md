# Chapter 8 I/O Stream Objects and Methods

# Point of Information

Checking for a Successful Connection

You must check that the open() method established a connection between a file stream and an external file successfully because the open() call is a request to the OS that can fail for various reasons. Among these reasons is a request to open an existing file for reading that the OS can't locate or a request to open a file for output in a nonexistent folder. Failure to check the open() request can result in abnormal behavior or a program crash.

There are two types of coding for checking the return value. The most common method for checking that a failure didn't occur when attempting to use a file for input is the code shown in Program 8.2. It's better to distinguish the open() request from the check made via the fail() call and is repeated here for convenience:

```
inFile.open("prices.dat"); // request to open the file
if (inFile.fail()) // check for a failed connection

cout << "\nThe file was not successfully opened\n"
     << "\nPlease check that the file currently exists.\\n"
     << endl;
exit(1);
```

Similarly, the check made in Program 8.2 is typically included when a file is being opened in output mode. Alternatively, you might encounter programs that use fstream objects. When using fstream's open() method, two arguments are required: the file's name and an explicit mode indication. Using a fstream, the open request and check for an input file typically appear as follows:

```
inFile.open("external name", ios::in);
if (inFile.fail())
{

cout << "\nThe file was not successfully opened\n"
     << "\nPlease check that the file currently exists.\\n"
     << endl;
exit(1);
}
```

Many times, the conditional expression inFile.fail() is replaced by the equivalent expression !inFile.fail(). Although fstream and ofstream objects are always used in this book, be prepared to encounter styles that use fstream objects.
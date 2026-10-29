# Point of Information

# Using fstream Objects

In using ifstream and ofstream objects, the input or output mode is indicated by the object. Therefore, ifstream objects must be used for input, and ofstream objects must be used for output. Another means of creating file streams is with fstream objects that can be used for input or output, but this method requires an explicit mode designation. An fstream object is declared by using the following syntax:

```
fstream objectName;
```

When using the fstream class's open() method, two arguments are required: a file's external name and a mode indicator. Here are the permissible mode indicators; except for the first two, they can also be used when opening ifstream and ofstream objects:

| Indicator | Description |
|---|---|
| ios::in | Open a text file in input mode (not used for ifstream objects) |
| ios::out | Open a text file in output mode (not used for ofstream objects) |
| ios::app | Open a text file in append mode |
| ios::ate | Go to the end of the opened file |
| ios::binary | Open a binary file in input mode (default is text file) |
| ios::trunc | Delete file contents if it exists |
| ios::nocreate | If file doesn't exist, open fails |
| ios::noreplace | If file exists, open for output fails |

As with ofstream objects, an fstream object in output mode creates a new file and makes the file available for writing. If a file exists with the same name as a file opened for output, the old file is erased. For example, the following statement declares file1 as an object of type fstream

```
fstream file1;
```

The following statement attempts to open the text file prices.dat for output:

```
file1.open("prices.dat",ios::out);
```

After this file has been opened, the program accesses the file by using the internal object name file1, and the computer saves the file under the external name prices.dat.

An fstream file object opened in append mode means an existing file is available for data to be added to the end of the file. If the file opened for appending doesn't exist, a new file with the designated name is created and made available to receive output from the program. For example, the following statement declares file1 as an fstream object and attempts to open a text file named prices.dat and make it available for data to be added to the end of the file:

```
file1.open("prices.dat",ios::app);
```
# FIGURE G-7 Reading an integer from a text file

![](bbox=[0.058, 0.136, 0.835, 0.216])

![](bbox=[0.058, 0.276, 0.835, 0.346])

sequence 2, 3, 4 and then writes these characters to the file. For the output stream variable outFile and the integer variable x, the statement

```
outFile << x;
```

has the following effect:

+   Convert the value of x into a sequence of characters
+   Append this sequence of characters to the file
+   Position the file window just past the last character written

The following function reads and displays the contents of an entire text file of integers:

```
void echoFile(string fileName)
{
    ifstream inFile(fileName);
    int x = 0;
    while (inFile >> x)    // Read fails at end of file.
        cout << x << " ";
    cout << endl;
    inFile.close();
} // end echoFile
```

The function ignores the end-of-line symbols in the file and displays the integers all on one line.

Suppose that you want to display each line in the file regardless of the number of integers per line. You can use the peek and ignore methods to accomplish this. Note that you always pass a stream variable to a function as a reference argument.

```
// Skips blanks in a text file.
void skipBlanks(ifstream& inFile)
{
    while (inFile.peek() == ' ')  // While the current character is a blank:
        inFile.ignore(1);         // Ignore character, advance file window.
} // end skipBlanks
```

```
// Displays one line of a text file.
void echoLine(ifstream& inFile)
```
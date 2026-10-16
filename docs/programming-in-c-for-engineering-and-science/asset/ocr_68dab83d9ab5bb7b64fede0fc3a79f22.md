# 11.2.2.5 File Streams as Parameters

An example of a function that allowed a user to enter the name of an input file repeatedly until it was located and could be opened was given earlier in this section:

```
void getInputFile(ifstream & inStream)
{
    char response;
    do
    {
        cout << "Enter the name of the input file: ";
        string inputFileName;
        getline(cin, inputFileName);

        inStream.open(inputFileName.data());

        if (inStream.is_open()) break;

        cerr << "\n***Unable to open << inputFileName
             << "\nTry again (Y or N)? ";
        cin >> response;
    }
    while (response != 'N' && response != 'n');
}
```

Note that the parameter inStream is of type ifstream and is a reference parameter, which must always be the case; parameters corresponding to file stream arguments must be reference parameters because

+   - Reading from an ifstream object alters its read position; and
+   - Writing to an ofstream object alters its write position.

If the file stream parameters were not reference parameters, these changes would not have been propagated back to main() or another function that calls this function.

# 11.2.3 Summary

The following points summarize some of the important points regarding file I/O in C++.

+   - A text file stores characters on a secondary memory device.
+   - Input from or output to a file from a program can only be done indirectly through a file stream—an abstract conduit between the program and the file.
+   - A file stream can be connected to a file by using open() or the initialization-at-declaration mechanism.
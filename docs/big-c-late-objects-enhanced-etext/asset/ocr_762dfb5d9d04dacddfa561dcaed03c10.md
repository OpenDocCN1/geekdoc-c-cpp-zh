When you specify the file name as a string literal, and the name contains backslash characters (as in a Windows filename), you must supply each backslash twice:

```
in_file.open("c:\\homework\\input.dat");
```

Recall that a single backslash inside a string literal is an escape character that is combined with another character to form a special meaning, such as \n for a newline character. The \\ combination denotes a single backslash.

In older versions of C++, you must be careful when opening a file with a name that is stored in a string variable. Use the c_str function to convert the C++ string to a C string:

```
cout << "Please enter the file name:";
string filename;
cin >> filename;
ifstream in_file;
in_file.open(filename.c_str()); // Before C++ 11
```

If it is not possible to open a stream, then the stream variable is set to a failed state. You can test for that condition:

```
in_file.open("input.dat");
if (in_file.fail())
{
    cout << "Cannot read from input.dat" << endl;
}
else
{
    Read input.
}
```

When the program ends, all streams that you have opened will be automatically closed. You can also manually close a stream with the close member function:

```
in_file.close();
```

Manual closing is only necessary if you want to use the stream variable again to process another file.

# 8.1.2 Reading from a File

Read from a file stream with the same operations that you use with cin.

Reading data from a file stream is completely straightforward: You simply use the same functions that you have always used for reading from cin:

```
string name;
double value;
in_file >> name >> value;
```

The fail function tells you whether input has failed. You have already used this function with cin, to check for errors in console input. File streams behave in the same way. When you try to read a number from a file, and the next data item is not a properly formatted number, then the stream fails. After reading data, you should test for success before processing:

```
if (!in_file.fail())
{
    Process input.
}
```

When you read input from a file, number format errors are not the only reason for failure. Suppose you have consumed all of the data contained in a file and try to read
File names can contain directory path information, such as
`~/homework/input.dat` (UNIX)
`c:\homework\input.dat` (Windows)

When you specify the file name as a string literal, and the name contains backslash characters (as in a Windows filename), you must supply each backslash *twice*:

```
```cpp
in_file.open("c:\\homework\\input.dat");
```
```

Recall that a single backslash inside a string literal is an *escape character* that is combined with another character to form a special meaning, such as `\n` for a newline character. The `\\` combination denotes a single backslash.

If you want to pass a name that is stored in a string variable, use the `c_str` function to convert the C++ string to a C string:

```
```cpp
cout << "Please enter the file name:";
string filename;
cin >> filename;
ifstream in_file;
in_file.open(filename.c_str());
```
```

When the program ends, all streams that you have opened will be automatically closed. You can also manually close a stream with the `close` member function:

```
```cpp
in_file.close();
```
```

Manual closing is only necessary if you want to use the stream variable again to process another file.

# ## 8.1.2 Reading from a File

> > Read from a file stream with the same operations that you use with `cin`.

Reading data from a file stream is completely straightforward: You simply use the same functions that you have always used for reading from `cin`:

```
```cpp
string name;
double value;
in_file >> name >> value;
```
```

The `fail` function tells you whether input has failed. You have already used this function with `cin`, to check for errors in console input. File streams behave in the same way. When you try to read a number from a file, and the next data item is not a properly formatted number, then the stream fails. After reading data, you should test for success before processing:

```
```cpp
if (!in_file.fail())
{
   Process input.
}
```
```

Alternatively, you can use the fact that the `>>` operator returns a “not failed” condition, allowing you to combine an input statement and a test:

```
```cpp
if (in_file >> name >> value)
{
   Process input.
}
```
```

When you read input from a file, number format errors are not the only reason for failure. Suppose you have consumed all of the data contained in a file and try to read more items. A file stream enters the failed state, whereas `cin` would just wait for more
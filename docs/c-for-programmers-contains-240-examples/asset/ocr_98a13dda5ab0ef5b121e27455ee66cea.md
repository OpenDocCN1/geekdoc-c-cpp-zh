```
```cpp
// display single record from file
void outputLine( int account, const string name, double balance )
{
   cout << left << setw( 10 ) << account << setw( 13 ) << name
        << setw( 7 ) << setprecision( 2 ) << right << balance << endl;
} // end function outputLine
```
```

| Account | Name  | Balance |
|---:|---|---:|
| 100 | Jones | 24.98 |
| 200 | Doe | 345.67 |
| 300 | White | 0.00 |
| 400 | Stone | -42.16 |
| 500 | Rich | 224.62 |

Objects of class `ifstream` are opened for input by default. We could have used the statement

```cpp
ifstream inClientFile( "clients.dat" );
```

to open `clients.dat` for input. Just as with an `ofstream` object, an `ifstream` object can be created without opening a specific file, because a file can be attached to it later.

The program uses the condition `!inClientFile` to determine whether the file was opened successfully before attempting to retrieve data from the file. Line 48 reads a set of data (i.e., a record) from the file. After the preceding line is executed the first time, account has the value 100, name has the value "Jones" and balance has the value 24.98. Each time line 48 executes, it reads another record from the file into the variables account, name and balance. Line 49 displays the records, using function `outputLine` (lines 55–59), which uses parameterized stream manipulators to format the data for display. When the end of file has been reached, the implicit call to `operator void *` in the `while` condition returns the null pointer (which converts to the bool value `false`), the `ifstream` destructor function closes the file and the program terminates.

To retrieve data sequentially from a file, programs normally start reading from the beginning of the file and read all the data consecutively until the desired data is found. It might be necessary to process the file sequentially several times (from the beginning of the file) during the execution of a program. Both `istream` and `ostream` provide member functions for repositioning the *file-position pointer* (the byte number of the next byte in the file to be read or written). These member functions are `seekg` (“seek get”) for `istream` and `seekp` (“seek put”) for `ostream`. Each `istream` object has a “get pointer,” which indicates the byte number in the file from which the next input is to occur, and each `ostream` object has a “put pointer,” which indicates the byte number in the file at which the next output should be placed. The statement

```cpp
inClientFile.seekg( 0 );
```

repositions the file-position pointer to the beginning of the file (location 0) attached to `inClientFile`. The argument to `seekg` normally is a long integer. A second argument can be specified to indicate the *seek direction*, which can be `ios::beg` (the default) for positioning relative to the beginning of a stream, `ios::cur` for positioning relative to the current position.
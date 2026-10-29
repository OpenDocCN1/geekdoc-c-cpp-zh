
## I/O Streams and Data Files

### Point of Information

### Checking for a Successful Connection

You should always check that the `open()` method established a connection between a file stream and an external file successfully because the `open()` call is a request to the OS that can fail for various reasons. Chief among these reasons is a request to open an existing file for reading that the OS can’t locate or a request to open a file for output in a nonexistent folder. If the OS can’t satisfy the open request, you need to know about it and terminate your program. Failure to do so can result in abnormal program behavior or a program crash.

The most common method for checking that a failure didn’t occur when attempting to use a file for input is the one coded in Program 9.1, which uses separate calls to the `open()` and `fail()` methods. Similarly, the check made in Program 9.2 is typically included when a file is being opened in output mode.

Alternatively, you might encounter programs that use `fstream` objects in place of `ifstream` and `ofstream` objects (see the previous Point of Information box). Except for the `open()` method (which requires two arguments: a file’s external name and a mode indicator), the `fail()` method is called the same as in Program 9.1 or Program 9.2.

In all these cases, you can substitute the expression `!inFile` for the conditional expression `inFile.fail()`.

- 4. **(Practice)** Enter and run Program 9.1 on your computer.
- 5. **(Practice)** Enter and run Program 9.2 on your computer.
- 6. **(Practice)**
  - a. Enter and run Program 9.3a on your computer.
  - b. Add a `close()` method to Program 9.3a, and then run the program.
- 7. **(Practice)**
  - a. Enter and run Program 9.3b on your computer.
  - b. Add a `close()` method to Program 9.3b, and then run the program.
- 8. **(Practice)** Using the reference manuals provided with your computer’s OS, determine the following:
  - a. The maximum number of characters the computer can use to name a file for storage
  - b. The maximum number of data files that can be open at the same time
- 9. **(Practice)** Is calling a saved C++ program a file appropriate? Why or why not?

10. (Practice) a. Write declaration and open statements to link the following external filenames to their corresponding internal filenames. Use only ifstream and ofstream objects.

| External Filename | Internal Filename | Mode |
|---|---|---|
| coba.mem | memo | binary and output |
| coupons.bnd | coups | binary and append |
| prices.dat | priFile | binary and input |

b. Redo Exercise 10a, using only fstream objects.

c. Write close() statements for each file opened in Exercise 10a.

## 9.2 Reading and Writing Text Files

Reading or writing text files involves almost the identical operations for reading input from the keyboard and writing data to the screen. For writing to a file, the cout object is replaced by the ofstream object name declared in the program. For example, if outFile is declared as an object of type ofstream, the following output statements are valid:

```
outFile << 'a';
outFile << "Hello World!";
outFile << descrip << ' ' << price;
```

The filename in each of these statements, in place of cout, directs the output stream to a specific file instead of to the screen. Program 9.4 shows using the insertion operator, <<, to write a list of descriptions and prices to a file.

When Program 9.4 runs, the prices.dat file is created and saved by the computer as a text file (the default file type) in the same folder where the program is located. It's a sequential file consisting of the following data:

```
Mats 39.95
Bulbs 3.22
Fuses 1.08
```

The actual storage of characters in the file depends on the character codes the computer uses. Although only 30 characters appear to be stored in the file—corresponding to the descriptions, blanks, and prices written to the file—the file contains 36 characters.

### Program 9.4

```
#include <iostream>
#include <fstream>
#include <cstdlib>  // needed for exit()
#include <string>  // needed for the string class
#include <iomanip>  // needed for formatting
using namespace std;

int main()
{
    string filename = "prices.dat";  // put the filename up front
    ofstream outFile;

    outFile.open(filename.c_str());

    if (outFile.fail())
    {
        cout << "The file was not successfully opened" << endl;
        exit(1);
    }

    // set the output file stream formats
    outFile << setiosflags(ios::fixed)
            << setiosflags(ios::showpoint)
            << setprecision(2);

    // send data to the file
    outFile << "Mats " << 39.95 << endl
            << "Bulbs " << 3.22 << endl
            << "Fuses " << 1.08 << endl;

    outFile.close();
    cout << "The file " << filename
         << " has been successfully written." << endl;

    return 0;
}
```

The extra characters consist of the newline escape sequence at the end of each line created by the endl manipulator, which is created as a carriage return character (cr) and linefeed (lf). Assuming characters are stored with the ASCII code, the prices.dat file is physically stored as shown in Figure 9.2. For convenience, the character corresponding to each hexadecimal code is listed below the code. A code of 20 represents the blank character. Additionally,

### Point of Information

### Formatting Text File Output Stream Data

Output file streams can be formatted in the same manner as the cout standard output stream. For example, if an output stream named `fileOut` has been declared, the following statement formats all data inserted in the `fileOut` stream in the same way these manipulators work for the cout stream:

```
fileOut << setiosflags(ios::fixed)
        << setiosflags(ios::showpoint)
        << setprecision(2);
```

The first manipulator parameter, `ios::fixed`, causes the stream to output all numbers as though they were floating-point values. The next parameter, `ios::showpoint`, tells the stream to always provide a decimal point. Therefore, a value such as 1.0 appears as 1.0, not as 1, which doesn't contain a decimal point. Finally, the `setprecision()` manipulator tells the stream to display two decimal values after the decimal point. Therefore, the number 1.0, for example, appears as 1.00.

Instead of using manipulators, you can use the stream methods `setf()` and `precision()`. For example, the previous formatting can be accomplished with the following code:

```
fileOut.setf(ios::fixed);
fileOut.setf(ios::showpoint);
fileOut.precision(2);
```

The style you select is a matter of preference. In both cases, the formats need be specified only once and remain in effect for every number subsequently inserted in the file stream.

C and C++ append the low-value hexadecimal byte 0x00 as the end-of-file (EOF) sentinel when the file is closed. This EOF sentinel is never counted as part of the file.

```
4D 61 74 73 20 33 39 2E 39 35 00 0A 42 75 6C 62 73 20
 M  a  t  s     3  9  .  9  5 cr 1f  B  u  l  b  s

33 2E 32 32 00 0A 46 75 73 65 73 20 31 2E 30 38 0D 0A
 3  .  2  2 cr 1f  F  u  s  e  s     1  .  0  8 cr 1f
```

**Figure 9.2**  The prices.dat file as stored by the computer

## I/O Streams and Data Files

### Point of Information

### Writing One Character at a Time with the `put()` Method

All output streams have access to the `fstream` class’s `put()` method, which permits character-by-character output to a stream. This method works in the same manner as the character insertion operator, `<<`. The syntax of this method call is the following:

```
ofstreamName.put(characterExpression);
```

The *characterExpression* can be a character variable or literal value. For example, the following code can be used to output an 'a' to the screen:

```
cin.put('a');
```

In a similar manner, if `outFile` is an `ofstream` object that has been opened, the following code outputs the character value in the character variable named `keycode` to the `outFile` stream:

```
char keycode;
.
.
outFile.put(keycode);
```

### Reading from a Text File

Reading data from a text file is almost identical to reading data from a standard keyboard, except the `cin` object is replaced by the `ifstream` object declared in the program. For example, if `inFile` is declared as an object of type `ifstream` that’s opened for input, the following statement reads the next two items in the file and stores them in the variables `descrip` and `price`:

```
inFile >> descrip >> price;
```

The file stream name in this statement, in place of `cin`, directs the input to come from the file stream rather than the keyboard. Table 9.3 lists other methods that can be used for stream input. When called, these methods must be preceded by a stream object name.

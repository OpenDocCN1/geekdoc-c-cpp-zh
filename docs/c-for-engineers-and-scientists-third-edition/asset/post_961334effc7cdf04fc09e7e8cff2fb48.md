
# Point of Information

Using fstream Objects (continued)

Finally, an fstream object opened in input mode means an existing external file has been connected and its data is available as input. For example, the following statement declares file to be of type fstream and attempts to open a text file named prices.dat for input:

```
file1.open("prices.dat", ios::in);
```

The indicators can be combined by the bitwise OR operator, | (see Section 15.2). For example, the following statement opens the file stream, which can be an fstream or a binary stream:

```
file1.open("prices.dat", ios::in | ios::binary);
```

If the mode indicator is omitted as the second argument for an fstream object, the stream is opened as a text file by default; if the mode indicator is omitted for an fstream object, the stream is opened as a output file by default.

The following is a sample output of Program 8.3b:

```
Please enter the name of the file you wish to open: foobar
The file named foobar was not successfully opened
Please check that the file currently exists.
```

Closing a File is closed by the close() method. This method breaks the connection between the file's external name and the file stream object, which can be used for another file. Examine the following statement, which closes the inFile stream's connection to its current file:

```
inFile.close();
```

As indicated, the close() method takes no argument. Because all computers have a limit on the maximum number of files that can be open, closing files that no longer needed makes sense. Any open files existing at the end of execution are closed automatically by the OS.

# EXERCISES 8.1

1. (Practice) Write declaration and open statements that link the following filenames to their corresponding object names. All files are text-based.

| External Filename | Internal Object Name | Mode |
| :--- | :--- | :--- |
| coba.mem | memo | output |
| book.let | letter | output |
| coupons.dat | coups | append |
| yield.dat | yield | append |
| prices.dat | priFile | input |
| rates.dat | rates | input |

2. (Practice) a. Write a set of two statements that declares the following objects as ifstream objects, and then opens them as text files: in.txt, prices.txt, coupons.dat, and exper.dat. b. Rewrite the two statements for Exercise 2a, using a single statement.

3. (Practice) a. Write a set of two statements that declares the following objects as ofstream objects, and then opens them as text files: out.txt, rates.txt, distance.txt, and file.txt. b. Rewrite the two statements for Exercise 3a, using a single statement.

4. (Practice) Enter and execute Program 8.1.

5. (Practice) Enter and execute Program 8.2.

6. (Practice) a. Enter and execute Program 8.3a. b. Add a close() method to Program 8.3a, and then execute the program.

7. (Practice) a. Enter and execute Program 8.3b. b. Add a close() method to Program 8.3b, and then execute the program.

8. (Practice) Using the reference manuals provided with your computer's OS, determine the following:
a. The maximum number of characters the computer can use to name a file for storage
b. The maximum number of data files that can be open at time

9. (Practice) Would it be appropriate to call a saved C++ program? Why or not?

10. (Practice) a. Write declaration and open statements to link the following external files to their corresponding object names. Use only fstream and ofstream objects.

| External Name | Internal Object Name | Mode |
| :--- | :--- | :--- |
| coba.mem | memo | binary and output |
| coupons.dat | coups | binary and append |
| prices.dat | priFile | binary and input |

b. Redo Exercise 10a, using only fstream objects. c. Write close statements for each file opened in 10a.

# Chapter 8 I/O Stream Objects and Methods

## Point of Information Checking for a Successful Connection

You must check that the open() method established a connection between a file stream and an external file successfully because the open() call is a request to the OS that can fail for various reasons. Among these reasons is a request to open an existing file for reading that the OS can't locate or a request to open a file for output in a nonexistent folder. Failure to check the open() request can result in abnormal behavior or a program crash.

There are two types of coding for checking the return value. The most common method for checking that a failure didn't occur when attempting to use a file for input is the code shown in Program 8.2. It's better to distinguish the open() request from the check made via the fail() call and is repeated here for convenience:

```
inFile.open("prices.dat"); // request to open the file
if (inFile.fail()) // check for a failed connection

    cout << "\nThe file was not successfully opened\n"
         << "\nPlease check that the file currently exists.\n"
         << endl;
exit(1);
```

Similarly, the check made in Program 8.2 is typically included when a file is being opened in output mode. Alternatively, you might encounter programs that use fstream objects. When using fstream's open() method, two arguments are required: the file's name and an explicit mode indication. Using a fstream, the open request and check for an input file typically appear as follows:

```
inFile.open("external name", ios::in);
if (inFile.fail())
{

    cout << "\nThe file was not successfully opened\n"
         << "\nPlease check that the file currently exists.\n"
         << endl;
exit(1);
}
```

Many times, the conditional expression inFile.fail() is replaced by the equivalent expression !inFile.fail(). Although fstream and ofstream objects are always used in this book, be prepared to encounter styles that use fstream objects.

## 8.2 Reading and Writing Character-Based Files

Reading or writing character-based files involves almost the identical operations for reading input from the keyboard and writing data to the screen. For writing to a file, the cout object is replaced by the ofstream object named in the program. For example, if outFile is valid as an object of type ofstream, the following output statements are valid:

```
outFile << 'a';
out << "Hello World";
outFile << desc << ' ' << price;
```

The filename in all of these statements, in place of cout, directs the output to the specific device (the screen). Program 8.4 shows using the insertion operator, <<, to write a list of descriptions and prices to a file.

```
```cpp
#include <iostream>
#include <fstream>
#include <cstdlib>
#include <string>
#include <iomanip>

using namespace std;

int main()
{
    string filename = "prices.dat";
    ofstream outFile;

    outFile.open(filename.c_str());

    if (outFile.fail()) {
        cout << "The file was not opened" << endl;
        exit(1);
    }

    // set the output formats
    outFile << setflags(ios::fixed)
           << setflags(ios::showpoint)
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

When Program 8.4 runs, the prices.dat file is created and saved by the computer as a text file. Its sequential file consisting of the following data:

Mats 39.95
Bulbs 3.22
Fuses 1.08

The actual storage of characters in the file depends on the character codes the computer uses. Using only 30 characters to be stored in the file—corresponding to the descriptions, blanks, and prices—the file contains 36 characters. The extra characters consist of the newline escape sequence at the end of each line created by the endl manipulator, which is created as a carriage return (cr) and linefeed (lf). Assuming characters are stored with the ASCII code, the prices.dat file is physically stored as in Figure 8.2. For convenience, the character corresponding to each hexadecimal code below represents the character. Additionally, C and C++ append the lowvalue byte 0x00, as the end-of-file (EOF) sentinel when the file is closed. This EOF sentinel is never counted as part of the file.

| Hexadecimal Code | Character |
| :--- | :--- |
| 4D 61 74 73 20 33 39 22 39 35 30 0D 0A 42 75 6C 62 73 20 | M a t s 3 9 . 9 5 cr 1f B u l b s |
| 33 2E 32 32 0D 0A 46 75 73 65 21 2E 30 38 0D 0A | 3 . 2 cr 1f F u s e s 1 . 0 8 cr 1f |

**Figure 8.2** prices.dat file as stored by the computer

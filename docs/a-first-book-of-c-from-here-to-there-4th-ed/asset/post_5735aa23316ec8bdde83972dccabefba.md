
a file exists with the same name as a file opened in output mode, the old file is erased (overwritten) and all its data is lost.

When opening a file for input or output, good programming practice requires checking that the connection has been established before attempting to use the file. You can do this with the fail() method, which returns a true value if the file was opened unsuccessfully (that is, it's true the open failed) or a false value if the open succeeded. Typically, the fail() method is used in code similar to the following, which attempts to open the prices.dat file for input, checks that a valid connection was made, and reports an error message if the file wasn't opened for input successfully:

```
ifstream inFile; // any object name can be used here
inFile.open("prices.dat"); // open the file

// check that the connection was opened successfully
if (inFile.fail())
{
    cout << "\nThe file was not successfully opened"
         << "\n Please check that the file currently exists."
         << endl;
    exit(1);
}
```

If the fail() method returns a true, indicating that the open failed, this code displays an error message. In addition, the exit() function, which is a request to the OS to end program execution immediately, is called. The cstdlib header function must be included in any program using exit(), and exit()'s single-integer argument is passed directly to the OS for any further program action or user inspection. Throughout the remainder of the book, this type of error checking is included whenever a file is opened. (Section 14.4 shows how to use exception handling for the same type of error checking.) In addition to the fail() method, C++ provides three other methods, listed in Table 9.2, for detecting a file's status.

## Table 9.2 File Status Methods

| Prototype | Description |
|---|---|
| fail() | Returns a Boolean true if the file hasn't been opened successfully; otherwise, returns a Boolean false value. |
| eof() | Returns a Boolean true if a read has been attempted past the end of file; otherwise, returns a Boolean false. The value becomes true only when the first character after the last valid file character is read. |

## Table 9.2 File Status Methods (continued)

| Prototype | Description |
|---|---|
| good() | Returns a Boolean true while the file is available for program use. Returns a Boolean false if a read has been attempted past the end of file. The value becomes false only when the first character after the last valid file character is read. |
| bad() | Returns a Boolean true if a read has been attempted past the end of file; otherwise, returns a false. The value becomes true only when the first character after the last valid file character is read. |

Program 9.1 shows the statements required to open a file for input, including an error-checking routine to ensure that the open was successful. A file opened for input is said to be in read mode or input mode. (These two terms are synonymous.)

## Program 9.1

```
#include <iostream>
#include <fstream>
#include <cstdlib>  // needed for exit()
using namespace std;
int main()
{
    ifstream inFile;
    inFile.open("prices.dat");  // open the file with the
                                // external name prices.dat
    if (inFile.fail())  // check for a successful open
    {
        cout << "\nThe file was not successfully opened"
             << "\n Please check that the file currently exists."
             << endl;
        exit(1);
    }
    cout << "\nThe file has been successfully opened for reading."
         << endl;
    // statements to read data from the file are placed here
    return 0;
}
```

A sample run of Program 9.1 produces the following output:

```
The file has been successfully opened for reading.
```

A different check is required for output files (files that are written to) because if a file exists with the same name as the file to be opened in output mode, the existing file is erased and all its data is lost. To avoid this situation, the file is first opened in input mode to see whether it exists. If it does, the user is given the choice of permitting it to be overwritten when it's opened in output mode. The code to perform this check is shaded in Program 9.2.

## Program 9.2

```
#include <iostream>
#include <fstream>
#include <cstdlib>  // needed for exit()
using namespace std;

int main()
{
    ifstream inFile;
    ofstream outFile;
    char response;
    inFile.open("prices.dat");  // attempt to open the file for input

if (!inFile.fail())  // if it doesn't fail, the file exists
{
    cout << "A file by the name prices.dat exists.\n"
         << "Do you want to continue and overwrite it\n"
         << "with the new data (Y or N): ";
    cin >> response;
    if (tolower(response) == 'n')
    {
        cout << "The existing file will not be overwritten." << endl;
        exit(1);  //terminate program execution
    }
}

outFile.open("prices.dat");  // now open the file for writing

if (inFile.fail()) // check for a successful open
{
    cout << "\nThe file was not successfully opened" << endl;
    exit(1);
}

cout << "The file has been successfully opened for output." << endl;

// statements to write to the file would be placed here

return 0;
}
```

The following two runs were made with Program 9.2:

```
A file by the name prices.dat exists.
Do you want to continue and overwrite it
with the new data (y or n): n
The existing file will not be overwritten.
```

and

```
A file by the name prices.dat exists.
Do you want to continue and overwrite it
with the new data (y or n): y
The file has been successfully opened for output.
```

Although Programs 9.1 and 9.2 can be used to open an existing file for reading and writing, both programs lack statements to perform a read or write and close the file. These topics are discussed shortly. Before moving on, however, note that it's possible to combine the declaration of an ifstream or ofstream object and its associated open() statement into one statement. For example, examine these two statements in Program 9.1:

```
ifstream inFile;
inFile.open("prices.dat");
```

They can be combined into a single statement:

```
ifstream inFile("prices.dat");
```

## Embedded and Interactive Filenames

Programs 9.1 and 9.2 have two problems:

- The external filename is embedded in the program code.
- There's no provision for a user to enter the filename while the program is running.

As both programs are written, if the filename is to change, a programmer must modify the external filename embedded in the call to open() and recompile the program. Both these problems can be avoided by assigning the filename to a string variable.

## Point of Information

## Using C-Strings as Filenames

If you use a C-string (which is simply a one-dimensional array of characters) to store an external filename, you must specify the C-string's maximum length in brackets immediately after it's declared. For example, examine the following declaration:

```
char filename[21] = "prices.dat";
```

The number in brackets (21) is one more than the maximum number of characters that can be assigned to the variable filename because the compiler adds an end-of-string character to terminate the string. Therefore, the string value "prices.dat", which consists of 10 characters, is actually stored as 11 characters. In this example, the maximum value that can be assigned to the string variable filename is a string value consisting of 20 characters.

In declaring and initializing a string variable for use in an open() method, the variable must represent a C-string, a one-dimensional array of characters terminated with a null character. (See the Point of Information "Using C-Strings as Filenames" for precautions when using a C-string.) A safer alternative, as it doesn't require specifying a character count—and one used throughout this book—is to use an object created from the string class. To do this, add an #include <string> directive, declare an object to be of this class, and convert the object to a C-string in the open() method call by using the string class method c_str().

After a string variable is declared to store a filename, it can be used in one of two ways. First, as shown in Program 9.3a, it can be used to avoid embedding a filename in the open() method by placing the declaration statement at the top of a program. This method also clearly identifies the file's name up front.

## Program 9.3a

```
#include <iostream>
#include <fstream>
#include <cstdlib>  // needed for exit()
#include <string>   // needed for the string class
using namespace std;

int main()
{
    string filename = "prices.dat";  // create and initialize a string object
                                     // with the filename at the top of the
                                     // main() function
    ifstream inFile;
```

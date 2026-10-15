
Figure 17.4 creates a sequential file that might be used in an accounts-receivable system to help manage the money owed by a company’s credit clients. For each client, the program obtains the client’s account number, name and balance (i.e., the amount the client owes the company for goods and services received in the past). The data obtained for each client constitutes a record for that client. The account number serves as the record key; that is, the program creates and maintains the file in account number order. This program assumes the user enters the records in account number order. In a comprehensive

```
// Fig. 17.4: Fig17_04.cpp
// Create a sequential file.
#include <iostream>
using std::cerr;
using std::cin;
using std::cout;
using std::endl;
using std::ios;

#include <fstream> // file stream
using std::ofstream; // output file stream

#include <cstdlib>
using std::exit; // exit function prototype

int main()
{
    // ofstream constructor opens file
    ofstream outClientFile( "clients.dat", ios::out );

    // exit program if unable to create file
    if ( !outClientFile ) // overloaded ! operator
    {
        cerr << "File could not be opened" << endl;
        exit( 1 );
    } // end if

    cout << "Enter the account, name, and balance." << endl
         << "Enter end-of-file to end input.\n?";

    int account;
    char name[ 30 ];
    double balance;

    // read account, name and balance from cin, then place in file
    while ( cin >> account >> name >> balance )
    {
        outClientFile << account << ' ' << name << ' ' << balance << endl;
        cout << "?";
    } // end while

    return 0; // ofstream destructor closes file
} // end main
```

Fig. 17.4 | Creating a sequential file. (Part 1 of 2.)

```
Enter the account, name, and balance.
Enter end-of-file to end input.
? 100 Jones 24.98
? 200 Doe 345.67
? 300 White 0.00
? 400 Stone -42.16
? 500 Rich 224.62
? ^Z
```

Fig. 17.4 | Creating a sequential file. (Part 2 of 2.)

accounts receivable system, a sorting capability would be provided for the user to enter records in any order—the records then would be sorted and written to the file.

Let us examine this program. As stated previously, files are opened by creating ifstream, ofstream or fstream objects. In Fig. 17.4, the file is to be opened for output, so an ofstream object is created. Two arguments are passed to the object’s constructor—the filename and the file-open mode (line 19). For an ofstream object, the file-open mode can be either ios::out to output data to a file or ios::app to append data to the end of a file (without modifying any data already in the file). Existing files opened with mode ios::out are truncated—all data in the file is discarded. If the specified file does not yet exist, then the ofstream object creates the file, using that filename.

Line 19 creates an ofstream object named outClientFile associated with the file clients.dat that is opened for output. The arguments "clients.dat" and ios::out are passed to the ofstream constructor, which opens the file—this establishes a “line of communication” with the file. By default, ofstream objects are opened for output, so line 19 could have used the alternate statement

```
ofstream outClientFile( "clients.dat" );
```

to open clients.dat for output. Figure 17.5 lists the file-open modes.

## Common Programming Error 17.1

> Use caution when opening an existing file for output (ios::out), especially when you want to preserve the file’s contents, which will be discarded without warning.

| Mode | Description |
|------|-------------|
| ios::app | Append all output to the end of the file. |
| ios::ate | Open a file for output and move to the end of the file (normally used to append data to a file). Data can be written anywhere in the file. |
| ios::in | Open a file for input. |
| ios::out | Open a file for output. |
| ios::trunc | Discard the file’s contents if they exist (this also is the default action for ios::out). |
| ios::binary | Open a file for binary (i.e., nontext) input or output. |

Fig. 17.5 | File open modes.

An ofstream object can be created without opening a specific file—a file can be attached to the object later. For example, the statement

```
ofstream outClientFile;
```

creates an ofstream object named outClientFile. The ofstream member function open opens a file and attaches it to an existing ofstream object as follows:

```
outClientFile.open( "clients.dat", ios::out );
```

## Common Programming Error 17.2

> Not opening a file before attempting to reference it in a program will result in an error.

After creating an ofstream object and attempting to open it, the program tests whether the open operation was successful. The if statement in lines 22–26 uses the overloaded ios operator member function operator! to determine whether the open operation succeeded. The condition returns a true value if either the failbit or the badbit is set for the stream on the open operation. Some possible errors are attempting to open a nonexistent file for reading, attempting to open a file for reading or writing without permission, and opening a file for writing when no disk space is available.

If the condition indicates an unsuccessful attempt to open the file, line 24 outputs the error message "File could not be opened", and line 25 invokes function exit to terminate the program. The argument to exit is returned to the environment from which the program was invoked. Argument 0 indicates that the program terminated normally; any other value indicates that the program terminated due to an error. The calling environment (most likely the operating system) uses the value returned by exit to respond appropriately to the error.

Another overloaded ios operator member function—operator void *—converts the stream to a pointer, so it can be tested as 0 (i.e., the null pointer) or nonzero (i.e., any other pointer value). When a pointer value is used as a condition, C++ converts a null pointer to the bool value false and converts a non-null pointer to the bool value true. If the failbit or badbit (see Chapter 15) has been set for the stream, 0 (false) is returned. The condition in the while statement of lines 36–40 invokes the operator void * member function on cin implicitly. The condition remains true as long as neither the failbit nor the badbit has been set for cin. Entering the end-of-file indicator sets the failbit for cin. The operator void * function can be used to test an input object for end-of-file instead of calling the eof member function explicitly on the input object.

If line 19 opened the file successfully, the program begins processing data. Lines 28–29 prompt the user to enter either the various fields for each record or the end-of-file indicator when data entry is complete. Figure 17.6 lists the keyboard combinations for entering end-of-file for various computer systems. Line 36 extracts each set of data and determines whether end-of-file has been entered. When end-of-file is encountered or bad data is entered, operator void * returns the null pointer (which converts to the bool value false) and the while statement terminates. The user enters end-of-file to inform the program to process no additional data. The end-of-file indicator is set when the user enters the end-of-file key combination. The while statement loops until the end-of-file indicator is set.

| Computer system | Keyboard combination |
|---|---|
| UNIX/Linux/Mac OS X | <Ctrl-d> (on a line by itself) |
| Microsoft Windows | <Ctrl-z> (sometimes followed by pressing Enter) |
| VAX (VMS) | <Ctrl-z> |

Fig. 17.6 | End-of-file key combinations for various popular computer systems.

Line 38 writes a set of data to the file clients.dat, using the stream insertion operator << and the outClientFile object associated with the file at the beginning of the program. The data may be retrieved by a program designed to read the file (see Section 17.5). Note that, because the file created in Fig. 17.4 is simply a text file, it can be viewed by any text editor.

Once the user enters the end-of-file indicator, main terminates. This implicitly invokes the outClientFile object’s destructor function, which closes the clients.dat file. You also can close the ofstream object explicitly, using member function close in the statement

```
outClientFile.close();
```

## Performance Tip 17.1

> Closing files explicitly when the program no longer needs to reference them can reduce resource usage (especially if the program continues execution after closing the files).

In the sample execution for the program of Fig. 17.4, the user enters information for five accounts, then signals that data entry is complete by entering end-of-file (^Z is displayed for Microsoft Windows). This dialog window does not show how the data records appear in the file. To verify that the program created the file successfully, the next section shows how to create a program that reads this file and prints its contents.

## 17.5 Reading Data from a Sequential File

Files store data so it may be retrieved for processing when needed. The previous section demonstrated how to create a file for sequential access. In this section, we discuss how to read data sequentially from a file.

Figure 17.7 reads records from the clients.dat file that we created using the program of Fig. 17.4 and displays the contents of these records. Creating an ifstream object opens a file for input. The ifstream constructor can receive the filename and the file open mode as arguments. Line 31 creates an ifstream object called inClientFile and associates it with the clients.dat file. The arguments in parentheses are passed to the ifstream constructor function, which opens the file and establishes a “line of communication” with the file.

## Good Programming Practice 17.1

> Open a file for input only (using ios::in) if the file’s contents should not be modified. This prevents unintentional modification of the file’s contents and is an example of the principle of least privilege.

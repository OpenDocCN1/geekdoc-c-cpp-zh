
Returns a nonzero value to indicate a serious I/O error. This is the same as setting the badbit error state. Do not continue I/O operations on the stream in this situation.

## 3. The fail Function

```
SYNTAX : int fail ( ) const;
```

Returns a nonzero value if any I/O error (not end of file) has occurred. This condition corresponds to either the badbit or failbit error flag being set. If a call to bad returns 0, you can assume that the error condition is nonfatal and that you can probably continue processing after you clear the flags.

## 4. The clear Function

```
SYNTAX : void clear (int nState = 0);
```

The parameter nState, if 0, then all error bits are cleared, otherwise bits are set according to the following masks (ios enumerators) that can be combined using the bitwise OR (|) operator. The nState parameter must have one of the following values :

- ios :: goodbit          No error condition (no bits set).
- ios :: eofbit           End of file reached.
- ios :: failbit          A possibly recoverable formatting or conversion error.
- ios :: badbit           A serious I/O error.

The function sets or clears the error-state flags. The rdstate function can be used to read the current error state.

## 5. The eof( ) Function

```
SYNTAX : int eof( ) const;
```

Returns a nonzero value if end of file has been reached. This is the same as setting the eofbit error flag.

## 6. The rdstate Function

```
SYNTAX : int rdstate ( ) const;
```

Returns the current error state as specified by the following masks (ios enumerators).

- ios :: goodbit          No error condition (no bits set).
- ios :: eofbit           End of file reached.
- ios :: failbit          A possibly recoverable formatting or conversion error.
- ios :: badbit           A serious I/O error or unknown state.

This is shown in the figure given below. The last 4 bits are unused.

The returned value can be tested against a mask with the AND (&) operator, but we do not have to as we can have functions which tells us which bit is set or reset.

![](img/ad5299318df8d4d7c6df5eaa86590ea3_623_0.png)

/* PROG 12.28 ERROR HANDLING WITH FILES */

#include <iostream.h>
#include <conio.h>
#include <fstream.h>
void main( )
{
        clrscr( );
        ofstream file("silly.txt", ios :: noreplace);
        if(!file)
        {
                cout << "FILE OPENING ERROR";
                endl(cout);
        }
        cout << "THE VARIOUS FLAGS SET/ RESET ARE";
        endl(cout);
        cout << "rdstate=" << file.rdstate( );
        endl(cout);
        cout << "bad=" << file.bad( );
        endl(cout);
        cout << "fail=" << file.fail( );
        endl(cout);
        cout << "good=" << file.good( );
        endl(cout);
        cout << "eof=" << file.eof( );
        endl(cout);
        getch( );
}

OUTPUT :
FILE OPENING ERROR
THE VARIOUS FLAGS SET/ RESET ARE
rdstate=2
bad=0
fail=2
good=0
eof=0

**EXPLANATION :** The file silly.txt was existing earlier. The noreplace raises error if file was existing and we tried to open it for writing. That is using this flag we come to know that file already exist and we do not have to modify the file. The file opening error occurred so fail will returned a non zero value, good returns 1 only when no error of any type occurs *i.e.*, all

the bits are cleared. The bad returns 0 as there is no I/O error. Eof was not reached so eof returns 0. Now checking from the figure, the rdstate will be as :

![](img/ad5299318df8d4d7c6df5eaa86590ea3_625_0.png)

Figure 12.16. Logical Implementation of rdstate( )

# 0010 is decimal 2, so rdstate return 2.

In the program if file was not opened and we try to write to the file then function bad returns true and badbit which indicates file input/output error. This can be checked again as :

```
file << "WRITING TO THE FILE" << endl;
if(!file)
{
    cout << "WRITING ERROR";
    endl(cout);
}
//check all flags here;
```

```
/*PROG 12.29 DEMO OF FAIL AND GOOD */

#include <iostream.h>
#include <fstream.h>
#include <conio.h>
void main()
{
    clrscr();
    ifstream file("num.txt",ios ::nocreate);
    if(file.good())
    {
        cout << "File is opened successfully" << endl;
        cout << "good flag :=" << file.good() << endl;
    }
    else if(file.fail())
    {
        cout << "Error in opening file \n";
        cout << "Fail flag :=" << file.bad() << endl;
    }
}

OUTPUT :
File is opened successfully
good flag := 1
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_626_0.png)

Figure 12.17. Showing the output screen of the program 12.29.

EXPLANATION : The program is self-explanatory.

## 12.10 PONDERABLE POINTS

- 1. Opening a file links the program with the files. The link is made through an object of any of the file stream classes like fstream, ifstream, ofstream etc., which are defined in header file fstream.h.
- 2. The files which are accessed using library functions are known as high level files and those by system-calls are known as low level files. System calls are special command to the operating system (OS) and are specified to a particular OS.
- 3. High level files are also known as stream oriented files and low level files are also known as system oriented files.
- 4. There are two types of stream in general
  - (a) Text streams which is a sequence of bytes (lines of text).
  - (b) Binary stream which is a sequence of unprocessed bytes.
- 5. Normally all files are opened and accessed in text mode. For opening a file a binary mode ios :: binary mode has to be specified.
- 6. For opening file either the constructor method or open function can be used.
- 7. The various modes like ios :: in, ios :: out, ios :: ate etc., are enumeration constants of ios class.
- 8. The various functions for handling error are good, bad, clear etc.

## EXERCISE

### A. True and False :

- 1. read( ) and write( ) method are used for character input and output.
- 2. The fstream can only be used for reading the data.
- 3. The read and write functions are used to read and write objects from/to file.
- 4. A stream may be connected to more than one file at a time.

### B. Answer the Following Questions :

- 1. What different types of file streams C++ provides ?
- 2. Why we need fstream. Header file ?
- 3. What is the advantage of files ?
- 4. How text file different from binary file ?
- 5. Discuss function for random access of a file.
- 6. What are the opening modes ? Explain the purpose of each mode.
- 7. What are command line arguments ? How do we use them in our program ?
- 8. How can we read write object from/to file ?
- 9. What are various error handling functions C++ provides ?
- 10. What is eof ? How it can detect end of file ?

### C. Brain Drill :

- 1. Write a program that displays on the screen the contents of text file line by line backwards. It should be possible to run your program by providing the file name as a command line argument.
- 2. Write a C++ class to read an existing file and create another file with all words of the source file stored in reverse order. It is assumed that successive words are separated by one or more white space characters.
- 3. Write a C++ program to compare contents of two files whose names are supplied through the command line. Display the first line having mismatch along with its number.
- 4. Write a C++ program to copy the alternate lines in reverse order from a source file to target file with the file names are entered at the command prompt.
- 5. Write a program that emulates the DOS COPY command. That is, it should copy the contents of a text file (such as any .CPP file) to another file. Invoke the program with two command-line arguments—the source file and the destination file-like this :
  C>copy srcfile.cpp destfile.cpp
  In the program, check that the user has typed the correct number of command-line arguments, and that the files specified can be opened.
- 6. Write a program that returns the size in bytes of a program entered on the command line :
  C>filesize program.exe
- 7. In a loop, prompt the user to enter name data consisting of a first name, middle initial, last name, and employee number (type unsigned long). Then, using formatted I/O with the insertion (<<) operator, write these four data items to an ofstream object. Don't forget that strings must be terminated with a space or other white space character. When the user indicates that no more name data will be entered, close the ofstream object, open an ifstream object, read and display all the data in the file, and terminate the program.
- 8. Create a time class that includes integer member values for hours, minutes, and seconds. Make a member function get_time ( ) that gets a time value from the user, and a function put_time ( ) that displays a time in 12 :59 :59 format. Add error checking to the get_time ( ) function to minimize user mistake. This function should request hours, minutes, and second separately, and check each one for ios error status flags and the correct range. Hours should be between 0 and 23, and minutes and seconds between 0 to 59. Don't input these values as strings and then convert them; read them directly as integers. This implies that you won't be able to screen out entries with superfluous decimal points.
  In main ( ), use a loop to repeatedly get a time vale from the user with get_time ( ) and then display it with put_time ( ), like this :
  Enter hours : 11
  Enter minutes : 59
  Enter seconds : 59
  Time = 11 :59 :59
  Do another (y/n) ? y

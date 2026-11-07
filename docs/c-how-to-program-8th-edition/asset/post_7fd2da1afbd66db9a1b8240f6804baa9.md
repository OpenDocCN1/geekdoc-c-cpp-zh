
```cpp
// Fig. F.3: figF_03.cpp
// Using command-line arguments
#include <iostream>
#include <fstream>
using namespace std;

int main( int argc, char *argv[] )
{
    // check number of command-line arguments
    if ( argc != 3 )
        cout << "Usage: copyFile infile_name outfile_name" << endl;
    else
    {
        ifstream inFile( argv[1], ios::in );

        // input file could not be opened
        if ( !inFile )
        {
            cout << argv[1] << " could not be opened" << endl;
            return -1;
        } // end if

        ofstream outFile( argv[2], ios::out );

        // output file could not be opened
        if ( !outFile )
        {
            cout << argv[2] << " could not be opened" << endl;
            inFile.close();
            return -2;
        } // end if

        char c = inFile.get(); // read first character

        while ( inFile )
        {
            outFile.put( c );  // output character
            c = inFile.get();  // read next character
        } // end while
    } // end else
} // end main
```

**Fig. F.3** Using command-line arguments.

This command line indicates that file input is to be copied to file output. When the program executes, if argc is not 3 (copyFile counts as one of the arguments), the program prints an error message (line 11). Otherwise, argv contains the strings "copyFile", "input" and "output". The second and third arguments on the command line are used as file names by the program. The files are opened by creating ifstream object inFile and ofstream object outFile (lines 14 and 23). If both files are opened successfully, characters are read from file input with member function get and written to file output with member function put until the end-of-file indicator for file input is set (lines 35–39). Then the program terminates. The result is an exact copy of file input. Note that not all computer systems support command-line arguments as easily as UNIX, LINUX, Mac OS X and Windows. Some VMS and older Macintosh systems, for example, require special settings for processing command-line arguments. See the manuals for your system for more information on command-line arguments.

## F.5 Notes on Compiling Multiple-Source-File Programs

As stated earlier in the text, it is normal to build programs that consist of multiple source files (see Chapter 9). There are several considerations when creating programs in multiple files. For example, the definition of a function must be entirely contained in one file—it cannot span two or more files.

In Chapter 6, we introduced the concepts of storage class and scope. We learned that variables declared outside any function definition are of storage class static by default and are referred to as global variables. Global variables are accessible to any function defined in the same file after the variable is declared. Global variables also are accessible to functions in other files; however, the global variables must be declared in each file in which they are used. For example, if we define global integer variable flag in one file, and refer to it in a second file, the second file must contain the declaration

```cpp
extern int flag;
```

prior to the variable’s use in that file. In the preceding declaration, the storage class-specifier extern indicates to the compiler that variable flag is defined either later in the same file or in a different file. The compiler informs the linker that unresolved references to variable flag appear in the file. (The compiler does not know where flag is defined, so it lets the linker attempt to find flag.) If the linker cannot locate a definition of flag, a linker error is reported. If a proper global definition is located, the linker resolves the references by indicating where flag is located.

> **Performance Tip F.1**
>
> *Global variables increase performance because they can be accessed directly by any function—the overhead of passing data to functions is eliminated.*

> **Software Engineering Observation F.2**
>
> *Global variables should be avoided unless application performance is critical or the variable represents a shared global resource such as cin, because they violate the principle of least privilege, and they make software difficult to maintain.*

Just as extern declarations can be used to declare global variables to other program files, function prototypes can be used to declare functions in other program files. (The extern specifier is not required in prototypes.) This is accomplished by including the function prototype in each file in which the function is invoked, then compiling each source file and linking the resulting object code files together. Function prototypes indicate to the compiler that the specified function is defined either later in the same file or in a different file. The compiler does not attempt to resolve references to such a function—that task is left to the linker. If the linker cannot locate a function definition, an error is generated.

As an example of using function prototypes to extend the scope of a function, consider any program containing the preprocessor directive `#include <cstring>`. This directive

```cpp
// display message before termination
void print()
{
    cout << "Executing function print at program termination\n"
         << "Program terminated" << endl;
} // end function print
```

```
Enter 1 to terminate program with function exit
Enter 2 to terminate program normally
2

Terminating program by reaching the end of main
Executing function print at program termination
Program terminated
```

```
Enter 1 to terminate program with function exit
Enter 2 to terminate program normally
1

Terminating program with function exit
Executing function print at program termination
Program terminated
```

**Fig. F.4** | Using functions exit and atexit. (Part 2 of 2.)

Terminating a program with function exit runs the destructors for only the static and global objects in the program. Terminating with function abort ends the program without running any destructors.

## F.7 Type Qualifier volatile

The **volatile** type qualifier is applied to a definition of a variable that may be altered from outside the program (i.e., the variable is not completely under the control of the program). Thus, the compiler cannot perform optimizations (such as speeding program execution or reducing memory consumption, for example) that depend on “knowing” that a variable’s behavior is influenced only by program activities the compiler can observe.

## F.8 Suffixes for Integer and Floating-Point Constants

C++ provides integer and floating-point suffixes for specifying the types of integer and floating-point constants. The integer suffixes are: **u** or **U** for an **unsigned** integer, **l** or **L** for a **long** integer, and **ul** or **UL** for an **unsigned long** integer. The following constants are of type unsigned, long and unsigned long, respectively:

```
174u
8358L
26373ul
```

If an integer constant is not suffixed, its type is int; if the constant cannot be stored in an int, it is stored in a long.

The floating-point suffixes are **f** or **F** for a float and **l** or **L** for a *long double*. The following constants are of type long double and float, respectively:

```
3.14159L
1.2F
```

A floating-point constant that is not suffixed is of type double. A constant with an improper suffix results in either a compiler warning or an error.

## F.9 Signal Handling

An unexpected event, or **signal**, can terminate a program prematurely. Such events include **interrupts** (pressing **\<Ctrl\> C** on a UNIX, LINUX, Mac OS X or Windows system), **illegal instructions**, **segmentation violations**, **termination orders from the operating system** and **floating-point exceptions** (division by zero or multiplying large floating-point values). The **signal-handling library** provides function signal to **trap unexpected events**. Function **signal** receives two arguments—an integer signal number and a pointer to a signal-handling function. Signals can be generated by function **raise**, which takes an integer signal number as an argument. Figure F.5 summarizes the standard signals defined in header file **\<signal\>**. The next example demonstrates functional signal and raise.

Figure F.6 traps an interactive signal (SIGINT) with function signal. The program calls signal with SIGINT and a pointer to function signalHandler. (Recall that a function's name is a pointer to that function.) When a signal of type SIGINT occurs, function signalHandler is called, a message is printed and the user is given the option to continue normal program execution. If the user wishes to continue the execution, the signal handler is reinitialized by calling signal again (some systems require the signal handler to be reinitialized), and control returns to the point in the program at which the signal was detected. In this program, function raise is used to simulate an interactive signal. A random number between 1 and 50 is chosen. If the number is 25, then raise is called to generate the signal. Normally, interactive signals are initiated outside the program. For example, pressing **\<Ctrl\> C** during program execution on a UNIX, LINUX, Mac OS X or Windows system generates an interactive signal that terminates program execution. Signal handling can be used to trap the interactive signal and prevent the program from terminating.

| Signal | Explanation |
|---|---|
| SIGABRT | Abnormal termination of the program (such as a call to abort). |
| SIGFPE | An erroneous arithmetic operation, such as a divide by zero or an operation resulting in overflow. |
| SIGILL | Detection of an illegal instruction. |
| SIGINT | Receipt of an interactive attention signal. |
| SIGSEGV | An invalid access to storage. |
| SIGTERM | A termination request sent to the program. |

**Fig. F.5** | Signals defined in header **\<csignal\>**.

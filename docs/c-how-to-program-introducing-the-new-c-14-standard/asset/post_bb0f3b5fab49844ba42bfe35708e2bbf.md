
## 14.3 Creating a Sequential File

C++ imposes no structure on files. Thus, a concept like that of a record ([Section 1.4](#)) does not exist in C++. You must structure files to meet the application’s requirements. The following example shows how you can impose a simple record structure on a file.

[Figure 14.2](#) creates a sequential file that might be used in an accounts-receivable system to help manage the money owed to a company by its credit clients. For each client, the program obtains the client’s account number, name and balance (i.e., the amount the client owes the company for goods and services received in the past). The data obtained for each client constitutes a *record* for that client. The account number serves as the *record key*; that is, the program creates and maintains the records of the file in account-number order. This program assumes the user enters the records in account-number order. In a comprehensive accounts receivable system, a *sorting* capability would be provided for the user to enter records *in any order*—the records then would be sorted and written to the file.

```cpp
// Fig. 14.2: Fig14_02.cpp
// Creating a sequential file.
#include <iostream>
#include <string>
#include <fstream>  // contains file stream processing types
#include <cstdlib>  // exit function prototype
using namespace std;

int main() {
   // ofstream constructor opens file
   ofstream outClientFile( "clients.txt", ios::out );

   // exit program if unable to create file
   if ( !outClientFile ) {  // overloaded operator
      cerr << "File could not be opened" << endl;
      exit(EXIT_FAILURE);
   }

   cout << "Enter the account, name, and balance.\n"
        << "Enter end-of-file to end input.\n? ";

   int account;       // the account number
   string name;       // the account owner's name
   double balance;    // the account balance

   // read account, name and balance from cin, then place in file
   while ( cin >> account >> name >> balance ) {
      outClientFile << account << " " << name << " " << balance << endl;
      cout << "? ";
   }
}
```

```text
Enter the account, name, and balance.
Enter end-of-file to end input.
? 100 Jones 24.98
? 200 Doe 345.67
? 300 White 0.00
? 400 Stone -42.16
? 500 Rich 224.62
? ^Z
```

**Fig. 14.2 Creating a sequential file.**

### 14.3.1 Opening a File

Figure 14.2 writes data to a file, so we open the file for output by creating an `ofstream` object. Two arguments are passed to the object’s constructor (line 11)—the **filename** and the **file-open mode**. For an `ofstream` object, the file-open mode can be either `ios::out` (the default) to *output* data to a file or `ios::app` to *append* data to the end of a file (without modifying any data already in the file). Line 11 creates an `ofstream` object named `outClientFile` associated with the file `clients.txt` that’s opened for output—because we did not specify a path to the file (that is, its location), the file will be in the same directory as the program. The `ofstream` constructor opens the file—this establishes a “line of communication” with the file. Prior to C++11, the filename was specified as a pointer-based string—as of C++11, it also can be specified as a `string` object.

Since `ios::out` is the default, the second constructor argument in line 11 is not required, so we could have used the statement

```cpp
ofstream outClientFile("clients.txt");
```

Existing files opened with mode `ios::out` are **truncated**—all data in the file is *discarded*. If the specified file does **not** yet exist, then the `ofstream` object *creates* the file, using that filename. Figure 14.3 lists the file-open modes. These modes can also be combined, as we discuss in **Section 14.9**.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1772_0.png)

**Error-Prevention Tip 14.1**

*Use caution when opening an existing file for output (`ios::out`), especially when you want to preserve the file’s contents, which will be discarded without warning.*

**Fig. 14.3 File-open modes.**

| Mode | Description |
|---|---|
| `ios::app` | Append all output to the end of the file. |
| `ios::ate` | Open a file for output and move to the end of the file (normally used to append data to a file). Data can be written *anywhere* in the file. |
| `ios::in` | Open a file for *input*. |
| `ios::out` | Open a file for *output*. |
| `ios::trunc` | *Discard* the file’s contents (this also is the default action for `ios::out`). |
| `ios::binary` | Open a file for binary, i.e., *nontext*, input or output. |

### 14.3.2 Opening a File via the `open` Member Function

You can create an `ofstream` object *without* opening a specific file—in this case, a file can be attached to the object later. For example, the statement

```cpp
    ofstream outClientFile;
```

creates an `ofstream` object that’s not yet associated with a file. The `ofstream` member function **open** opens a file and attaches it to an *existing* `ofstream` object as follows:

```cpp
    outClientFile.open("clients.txt", ios::out);
```

Once again, `ios::out` is the default value for the second argument.

### 14.3.3 Testing Whether a File Was Opened Successfully

After creating an `ofstream` object and *attempting* to open it, the `if` statement in lines 14–17 (**Fig. 14.2**) uses the overloaded `ios` member function `operator!` (discussed in **Chapter 13**) to determine whether the `open` operation succeeded. Recall that `operator!` returns `true` if either the `failbit` or the `badbit` is set for the stream—in this case, one or both would be set because the `open` operation failed. Some possible reasons are:

- attempting to open a *nonexistent* file for reading
- attempting to open a file for reading or writing from a directory that you don’t have permission to access, and
- opening a file for writing when no disk space is available.

If the condition indicates an unsuccessful attempt to open the file, line 15 outputs an error message, and line 16 invokes function `exit` to terminate the program. The argument to `exit` is returned to the environment from which the program was invoked. Passing `EXIT_SUCCESS` (defined in `<cstdlib>`) to `exit` indicates that the program terminated *normally*; passing any other value (in this case `EXIT_FAILURE`) indicates that the program terminated due to an *error*.

### 14.3.4 Overloaded `bool` Operator

As we discussed in **Chapter 13**, a stream’s overloaded `operator bool` (added in C++11) converts the stream to a `true` or `false` value, so it can be tested in a condition. If the `failbit` or `badbit` has been set for the stream, the overloaded operator returns `false`. The condition in the `while` statement (lines 27–30) *implicitly* invokes the `operator bool` member function on `cin`. The condition remains *true* as long as neither the `failbit` nor the `badbit` has been set for `cin`. Entering the *end-of-file* indicator sets the `failbit` for `cin`. Recall from **Chapter 13** that you also can call member function `eof` on the input object.

### 14.3.5 Processing Data

If line 11 opens the file successfully, the program begins processing data. Lines 19–20 prompt the user to enter either the various fields for each record or the end-of-file indicator when data entry is complete. **Figure 14.4** lists the keyboard combinations for entering end-of-file for various computer systems.

**Fig. 14.4 End-of-file key combinations.**

| Computer system | Keyboard combination |
|---|---|
| UNIX/Linux/Mac OS X | `<Ctrl-d>` (on a line by itself) |
| Microsoft Windows | `<Ctrl-z>` (followed by pressing *Enter*) |

Line 27 extracts each set of data and determines whether end-of-file has been entered. When end-of-file is encountered or bad data is entered, `operator bool` returns `false` and the `while` statement terminates. The user enters end-of-file to inform the program to process no additional data. The end-of-file indicator is set when the user enters the end-of-file key combination. The `while` statement loops until the end-of-file indicator is set (or bad data is entered).

Line 28 writes a set of data to the file `clients.txt`, using the stream insertion operator `<<` and the `outClientFile` object associated with the file at the beginning of the program. The data may be retrieved by a program designed to read the file (see Section 14.4). The file created in Fig. 14.2 is simply a text file, so it can be viewed by any text editor.

### 14.3.6 Closing a File

Once the user enters the end-of-file indicator, `main` terminates. This implicitly invokes `outClientFile`’s destructor, which *closes* the `clients.txt` file. You also can close the `ofstream` object *explicitly*, using member function `close` as follows:

```cpp
outClientFile.close();
```

a program to get data directly from and save output directly to secondary storage. A program can use the file I/O and read data from or write data to a file. Formally, a file is defined as follows:

**File:** An area in secondary storage used to hold information.

The standard I/O header file, `iostream`, contains data types and variables that are used only for input from the standard input device and output to the standard output device. In addition, C++ provides a header file called `fstream`, which is used for file I/O. Among other things, the `fstream` header file contains the definitions of two data types: `ifstream`, which means input file stream and is similar to `istream`, and `ofstream`, which means output file stream and is similar to `ostream`.

The variables `cin` and `cout` are already defined and associated with the standard I/O devices. In addition, `>>`, `get`, `ignore`, `putback`, `peek`, and so on can be used with `cin`, whereas `<<`, `setfill`, and so on can be used with `cout`. These same operators and functions are also available for file I/O, but the header file `fstream` does not declare variables to use them. You must declare variables called **file stream variables**, which include `ifstream` variables for input and `ofstream` variables for output. You then use these variables together with `>>`, `<<`, or other functions for I/O. Remember that C++ does not automatically initialize user-defined variables. Once you declare the `fstream` variables, you must associate these file variables with the I/O sources.

File I/O is a five-step process:

+   1. Include the header file fstream in the program.
+   2. Declare file stream variables.
+   3. Associate the file stream variables with the I/O sources.
+   4. Use the file stream variables with >>, <<, or other I/O functions.
+   5. Close the files.

We will now describe these five steps in detail. A skeleton program then shows how the steps might appear in a program.

Step 1 requires that the header file `fstream` be included in the program. The following statement accomplishes this task:

```
```cpp
#include <fstream>
```
```

Step 2 requires you to declare file stream variables. Consider the following statements:

```
```cpp
ifstream inData;
ofstream outData;
```
```

The first statement declares `inData` to be an input file stream variable. The second statement declares `outData` to be an output file stream variable.

![](bbox=[0.927, 0.185, 1.0, 0.296])
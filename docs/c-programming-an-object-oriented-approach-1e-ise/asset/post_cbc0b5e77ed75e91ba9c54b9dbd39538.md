
**Table 16.5** Reading a C string

| The *istream* class | The *ostream* class |
|---|---|
| `istream& get (char* s, int n)` | |
| `istream& getline (char* s, int n, char d = '\n')` | |

removed from the stream, but it is not added to the array. The prototypes of these functions are shown in Table 16.5.

Note that in both cases shown in the table, when n characters are read or the delimiter is reached, the eofbit is set and no more characters can be read from the stream.

We test the second function in Program 16.4. We create an array of 80 characters to accept a line. We then type a line and enter the return key. The program creates a string out of the line (without the '\n' character) and adds a null character at the end.

## Input/Output of Fundamental Data Types

The istream and ostream classes are basically character stream classes, but this does not mean that we cannot extract the value of a fundamental type from an input stream or insert the value of a fundamental data type into an output stream. Inputting and outputting of fundamental data types is also considered text input/output because the function extracts several characters and puts them together to get a fundamental data type or the function creates several characters from a fundamental data type and inserts them into the output stream. This is done by two overloaded operators called the insertion operator and the extraction operator. Table 16.6 shows the general declaration of these two operators in which the type can be bool, char, short (signed and unsigned), int (signed and unsigned), long (signed and unsigned), float, double, long double, or void*.

**Program 16.4** Testing getline

```cpp
/**************************************************************
 * A program to test the getline functions                    *
 **************************************************************/
#include <iostream>
using namespace std;

int main ()
{
   char str2 [80];
   cin.getline (str2, 80, '\n');
   cout << str2;
   return 0;
}
```

Run:

This is a line to make a string out of it.
This is a line to make a string out of it.

| Table 16.6 Extracting and inserting a fundamental data type |
|---|
| `istream& operator >> (type& x);` — Extracting next data item |
| `ostream& operator << (type& x);` — Inserting next data item |

The behavior of the extraction and insertion operators is different for fundamental data types. We review these operations briefly.

### Extracting Fundamental Data Types

The extraction operator for the fundamental data types uses the following four rules when it encounters a statement such as `cin >> variable`. The operator reads the characters one by one until it finds a character that does not belong to the syntax of the corresponding type:

- a. If it is extracting a Boolean value, it must see a value that can be interpreted as 0 or 1.
- b. If it is extracting a character value, it reads the next character in the input stream (including a whitespace character) and stores it in the corresponding variable.
- c. If it is extracting an integral value, it reads digits until it encounters a nondigit character. It makes an integer value of the extracted characters. The unextracted characters remain in the stream.
- d. If it is extracting a floating-point value, it reads digits with only one decimal point between them. If it encounters a second decimal point or a nondigit character, it stops and makes the floating-point value.

### Inserting Fundamental Data Types

Fundamental data types can be inserted into streams using the insertion operator (`<<`). The value is considered a set of characters and inserted into the stream. For example, the integer 124 is inserted as three characters (1, 2, and 4) into the stream.

## Input/Output of C-Type Strings

When we use the `cin` object to input a C string, we must be careful that we do not exceed the size of the array; otherwise, a run-time error occurs and the program is aborted. There is no problem when we output a C string.

## Input/Output of C++ Strings

The extractor and inserter operators are overloaded for the *string* class; they can be used as they have been defined. However, the input stops when the first whitespace is encountered. If we want to read the whitespace characters (the whole line), we must use the `getline` function (a global function) defined in the `<string>` header. It has the following signature:

```cpp
istream& getline (istream& in, string& str);
```

## Other Member Functions

There are other member functions defined in *istream* and *ostream* classes, but they are not used by the objects instantiated from these classes. They are, however, inherited by the other stream classes in the hierarchy; we discuss these classes in the next sections.

## 16.3 FILE STREAMS

In the previous section we used the keyboard and monitor as the source and sink for data, but they are temporary. After the program terminates, the data do not exist and cannot be used again; if needed, the data must be re-created. A file is a permanent source or sink for data. After creation, it can be used by another program. Files can be saved for future use.

To use files, we must use the file stream classes defined in the `<fstream>` header; doing so allows us to connect the files to our program so we can read or write them.

> We must include the `<fstream>` header to use file streams.

As shown in Figure 16.5, file stream classes are made from three classes: `ifstream`, `ofstream`, and `fstream`. These classes are used to input data from or output data to files or to input and output to the same file. They are inherited, respectively, from the `istream`, `ostream`, and `iostream` classes, and they inherit all member functions of these classes. The file stream classes define some new functions, mostly for instantiation and opening files.

> All of the member functions defined in the console streams are inherited in the file streams.

### 16.3.1 File Input/Output

The source or the sink of data is always an entity that must be connected to a stream object. In the case of file input/output, the source is a file and the sink is a file. Files are entities that reside on disk (auxiliary storage). In other words, we have files and we have stream objects that must be connected to the files as shown in Figure 16.9. This means that we must construct a stream, connect the stream to the corresponding file, read or write from the file, disconnect the file, and destruct the stream.

### Construct the Stream

We can instantiate any of the three streams as shown below. To do so we must include the `<fstream>` header file in our program.

![](img/d68f6199646ca63591a6d8419e0ed4ba_747_0.png)

**Figure 16.9** A file stream object connecting our program to a file

## Program 16.5 Testing the five steps in outputting to a file

```cpp
/*************************************************************
 * A program to create an output file and write to it         *
 *************************************************************/
#include <iostream>
#include <fstream>
#include <cassert>
using namespace std;

int main ()
{
    // Instantiation of an ofstream object
    ofstream outStrm;
    // Creation of a file and connecting it to the ofstream object
    outStrm.open ("integerFile");
    if (!outStrm.is_open())
    {
        cout << "integerFile cannot be opened!";
        assert (false);
    }
    // Writing to the file using overloaded insertion operator
    for (int i = 1; i <= 10; i++)
    {
        outStrm << i * 10 << " ";
    }
    // Closing the file
    outStrm.close ();
    // The ofstream object is destroyed after return statement
    return 0;
}
```

## Two Examples

Program 16.5 shows how we can use the steps described above to instantiate a stream, open a file and test if it is open, to write to the file, and close the file (destruction of the stream object is done in the background).

In Program 16.6, we instantiate an *ifstream* class and connect it to the *integerFile* we created in Program 16.5. We then read the integers one by one and display them. Note that we are using two streams: the *ifstream*, which is connected to the *integerFile*, and the *ostream*, which is automatically connected to the monitor. As we said, the *ostream* is instantiated automatically by the system (*cout* object).

Nothing will be output to the monitor from Program 16.5 when it is run, but we can check the contents of a file named *integerFile* (a data file) with a text editor to find that the following line was stored in it.

```text
10 20 30 40 50 60 70 80 90 100
```


When we open *file* with a text editor, we see that the date has been added at the end of the file (in a new line) as shown below:

> This is the file that we want to open  
> and read its contents.  
> October 15, 2015.

## Opening for Input/Output

We can open a file for input/output if we connect our file to an *fstream* object using the mode (`ios::in | ios::out`). Assume that we have a file of integers. We decide to add the sum of the integers at the end of the file. We can open the file for both read and write (`ios::in | ios::out`). Note that this situation is different from the previous example. We must read the integers, one by one (input), and then write the sum at the end of the file (output). The contents of our file before the change is shown below:

> 12 14 17 20 21 25 32 27 56 18

Program 16.10 shows the solution.

### Program 16.10 Opening a file for both input and output

```cpp
/***************************************************************
 * A program that opens a file, sums its contents, and writes   *
 * the sum at the end of the file.                              *
 ***************************************************************/
#include <iostream>
#include <fstream>
#include <cassert>
using namespace std;

int main()
{
    // Instantiate an fstream object
    fstream fstr;
    // Open the intFile and connected to the fstream object
    fstr.open("intFile", ios::in | ios::out);
    if (!fstr.is_open())
    {
        cout << "intFile cannot be opened!";
        assert(false);
    }
    // Read all integers and add to the sum until end of file is detected
    int num;
    int sum = 0;
    while (fstr >> num)
    {
        sum += num;
    }
    // Clear the stream and add the message and the sum to the file
    fstr.clear();
    fstr << "\nThe sum of the numbers is: ";
    fstr << sum;
    // Close the stream
    fstr.close();
    return 0;
}
```

When the loop (lines 24 to 27 in Program 16.10) terminates, the *eofbit* is set and we cannot use the stream. In line 29 we clear the stream and then write the message and the sum to the end of the file. The result is a file with the following contents:

> 12 14 17 20 21 25 32 27 56 18  
> **The sum of the numbers is: 242**

## EXAMPLE 16.1

The last file mode in Figure 16.10 (`ios::in | ios::out | ios::trunc`) allows us to open the file, truncate its contents, and write new data to it. This is the same as the mode (`ios::out`) with one difference. In the second mode, we create a new file; in the first we delete the contents of an old file and replace it with new data. The second method is used when we want to keep the name of the file, but with new contents.

## Other Opening Modes

We have not used the last three modes listed in Table 16.7, but we use them later in the chapter.

## 16.3.3 Other Member Functions

There are additional member functions that have been defined for the *istream* class, but they have more applications in the *ifstream* class (Table 16.8).

The function *gcount* gives the count of the number of characters extracted in the last input. The function *unget* puts the last character extracted from the stream back into the stream. The function *putback* does the same as *unget*. The function *peek* looks at the value of the next character without removing it. The function *ignore* skips over a number of characters without extracting them. We show how to use the *unget* function; we leave the rest as exercises.

Assume we have a file that includes only text and integers as shown below:

> **We have 7, 12, 23, and 442 in this file.**

**Table 16.8 Other member functions used in file streams**

| Function | Description |
|---|---|
| `int gcount() const` | `// counts the number of characters` |
| `istream& unget()` | `// put back the last character in stream` |
| `istream& putback(char c)` | `// same as unget` |
| `int peek()` | `// look without extracting` |
| `istream& ignore(int n = 1, int d = EOF)` | `// ignore some characters` |

We want to extract the integers from this file and ignore the text. Program 16.11 shows how we can use the `unget` function to do so.

The program goes through the whole file, character by character. If the character is a nondigit, it is thrown away. If the character is a digit, it is put back into the stream to be extracted again as an integer.

### Program 16.11 Using the unget function

```cpp
/***************************************************************
 * A program that extracts only integers from an input file     *
 * that contains both integer and character data types          *
 ***************************************************************/
#include <iostream>
#include <fstream>
#include <cassert>
using namespace std;

int main()
{
    // Instantiation of an ifstream object and connection to the file
    ifstream ifstr;
    ifstr.open("mixedFile", ios::in);
    if (!ifstr.is_open())
    {
        cout << "The file mixedFile cannot be opened for reading!";
        assert(false);
    }
    // Reading only integers by putting back the non-digit characters
    char ch;
    int n;
    while (ifstr.get(ch))
    {
        if (ch >= '0' && ch <= '9')
        {
            ifstr.unget();
            ifstr >> n;
            cout << n << " ";
        }
    }
    // Closing the file
    ifstr.close();
    return 0;
}

Run:
7 12 23 442
```

## 16.3.4 Sequential versus Random Access

A file is a sequential collection of 8-bit bytes. We do not read or write to a file directly; we read from or write to the buffer in the stream object. In reading, the contents of the file are copied to the buffer by the system in bulk movement; in writing, the contents of the buffer are moved from the buffer to the file in bulk movement. Transferring bytes from the file to the buffer or from the buffer to the file is out of our control.

When we talk about **sequential access** or **random access**, we do not mean that the file is arranged sequentially or randomly (a file is always a sequence collection of bytes), we are referring to how we access the buffer in the stream object: sequentially or randomly. If we think about the buffer, we see that it is like an array; we can always access an array either sequentially (element after element) or randomly (any element we want). In fact, the buffer in a stream is made of elements, and the elements are indexed from 0 to *n* − 1, where *n* is the size of the buffer defined by the system.

The buffer in an *ifstream* has a marker that points to the next byte to be read. The buffer in an *ofstream* has a marker that points to the next byte to be written. The buffer in an *fstream* has only one marker for read or write.

> **Each stream has only one marker that indicates whether the next byte should be read or written.**

### Sequential Access

All of the examples we have shown so far have used sequential access. In sequential access, the movement of the stream marker is controlled by the read/write functions. The marker starts at the beginning of the buffer (index 0) when the file is opened. It moves toward the end of the buffer with each read or write. The marker is pointing to the next byte to be read or written, but the number of bytes in each read or write depends on the type of data. If we are reading or writing characters, movement is one byte at a time; if we are reading or writing formatted data (fundamental type or class type), the movement can be a number of bytes for each read or write.

### Random Access

Reading or writing using the console system can be done only sequentially, but we can use random access when we use the file stream or string streams. In random access, we can read data from any location and we can write data to any location. We simply move the stream marker to the corresponding character. The *istream* and *ostream* classes provide member functions that allow us to find the location of the marker and to move the marker to the desired location. Table 16.9 shows the six member functions used for this purpose.

**Table 16.9 Member functions for random access**

| direction (dir) values |
|---|
| `ios::beg` `ios::cur` `ios::end` |

| Input | Output |
|---|---|
| `int tellg();`<br>`istream& seekg(int pos);`<br>`istream& seekg(int off, ios::dir);` | `int tellp();`<br>`ostream& seekp(int pos);`<br>`ostream& seekp(int off, ios::dir);` |

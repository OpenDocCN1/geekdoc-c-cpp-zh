
## Program 9.4

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

## Point of Information
### Formatting Text File Output Stream Data

Output file streams can be formatted in the same manner as the cout standard output stream. For example, if an output stream named fileOut has been declared, the following statement formats all data inserted in the fileOut stream in the same way these manipulators work for the cout stream:

```
fileOut << setiosflags(ios::fixed)
        << setiosflags(ios::showpoint)
        << setprecision(2);
```

The first manipulator parameter, ios::fixed, causes the stream to output all numbers as though they were floating-point values. The next parameter, ios::showpoint, tells the stream to always provide a decimal point. Therefore, a value such as 1.0 appears as 1.0, not as 1, which doesn't contain a decimal point. Finally, the setprecision() manipulator tells the stream to display two decimal values after the decimal point. Therefore, the number 1.0, for example, appears as 1.00.

Instead of using manipulators, you can use the stream methods setf() and precision(). For example, the previous formatting can be accomplished with the following code:

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

## Point of Information
### Writing One Character at a Time with the put() Method

All output streams have access to the fstream class's put() method, which permits character-by-character output to a stream. This method works in the same manner as the character insertion operator, <<. The syntax of this method call is the following:

```
ofstreamName.put(characterExpression);
```

The characterExpression can be a character variable or literal value. For example, the following code can be used to output an 'a' to the screen:

```
cin.put('a');
```

In a similar manner, if outFile is an ofstream object file that has been opened, the following code outputs the character value in the character variable named keycode to the outFile stream:

```
char keycode;
.
.
outFile.put(keycode);
```

## Reading from a Text File

Reading data from a text file is almost identical to reading data from a standard keyboard, except the cin object is replaced by the ifstream object declared in the program. For example, if inFile is declared as an object of type ifstream that's opened for input, the following statement reads the next two items in the file and stores them in the variables descrip and price:

```
inFile >> descrip >> price;
```

The file stream name in this statement, in place of cin, directs the input to come from the file stream rather than the keyboard. Table 9.3 lists other methods that can be used for stream input. When called, these methods must be preceded by a stream object name.

## Table 9.3 fstream Methods

| Method Name | Description |
|---|---|
| get() | Returns the next character extracted from the input stream as an int. |
| get(charVar) | Overloaded version of get() that extracts the next character from the input stream and assigns it to the specified character variable, charVar. |
| getline(strObj, termChar) | Extracts characters from the specified input stream, strObj, until the terminating character, termChar, is encountered. Assigns the characters to the specified string class object, strObj. |
| peek() | Returns the next character in the input stream without extracting it from the stream. |
| ignore(int n) | Skips over the next n characters. If n is omitted, the default is to skip over the next single character. |

Program 9.5 shows how the prices.dat file created in Program 9.4 can be read. This program illustrates one way of detecting the EOF marker by using the good() method (see Table 9.2). Because this method returns a Boolean true value before the EOF marker has been read or passed over, it can be used to verify that the data read is valid file data. Only after the EOF marker has been read or passed over does this method return a Boolean false. Therefore, the notation while(infile.good()) used in Program 9.5 ensures that data is from the file before the EOF has been read.

## Program 9.5

```
#include <iostream>
#include <fstream>
#include <cstdlib>  // needed for exit()
#include <string>  // needed for the string class
using namespace std;

int main()
{
    string filename = "prices.dat";  // put the filename up front
    string descrip;
    double price;

    ifstream inFile;

    inFile.open(filename.c_str());

    if (inFile.fail())  // check for successful open
    {
        cout << "\nThe file was not successfully opened"
             << "\n Please check that the file currently exists."
             << endl;
        exit(1);
    }

    // read and display the file's contents
    inFile >> descrip >> price;
    while (inFile.good())  // check next character
    {
        cout << descrip << ' ' << price << endl;
        inFile >> descrip >> price;
    }

    inFile.close();

    return 0;
}
```

## Chapter 9

Program 9.5 produces the following display:

```
Mats 39.95
Bulbs 3.22
Fuses 1.08
```

Examine the expression `inFile.good()` used in the while statement. This expression is true as long as the EOF marker hasn't been read. Therefore, as long as the last character read is good (that is, the EOF marker hasn't been passed), the loop continues to read the file. Inside the loop, the items just read are displayed, and then a new string and a double-precision number are input to the program. When the EOF has been detected, the expression returns a Boolean value of false and the loop terminates. This termination ensures that data is read and displayed up to, but not including, the EOF marker.

A replacement for the expression `while(inFile.good())` is the expression `while(!inFile.eof())`, which is read as "while the end of file has not been reached." This replacement works because the `eof()` method returns a true only after the EOF marker has been read or passed over. In effect, the relational expression checks that the EOF hasn't been read—hence, the use of the NOT operator, `!`.

Another means of detecting the EOF is to use the fact that the extraction operator, `>>`, returns a Boolean value of true if data is extracted from a stream; otherwise, it returns a Boolean false value. Using this return value, the following code can be used in Program 9.5 to read the file:

```
// read and display the file's contents
while (inFile >> descrip >> price) // check next character
  cout << descrip << ' ' << price << endl;
```

Although this code seems a bit cryptic at first glance, it makes perfect sense when you understand that the expression being tested extracts data from the file and returns a Boolean value to indicate whether the extraction was successful.

Finally, in the previous `while` statement or in Program 9.5, the expression `inFile >> descrip >> price` can be replaced by a `getline()` method (see Table 9.3). For file input, this method has the following syntax:

```
getline(fileObject, strObj, terminatingChar)
```

`fileObject` is the name of the input stream, `strObj` is a string class object, and `terminatingChar` is an optional character constant or variable specifying the terminating character. If this optional third argument is omitted, the default terminating character is the newline ('\n') character. Program 9.6 shows using `getline()` in the context of a complete program.

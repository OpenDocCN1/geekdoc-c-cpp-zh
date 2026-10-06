# 11.2 Output Stream 455

Tab. 11.2: Opening Model of Output File Stream.

| Label | Function |
| --- | --- |
| ios_base::app | Open an output file to add data at the bottom. |
| ios_base::ate | Open an extant file (used for input or output) and search its end. |
| ios_base::in | Open an input file, to ofstream, use ios_base::in as an open mode to avoid deleting the contents of an extant. |
| ios_base::out | Open a used file for output. If all ofstream objects, this mode is implicit. |
| ios_base::trunc | Open a file. If it already exists, delete the intrinsic content. If ios_base::out is appointed, ios_base::ate, ios_base::app and ios_base::in are not appointed, this mode is implicit. |
| ios_base::binary | Use binary mode to open a file (text mode is the default mode). |

If the constructor or member function open is used to open this file, the destructor of the output stream will automatically close a stream's file.

# 3. Function put

Function put writes a character to the output stream. The default of the following two statements are the same, but the second one is impacted by the format parameter of the stream:

```
cout.put('A'); //output a character precisely
cout << 'A'; //output a character, the width and filling method
//installed before it does its work
```

# 4. Function write

Function write writes a part of memory content to the output file stream. The length parameter indicates the number of bytes. The following example builds an output stream and writes the binary value of Date into a file.

Example 11.5: Output to a file.

```
//11_5.cpp
#include <fstream>
using namespace std;
struct Date
{
    int mo,da,yr;
};
int main()
{
    Date dt = {6,10,92};
    ofstream tfile("date.dat",ios_base::binary);
```
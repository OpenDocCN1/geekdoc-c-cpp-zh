| Function | Description |
|---|---|
| bool bad() | Returns true if badbit is set. |
| bool eof() | Returns true if eofbit is set. |
| bool fail() | Returns true if failbit is set. |
| bool good() | Returns true if goodbit is set. |
| void clear(iostate flag=goodbit) | Sets the state flags. |
| iostate rdstate() | Returns value of state flags. |

The badbit will be set to true if the stream becomes corrupted and data is assumed to be lost. Input routines in some user-defined class types and class templates set the bad bit to true when input data does not match the required format.

The state of a stream can be tested and directly modified using functions defined within the stream class hierarchy. These functions are designed to facilitate error handling, and should be used in all programs that rely on correct input for correct results. Table 5.2 provides a partial list of functions defined within the stream class hierarchy.

Program chapter5_7 illustrates the use of these functions to handle input errors.

```
```cpp
/*
 * Program chapter5_7
 *
 * This program illustrates the use of stream
 * flags and stream functions for detecting
 * and handling input errors.
 */
#include<iostream> //Required for cin, cout, cerr.
#include<fstream> //Required for ifstream, ofstream.
#include<string> //Required of string
#include<lomanip> //Required for setw()
using namespace std;

int main()
{
    //Declare variables.
    ifstream fin;
    ofstream fout;
    int iVar1, count(0);
    string filename;
    char junk;

    //Request name of input file.
    cout << "Enter the name of input file";
    cin >> filename;

    //Open file and check for failure.
    fin.open(ifilename.c_str());
    while(fin.fail())
    {
    ++count;
```
```
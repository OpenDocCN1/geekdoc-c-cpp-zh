# ## EXAMPLE E-3

Suppose you have the following line of text stored in a file, say, `digitsAndLetters.txt`:

```
```
0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ
```
```

Also, suppose that `inFile` is an `ifstream` object and the file `digitsAndLetters.txt` has been opened using the object `inFile`. One byte is used to store each character of this line of text. Moreover, the position of the first character is 0.

| Statement | Explanation |
|---|---|
| `inFile.seekp(10L, ios::beg);` | Sets the reading position of `inFile` to the 11th byte (character), which is at position 10. That is, it sets the reading position just after the digit 9 or just before the letter A. |
| `inFile.seekp(5L, ios::cur);` | Moves the reading position of `inFile` five bytes to the right of its current position. |
| `inFile.seekp(-6L, ios::end);` | Sets the reading position of `inFile` to the sixth byte (character) from the end. That is, it sets the reading position just before the letter U. |

The program in the following example further explains how the functions `seekg` and `seekp` work.

# ## EXAMPLE E-4

```
```cpp
#include <iostream>                         //Line 1
#include <fstream>                          //Line 2

using namespace std;                        //Line 3

int main()                                  //Line 4
{                                           //Line 5
    char ch;                                //Line 6
    ifstream inFile;                        //Line 7

    inFile.open("digitsAndAlphabet.txt");   //Line 8

    if (!inFile)                            //Line 9
    {                                       //Line 10
        cout << "The input file does not exist. "
             << "The program terminates!!" << endl; //Line 11
        return 1;                           //Line 12
    }                                       //Line 13
}
```
```
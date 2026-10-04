# I/O Streams and Data Files

# Point of C-Strings as Filenames

Using C-Strings as Filenames
If you use a C-string (which is simply a one-dimensional array of characters) to store an external filename, you must specify the C-string's maximum length in brackets immediately after it is declared. For example, examine the following declaration:
```c
char filename[21] = "prices.dat";
```
The number in brackets (21) is one more than the maximum number of characters that can be assigned to the variable filename because the compiler adds an end-string character to terminate the string. Therefore the string "prices.dat", which consists of 10 characters, is actually stored as 11 characters. In this example, the maximum value that can be assigned to the variable filename is a string value consisting of 20 characters.

After a string variable is declared to store a filename, it can be used in one of two ways. First, as shown in Program 8.3a, it can be placed at the top of a program to clearly identify a file's name, instead of embedding it in an open() method.

![](bbox=[0.105, 0.473, 0.168, 0.513])

# Program 8.3a

```
#include <iostream>
#include <fstream>
#include <cstdlib> // needed for exit())
#include <string>
using namespace std;
int main()
{
    string filename = "prices.dat"; // place the filename up front
    ifstream infile;
    infile.open(filename.c_str()); // open the file
    if (infile.fail()) // check for successful open
    {
        cout << "\nThe file named *" << filename << "
";n        cout << " was not successfully opened";
        cout << "\nnPlease check that the file currently exists.";
        cout << endl;
        exit(1);
    }

    cout << "\nThe file has been successfully opened for reading.\n";
    return 0;
}

```
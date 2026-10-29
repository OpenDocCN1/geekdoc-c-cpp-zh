# Point of Information

# Using C-Strings as Filenames

If you use a C-string (which is simply a one-dimensional array of characters) to store an external filename, you must specify the C-string's maximum length in brackets immediately after it's declared. For example, examine the following declaration:

```
char filename[21] = "prices.dat";
```

The number in brackets (21) is one more than the maximum number of characters that can be assigned to the variable filename because the compiler adds an end-of-string character to terminate the string. Therefore, the string value "prices.dat", which consists of 10 characters, is actually stored as 11 characters. In this example, the maximum value that can be assigned to the string variable filename is a string value consisting of 20 characters.

In declaring and initializing a string variable for use in an open() method, the variable must represent a C-string, a one-dimensional array of characters terminated with a null character. (See the Point of Information "Using C-Strings as Filenames" for precautions when using a C-string.) A safer alternative, as it doesn't require specifying a character count—and one used throughout this book—is to use an object created from the string class. To do this, add an #include <string> directive, declare an object to be of this class, and convert the object to a C-string in the open() method call by using the string class method c_str().

After a string variable is declared to store a filename, it can be used in one of two ways. First, as shown in Program 9.3a, it can be used to avoid embedding a filename in the open() method by placing the declaration statement at the top of a program. This method also clearly identifies the file's name up front.

# Program 9.3a

```
#include <iostream>
#include <fstream>
#include <cstdlib>  // needed for exit()
#include <string>  // needed for the string class
using namespace std;

int main()
{
    string filename = "prices.dat";  // create and initialize a string object
                                     // with the filename at the top of the
                                     // main() function
    ifstream inFile;
```
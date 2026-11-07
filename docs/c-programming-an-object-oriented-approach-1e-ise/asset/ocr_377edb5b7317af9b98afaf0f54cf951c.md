# **Finding the Index of Current Location**

The first functions in each category, *tellg* or *tellp*, give the index of the current byte pointed to by the marker. Although there is only one marker, we must use *tellg* (g is for get) when we are using an *istream* object and *tellp* (p is for put) when we are using an *ostream* object.

Program 16.12 shows how we print the location of the marker and the value of the corresponding character in a file that has one word in it (“Hello!”).

# **Moving the Marker**

Using the other four member functions in Table 16.9, we can move the marker to point to the byte we want to read or write next. Movement can be absolute or relative. If we know the index of the byte we want to move to, we can use an

# **Program 16.12** Printing location and value of characters

```
```cpp
/************************************************************
* A program to print characters and their locations in a file
************************************************************/
#include <iostream>
#include <fstream>
using namespace std;

int main ()
{
    // Declaration of variables
    char ch;
    int n;
    // Instantiation of stream and opening the file
    ifstream istr;
    istr.open ("sample", ios :: in);
    // Getting characters and their locations
    n = istr.tellg();
    while (istr.get(ch))
    {
        cout << n << " " << ch << endl;
        n = istr.tellg();
    }
    // Closing the file
    istr.close ();
    return 0;
}

Run:
0 H
1 e
2 l
3 l
4 o
5 !
```
```
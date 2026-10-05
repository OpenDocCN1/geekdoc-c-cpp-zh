# 782 Introduction to C++

In case of an fstream object the inherited input and output pointers move in tandem. Therefore, the tellg() and tellp() return the same value.

> If the file is opened for both reading and writing, switch from reading to writing and vice versa a file positioning (e.g., seekp()) should be first called or the buffer is flushed (e.g., by flush).

If we want to check seekg() or seekp() was executed successfully we can use fail(). For example:

```
if(fout.fail())
{
    // An error occurred
}
```

For simplicity, I won't check the return values of the functions I use. That is, I assume that the functions are executed successfully.

# END OF FILE

As discussed, the operating system may add a special character at the end of a text file to mark its end, whereas none characters mark the end of a binary file. In Dos/Windows applications, for example, the Ctrl+Z with ASCII value 26 is typically used to mark the end of a text file. For example, suppose that the following program runs in your system:

```
#include <iostream> // Example 24.4
#include <fstream>
#include <cstdlib>
using namespace std;

int main()
{
    int ch;

    fstream fstr("test.txt", ios_base::in | ios_base::out | ios_base::trunc);
    if(fstr.is_open())
{
        cout << "Error: is_open() failed\n";
        exit(EXIT_FAILURE);
    }
    fstr << 'a' << 'b' << (char)26 << 'c' << 'd';
    fstr.seekg(0);
    while (1)
    {
        ch = fstr.get();
        if(ch == EOF)
        {
            break;
        }
        cout << (char)ch;
    }
    fstr.close();
    return 0;
}
```
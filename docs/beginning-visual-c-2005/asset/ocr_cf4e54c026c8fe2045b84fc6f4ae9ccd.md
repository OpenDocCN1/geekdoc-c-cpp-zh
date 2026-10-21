```
```cpp
using std::cout;
using std::endl;

int main()
{
    const int MAX = 80;                 // Maximum array dimension
    char buffer[MAX];                   // Input buffer
    int count = 0;                      // Character count

    cout << "Enter a string of less than 80 characters:\n";
    cin.getline(buffer, MAX, '\n');     // Read a string until \n

    while(buffer[count] != '\0')       // Increment count as long as
        count++;                        // the current character is not null

    cout << endl
         << "The string \"" << buffer
         << "\" has " << count << " characters.";

    cout << endl;
    return 0;
}
```
```

Typical output from this program is as follows:

```
```text
Enter a string of less than 80 characters:
Radiation fades your genes

The string "Radiation fades your genes" has 26 characters.
```
```

# How It Works

This program declares a character array buffer and reads a character string into the array from the keyboard after displaying a prompt for the input. Reading from the keyboard ends when the user presses *Return*, or when MAX−1 characters have been read.

A while loop is used to count the number of characters read. The loop continues as long as the current character referenced with `buffer[count]` is not '\0'. This sort of checking on the current character while stepping through an array is a common technique in native C++. The only action in the loop is to increment count for each non-null character.

There is also a library function, `strlen()`, that can save you the trouble of coding it yourself. If you use it, you need to include the `<cstring>` header file in your program with an `#include` directive like this:

```
```cpp
#include <cstring>
```
```

The ‘c’ in the header file name indicates that this file contains definitions that belong to the C language library that forms part of the C++ standard library. This header also contains the `wcslen()` function that will return the length of a wide character string.

By using the `strlen()` function you could replace the while loop with the following statement:

```
```cpp
count = std::strlen(buffer);
```
```
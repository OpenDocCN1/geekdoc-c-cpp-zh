# **Program 10.6**  Finding the start of a substring (Continued)

```
```cpp
// Declaration of a string
char str[ ] = "Hello friends.";
// Capitalizing the first occurrence of character e
char* cPtr = strchr (str, 'e');
*cPtr = 'E';
cout << "str after first change: " << str << endl;
// Capitalizing the last occurrence of character e
cPtr = strrchr (str, 'e');
*cPtr = 'E';
cout << "str after last change: " << str << endl;
return 0;
}
```
```

```
```text
Run:
str after first change: HEllo friends.
str after last change: HEllo friEnds.
```
```

# Searching for a Substring

We can search a string to find the position of a substring using the *strstr* function. The function returns a pointer to the first character in the substring. If the substring cannot be found in the string, a null pointer is returned.

```
```cpp
char* ptr = strstr (str, substr);        // Searching for a substring
```
```

# EXAMPLE 10.8

Program 10.7 shows how to find a substring.

# **Program 10.7**  Finding a substring

```
```cpp
/************************************************************
 * The program shows how to use the strstr member function to
 * find the occurrence of a substring in a string.
 ************************************************************/
#include <cstring>
#include <iostream>
using namespace std;

int main ( )
{
    // Creating a string
    char str[ ] = "Hello friends of mine.";
    // Finding the location of the substring
    char* sPtr = strstr (str, "friends");
    cout << "The substring starts at index: " << sPtr - str;
```
```
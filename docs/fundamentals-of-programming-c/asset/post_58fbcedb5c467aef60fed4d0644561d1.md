
## F.7. C STRINGS

```cpp
using namespace std;
bool find_char(const char *s, char ch) {
    while (*s != '\0') { // Scan until we see the null character
        if (*s == ch) // Found the matching character
            return true;
        }
        s++; // Advance to the next position within the string
    }
    return false; // Not found
}

int main() {
    const char *phrase = "this is a phrase";
    // Try all the characters a through z
    for (char ch = 'a'; ch <= 'z'; ch++) {
        cout << '\' << ch << '\' << " is ";
        if (!find_char(phrase, ch))
            cout << " NOT ";
    }
    cout << "in " << '\' << phrase << '\' << endl;
}
return 0;
```

The output of Listing F.9 (findchar.cpp) is

```
'a' is in "this is a phrase"
'b' is NOT in "this is a phrase"
'c' is NOT in "this is a phrase"
'd' is NOT in "this is a phrase"
'e' is in "this is a phrase"
'f' is NOT in "this is a phrase"
'g' is NOT in "this is a phrase"
'h' is in "this is a phrase"
'i' is in "this is a phrase"
'j' is NOT in "this is a phrase"
'k' is NOT in "this is a phrase"
'l' is NOT in "this is a phrase"
'm' is NOT in "this is a phrase"
'n' is NOT in "this is a phrase"
'o' is in "this is a phrase"
'p' is NOT in "this is a phrase"
'q' is NOT in "this is a phrase"
'r' is in "this is a phrase"
's' is in "this is a phrase"
't' is in "this is a phrase"
'u' is NOT in "this is a phrase"
'v' is NOT in "this is a phrase"
'w' is NOT in "this is a phrase"
'x' is NOT in "this is a phrase"
'y' is in "this is a phrase"
'z' is NOT in "this is a phrase"
```

The **find_char** function in Listing F.9 (findchar.cpp) uses pointer notation to traverse the string. It does not need to know the number of characters in the string because it starts at the beginning and scans each character in unit until it finds it or encounters the null terminating character.

Recall from Section 5.1 that for Boolean expressions C++ treats zero value as false and any non-zero as true. Because of such a loose interpretation of Boolean expressions, the **find_char** function above may be written more compactly

```cpp
char find(const char *cs, char ch) {
    // Scan until we see the null character or the character
    // we seek
    while (*cs != '\0' && *cs == ch) {
        cs++; // Advance to the next position within the string
    }
    return *cs; // Null character = false, any other is true
}
```

The only way out of the loop is to scan the null terminating character or the character sought. Here, if the loop encounters the null terminating character, it exits and returns null character. The null character is simply ASCII zero—Boolean false. If the loop locates the sought character, it exits and returns that character which will not be ASCII zero. Any character except the null character has an ASCII value greater than zero; Boolean true.

## F.8. DYNAMIC ARRAYS

Most routines that process strings depend on the strings to be null terminated in order to work properly. Some standard C string functions include

- int strlen(const char *s) returns the number of characters in s, not including the null terminator.
- char *strcpy(char *s, const char *t) copies the contents of string t into string s and including the null terminator; s point to a buffer large enough to hold all the characters of C string.
- char *strnpy(char *s, const char *t, unsigned n) works by copying a number of n characters; s point to a buffer that can hold at least n characters.
- int strcmp(const char *s, const char *t) compares two strings for lexicographic (dictionary) ordering. The function returns an integer less than zero if s appears lexicographically before t. The function returns an integer greater than zero if s appears lexicographically after t. 

The following code fragment

```cpp
cout << strcmp("ABC", "XYZ") << endl;
cout << strcmp("XYZ", "ABC") << endl;
cout << strcmp("ABC", "ABC") << endl;
```

prints

![](img/e326304bd50fbc4f7d5a64c1487eb635_614_0.png)

- int strncmp(const char *s, const char *t, int n) compares the first n characters of two strings for lexicographic (dictionary) ordering. The function returns an integer less than zero if the first n characters of s appears lexicographically before the first n characters of t; as s would appear before t: The function returns an integer greater than zero if s appears lexicographically after the first n characters of t. The function returns zero if the first n characters of the two strings are identical.

You should be careful with C strings because C++ can use C libraries, and C libraries often use C strings. Since strings tend to be problematic, however, in most cases you should use the new string objects (see Section 13.1) whenever possible.

## F.8 Dynamic Arrays

In all the programs we have examined so far in this chapter the size of the arrays were determined at compile time. The programmer may change the size of the arrays in the source code, but the program must be recompiled. We would like a program that is flexible and able to handle any number of entries the user may need.

One approach to the flexibly-sized array is to define the array to hold as many items as conceptually be needed. F.10 (largearrayaverage.cpp) uses this approach.

## F.8. DYNAMIC ARRAYS

Listing F10: largearrayaverage.cpp

```cpp
#include <iostream>

using namespace std;

// Maximum number of expected values is 1,000,000
const int MAX_NUMBER_OF_ENTRIES = 1000000;
double numbers[MAX_NUMBER_OF_ENTRIES];

int main() {
    double sum = 0.0;
    int size; // Actual number of entries

    // Get effective size of the array
    cout << "Please enter number of values to process: ";
    cin >> size;

    if (size > 0) { // Nothing to do with no entries
        cout << "Please enter " << size << " numbers: ";
        // Allow the user to enter in the values.
        for (int i = 0; i < size; i++) {
            cin >> numbers[i];
            sum += numbers[i];
        }

        cout << "The average of ";
        for (int i = 0; i < size; i++) {
            cout << numbers[i] << " ";
        }
        // No comma following element
        cout << numbers[size - 1] << " is " << sum / size << endl;
    }

    return 0;
}
```

While the approach taken in F10(largearrayaverage.cpp) works, it wastes memory. In modern computing, a user may have multiple programs open at the same time. The stack size is only one megabyte, there may not be enough real memory (RAM) the computer will be forced to use more virtual memory (on disk). Virtual memory access greatly degrades the speed of a program, and so the user's experience suffers. It is important that each program uses its resources wisely. Fortunately, there is a way for a programmer to create an array of the exact size, even if that size is not known until runtime. Listing F11 (flexiblearrayaverage.cpp) shows how.

Listing F11: flexiblearrayaverage.cpp

```cpp
#include <iostream>

using namespace std;

int main() {
    double sum = 0.0;
    double *numbers; // Note: numbers is a pointer, not an array
    int size; // Actual number of entries

    // Get effective size of the array
    cout << "Please enter number of values to process: ";
    cin >> size;

    if (size > 0) { // Nothing to do with no entries
        cout << "Please enter " << size << " numbers: ";
        // Allocate the exact size needed
        numbers = new double[size]; // Dynamically allocated array
        // Allow the user to enter in the values.
        for (int i = 0; i < size; i++) {
            cin >> numbers[i];
            sum += numbers[i];
        }

        cout << "The average of ";
        for (int i = 0; i < size; i++) {
            cout << numbers[i] << " ";
        }
        // No comma following element
        cout << numbers[size - 1] << " is " << sum / size << endl;
        delete [] numbers; // Free up the space held by numbers
    }
}
```

Note that numbers is not declared to be an array; it is a pointer:

double *numbers; // Note: numbers is a pointer, not an array

This statement makes space for a single pointer, merely four bytes on a 32-bit system or eight bytes on a 64-bit system. The expression

```
new double[size]
```

allocates at runtime a block of memory for an array that can hold exactly size double-precision floating-point elements. The value of this expression is the starting address of the newly allocated memory block.

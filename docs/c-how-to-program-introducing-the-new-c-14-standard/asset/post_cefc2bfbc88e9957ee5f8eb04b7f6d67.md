
Function `strtod` (Fig. 22.31) converts a sequence of characters representing a floating-point value to `double`. Function `strtod` receives two arguments—a string (`char*`) and the address of a `char*` pointer (i.e., a `char**`). The string contains the character sequence to be converted to `double`. The second argument enables `strtod` to modify a `char*` pointer in the calling function, such that the pointer points to the location of the first character after the converted portion of the string. Line 11 indicates that `d` is assigned the `double` value converted from `string1` and that `stringPtr` is assigned the location of the first character after the converted value (51.2) in `string1`.

```cpp
// Fig. 22.31: fig22_31.cpp
// Using strtod.
#include <iostream>
#include <cstdlib> // strtod prototype
using namespace std;

int main() {
    const char* string1{"51.2% are admitted"};
    char* stringPtr{nullptr};

    double d{strtod(string1, &stringPtr)}; // convert to double

    cout << "The string \"" << string1
         << "\" is converted to the\\ndouble value " << d
         << " and the string \"" << stringPtr << "\"" << endl;
}
```

```text
The string "51.2% are admitted" is converted to the\ndouble value 51.2 and the string "% are admitted"
```

### Fig. 22.31 String-conversion function `strtod`.

Function `strtol` (Fig. 22.32) converts to `long` a sequence of characters representing an integer. The function receives a string (`char*`), the address of a `char*` pointer and an integer. The string contains the character sequence to convert. The second argument is assigned the location of the first character after the converted portion of the string. The integer specifies the *base* of the value being converted. Line 11 indicates that `x` is assigned the `long` value converted from `string` and that `remainderPtr` is assigned the location of the first character after the converted value (`-1234567`) in `string1`. Using a null pointer for the second argument causes the remainder of the string to be ignored. The third argument, `0`, indicates that the value to be converted can be in octal (base 8), decimal (base 10) or hexadecimal (base 16). This is determined by the initial characters in the string—`0` indicates an octal number, `0x` indicates hexadecimal and a number from `1` to `9` indicates decimal.

```cpp
// Fig. 22.32: fig22_32.cpp
// Using strtol.
#include <iostream>
#include <cstdlib> // strtol prototype
using namespace std;

int main() {
   const char* string1{"-1234567abc"};
   char* remainderPtr{nullptr};

   long x{strtol(string1, &remainderPtr, 0)}; // convert to long
   cout << "The original string is \"" << string1
      << "\nThe converted value is " << x
      << "\nThe remainder of the original string is \"" << remainderPtr
      << "\"\nThe converted value plus 567 is " << x + 567 << endl;
}
```

```text
The original string is "-1234567abc"
The converted value is -1234567
The remainder of the original string is "abc"
The converted value plus 567 is -1234000
```

### Fig. 22.32 String-conversion function `strtol`.

In a call to function `strtol`, the base can be specified as zero or as any value between 2 and 36. (See **Appendix D** for a detailed explanation of the octal, decimal, hexadecimal and binary number systems.) Numeric representations of integers from base 11 to base 36 use the characters A–Z to represent the values 10 to 35. For example, hexadecimal values can consist of the digits 0–9 and the characters A–F. A base-11 integer can consist of the digits 0–9 and the character A. A base-24 integer can consist of the digits 0–9 and the characters A–N. A base-36 integer can consist of the digits 0–9 and the characters A–Z. [*Note: The case of the letter used is ignored.*]

Function `strtoul` (**Fig. 22.33**) converts to `unsigned long` a sequence of characters representing an `unsigned long` integer. The function works identically to `strtol`. Line 12 indicates that `x` is assigned the `unsigned long` value converted from `string` and that `remainderPtr` is assigned the location of the first character after the converted value (`1234567`) in `string1`. The third argument, `0`, indicates that the value to be converted can be in octal, decimal or hexadecimal format, depending on the initial characters.

```cpp
// Fig. 22.33: fig22_33.cpp
// Using strtoul.
#include <iostream>
#include <cstdlib> // strtoul prototype
using namespace std;

int main() {
   const char* string1{"1234567abc"};
   char* remainderPtr{nullptr};

   // convert a sequence of characters to unsigned long
   unsigned long x{strtoul(string1, &remainderPtr, 0)};

   cout << "The original string is \"" << string1
      << "\nThe converted value is " << x
      << "\nThe remainder of the original string is \"" << remainderPtr
      << "\"\nThe converted value minus 567 is " << x - 567 << endl;
}
```

```text
The original string is "1234567abc"
The converted value is 1234567
The remainder of the original string is "abc"
The converted value minus 567 is 1234000
```

### Fig. 22.33 String-conversion function `strtoul`.

## 22.10 Search Functions of the C String-Handling Library

This section presents the functions of the string-handling library used to search strings for characters and other strings. The functions are summarized in **Fig. 22.34**. Functions `strspn` and `strcspn` specify return type `size_t`. Type `size_t` is a type defined by the standard as the integral type of the value returned by operator `sizeof`.

### Fig. 22.34 Search functions of the C string-handling library.

| Prototype | Description |
| --- | --- |
| `char* strchr(const char* s, int c)` | Locates the first occurrence of character `c` in string `s`. If `c` is found, a pointer to `c` in `s` is returned. Otherwise, a null pointer is returned. |
| `char* strrchr(const char* s, int c)` | Searches from the end of string `s` and locates the last occurrence of character `c` in string `s`. If `c` is found, a pointer to `c` in string `s` is returned. Otherwise, a null pointer is returned. |
| `size_t strspn(const char* s1, const char* s2)` | Determines and returns the length of the initial segment of string `s1` consisting only of characters contained in string `s2`. |
| `char* strpbrk(const char* s1, const char* s2)` | Locates the first occurrence in string `s1` of any character in string `s2`. If a character from string `s2` is found, a pointer to the character in string `s1` is returned. Otherwise, a null pointer is returned. |
| `size_t strcspn(const char* s1, const char* s2)` | Determines and returns the length of the initial segment of string `s1` consisting of characters not contained in string `s2`. |
| `char* strstr(const char* s1, const char* s2)` | Locates the first occurrence in string `s1` of string `s2`. If the string is found, a pointer to the string in `s1` is returned. Otherwise, a null pointer is returned. |

Function `strchr` searches for the first occurrence of a character in a string. If the character is found, `strchr` returns a pointer to the character in the string; otherwise, `strchr` returns a null pointer. The program of **Fig. 22.35** uses `strchr` (lines 13 and 23) to search for the first occurrences of `'a'` and `'z'` in the string `"This is a test"`.

```cpp
// Fig. 22.35: fig22_35.cpp
// Using strchr.
#include <iostream>
#include <cstring> // strchr prototype
using namespace std;

int main() {
   const char* string1{"This is a test"};
   char character1{'a'};
   char character2{'z'};

   // search for character1 in string1
   if (strchr(string1, character1) != NULL) {
      cout << '\'' << character1 << "' was found in \""
         << string1 << "\".\n";
   }
   else {
      cout << '\'' << character1 << "' was not found in \""
         << string1 << "\".\n";
   }

   // search for character2 in string1
   if (strchr(string1, character2) != NULL) {
      cout << '\'' << character2 << "' was found in \""
         << string1 << "\".\n";
   }
   else
      cout << '\'' << character2 << "' was not found in \""
         << string1 << "\"." << endl;
}
```

```text
'a' was found in "This is a test".
'z' was not found in "This is a test".
```

### Fig. 22.35 String-search function `strchr`.


## Copying

Since a C string is not defined as a class, there is no copy constructor. However, the designers of the library have defined two member functions: `strcpy` and `strncpy`. The function `strcpy` replaces the first string with the whole second string; the function `strncpy` replaces the first *n* characters in the first string with the first *n* characters of the second string. Note that the copying changes the destination string, but not the source string.

```cpp
strcpy (str1, str2);                    // Using the whole str2
strncpy (str1, str2, n);                 // Using part of str2
```

> The two functions strcpy (…) and strncpy (…) can be used
> to replace one string with another.

### EXAMPLE 10.2

In Program 10.1 the first function totally erases *str1* and replaces it with *str2*. The second function replaces the first *n* character of *str1* with the first *n* characters of *str2* and leaves the rest of *str1* unchanged.

### Program 10.1 Copying in a C string library

```cpp
/****************************************************************
 * The program shows how to use strcpy and strncpy to replace   *
 * the whole string or part of it with the whole or part of     *
 * another string.                                             *
 ***************************************************************/
#include <cstring>
#include <iostream>
using namespace std;

int main ( )
{
    // Copy the whole str2 to str1. String str1 is erased.
    char str1[ ] = "This is the first string";
    char str2[ ] = "This is the second string";
    strcpy (str1, str2);
    cout << "str1: " << str1 << endl;
    // Copy part of str4 to str3. str3 is partially erased.
    char str3[ ] = "abcdefghijkl";
    const char* str4 = "ABCDEFGHIJK";
    strncpy (str3, str4, 4);
    cout << "str3: " << str3 << endl;
    return 0;
}
```

```
Run:
str1: This is the second string
str3: ABCDefghijkl
```

## String Length

Each C string has a size (length) that is the number of characters in the string without counting the null character. The C string library defines the *strlen* function to find the length of the string. The function accepts a C string and returns its length as a *size_t* type, which is defined as an *unsigned int* in the library.

```cpp
size_t n = strlen (str); // Finding the length of str
```

> The *strlen* (...) function returns the number of characters in a C string without counting the null character.

### EXAMPLE 10.3

Program 10.2 shows how we can find the length of a C string.

### Input and Output

In addition to initialization with a compact form or assignment using a literal string, we can read the characters into a C string that is declared as an array of characters. We cannot do so when the string is declared as a type (`char*` or `const char*`) because the compiler must allocate memory before reading the characters.

**Overloaded Extraction and Insertion Operators** Consider the situation in which a `<cstring>` library has overloaded the extraction operator (`>>`) and the insertion operator (`<<`) to be used for string input and output. The extraction operator extracts characters one by one from an input object (keyboard or a file) and stores them in the array until a whitespace character is encountered. It then adds the null character at the end. The problem is that the character array that stores the input must have allocated enough memory locations to store all characters entered (before a whitespace) plus one for the null character. If the allocation is not large enough, the result is unpredictable. The insertion operator writes characters in the array to an output device until a null character is encountered.

```cpp
cin >> str;                         // Input
cout << str;                         // Output
```

### EXAMPLE 10.4

Program 10.3 includes a null character in the literal string for str4 just to show that the literal string is terminated by the null character and the rest of the characters are not part of the literal string (line 15). In other words, the string has only 8 characters and not 19. We have input the characters for str5, but note that only the first word is stored in the string; the rest are ignored because the extraction operator stops at the first whitespace.

### Program 10.3 Using C strings

```cpp
/******************************************************
 * The program shows how to create C-strings and use input and
 * output operations with strings.
 ******************************************************/
#include <iostream>
using namespace std;

int main ( )
{
    // Create one constant and one non-constant string.
    char str1[ ] = {'h', 'e', 'l', 'l', 'o', '\0'};
    const char str2[ ] = {'h', 'e', 'l', 'l', 'o', '\0'};
    // Create two constant string types and use string literals.
    const char* str3 = "Goodbye";
    const char* str4 = "Goodbye\0 my friend";
    // Printing four strings
    cout << "str1: " << str1 << endl;
    cout << "str2: " << str2 << endl;
    cout << "str3: " << str3 << endl;
    cout << "str4: " << str4 << endl << endl;
    // Create and input a fifth string.
    char str5[20];
    cout << "Enter the characters for str5: ";
    cin >> str5;
    cout << "str5: " << str5;
    return 0;
}
```

```
Run:
str1: Hello
str2: Hello
str3: Goodbye
str4: Goodbye

Enter the characters for str5: This is the one.
str5: This
```

**The getline Function** To read a line of characters that includes whitespace, we must use the function defined for this purpose, the *getline* function. The *getline* function is a member of the *istream* class, which means that we must have an object of type *cin*. If the *delim* parameter is missing, we use the '\n' character.

```cpp
cin.getline (str, n);                      // Using '\n' as the delimiter
cin.get (str, n, 'delimiter');             // Using a specific delimiter
```

### EXAMPLE 10.5

Program 10.4 creates an array of strings, reads lines into the array, and prints the lines.

### Program 10.4 Using an array of strings

```cpp
/*************************************************************
 * The program shows how to read a set of lines using the     *
 * getline function and print them.                           *
 *************************************************************/
#include <iostream>
#include <cstring>
using namespace std;

int main ()
{
    // Declaration of an array of strings
    char lines [3][80];
    // Inputting three lines
    for (int i = 0; i < 3; i++)
    {
        cout << "Enter a line of characters: ";
        cin.getline (lines [i], 80);
    }
    // Outputting three lines
    cout << endl;
    cout << "Output: " << endl;
    for (int i = 0; i < 3; i++)
    {
        cout << lines[i] << endl;
    }
    return 0;
}
```

```
Run:
Enter a line of characters: This is the first line.
Enter a line of characters: This is the second line.
Enter a line of characters: This is the third line.

Output:
This is the first line.
This is the second line.
This is the third line.
```

## Accessing Characters

The next operation we discuss is how to access any character in a string. We can use the subscript operator to access a character if we know its position in the string. Accessing means retrieving only if the string is a constant. Accessing can mean retrieving or changing if the string is nonconstant.

```cpp
char c = str[i];                         // The string str is a constant
str[i] = c;                              // The string str is nonconstant
```

### EXAMPLE 10.6

Program 10.5 shows how to access characters in constant and nonconstant strings.

### Program 10.5 Accessing characters in a C string

```cpp
/***************************************************************
 * The program shows how to access a character in a string      *
 * using the subscript operator.                                *
 ***************************************************************/
#include <cstring>
#include <iostream>
using namespace std;

int main()
{
```

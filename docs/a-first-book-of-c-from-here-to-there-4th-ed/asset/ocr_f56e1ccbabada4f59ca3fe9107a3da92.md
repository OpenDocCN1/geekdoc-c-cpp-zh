"Hello there World!" to dest_string. As with the strcpy() function, it's the programmer's responsibility to ensure that the destination C-string is defined as large enough to hold the additional concatenated characters.

The strlen() function returns the number of characters in its C-string parameter but doesn't include the terminating NULL character in the count. For example, the value returned by the function call strlen("Hello World!") is 12.

Finally, two string expressions can be compared for equality by using the strcmp() function. This comparison is done character by character in the same manner described in Section 14.1 for string class objects. Program 15.5 uses these C-string functions in the context of a complete program.

# Program 15.5

```
#include <iostream>
#include <cstring>  // required for the string function library
using namespace std;
int main()
{
    const int MAXELS = 50;
    char string1[MAXELS] = "Hello";
    char string2[MAXELS] = "Hello there";
    int n;

    n = strcmp(string1, string2);

    if (n < 0)
        cout << string1 << " is less than " << string2 << endl;
    else if (n == 0)
        cout << string1 << " is equal to " << string2 << endl;
    else
        cout << string1 << " is greater than " << string2 << endl;

    cout << "\nThe length of string1 is " << strlen(string1)
         << " characters" << endl;
    cout << "The length of string2 is " << strlen(string2)
         << " characters" << endl;

    strcat(string1, " there World!");

    cout << "\nAfter concatenation, string1 contains "
         << "the string value\n" << string1
         << "\nThe length of this string is "
         << strlen(string1) << " characters" << endl;
```
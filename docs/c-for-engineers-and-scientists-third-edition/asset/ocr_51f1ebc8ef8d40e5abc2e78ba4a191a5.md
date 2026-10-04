# Chapter 9 Character Manipulation Functions 525

Typically, as in Program 9.13, the functions in Table 9.5 are used in a character-by-character manner on each character in a string. You see this again in Program 9.14, where lowercase string character is converted to its uppercase equivalent using the toupper() function. This function converts only lowercase letters, leaving all other characters unaffected.

In Program 9.14, pay particular attention to the statement for (i = 0; i < int(str.length()); i++) to cycle through each character in the string. Typically, by cycling through the string, a character at a time, how each element in a string is accessed, using the length() function to determine when the end of the string has been reached. Review Program 9.13 to see that it is used in the same way). The only real difference is that in Program 9.14, each element is accessed using the subscript notation str[i]; in Program 9.14, the at() function is used. Although these two notations are interchangeable—and which one you use is a matter of choice—consistency, the two notations should not be mixed in the same program.

![](bbox=[0.118, 0.368, 0.183, 0.403])

# Program 9.14

```
#include <iostream>
#include <string>
using namespace std;

int main()
{
    int i;
    string str;

    cout << "Type in any sequence of characters: *";
    getline(cin,str);

    // cycle through all elements of the string
    for (i = 0; i < int(str.length()); i++)
        str[i] = toupper(str[i]);

    cout << "The characters just entered, in uppercase, are: ";
        << str << endl;

    cin.ignore();
    return 0;
}
```

A sample run of Program 9.14 produced the following output:

Type in any sequence of characters: this is a test of 12345.
The characters just entered, in uppercase, are: THIS IS A TEST OF 12345.
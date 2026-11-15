| Function | Description |
| :--- | :--- |
| `size()` | // Returns the length of the calling string. |
| `empty()` | // Returns true if the calling string contains no characters. |
| `substr(int start, int len)` | // Returns the substring of length len, beginning at start of the calling string. |
| `c_str()` | // Returns the equivalent C-style string. |

Numerous operators have been overloaded in the string class to support the use of string objects. The assignment operator, as well as the relational operators, <, >, <=, >=, ==, and the operators + and +=, can be used with string objects. The binary operator + concatenates two strings, and the binary operator += appends one string to the end of the other. To illustrate the use of some of these operators and functions, we will rewrite program7_8, adding a few additional statements and using the string class instead of C-style strings (recall that we must include the header file string in order to use the string class):

```
/*------------------------------------------------------------*/
/* Program chapter7_10 */
/* This program illustrates the use of several */
/* operators and functions supported by the string class. */
/*------------------------------------------------------------*/

#include<iostream> //Required for cout
#include<string> //Required for string, size()

int main()
{
    // Declare and initialize string objects.
    string strg1 = "Engineering Problem Solving: ";
    string strg2 = "with C++11", strg3;

    // Print the length of each string.
    cout << "String lengths: " << strg1.size() << " "
         << strg2.size() << " " << strg3.size() << endl;

    // Swap strings if strg1 is larger than strg2
    if(strg1 > strg2)
    {
        strg3 = strg2;
        strg2 = strg1;
        strg1 = strg3;
    }

    // Append a string.
    strg2 += " Using C++";

    // Concatenate two strings.
    strg3 = strg1 + strg2;
```
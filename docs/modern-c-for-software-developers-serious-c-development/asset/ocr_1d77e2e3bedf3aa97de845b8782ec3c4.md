< Less than

<= Less or equal to

>, >= Greater than and greater or equal to

[] Index operator

<< Output

>> Input

These operators eliminate the need for calls to functions such as strcpy and strcat.

# String Concatenation

The + operator can be used to concatenate a string object with another string object with a C-style string.

```
// A string demonstration
#include <iostream>
#include <string>
using namespace std;
int main() {
    string str1("Alpha");
    string str2("Beta");
    string str3("Omega");
    string str4;
    // assign a string
    str4 = str1;
    cout << str1 << "\n" << str4 << "\n";

    // concatenate two strings
    str4 = str1 + str2;
    cout << str4 << "\n";

    // concatenate a string with a C-string
    str4 = str1 + " " + str3;
    cout << str4 << "\n";

    // compare strings
    if(str3 > str1) cout << str3 > str1 << "\n";

    if(str3 == str1 + str2)
    cout << "str3 == str1+str2\n";
```
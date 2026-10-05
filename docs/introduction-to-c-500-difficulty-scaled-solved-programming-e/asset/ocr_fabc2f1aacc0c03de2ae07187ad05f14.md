# 10 • Strings 249

with the space character. For example, if the user enters "aabcdaaa", the program should display " bcd \ while the input string is "bcddaa", the program should display "bcd ",

```
#include <iostream>
#include <string>
using std::cout;
using std::cin;
using std::string;

int main() {
    string str;
    int i, len;

    cout << "Enter text: ";
    getline(cin, str);
    len = str.size();

    for(i = 0; i < len; i++) {
        if(str[i] == 'a')
            str[i] = ' ';
        else
            break;
    }
    for(i = len-1; i >= 0; i--) {
        if(str[i] == 'a')
            str[i] = ' ';
        else
            break;
    }
    cout << "New text: " << str << '\\n';
    return 0;
}
```

**Comments:** The first loop compares the characters in the beginning of the string with 'a'. If it is an 'a', it is replaced with the space character, otherwise the loop is terminated. Similarly, the second loop replaces all 'a' characters at the end of the string with the space character.

**C.10.16** is the output of the following program?

```
#include <iostream>
#include <string>
int main() {
    char str[] = "csfbl", *p = str;
    while(*p) {
        --p; /* To make it harder, I could merge the two statements
        into --p++; */
        p++;
    }
    std::cout << strlen(str) << '\\n';
    return 0;
}
```
# Chapter 9 535

```
// check that there is at least one character after the sign
if (sign && int(str.length()) == 1) valid = false;
```

```
// now check the string, which you know
// has at least one non-digit character
i = start;
while(valid && i < int(str.length()))
{
    if(!isdigit(str.at(i))) valid = false; //found a non-digit character
    i++; // move to next character
}

return valid;
```

In the code for the isValidInt() function, pay attention to the conditions being checked. They are mentioned in the code and consist of the following:

+   - The string is not empty.
- A valid sign (+ -) is present.
- If a sign is present, at least one digit follows it.
- All the remaining characters in the string are digits.

Only if all these conditions are met does the function return a Boolean true value. After this value is returned, the string can be converted into an integer safely with the assurance that no unexpected value will result to hamper further data processing. Program 9.18 uses this function in the context of a complete program.

# Program 9.18

```
#include <iostream>
#include <string>
using namespace std;

int main()
{
    bool isValidInt(string); // function prototype (declaration)
    string value;
    int number;

    cout << "Enter an integer: ";
    getline(cin, value);
```

![](bbox=[0.11, 0.535, 0.181, 0.578])
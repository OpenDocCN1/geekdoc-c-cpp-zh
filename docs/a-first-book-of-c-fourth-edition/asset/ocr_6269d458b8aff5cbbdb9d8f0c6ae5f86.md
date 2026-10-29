# Program 15.2

```
#include <iostream>
using namespace std;

void strcpy(char [], char []); // function prototype

int main()
{
    const int MAXCHARS = 81;
    char message[MAXCHARS];    // enough storage for a complete line
    char newMessage[MAXCHARS]; // enough storage for a copy of message
    int i;

    cout << "Enter a sentence: ";
    cin.getline(message,MAXCHARS);    // get the string
    strcpy(newMessage,message);      // pass two array addresses
    cout << newMessage << endl;

    return 0;
}

void strcpy(char string1[], char string2[]) // copy string2 to string1
{
    int i = 0;                        // i is used as a subscript

    while (string2[i] != '\0')        // check for end of string
    {
        string1[i] = string2[i];      // copy the element to string1
        i++;
    }
    string1[i] = '\0';               // terminate the first string

    return;
}
```

The following is a sample run of Program 15.2:

```
Enter a sentence: How much wood could a woodchuck chuck.
How much wood could a woodchuck chuck.
```

# Character-by-Character Input

Just as C-strings can be processed by using character-by-character techniques, they can also be entered and displayed in this manner. For example, take a look at Program 15.3, which uses the character input function cin.get() to accept a string one character at a time. The shaded portion of Program 15.3 essentially replaces the cin.getline() function used in Program 15.1.
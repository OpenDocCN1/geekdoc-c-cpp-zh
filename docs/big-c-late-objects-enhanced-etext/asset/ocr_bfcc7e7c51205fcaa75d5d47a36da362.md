Here is a simple program that puts these concepts to work. The program asks for your name and that of your significant other. It then prints out your initials.

The operation first.substr(0, 1) makes a string consisting of one character, taken from the start of first. The program does the same for second. Then it concatenates the resulting one-character strings with the string literal "&" to get a string of length 3, the initials string. (See Figure 4.)

first = R o d o l f o
0 1 2 3 4 5 6

second = S a l l y
0 1 2 3 4

initials = R & S
0 1 2

![](bbox=[0.7, 0.2, 0.9, 0.42])

© Rich Legg/iStockphoto.

*Initials are formed from the first letter of each name.*

# Figure 4 Building the initials String

# sec05/initials.cpp

```
#include <iostream>
#include <string>

using namespace std;

int main()
{
    cout << "Enter your first name: ";
    string first;
    cin >> first;
    cout << "Enter your significant other's first name: ";
    string second;
    cin >> second;
    string initials = first.substr(0, 1)
        + "&" + second.substr(0, 1);
    cout << initials << endl;
    return 0;
}
```

# Program Run

Enter your first name: Rodolfo
Enter your significant other's first name: Sally
R&S
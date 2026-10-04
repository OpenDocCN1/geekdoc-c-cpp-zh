This variation on the program is designed to handle both first and last names. You have 2 string variables declared: firstname and lastname. You also adjust your prompt to ask for both first and last names.

Then, you stream in both variables, firstname and lastname. This means that the first string entered will go into the first variable, firstname, and the next string entered will go into the second variable, lastname.

The output statement is also changed. Notice that in the streaming output, you have to explicitly output a space between the first name and last name; otherwise, they would run together.

When you run the program, if you enter the name John Keyser, you get the complete greeting, Howdy, John Keyser!, back from the computer.

```
// Program 9_3
// A greeting program handling first and last names
#include <iostream>
#include <string>
using namespace std;

int main() {
    string firstname, lastname;
    cout << "What's your name? (Enter first name and last name) ";
    cin >> firstname >> lastname;
    cout << "Howdy, " << firstname << " " << lastname << "!" << endl;
}
```

Suppose you want to write a program that asks a user for his or her name and favorite color and reads that information. Then, a reply is printed, telling the person that the computer likes that color, too, using both the person's name and favorite color in the output. How might you program this?

![](bbox=[0.773, 0.856, 0.943, 0.881])
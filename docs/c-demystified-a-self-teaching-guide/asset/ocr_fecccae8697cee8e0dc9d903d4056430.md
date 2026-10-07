# The Do While Loop

The do while loop is similar to the while loop. The primary difference is that with a do while loop the condition is tested at the bottom, unlike a while loop where the condition is tested at the top. This means that a do while loop will always execute at least once, whereas a while loop may never execute if all its condition is false at the outset.

# Syntax

The syntax of a do while loop is

```
do {
    statement(s);
} while (condition);
```

The do keyword starts the loop. The statement or statements belonging to the loop are enclosed in curly braces. After the close curly brace, the keyword appears, followed by the condition in parentheses, terminated by a semicolon.

# A Do While Loop Example

The following program is a modification of the one earlier in this chapter that used a while loop to continue to prompt the user a positive number until either the user did or quit, and then outitted the positive number or the message that the user did not enter a positive number. This modification uses a do loop instead of a while loop.

```
#include <iostream>
using namespace std;
int main(void) {
    int num;
    char choice;
    bool quit = false;
    do {
        cout << "Enter a positive number: ";
        cin >> num;
        if (num <= 0) {
            cout << "Number must be positive; try again (Y/N) : ";
            cin >> choice;
            if (choice != 'Y')
                quit = true;
        }
    } while (num <= 0 && quit == false);
    if (quit) {
        cout << "The number you entered is " << num << " ";
    } else {
        cout << "You did not enter a positive number";
        return 0;
    }
}
```

The following are sample inputs and outputs. The first one has the user successfully enter a positive number first time.
![](bbox=[0.174, 0.094, 0.238, 0.161])

TIP

Note the end of the example switch block has a final `default` case. It applies to the situation when none of the preceding cases applies. The `default` case isn’t required; you can leave it off if you don’t need it. However, if you do include it, you put it at the end of the `switch` block because it’s the catchall case.

The `SwitchStatement` example in Listing 2-5 is a complete application that demonstrates a `switch` statement. It also shows you how you can make a simple, antiquated-looking *menu* application on the console. You don’t need to press Enter after you choose the menu item; you just press the key for your menu selection. That’s thanks to the use of `getch()` rather than `cin`.

# LISTING 2-5: Making Multiple Comparisons in One Big Block

```
```cpp
#include <iostream>
#include <conio.h>

using namespace std;

int main() {
    // Display a list of options.
    cout << "Choose your favorite:" << endl;
    cout << "1. Apples " << endl;
    cout << "2. Bananas " << endl;
    cout << "3. Lobster " << endl;

    // Obtain the user’s selection.
    char ch = getch();

    // Continue getting user selections until the user
    // enters a valid number.
    while (ch < '1' || ch > '3') {
        ch = getch();
    }

    // Use a switch to display the user’s selection.
    cout << "You chose " << ch << endl;
    switch (ch) {
    case '1':
        cout << "Apples are good for you!" << endl;
        break;
    case '2':
        cout << "Bananas have plenty of potassium!" << endl;
        break;
```
```

*(continued)*
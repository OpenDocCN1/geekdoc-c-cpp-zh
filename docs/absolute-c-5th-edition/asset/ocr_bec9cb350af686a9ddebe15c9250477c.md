# Exception Handling Basics

18.2 Same Thing Using Exception Handling (part 1 of 2)

```
#include <iostream>
using std::cin;
using std::cout;

int main ( ) {
    int donuts, milk;
    double dpg;

    try {
        cout << "Enter number of donuts:\\n";
        cin >> donuts;
        cout << "Enter number of milk:\\n";
        cin >> milk;

        if (milk <= 0) {
            throw donuts;
        }

        dpg = donuts / static_cast<double>(milk);
        cout << " donuts.\\n";
        cout << "You have " << dpg << " donuts for each glass of milk.\\n";
    } catch (int e) {
        cout << e << " donuts, and No Milk!\n";
        cout << "Go buy some milk.\\n";
    }

    cout << "End of program.\\n";
    return 0;
}
```

> This is just a toy example to learn C++nsyntax. Do not take it as an example of good
typical use of exception handling.

(continued)